## JS 파일 적용하기

### HTML 내부

- `script` 태그를 이용해서 적용할 수 있다.

```html
<body>
    <p id="demo">text</p>
    <button type="button" onclick="change()">change</button>
    
    <script>
        fuction change() {
            document.querySelector("#demo").innerHTML = "Hello";
        }
    </script>
</body>
```

### 외부 파일 이용

- `.js` 확장자의 파일을 작성해서 적용한다

```HTML
<body>
    <p id="demo">text</p>
    <button type="button" onclick="change()">change</button>
    <!--소스코드 경로를 적당히 알려준다-->
    <script src="./src/01-02-script.js"></script>
</body>
```

### 출력 method 예시

`innerHTML` : HTML 요소에 출력

```JavaScript
function changeToHello() {
    // CSS 선택자에 맞는 첫 번째 요소를 선택
    // id가 demo인 id를 선택해서 변환
    document.querySelector("#demo").innerHTML = "Hello";
}
```

`window.alert()` : 경고창에 메세지 출력
```JavaScript
/* 경고창에 출력 */
function warningMessage(){
    window.alert("This is warning Message");
}
```

`document.write()` :  body에 내용 출력
```JavaScript        
/* body의 내용이 바뀐다. */
function changeBody(){
    document.write("body 내용이 바뀌었습니다.");
}
```

`console.log()` : 브라우저 콘솔에 내용 쓰기
```JavaScript        
/* 개발자 도구 콘솔창에 쓰기*/
function writeConsole(){
    console.log("hello world");
}
```

```JavaScript
/* 페이지 프린터로 연결 */
function printPage(){
    window.print()
}
```