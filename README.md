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
호이스팅이란 끌러올림 이란 뜻이고 JavaScript 에서 또한 비슷한 의미로 사용되고 있다. 변수의 정의가 그 범위에 따라 선언과 할당으로 분리되어 변수의 선언을 항상 컨텍스트 내의 최상위로 끌어올리는것을 의미힌다. 

변수뿐만 아니라 함수또한 동일하게 동작한다. 

JavaScript 는 호이스팅시 초기화가 아닌 선언만 끌어올린다.
```javascript
// 예제1
var x = 1; // 초기화
console.log(x + " " + y); 
// ReferenceError: y is not defined
```

```javascript
// 예제2
var x = 1; // 초기화
console.log(x + " " + y); // 1 undefined
var y = 2;
```
위의 두 예제를 보면 y가 없을경우에는 에러가 발생하고 밑에 예제는 y 에 2라는 값으로 초기화를 시켜도 값이아닌 선언된 y 에 대해서만 호이스팅이 이루어지고있다.




> ## Event Bublling & Captureing

> ## Event 위임 패턴
