## 변수

변수는 크게 `선언` 과 `할당(초기화)` 의 과정을 거친다.

- 변수의 선언

## 변수선언과 할당

### `키워드 없는` 변수 선언
- 키워드 없이 선언되는 변수는 암묵적으로 `global` 변수로 선언된다
- 블록 내부에서 전역변수의 초기화가 가능하다.
```JavaScript
title = 'this is global keyword';
{
    title = '글로벌 변수 초기화' // 조금 위험한 방법
}
console.log(title);
```

<br>

### `var` 키워드

- `var` 을 이용하여 선언한 변수는 `global` 하게 참조될 수 있다.
  - 이 역시 위험할 수 있다.

```JavaScript
let globalScope = 'global name';
{
    var name = 'javascript';
    console.log(name); // javascript
}
console.log(name); // javascript 
console.log(globalScope) // global name
```

<br>

- `var` 키워드를 이용해 선언된 변수 선언이 먼저 호이스팅 되어 런타임 이전에 실행된다.

- 그래서 아래와 같은 코드를 실행하면 언제나 `undefined` 를 반환한다.

```JavaScript
var test; // 변수선언
console.log(test) // undefined
```

<br>

- 또한 중복 선언이 가능하기 때문에 기존에 사용하던 `중요한`변수를 초기화하는 불상사가 발생할 수 있다.
```JavaScript
var a = 1;
var a = 100;
console.log(a) // 100 
```

### `let` 키워드

- `var` 키워드의 문제를 해결하기 위해 나온 키워드이다.

- 변수명은 `Identifier` 하게 선언하여야 한다.
  
- `let`을 이용하여 선언시 중복되는 변수명은 에러를 발생


```JavaScript
let title = '제목';
let title = '제목수정'; // SyntaxError
console.log(title);
```

- `let` 변수는 업데이트 될 수 있지만, 재선언이 불가능하다는 것이다.
```JavaScript
let title = '제목';
title = '제목수정'; // let으로 선언된 변수의 업데이트
console.log(title); // 제목수정
```

<br>

- `let` 을 이용하여 선언한 변수는 `local` 하게만 사용 가능하다.
- 이는 `let` 키워드는 블록범위 이기 때문이다.
- 블록 내에서만 독립적으로 사용할 수 있다.

```JavaScript
let globalScope = 'global name';
    {
        let name = 'javascript';
        console.log(name); // javascript
    }
console.log(name); // 아무것도 출력되지 않는다.
console.log(globalScope); // global name
```

- 당연하게 함수 스코프 내에서도 따로 관리하여 사용 가능하다.
```JavaScript
let name = "hi";
function print(){
    let name = "hello";
    console.log(name);
}
print(); // hello
console.log(name); // hi
```

### `const` 키워드
`const` 키워드는 `let` 키워드와 함께 `var` 키워드의 문제를 해결하기 위해 등장했다.

- 재선언도 불가능하고, 업데이트도 불가능하다
  - Java의 `static final` 과 비슷한 맥락이다.

```JavaScript
const title = '제목';
title = '제목수정';
console.log(title); // TypeError
```

### `hoisting`
`var` 과 같은 키워드로 선언된 변수는 선언문을 먼저 실행하여 문제가 생겼다. (할당되지 않은 변수가 `undefined`로 출력된다.)

또한 `let` 으로 변수를 선언 및 할당한 경우에 먼저 초기화 전에 해당 변수를 호출하면 컴파일러가 에러를 발생시킨다.

하지만 함수의 경우 컴파일러가 작동하는 과정에서 호출 시점에 함수를 스택에 추가하여 에러를 발생시키지 않는다.

```JavaScript
example()

fuction exampe(){
    console.log("this is okay")
}
```