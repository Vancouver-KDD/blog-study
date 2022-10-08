## Server Side Rendering (SSR) 이 무엇인가?

우선 Server Side Rendering의 개념을 이해하기 위해서는 웹사이트가 기본적으로 어떻게 돌아가는지 이해할 필요가 있을것 같다. 

모든 웹사이트의 entry point 는 html 파일이다. 

아래의 html 의 예를들어보자.

    <!DOCTYPE html>
    <html lang="en">
      <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
        <script src="pathToJS.js"></script>
        <style src="pathToCSS.css"></style>
      </head>

      <body>
        Hello World
      </body>
    </html>
html을 로드한후에 html이 필요한 pathToJS.js 와 pathToCSS.css 을 추가로 로드하게 되며, 보통 js 같은경우 버튼을 눌렀을때 돌아가는 로직, 그리고 css는 웹 페이지의 스타일을 결정해주게 된다.

하지만 Hello World 대신 Hello Bob, Hello Eric 과 같이 유저 이름을 보여주고 싶을땐 어떻게 할까?

그래서 나온게 바로 PHP 이다

예들어서 index.html 대신 index.php 파일을 만들고

Hello World 대신 

    <?php
    $name = "Eric"; // Eric 은 User DB 에서 불러왔다고 가정하면
    echo "Hello " . $name;
    ?>
이렇게 하면 클라이언트는 index.php 대신 index.html 을 받게 되고 거기에 Hello Eric 과 같은 문장을 보게 될 것이다.

이게 바로 SSR 이고, 그와 반대되는 client-side-rendering 은 2010년대에 새로 적용하기 시작한 방식이다.

CSR 이 도입된 이유는 소비자의 user experience 를 더 좋게 만들기 위해서이다.

CSR은 모든 html 을 서버에서 만들고 그것을 html 형태로 쏴주는 대신, 빈껍대기 html 파일을 보내후 js 가 필요한 html 을 client side 에서 만들어 주는 형태이다.

하지만 여기서 CSR 의 문제점이 발생한다.

JS 를 다 로딩하고 실행시키기 전까지는 웹 페이지에 아무것도 나오지 않는다는 뜻이다.

다시말해, SSR 는 JS 파일이 로딩되고있는 중에도 바로 웹페이지가 바로 보이고, JS 다 로드된후에는 버튼클릭을 했을때 돌아가는 코드가 활성화되는것이다.

JS 가 로드되서 웹 페이지가 활성화가 되는 시간을 Time to be Interactive 라고 부르며, js 없이 html css 만으로 웹페이지가 로드되는것을 time to first paint 라고 한다.

즉 SSR 은 time to be interactive 는 CSR 과 거의 동일하지만 time to first paint 가 JS 파일 사이즈가 크면 클수록 월등히 빠르다.

## React Server Side Rendering

React 는 DOM 을 데이터화한 virtual DOM 을 만들어 Virtual DOM으로 DOM 을 효율적으로 변경해주는 라이브러리다.

React에서 사용하는 jsx 는 단순히 js 안에 xml 형태의 태그들을 뜻한다.

우리가 아래와 같은 Hello.jsx 파일이 있고

    let count = 0;
    export default function Home() {
      return (
        <div>
          <h1>Home</h1>
          <button onClick={() => alert("hello world")}>{count}</button>
        </div>
      );
    }
이것을 html 로 변경하고싶으면 아래와같이 renderToString 을 쓰면 된다.

    import { renderToString } from "react-dom/server";
    import Hello from "Hello"

    const html = renderToString(React.createElement(Hello));
우선 Hello 를 Component 에서 Element 로 변경해준뒤 (class 를 instance 로 변경해주는거과 비슷하다), renderToString 에 넣어주게되면 아래와같은 string 이 튀어나온다.

    <div>
        <h1>Home</h1>
        <button>0</button>
    </div>
여기서 주목할점은, onClick 과 같은 javascript 이 다 사라졌다 있다.

이것은 의도적인것으로, JS 를 돌리기위해선 inline JS 뿐만아니라 전체 JS 를 다 로드해야하기에 전체 JS 를 로드한후에 한가지더 필요한 작업이 있다.

Hello 의 html 을 전체 html 에 끼워 넣어 클라이언트에 제공해주면 SSR 의 첫번째 단계가 끝난다.

    <!DOCTYPE html>
    <html lang="en">
      <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
        <script src="pathToJS.js"></script>
        <style src="pathToCSS.css"></style>
      </head>

      <body>
        <div id="root">
          <div>
            <h1>Home</h1>
            <button>0</button>
          </div>
        </div>
      </body>
    </html>
보통 client side rendering 은 특정 div 에 renference 을 주고 거기 안에 render 을 해주면 html 과 event hookin을 둘다 넣어주게 된다.

하지만 위와 같이 SSR 을 이미 한 경우에는 기존 html 에 event hooking 만 하면 되기 때문에 render 대신 hydrate 만 하면 된다.

    import Hello from "./Hello.js";
    import { createElement } from "react";
    import { hydrate } from "react-dom";

    hydrate(createElement(Hello), document.getElementById("root"));
위에 컨셉을 이용하여 parcel 과 typescript 을 사용한 template 을 만들었습니다.

https://github.com/bosung90/ssr-from-scratch
