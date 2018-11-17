FontEnd Interview Question & Answer
===

> ## null 과 undefined의 차이
```javascript
let a
console.log(a) // undefined
console.log(typeof a) // undefined

let b = null
console.log(b) // null
console.log(typeof b) // object

console.log(null === undefined) // false
console.log(null == undefined) //true
```

* undefined: 변수는 선언되었지만 아직 값이 지정되지않음
* null: 할당 값, 변수에 의도적으로 값이 없음을 표현할 수 있다.
* undefined 와 null 은 javascript 에서 고유한 원시값이다.
* '==' 으로는 true 가 반환되지만 '===' 를통해 type 까지 확인하게되면 false 가 나온다.

> ## Closure

> ## Hoisting

> ## Event Bublling & Captureing

> ## Event 위임 패턴
