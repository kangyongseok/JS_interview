FontEnd Interview Question & Answer
===

> ## null 과 undefined의 차이
명시적으로 undefined 를 사용하지는 않는다. 그러나 null 은 객체를 사용해야 하지만 해당 객체를 이용할 수 없을때에는 항상 그자리에 null 이 와야한다. 이러한 규칙을 지키면 undefined 와 구분이 가능하다.
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
클로저란 다른 함수의 스코프에 있는 변수에 접근 가능한 함수를 말한다. 이는 익명함수와는 다르다. MDN의 정의에 따르면 클로저함수는 만들어진 환경을 기억한다 라고 한다. 
```javascript
function createClosure() {
    var name = "CodeReading";
    return function(hello) {
        return hello + name;
    };
}

var closure = createClosure();
console.log(closure("Hello ")) // Hello CodeReading
```
createClosure() 는 함수를 반환하고 그 함수는 createClosure() 함수 내에있는 변수를 참조하여 리턴하고 있다. 

```javascript
function example(hello) {
    var name = "CodeReading";
    hello + name;
}

console.log(example("Hello")) // undefined
```
example() 예제에서는 함수를 실행해도 undefined 값만 나오게 된다. 

반환해주는 값도 내부에서 참조해서 값을 계속 유지해주는 환경이 없기때문이다.

원래 함수는 실행이 끝남과 동시에 파괴되는것이 정상이지만 클로저 함수는 메모리에서 없어질떄까지 계속 남아있고 그 결과 값이 따라다닌다.

* 클로저는 다른 함수 안에서 정의된 함수. 따라서 클로저는 외부함수의 변수에 접근가능
* 클로저의 스코프 체인에는 자기자신과 외부함수, 전역 컨텍스트의 변수객체가 담긴다.
* 일반적으로 함수가 실행을 마치면 함수의 스코프 및 그에 담긴 변수 전체가 파괴된다.
* 함수가 클로저를 반환했다면 해당 함수의 스코프는 클로저가 존재하는 동안에는 메모리에 계속 존재 (메모리의 누수 발생)
* JavaScript 에서는 블록레벨스코프 라는 개념이 없어서 블록문장에서 정의한 변수는 해당 문장이 아니라 외부 함수에 묶인다.
    ```javascript
    function outputNumbers(count) {
        for(var i = 0; i < count; i++) {
            alert(i); // 0, 1, 2, 3, 4
        }
        alert(i) // 5
    }
    outputNumbers(5);
    ```
* 클로저를 사용하면 블록스코프를 흉내낼수 있음
    ```javascript
    function outputNumbers(count) {
        (function() { // 즉시실행함수 끝나면 파괴
            for(var i = 0; i < count; i++) {
                alert(i); 
            }
        })(); // 0, 1, 2, 3, 4 

        alert(i) // ReferenceError: i is not defined
    }
    outputNumbers(5);
    ```
* 함수를 생성하는 즉시 호출하면 내부의 코드를 실행하지만 그에 관한 참조는 남지않음
* 결과적으로 함수에서 사용한 변수는 모두 파괴되는데 외부스코프의 특정 변수로 설정된 변수는 예외
* 클로저를 활용하면 외부 스코프에 정의된 변수에 접근 가능한 공용 메서드 구현가능
    ```javascript
    function Person(name) {
        this.getName = function() {
            return name;
        };

        this.setName = function( value ) {
            name = value;
        };
    }
    
    var person = new Person("CodeReading");
    console.log(person.getName()); // CodeReading
    person.setName("Kang");
    console.log(person.getName()); // Kang
    ```

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

최신 JavaScript 문법에서는 let 이란 변수를 사용함으로써 이러한 예외적인 상황에 대해서 방지가 가능하게 되었다. 따라서 최근에는 var 가 아닌 let 으로 변수를 선언할 것을 권장하고 있다.

```javascript
// 예제3
let x = 1; // 초기화
console.log(x + " " + y); 
let y = 2;
// ReferenceError: y is not defined
```

> ## Event Bublling & Captureing


> ## Event 위임 패턴
이벤트위임은 다수의 자식 요소에 각각 이벤트 핸들러를 바인딩 하는 대신 하나의 부모요소에 이벤트 핸들러를 바인딩하는 방법이다.

**HTML**
```html
<ul>
    <li id="list-1">event #1</li>
    <li id="list-2">event #2</li>
    <li id="list-3">event #3</li>
    <li id="list-4">event #4</li>
    <li id="list-5">event #5</li>
    <li id="list-6">event #6</li>
</ul>
```

**JAVASCRIPT**
```javascript
eventPrint = (e) => {
    console.log(e.target.id)
}
document.querySelector('#list-1').addEventListener('click', eventPrint)
document.querySelector('#list-2').addEventListener('click', eventPrint)
document.querySelector('#list-3').addEventListener('click', eventPrint)
document.querySelector('#list-4').addEventListener('click', eventPrint)
document.querySelector('#list-5').addEventListener('click', eventPrint)
document.querySelector('#list-6').addEventListener('click', eventPrint)
```
위의 예제처럼 모든 li 요소가 클릭 이벤트에 반응하는 처리를 구현하고 싶은경우 li 요소에 이벤트핸들러를 바인딩하여 총 6개의 이벤트 핸들러를 바인딩 해 주어야 한다.

만약 이 목록이 100개라면 100개의 바인딩을 해줘야 하는것이다.

이것은 실행속도 저하의 원인이 되고, 코드 또한 매우 길어지며 작성도 불편하고 가독성도 떨어지게 된다.

**HTML**
```html
<ul id="parent-list">
    <li id="list-1">event #1</li>
    <li id="list-2">event #2</li>
    <li id="list-3">event #3</li>
    <li id="list-4">event #4</li>
    <li id="list-5">event #5</li>
    <li id="list-6">event #6</li>
</ul>

<script>
    document.querySelector('#parent-list').addEventListener('click', 
      function(e) {
          console.log(e.target.id + " 가 클릭 되었습니다.");
      })
</script>
```

위의 예제에서는 부모요소에 바인딩을 해주었기때문에 더이상의 추가 스크립트 작성은 불필요하고 li 요소가 추가되어도 별다른 추가 코드는 작성하지않아도 잘 작동하게 된다. 

이것은 이벤트 흐름에 의해 영향을 미치기 때문에 가능한 것이다.