## class 와 객체

### Class

- 연관 있는 데이터를 한 곳에 묶어 놓는 컨테이너
- 전체적인 모습은 같지만 내부 구성요소의 값은 다를 수 있음

```JavaScript
// 클래스 선언
class Person {
    // field
    name;
    age;

    //method
    speak() {}
}

// 클래스 표현식 (익명)
const Rect = class {

};

// 클래스 표현식2 (이름지정)
const rectange = class Rectange {
    //...
}
```

#### 생성자
  - `constructor` 메서드를 사용한다.
```JavaScript
class Rectangle {
    constructor(height, width) {
        this.heigh = height;
        this.width = widt;
    }
}

const rectangle = new Rectangle(10, 20);
console.log(rectangle); // Rectangle (height: 10, width: 20)
```

#### 메서드
- class 내부 메서드는 `function` 키워드를 사용하지 않는다
```JavaScript
class Person {
    constructor(name,age) {
        this.name = name;
        thisage = age;
    }
    
    // class 내부 메서드 정의는 키워드가 필요 없다
    speak() {
        console.log(`${this.name}: hello !`);
    }
}
const person = new Person('park',30); // 인스턴스화
```

#### 겟터와 셋터

- `Getter/Setter` 는 `get` 과 `set` 키워드를 사용한다
- 키워드만 차이가 있고 `함수명`은 통일한다.
```JavaScript
class Rectangle {
    constructor(height, width) {
        this.height = height;
        this.width = width;
    }

    // 겟터와 셋터의 함수명은 통일한다
    get height() {
        return this._height;
    }

    set height(value) {
        this._height = value;
    }
}
```

### Object
- 주로 데이터 관리를 위해서 사용 `({"key":"value"})` 의 형태

- 초기화에는 두 가지 방법이 있다

```JavaScript
const obj = {};
const obj = new Object{};
```

#### 속성 접근
```JavaScript
const obj = {name: 'Mike', age : 20};

// 대괄호, Dot 연산자
console.log(obj.name) // 'Mike'
console.log(obj.age) // 'age'

// 속성 삭제
delete obj.hasJob;
```

- `in` 키워드 : `key`의 존재 확인

```JavaScript
const user = {
    name:'Bill',
    age:20,
    hasCar: true
}

console.log('name' in user); //true
console.log('age' in user); //true
console.log('random' in user); //false
console.log(user.hasCar); // true
```

#### 얕은 복사
  - 대입연산자를 사용하면 원치 않는 값이 변경될 수 있다.

```JavaScript
const user = {name: 'Bill', age:20};

// user 객체의 주소를 복사해 온다
const user2 = user;

// user가 참조하는 객체의 값을 초기화한다
user2.name = 'steve';

console.log(user.name); //steve
```

#### 깊은 복사
  - 방법1) for 루프를 돌면서 하나씩 할당
  - 방법2) `assign()` 을 사용한다
```JavaScript
const user = {name: 'Bill', age :20};

const user2 = {}; // 전혀 다른 객체에

// 방법1) 루프를 돌면서 key와 value를 할당해 준다
for (const key in user) {
    user2[key] = user[key];
}
user2.name = 'Steve';
console.log(user2);

// 방법2) assign 메서드를 사용한다
const user3 = {};

// Object class의 메서드로 존재한다.
Object.assign(user3,user);
user3.age = 30;
console.log(user3); //

console.log(user); // user2,3에 다른 값을 할당해도 변화가 없다
```

#### `module` import & export

- 외부로 함수를 공개할 것인지에 여부를 `export` 키워드를 이용해 구분한다

- `import` 하는 스크립트 에서는 
  `import {함수} from '경로'` 의 노테이션을 따른다.

```JavaScript
export function plus() {
    return 2+1;
}

// another script
import {plus} from './module.js'

console.log(plus());
```

- `export`
```JavaScript
export function plus() { // public
    return 2+1;
}

// 상수 export
export const height = 171.4;

// 변수 export with 값 변경
export let weight = 74.3;
weight = 76; // import 하여 출력하면 해당 값이 출력된다.

// public class
export class Animal {
    constructor(name) {
        this.name = name;
    }
}
```

- 모든 내용을 import 할때 와일드 카드를 사용한다. 이때 중괄호는 필요 없다

```JavaScript
import * as module from 'dir'
```

- `default` 키워드를 이용해 `import` 시 따로 표기하지 않아도 접근 가능하다
- `default` 키워드를 이용한 객체는 모듈당 한번이다. (여러개면 어떤 default에 접근할지 모른다)

```JavaScript
export default function() {
    return 'Default!'
}

import func from 'dir'
console.log(func());

import {default as func2 } from 'dir'
console.log(func2());
```