Reactive Programming 이 무엇인가?
===============================

Reactive programming (반응형 프로그래밍) 이란 어떻게 프로그램을 짜는지 정의해주는 수많은 디자인 패턴중 하나이며,     
저는 리엑티브 프로그래밍이야 말로 프로그래머들이 꼭 알아야할 새로운 사고방식이라고 말하고 싶습니다.

Reactive programming을 이야기할때는 context 가 굉장히 중요합니다.
왜냐하면 reactivity가 variable 레벨 뿐만 아니라, UI level, event level, db level 에서도 적용될 수 있기 때문입니다.

Reactive Variable
--------------------------------

아래 코드를 한번 봅시다.

```
let a = 5
let b = 5 + a
a = 10
console.log(b)
```
마지막 b 안에는 어떤 값이 들어 있습니까?

코드를 좀 해보신분들은 쉽게 답이 10이라고 할것입니다.     
왜냐면 프로그램은 기본적으로 Sequential Execution 으로 돌아가고,     
숫자는 pass by value 로 되기 때문에 b 가 10으로 저장이 되고나서 a 를 10으로 변경하여도 b의 값에는 변화가 없기 때문입니다.

만약 b 를 pass by value 가 아닌 a 에 의존(derive)하게 하려면 어떻게 해야 할까요?

아래와 같이 함수를 사용 하면 됩니다.
```
let a = 5
function getB() {
   return 5 + a
}
a = 10
console.log(getB()) // prints 15
```
프로그래밍 언어에 따라서 반응형 변수를 조금더 잘 만들수 있는 방법도 있답니다.     
예를들어서 자바스크립트에서는 getter 를 사용하면 b 의 값을 불러 올때마다 일일히 함수를 부를 필요가 없습니다.
```
const obj = {
   a: 5,
   get b() {
    return this.a + 5;
  }
}
obj.a = 10
console.log(obj.b) // prints 15
```
b 의 값은 a 에 반응한다, 즉, b 는 reactive variable 이라고 할수 있겠습니다.

대부분의 프로그래밍 언어들은 reactive variable 을 만들기위해 필수적으로 함수를 사용해야 하는데 그럴경우 반응형 변수를 만들기 위해서 적어야 할 코드가 많아지고 복잡해집니다. Svelte 는 반응형 함수를 language level 에서 native 하게 제공해줍니다.

아래는 Svelte 의 반응형 변수 코드 예제 입니다.
```
<script>
	let count = 0;
	$: doubled = count * 2;
</script>

<p>{count} doubled is {doubled}</p>
```
반응형 변수는 앞에 $: 를 붙이며, 오른쪽에 들어가는 변수의 reference 가 바뀔때마다 반응형 변수 계산을 다시 해줍니다.

위 코드는 html 하고 비슷하지만 엄연히 다릅니다. 확장자는 .svelte 이며 js/html 으로 컴파일이 됩니다.

반응형 프로그래밍을 알면 좋은 코더가 될수 있는 이유
--------------------------------------------

변수가 celcius, fahrenheit 이렇게 2개 있다고 가정해 봅시다.     
개발의 경험이 많이 없으신 분들은 celcius 와 fahrenheit 를 2개의 변수로 각각 만들어 관리할것입니다.     
하지만 그럴경우 celcius 를 변경할때마다 fahrenheit 를, fahrenheit 를 변경할때마다 celcius 를 변경해줘야 하는 복잡한 상황이 발생하며, celcius 와 fahrenheit 중 하나만 변경하고 나머지를 변경하지 않으면 inconsistent 한 state 이 발생하게 됩니다.

on/off 스위치가 한개면 possible state 이 2가지 이지만     
on/off 스위치가 열개면 possible state 이 (2의 10승) 1024가지로 기하급수적으로 늘어나는만큼,     
프로그래머들은 스위치 갯수를 어떻게하면 최소화를 하느냐가 아주 중요한 관건입니다.

솔루션은 celcius 라는 변수를 한개만 사용하고, fahrenheit 은 celcius 에서 값을 derive 하는 식으로 하면 훨씬도 코드도 간결해지고 inconsistent state 이 발생할 염려도 사라지는 것이지요.

잘하는 프로그래머들은 어떻게하면 내가 원하는 기능을 최소한의 코드로 달성할수있는지 항상 고민을 합니다.

> *적는 코드가 짧아야 개발을 빨리 할 수 있으며,     
> 적는 코드가 짧아야 버그 갯수가 줄어들며,     
> 적는 코드가 짧아야 관리하는 시간을 아낄수 있습니다.     
> 출처: 에릭*

그렇기때문에 개발자의 paradigm shift 는 처음부터 지금까지 계속해서 low level language 에서 high level language,     
그리고 library/framework 도 less abstract 에서 more abstract 으로 변하고 있으며 그 추세는 한동안 지속되지 않을까 생각합니다.

물론, 무조건 high level, more abstract 으로 간다고해서 좋은것만은 아닙니다.     
프로그램의 requirements는 점점더 많아지고, 프로그램은 복잡해 지고 있습니다.     
그렇기에 그 적정 수준(right amount of abstraction)이 계속해서 올라간다고 생각합니다.

