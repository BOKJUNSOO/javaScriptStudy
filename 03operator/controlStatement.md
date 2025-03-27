## 제어문

- `조건문` , `for문 ` java와 문법이 동일하다

### `if / else if / else `

- 경우의 수가 작은 조건을 먼저 작성한다. (if 문 탈출조건)
- 여러 조건을 중복하여 작성시 `&&` 사용

```JavaScript
const job = 'programmer';
const name = 'junesoo';
// string type 은 heap에 객체를 생성하지 않으므로
// 객체간 주소비교와 차이가 존재 

// 여러 조건을 중복하여 작성시
// 부등호 비교도 마찬가지다.
if(job === 'programmer' && name ==='junesoo' ) {
    cosole.log('Welcome, Programmer!');
} else if (job === 'designer') {
    console.log('Good!');
} else {
    console.log('Unknown');
}
```


### `Date 라이브러리`

- 현재 시각에 따라 출력하는 내용 제어

```JavaScript
const date = new Date();
let hour = date.getHours();
let min = date.getMinutes();
let sec = date.getSeconds();

console.log("현재시각 :" + hour +":" + min + ":" +sec);

if (hour < 12) {
    console.log("아침");
} else if (hour < 18) {
    console.log("점심");
} else {
    console.log("저녁");
}
```

### `switch` 제어문

- switch에 인자로 어떤 값이 주어지면 해당 값이 일치여부를 판단한다.
- 조건으로 확인하는 객체가 정해져 있다면 `if` 문보다 효율적이다.
  - 코드 가독성등..
  - 범위 지정을 하지 못하므로 범위가 필요할 경우 `if` 문!
- `case` 에 존재하지 않는다면 `default` 를 실행한다.

- `break` 가 존재하지 않는다면 해당 `case` 를 진행하고 `switch` 문을 탈출하지 않는다.
    - 이는 `default` 문을 실행시키게 된다.

```JavaScript
const browser = 'IE';
switch(browser) {
    case 'IE':
        console.log('go away!');
        break; //break 필요
    case 'Chrome':
    case 'FireFox':
        console.log('love you!');
        break;
    default:
        console.log('same all');
}
```

### `navigator` 객체

- 웹에 접속할때 접속하는 수단을 제출하게 되어있다.
- 이에 `navigator` 를 활용하여 확인 가능하다.

```JavaScript
function getClient(){
    const userAgent = navigator.userAgent;
    console.log(userAgent);

    let os = '';
    
    // Android 문자열을 포함하고 있다면 (인덱스가 존재해서)
    if (userAgent.indexOf('Android') > -1) {
        os = 'Android';
    } else if (userAgent.indexOf('iPhone') > -1){
        os = 'iPhone';
    } else if (userAgent.indexOf('iPad') > -1) {
        os = 'iPad';
    } else if (userAgent.indexOf('Chrome') > -1) {
        os = 'Chrome';
    } else {
        os = 'ETC'
    }

    return os;
}
```

### `Math` 라이브러리의 `random` 함수

- `Math.random()` : 1미만의 양의 난수가 주어진다.

```JavaScript
const map = ['가위','바위','보'];

// 1미만의 양수값이 주어진다
const player = 1;
const com = parseInt(Math.random() * 3);
console.log(`player: ${map[player]}, com: ${map[com]}`);

let result = '';
function getResult() {
    if (player == com ) {
        result = '무승부';
    } else if (com == 0){
        result = 'player 승';
    } else if (com == 2){
        result = 'com 승';
    }
    return result;
}
    
getResult()
console.log(`결과 : ${result}`);
```

### `while` 제어문

- `while` 문의 조건식이 참인 경우에 블록 내부를 계속해서 실행한다.
  - 조건문을 갱신시키는 탈출문을 작성해 주어야 한다.

```JavaScript
let i = 3;
while(i>0) {
    console.log(`while: ${i}`);
    i--; // while 문 탈출 조건
}
```

- `do` 키워드와 함께 구현할 수도 있다.
  
```JavaScript
do {
    console.log(`do while: ${i}`);
    i--;
} while(i>0);
```

- 1에서 10 사이의 랜덤 숫자 맞추기
```JavaScript
const input = parseInt(Math.random() * 10 + 1);
// 탈출용 flag
let isContinue = true;
while (isContinue) {
    let number = prompt("숫자를 입력하세요.");
    if (input == number) {
        alert("정답");
        // 정답이므로 while 루프를 종료 (탈출)
        isContinue = false;
    } else {
        if (input > number) {
            alert("up");
        }
        if (input < number) {
            alert("down");
        }
    }
}
```

### `for` 제어문

- `for` 문은 (시작점; for문 condition; term)의 구조를 가지고 있다.
- `condition` 을 만족하는 동안 블럭내용을 수행한다.
- `term` 을 이용해 탈출 조건을 형성

```JavaScript
let i;
for(i=3; i>0; i--) {
    console.log(`for: ${i}`);
}
```

- for 구문 내부에서 변수선언과 함께 구성할 수 있다.
```JavaScript
for(let i =6; i>0; i -=2 ){
    console.log(`inline variable for : ${i}`);
}
```

- `for` 문은 중첩해서 사용할 수도 있다.

```JavaScript
for(let i = 0; i<3; i++) {
    for (let j = 0; j<3; j++) {
        console.log(`i:${i}, j : ${j}`);
    }   
}
```

