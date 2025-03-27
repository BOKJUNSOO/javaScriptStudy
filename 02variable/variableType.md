## 변수타입

### 1. `primitive`
더 이상 나눠지지 않는 하나의 값을 의미한다.

- `null, undefined, number, string, boolean`

`undefined` : 변수 선언은 되었지만 값이 할당되지 않았을때 또는 값이 주어지지 않았을때 자동 할당되는 값이다.

`null` : 아직 값이 없거나 비어 있는 값을 표현할 때 사용한다.

`number` : 정수, 실수 모두 `number` 타입으로 다룬다

- `typeof` 키워드를 통해 객체의 타입을 확인할 수 있다.

```JavaScript
const int = 17;
const float = 17.1;
console.log(typeof int) // number
console.log(typeof float) // number
```

- `parseInt` : 정수타입으로 바꿔준다
```JavaScript
let score = 90.5;
console.log(parseInt(score)); // 90
```

- `Number` : 넘버타입으로 바꿔준다.
```JavaScript
let string_ = "179";
console.log(typeof string_) // string
console.log(typeof Number(string_)) // Number
```

`string` 

- 문자열 타입은 덧셈 연산이 가능하다.
```JavaScript
const char = 'c';
const username = 'junesoo';

const greeting = 'hello' + username;
console.log('value : ' ${greeting}, 'type :' ${typeof greeting}); // bash 문법과 비슷하다
```

- 인덱스로 접근이 가능하고, 문자열 splice 연산을 제공한다
```JavaScript
const str = 'JavaScript';

// 인덱스로 접근
console.log(str[0]);
console.log(str[str.length-1]);

// splice 연산
console.log(str.substring(0,4));
console.log(str.slic(-6,str.length));

// 문자열 탐색 연산
console.log(str.indexOf('S'));

// 문자열 replace 연산
cosole.log(str.replace("Java", "자바")); // string을 리턴

// isin 함수
cosole.log(str.includes("v")); // bool type 리턴

// 스플릿 연산 => 문자열 리턴
console.log(str.split('S')); // Java,cript
```

### 2. `Reference`
primative 들을 관리하는 타입이다.

- `{} , [] , class`

### 3. `Function`
JavaScript에서는 함수를 `일급객체` 로 다룬다.
함수를 다른 변수와 같이 동일하게 다룰 수 있다. 