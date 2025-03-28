## `Advanced Fuction`

### Fist-class Fuction
JavaScript 에서 함수는 일급객체로 다뤄진다. 이에

- 함수를 `변수처럼` 처리가 가능하고

```JavaScript
const func = function() {};
```

- 변수에 값으로 `할당`이 가능하고

```JavaScript
const show = func; // show 라는 레퍼런스 변수에 func 함수를 저장
show();
```

- 함수를 다른 함수의 `인자`로 사용하고

```JavaScript
function action(f) {
}
action(func);
```

- 다른 함수를 함수의 return으로 사용 가능하다.
```JavaScript
function outer() {
    return function () {
        
    }
}
```

### callback
- 일정시간 경과 후 동작
  - 함수를 인자로 넘긴다!
  - 나중에 불려지는 함수라하여 `callback` 함수라고 지칭한다.

```JavaScript
function callback() {
    const label = document.querySelector('.label');
    label.innerHTML = '<h2>모습 변경</h2>';

    const figure = document.querySelector('.figure');
    figure.style.backgroudColor = 'red';
    figure.style.borderRadius = '100px';
}

setTimeout(callback, 2000);
```

### 함수 작성 형태

- 선언식
```JavaScript
funcA();
funcB();

function funcA() {
    console.log("java");
}

// 표현식
const funcB = function() { // error 호이스팅이 이루어짐
    console.log('script');
}
```
- 선언식과 표현식의 우선순위 (`const` 가 호이스팅에 의해 초기화 된다)
```JavaScript
const funcA = function() 
{
    console.log('script');
};

function funcA(){
    console.log('java');
}

funcA(); // java가 아닌 script 가 출력됨에 유의
```

### Arrow Function
- `=>`  표현식을 사용해 함수 작성이 가능하다.

```JavaScript
const simplePrint = function() {
    console.log('simplePrint!');
}

// 2번째 방식
const simplePrint = () => console.log('simplePrint!');

// 3번째 방식
const simplePrint = () => {
    console.log('simplePrint!');
}

// 항상 익명
// 파라미터가 1개인 경우 () 생략 가능
const minus = a => console.log(a);
minus(1);


```
### Closure

- 호출이 종료되고 삭제된 함수스택 내의 로컬변수를 살리는 방법

```JavaScript
function 함수1() {
    let 지역변수 = 10;
    return function() {
        지역변수 ++;
        console.log(지역변수);
    }
}
let a = 함수1(); // a는 함수1의 리턴을 가지므로 함수이다.
a(); // a를 호출할 때마다 지역변수 10을 초기화 시키는 것이 아니고 객체로서 저장한다.
```

- closure 활용
```JavaScript
function sequence() {
    let seq = 0;
    return function () {
        seq++;
        return seq;
    };
}
const check = sequence();
window.addEventListener('blur', () => {
    const count = check();
    if (count > 2) {
        alert('시험 종료!');
        window.close();
    }
});
```
