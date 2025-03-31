## Array

#### 배열 초기화

```JavaScript
const arr1 = new Array();
const arr2 = [1,2];
```

#### 인덱스를 이용한 접근
```JavaScript
const alpha = ["a","b","c"];
console.log(animals.length);
console.log(animals[0]);
```

#### 반복문을 이용한 접근
```JavaScript
const alpha = ["a","b","c"];
// key 참조 with in
for (const key in alpha) {
    console.log(key);
}

// value 참조 with of
for (const value of animals) {
    console.log(value);
}
```

#### `forEach` + `callback ft`

- `forEach` 메서드 안에 콜백함수를 인자로 전달할 수 있다. 

```JavaScript
const alpha = ["a","b","c"];
alpha.forEach(function(v,index,array) {
    console.log(v,index,array);
});

// arrow function
alpha.forEach((v,index,array) => {
    console.log(v,index,array);
})
```

#### 배열의 메서드

- `push` : 배열의 마지막에 요소 추가
  
- `pop` : 배열의 마지막 요소 삭제

- `shift` : 배열의 처음 요소 제거

- `unshift` : 배열의 처음에 요소 추가

- 인덱스에 요소 추가 : `dynamic array`
```JavaScript
const alpha = ['a','b','c'];

alpha[4] = "e";
console.log(alpha); // ['a','b','c',undefined,'e']
```

- 탐색연산
`includes -> boolean, indexOf, find, filter, some, every`

- 기능 적용
  - 모든 요소에 접근하여 제어가 가능하다
`map` : 인자로 콜백함수를 받는다 // 맵핑
`reduce` : 인자로 콜백함수를 받는다 // 누적

- 합치기
`join` : 배열 -> 문자열
`concat` : 다수의 배열 -> 하나의 배열

- 분리
`split` : 문자열 -> 배열
`slice, splice` : 지정 요소가 삭제된 배열 생성

- 정렬
`sort` : 요소 값을 기준으로 정렬
`reverse` : 인덱스를 기준으로 역순 정렬

