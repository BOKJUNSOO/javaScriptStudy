## 연산자

### 문자 연산자 : `+, +=`

```JavaScript
console.log("my" +"cat"); // my cat
console.log("1" + 2); // javascript 에서는 string으로 변환..
console.log(`string literals: 1+2 = ${1+2}`);

// 백틱의 이점
console.log(`string literals: 줄바꿈을 지원한다.
같은 문자열`);
```

<br>

### 산술 연산자 : `+ , - , * , / , % , ** `

<br>

### 증가,감소 연산자 : `++` ,`--` 의 위치에 따라 달라진다

```JavaScript
// 증가 연산자 (전위)
let counter = 2;
const preIncrement = ++counter;
// counter =  counter + 1;
// preIncrement = counter;
console.log(`preIncrement : ${preIncrement}`) // preIncrement : 3

// 증가 연산자 (후위)
const postIncrement = counter++;
// postIncrement = counter;
// counter = counter + 1;
console.log(`postIncrement : ${postIncrement}`) // preIncrement : 3
```

### 대입 연산자 (`+=`,`-=`,`*=`...)

<br>

### 논리 연산자 (`&&`,`||`,`!`)

<br>

### 비교 연산자 (`==`,`!=`,`<=`, `>=`)

- heap에 할당된 객체 수준의 비교는 주소를 비교한다.

```JavaScript
const stringFive = "5";
const numberFive = 5;

// 느슨한 비교 자료형 자동 변환
// stack 영역
console.log(stringFive == numberFive); // true

// 엄격한 비교
console.log(stringFive === numberFive); // false

// 객체 주소를 비교
const dev1 = {name : "dev"};
const dev2 = {name : "dev"};
console.log(dev1 == dev2); // false

// 할당시 레퍼런스 변수의 주소가 복사된다.
// 힙 영역에 할당된 같은 객체를 가르킨다.
const dev3 = dev2;
cosole.log(dev3 == dev2); // true
```

### 삼항 연산자 (`? :`)

```JavaScript
// 물음표 앞에 조건이 온다!
// true 시 1번째 elt, 아니라면 2번째 elt
let user_id = 'script';
console.log(user_id === 'script' ? 'yes' : 'no');
```


