# 5 things I wish I knew before applying for the first job - JavaScript core


> 부트캠프동안 계속 배웠고 앞으로도 쭉 사용하게 될 Javascript - 얼마나 알고 계십니까?

...

2015 - `Arrow function expression` 및 큰 변화가 있던 `ES6(ECMAScript 2015)`.

2016 - `VSCode 1.0` 출시

2017 - `Vue.js` 의 `Stable release 2.4.4` 발표.

2018 - `Node.js` 의 `v10 LTS` 시작.

2019 - `React`의 `function component` & `UseEffect` 소개.

2020 - `ECMAScript 2020`의 `??` - `nullish coalescing operator`

2022 - `React 18`.

...

JS와 그것을 둘러싼 생태계의 프레임워크/라이브러리 등은 정말 무서울 정도로 계속 바뀌고 또한 업데이트 되어가고 있다.

사실 새로운 기술 표준이라는게 만들어지고 나서 최소 수 개월, 또는 수 년동안은 유저가 모이고 커뮤니티가 발전하며 그 확장세가 커지지만 특히 2000년 중후반 이후로 웹 기반 기술이 빠르게 발전함과 동시에 많은 개발자들은 그 속도에 뒤쳐지지 않기 위해 절치부심하는 중이다.

2022년 현재, 만약 내가 다시 부트캠프로 돌아가 공부를 하고, 그리고 이제 막 끝낸 후에 점점 길어져만 가는 TO-DO List 에서 하나씩 꺼내서 다뤄볼까 한다.

이번에는 다들 한번은 봤지만 누가 물어봤을때 100% 대답하기는 쉽지 않던 다섯 가지 조그마한 것들을 모아보았다.

면접에서 이런 것들을 잘 물어보지는 않겠지만 최소한 자신이 작성하는 한 줄 한 줄마다 왜 이런 keyword/syntax를 쓰는지, 더 효율적으로 쓸 수 있는 방법은 없는지를 생각한다면 어느새부터 자신감이 쌓여가는 스스로를 볼 수 있을 것이다.


- 아래의 질문에 답해보면서 Chrome 브라우저의 console 탭을 열어서 실제로 작성도 해보고 확인해보자.

<br>

## 1. `var` vs. `const` vs. `let`
---
예전 레거시 코드를 보면 `var`만 사용하거나 심지어는 최근 코드에서도 `var`를 사용하는 분도 본적이 있다. (진짜로 계신다...)

예전에 `var` 만 있을 때에는 global scope, block scope 등 전역변수, 지역변수를 이해하고 이게 어떻게 되는지 알아야 했지만 현재는 `const` 와 `let` 으로 사용해보자.

```
  const name = "Jason"
  name = "Amy" // Error

  let name = "Jason"
  name = "Amy"
  console.log(name) // "Amy"
```

체크포인트
- 언제 const/let을 각각 쓰는가?
- object/Array 는 const/let 둘 중 어느 것을 써야 하는가

<br>

## 2. `for...of` vs. `for...in`
---
분명히 수업중에서도 배웠고 여기저기 검색하면서도 많이 보겠지만 상당히 많은 학생들이 `for (let i = 0; i < str.length; i++;) {...}` 를 사용하는 것을 보았다.

셋 다 유용하니 상황에 맞춰서 적절히 사용하면 좋다.

체크포인트
```
    const testArr = ['apple', 'banana'];
    const testObj = {
        1: 'cacao',
        2: 'date',
    };
    const testStr = "Car"
```
- 위 testArr 에서 `for...of`/`for...in`을 사용하면 console.log에 각각 무엇이 찍히는가?

- 위 testObj 에서 `for...of`/`for...in`을 사용하면 console.log에 각각 무엇이 찍히는가?

- 위 testStr 에서 `for...of`/`for...in`을 사용하면 console.log에 각각 무엇이 찍히는가?

<br>

## 3. `Big/fat arrow` (arrow function expression)
---
다른 언어에서 건너 오신 분들은 많이 익숙한 syntax지만 의외로 몇몇 학생들이 기존의 작성된 코드에서 arrow function 으로 변환하는 것이 익숙치 않아보였다.

```
function setToday(arg) {
    return new Date(arg);
}
```
1. function을 `const` 로 바꾸고
2. 함수 이름 뒤의 `()` 왼쪽에는 `=`, 우측에는 `=>`를 붙인다.

```
const setToday = (arg) => {
    return new Date(arg);
}
```
+ argument가 1개일때 `()` 를 생략하는 경우도 팀에 따라 상당히 많다.
+ 한 value만 return 할 경우 return 을 생략하기도 한다.
```
const setToday = arg => new Date(arg);
```

<br>

## 4. Array `push`/`pop`/`shift`/`unshift`
보통 `push` 까지는 잘 사용하시는데 그와 비슷한 pop/shift/unshift도 잘 사용하면 좋다.

물론 `time complexity`와 `space complexity`까지 생각해서 공부한다면 코딩 인터뷰에도 도움이 꽤 될 것이다.

체크포인트

```
    const colors = ['red', 'yellow', 'blue'];
```
- `red` 만 제거하려면?
- `red` 왼쪽에 `purple`을 넣으려면?
- `blue` 만 제거하려면?
- `blue` 오른쪽에 `white`를 넣으려면?
- 넷 중 누가 `O(n)` 이고 `O(1)` 일지?
- Array.splice 와도 비교해봅시다.

<br>

## 5. Spread Operator - `...`
---
2015년 ES6에서 나온 Spread는 그 많은 업데이트들 중 가운데서도 매일마다 볼 수 밖에 없는 syntax이다.

그 중에서도 가장 중요한 몇가지 케이스만을 살펴보자.

1. 다수의 Array 합치기
```
    const arr1 = [1, 2];
    const arr2 = [3, 4];

    const combinedArr = [...arr1, ...arr2]; // [1, 2, 3, 4]

```
2. 다수의 Object 합치기
```
    const obj1 = { 1: 'a'};
    const obj2 = { 2: 'b', 3: 'z'};

    const combeind Obj = {...obj1, ...obj2} // { 1: 'a', 2: 'b', 3:'z'}
```
3. 문자열 split
```
    const str = 'happy'
    console.log(...str); // ['h','a','p','p','y']
```

실제로는 더 많이 복잡한 data structure 를 가진 자료들을 합치거나 나누는 경우가 대부분이겠지만 복잡할수록 가장 간단하게 생각해 보는 것을 잊지 말자.

<br>

## 6. What's next?
---
다음 포스팅에서는 이번 주에 다루지 않은 것과 조금 더 까다로운 것들에 대해 이야기 해 보도록 하겠다.
