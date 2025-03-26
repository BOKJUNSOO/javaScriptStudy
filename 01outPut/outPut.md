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

`innerHTML`
    
- `document.getElementById(id)` 등을 사용하여 요소 선택후
- `innerHTML` 을 사용하여 문자열 출력

```HTML
<body>
    <h1>My First Web Page</h1>
    <p>My First Paragraph</p>
    <p id="demo"></p>
    <script>
        document.querySelector("#demo").innerHTML = 5+6;
    </script>
</body>
```

`document.write()`

- 테스트 목적으로 사용
- Popup 창에 내용을 독적으로 보여주기 위해 사용
- 기존 내용이 모두 삭제되므로 주의해서 사용

```HTML
/* body의 내용이 바뀐다. */
<button type="button" onclick="changeBody()">팝업</button>
<button type="button" onclick="documnet.write(5+6)">계산</button>

<script>
    function changeBody(){
        document.write("body 내용이 바뀌었습니다.");
    }
</script>
```

`window.alert()`

- 사용자에게 간단한 알림메세지 출력을 위해 경고 상자 사용
- `window` 키워드는 생략 가능하다.

```HTML

<h1>My First Web Page</h1>
<p>My first paragraph.</p>
<script>
    alert(5 + 6);
</script>
```

`console.log()`
- 디버깅을 위해서 사용한다
- 개발자가 연산 결과를 확인하기 위해서 사용

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