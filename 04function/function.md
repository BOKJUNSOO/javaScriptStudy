## 함수

- 작업을 수행하기 위한 명령문의 집합
- 프로그램의 기본 구성 요소

```JavaScript
function name (par1, par2) {
    // body
    // ...
    return;
}
```

### `Parameter`

#### `스택`에 저장되는 기본 자료형

```JavaScript
function changeName(name) {
    name = 'tom';
}
const name = 'john';
changeName(name); // 함수 종료후 스택 삭제
console.log(name); // john
```

#### `힙`에 저장되는 객체

- 함수의 인자로 함수 내부의 동작으로 객체를 참조하여 어떤 값을 할당할 수 있다.

- 코드 실행 순서
  - 힙에 `user` 객체 할당
  - 함수호출, 함수 스택 생성
  - 함수 함수 내부에서 힙에 저장된 객체 참조
  - 객체에 어떤 값 할당
```JavaScript
function changeNameByObject(obj) {
    obj.name = 'tom';
}
const user = {name : 'john'};
changeNameByObject(user);
console.log(user); // {name : 'tom'}
```

- `default` 값 생성

```JavaScript
function showMessage(message, from='unkwon') {
    console.log(`${message} by ${from}`)
}

showMessage('Hi!'); // 두번째 인자를 전달하지 않아도 된다.
```

<br>

#### 가변인자
- `...` 를 앞에 붙혀 사용한다.

```JavaScript
function printAll(...args){
    
    // 입력받은 인자를 모두 출력
    for (let i=0; i< args.length; i++) {
        console.log(args[i]);
    }
}
```

<br>

#### `of`, `in` 키워드 , `forEach()` 메서드

- `of` 키워드
  - 객체가 `iterator` 속성을 가지고 있어야 사용할 수 있다.

- `in` 키워드
  - 모든 객체에 사용 가능하다.
  - `key` 에만 접근이 가능하고, `value`에 접근 가능하지는 않다.
  - `for in` 반복문은 객체의 모든 열거 가능한 `속성`에 대해 반복한다.

```JavaScript
function printAll(...args) {
    // of 키워드    
    for (const arg of args) {
        console.log(arg);
    }
}
```

- `forEach` 메서드
  - `Array` 객체에서만 사용하는 메서드이다.
  - 배열의 요소들을 반복하여 사용 가능하다.
  - 인자로 `callback` 함수를 등록할 수 있고, 요소들이 반복될때 마다 `callback` 함수가 호출된다.

```JavaScript
function printAll(...args){
    args.forEach((arg) => console.log(arg));
}
```

#### `return`

- return 이 실행되는 순간 함수스택이 삭제된다.
```JavaScript
function sum (a,b) {
    return a+b;
}
```