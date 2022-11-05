# History of JavaScript (ECMAScript) I wish I knew before applying for the first job - JavaScript core



## History of JavaScript
---
### Beginning
- Invented by `Brendan Eich` in 1995
    - co-founder of `Mozilla` project/foundation/corporation - known for `Firefox` and `Rust`
    - `Mozilla`'s CTO and CEO
    - CEO of `Brave Software`

> Scripting language with `Java` syntax + `Scheme` by `Netscape`

> Written in `10 days` to meet `Navgator 2.0` Beta release schedule`

> Called `Mocha` -> `LiveScript` -> `JavaScript`(`Sun Microsystems`)

- In 1996, Netscaped Submitted `JavaScript` to Ecma international - for standard specification for all browsers
---
### Original JavaScripts (1997 - 1999)
- 1997 - ECMAScript 1 (ES1)
    - 1st Ed.
- 1998 - ECMAScript 2 (ES2)
    - Editorial changes
- 1999 - ECMAScript 3 (ES3)
    - [x] `RegExp`
    - [x] `Try/Catch`
    - [x] `Switch`
    - [x] `do/while`
---
### Never released ECMAScript 4 (2000-2008)
#### Lack of interest in the begining
- Microsoft reverse-engineered `JavaScript` and created `JScript`
- With `Internet Explorer`'s market share reaching to 95% by 2000, `JScript` became the standard for `client-side scripting` on Web.
- Microsoft stopped collaborating on Ecma

#### Growth in Web and technology
- Mozilla introduced `Firefox` in 2004, taking much market share from `Microsoft`
- Mozilla started working on on `ECMAScript for XML(E4X)`, along with `Macromedia` (acquired by `Adobe`), who's been working with `ActionScript 3`
- `ActionScript 3` was too different from established `client-side-scripting`
- Needed Microsoft's cooperation - oh well...
- Thus, it got never released
#### Growth in non-ecma libraries
- `jQuery`/`Ajax`
- Sparked the renaissance of `JavaScript`
#### V8 Chrome engine - JIT
- `Just-in-time complication (JIT)`
    - Compiles the required part in runtime
        - instead of compiling before execution
    - Caching the frequently used code
        - Improves the speed of interpereters
    - Java uses JIT compiler in translating Bytecode -> machine language

- Huge performance boost over its competitors
---
### Need of combining all branching works - 1st Main Reivsion (2009)
> Combine all relevant work and drive the language forward
- 2009 - ECMAScript 5 (ES5)
    - [x] `"strict mode"`
    - [x] `JSON support`
    - [x] `String.trim()`
    - [x] `Array.isArray()`
    - [x] `Array iteration methods`
    - [x] `Trailing commas for object literals`
---
### 2nd Revision (2015)
> Introduction of `Node.js` in 2009 - spiking outer browser use

> `Node.js` becacme a standalone system, thanks to `V8` + `event loop` + `I/O API`

> Huge popularity of `npm`

- ECMAScript draft is now maintained by `GitHub`
- **2015 - ECMAScript 2015 (ES6)**
    - [x] `let`/`Const`
    - [x] `Default parameter values`
    - [x] `Array.find()`
    - [x] `Array.findIndex()`
---
### Yearly Additions (2016 ~ Current)
- 2016 - ECMAScript 2016
    - [x] `**` - `Exponential operator`
    - [x] `Array.includes()`
- 2017 - ECMAScript 2017
    - [x] `String padding`
    - [x] `Object.entries()`
    - [x] `Object.values()`
    - [x] `Async`
    - [x] `Shared memory`
    - [x] `Trailing commas for function parameters`
- 2018 - ECMAScript 2018
    - [x] `rest`/`spread`
    - [x] `asynchronous iteration`
    - [x] `Promise.finally()`
    - [x] `Additions to RegExp`
- 2019 - ECMAScript 2019
    - [x] `String.trimStart()`
    - [x] `String.trimEnd()`
    - [x] `Array.flat()`
    - [x] `Object.fromEntries()`
    - [x] `Optional catch binding`
- 2020 - ECMAScript 2020
    - [x] `?.` - `Optional Chaining Operator`
    - [x] `??` - `Nullish Coalescing Operator`
    - [x] `&&=` - `Logical AND Assignment Operator`
    - [x] `||=` - `Logical OR Assignment Operator` 
    - [x] `BigInt`
    - [x] `String.matchAll()`

- 2021 - ECMAScript 2021
    - [x] `Promise.any()`
    - [x] `String.replaceAll`
    - [x] `_` - `Nuemeric seperator`
- 2022 - ECMAScript 2022
    - [x] `Top-level Await`
    - [x] `#` - `Private instance fields/methods/accessors`
    - [x] `static class initialization`
    - [x] `error cause` - `console.log(err.cause)`
    - [x] `Array.at()` - instead of `arr.length - 1`
    - [x] `Object.hasOwn()`
    - [x] `/d` flag of `RegExp` - start/indices position end of each match

### 2022
> As of 2022, 98% of websites use JavaScript on the client side for webpage behavior
---
## Reflection
- The history of JavaScript provides a profound understanding of how the web technology has developed
- Surprising to see `optional chaining` was only introduced in 2020. Should've been something like 2005... XD

- A lot of QOL updates happened in the last 3 years - `Array.at()`, `Top-level Await`, `error.cause`, `String.replaceAll()`

- Exicited for the ECMAScript 2023 with a few big surprises


> How can we stay up-to-date with all these changes? (ECMAScript, frameworks, libraries, tools)

> Browser support is one main issue why the newer versions can't be blatently used.


## 6. What's next?
---
다음 블로그에서는 React/Vue/Angular 에 대한 비교를 다뤄볼까 생각중이다.

---
## References

- w3schools - https://www.w3schools.com/js/js_versions.asp

- wikipedia - https://en.wikipedia.org/wiki/Brendan_Eich

- ECMAScript 2022 - https://dev.to/brayanarrieta/new-javascript-features-ecmascript-2022-with-examples-4nhg