많은 개발자들이 c/c++ 에서 Java/C#으로 그리고 JS/Python/Rust 로 넘어간만큼      
많은 웹 개발자들이 Jquery에서 React/Angular/Vue 넘어가였고, 다음 paradigm은 Svelte와 비슷한 (훨씬 적은 코드로 똑같은 기능을 구현 할 수 있는) framework 가 되지 않을까 생각합니다.

Svelte 의 대해서 소개
--------------------------

Svelte 는 React/Angular/Vue 와 같은 웹앱 개발 framework 입니다.     
React/Angular/Vue 는 DOM 을 바로 바꾸지 않고 먼저 virtual dom 을 만들어 DOM 과 reconcilation 을 통해 DOM update 를 batched를 통해 최적화를 함으로써 속도를 더 빠르게 하기 위해 개발되었습니다.     
(그 이유는 DOM을 update 하는것이 virtual dom 업데이트 하는것보다 월등히 느리기 때문에 O(n^2) vs O(n) DOM update 를 최적화 하기 위함입니다).

하지만 아이러니하게도 Svelte 는 virtual dom 없이 batched update를 할수 있고, 그렇기 때문에 react/angular/vue 보다도 더 빠르다고 합니다.

저는 Svelte 가 React 보다 훨씬 짧은 코드로 같은 기능을 달성할수 있는 이유에 대해서는 조금 부담스러울정도로 강력한 reactive programming 이라는 프로그래밍 패러다임을 variable 과 UI 에 동시에 적용을 하였기 때문이라고 생각합니다.

반응형 UI 소개
------------------------------

React 도 반응형 UI 입니다.     
DOM을 변경하기 위해서는 element 에 대한 reference 없이 react.state 만 업데이트 해주면 UI(DOM)이 그 state 에 반응합니다.

```
// index.html
<div id='fahrenheit'>0</div>
<script>
  document.getElementById('fahrenheit').innerHTML = '90' // DOM 에 reference 통해 업데이트 하는 방법
</script>
```

```
// React 로 UI 업데이트 하는 방법
function App() {
  const [fahrenheit, setFahrenheit] = useState('0')
  return (
      <button onClick={()=>setFahrenheit('90')>{fahrenheit}</button>
  )
}
```
반응형 UI 를 다른말로 declarative UI 라고도 하고, 반응형이지 않은 UI 를 imperative UI 라고 합니다.

여기서 중요한점은 React 는 one-way data binding 입니다.     
즉, setFahrenheit 를 통해 fahrenheit 을 업데이트 해주면 UI 가 바뀌지만, 반대로 UI 값을 바꾸면 fahrenheit variable 은 바뀌지 않는다는 것이죠.

React 에서는 JS 를 그대로 사용하기 때문에 fahrenheit 변수가 UI 값에 반응하게 하려면 필수적으로 함수를 사용해야 합니다.
```
import React from 'react'

let fahrenheit = 0
function App() {
  function onFahrenheitInputChange(event) {
    fahrenheit = event.target.value
  }
  return (
    <input type='number' onChange={onFahrenheitInputChange} />
  )
}
```
one-way data binding 의 문제점은 inconsistent state 이 발생할수 있다는 점에 있습니다.

state ----(updateOnChange)----> UI     
or     
UI -------(updateOnChange)----> state

즉, 왼쪽의 값을 변경하면 오른쪽의 값이 반응하지만, 오른쪽의 값을 변경하면 왼쪽은 변하지 않는다는 것이죠.     
on/off 스위치가 1개도 아니고 2개도 하니고 그것의 한 중간 정도 1.5개 정도 라고 보면 될것입니다.

이것의 해결책은 two-way data binding 입니다.

React 에서 two-way data binding 을 실현하기 위한 방법은 아래와 같습니다.

```
import React, {useState} from 'react'

function App() {
  const [fahrenheit, setFahrenheit] = useState(0)
  function onFahrenheitInputChange(event) {
    setFahrenheit(event.target.value)
  }
  return (
    <input type='number' value={fahrenheit} onChange={onFahrenheitInputChange} />
  )
}
```
여기서 문제점은 JS language 레벨에서 reactive variable 이 서포트 되지 않는 단점때문에 필요 이상으로 코드가 길어지고,     
setFahrenheit 을 사용하지 않고 바로 fahrenheit 을 변경할경우 inconsitent state 이 발생되며,     
그리고, 추후에 코드를 변경하면서 two-way data binding 이 깨질수있는 염려가 있습니다 (예를들어서 onFahrenheitInputChange 안에서 setFahrenheit 부르기전에 error exception 이 thrown 되는경우).

Svelte 에서는 two-way data binding 이 first-class citizen 으로 서포트 되므로 아주 간단하게 목적 달성을 할 수 있습니다.

```
<script>
  let fahrenheit = 0
</script>
<input type='number' bind:value={fahrenheit}>
```

여기서 DOM state 과 fahrenheit variable 은 항상 같은 값이므로 on/off 스위치가 한개만 존재하기때문에 code complexity 가 현저히 줄어드는 결과를 낳게 됩니다.

다음 파트에서는 Reactive Programming 을 Event 와 Database 에 적용시키기 방법에 대해 설명해 드리겠습니다.

포스팅 원문 출처:     
https://www.techtarget.com/searchapparchitecture/definition/reactive-programming#:~:text=Reactive%20programming%20describes%20a%20design,a%20user%20makes%20an%20inquiry     
https://reactivex.io/
