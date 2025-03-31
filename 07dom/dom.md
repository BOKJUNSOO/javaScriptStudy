## DOM (Document Object Model)

- 웹 브라우저가 HTML을 인식하는 방식
- document 객체와 관련된 객체의 집합
- HTML의 Tag를 자바스크립트에서 이용할 수 있도록 객체로 만든 것
- `Element Node` / `Text Node`

### 문서 객체 가져오기
`document.head` , `document.body` , `document.title`

```HTML
<head>
    <title>제목</title>
</head>
<body>
    <script>
        // 객체 속성 확인
        console.dir(document.head);
    </script>
</body>
```
### 문서 객체 생성
`OOP` 스러운 스크립트 작성

`document.body`와 같은 요소에는 직접 접근이 가능하지만
`h1` 태그 등에는 `querySelector`을 이용한다
```HTML
<body>
    <script>
        const h1 = document.createElement('h1'); // element node 생성
        const text = document.createTextNode("제목") // text node 생성
        
        h1.appendChild(text);
        document.body.appendChild(h1); // body 객체에 추가

        // += 기호를 쓰지 않으면 그대로 초기화 시킨다.
        // React에서 보통 쓰는 방식
        document.body.innerHTML += '<h1>제목2</h1>' // HTML 을 직접 작성하면서 추가
    </script>
</body>
```

### 코드 작성 순서

- `head` 태그가 생성되고 `body` 태그가 생성된다

```HTML
<!DOCTYPE html>
<html>

<head>
    <title>Document</title>
    <script>
        const h1 = (text) => `<h1>${text}</h1>`;
    </script>
    <script>
        // 해당 라인이 수행되지 않는다.
        document.body.innerHTML += h1('1번째 script 태그');
    </script>
</head>

<body>
    <script>
        document.body.innerHTML += h1('2번째 script 태그');
    </script>
    <h1>1번째 h1 태그</h1>
    <script>
        document.body.innerHTML += h1('3번째 script 태그');
    </script>
    <h1>2번째 h2 태그</h1>
</body>

</html>
```

- `DOMContentLoaded` 키워드 사용
```HTML
<!DOCTYPE html>
<html>

<head>
    <title>Document</title>
    <script>
        const h1 = (text) => `<h1>${text}</h1>`;
    </script>
    <script>
        // 웹 브라우저가 문서 객체를 모두 읽고 난 후 동작
        // body 가 생성되기 이전에 해당 라인이 실행됨
        document.addEventListener('DOMContentLoaded', () => {
            document.body.innerHTML += h1('h1 태그 추가');
        });
    </script>
</head>

<body>
    <h1>h1 태그</h1>
</body>

</html>
```

### 문서 객체 생성
`OOP` 스러운 스크립트 작성

`document.body`와 같은 요소에는 직접 접근이 가능하지만
`h1` 태그 등에는 `querySelector`을 이용한다
```HTML
<body>
    <script>
        const h1 = document.createElement('h1'); // element node 생성
        const text = document.createTextNode("제목") // text node 생성
        
        h1.appendChild(text);
        document.body.appendChild(h1); // body 객체에 추가

        // += 기호를 쓰지 않으면 그대로 초기화 시킨다.
        // React에서 보통 쓰는 방식
        document.body.innerHTML += '<h1>제목2</h1>' // HTML 을 직접 작성하면서 추가
    </script>
</body>
```
### Event

- 이벤트 처리 기본

`querySelector` + `addEventListener`
```JavaScript
// h1 객체를 클릭했을때 (event)
const h = document.querySelector('h1'); // 객체 선택
h.addEventListner('click', () => {
    h.style.backgroudColor = 'red';
});

window.addEventListener('resize', () => {
    console.log('resize');
});
```

- 제목을 클릭하면 클릭횟수 증가 후 출력하기
```HTML
<body>
    <h1>제목</h1>
    <h3>
        클릭 횟수: 0
    </h3>
</body>
<script>
    /* 마웃 드래그 방지 이벤트 */
    document.body.onselectstart = () => False;
    let count = 0;

    // 태그 객체를 일단 변수에 저장
    const h1 = document.querySelector('h1');
    const h3 = document.querySelector('h3');

    h1.addEventListener('click' ,() => {
        count +=1;
        // 해당 태그의 text 조정 (textContent는 string을 리턴한다)
        h3.textContent = `클릭 횟수 : ${count}`;
    });
</script>
```

- 버튼 클릭시 이벤트 (콜백함수 이용)

```HTML
<body>
    <div class="container">
        <div class="d-grid">
            <button type="button" class="button1">
                이미지 불러오기
            </button>
            <button class="button2">
                이미지 삭제하기
            </button>
        </div>
        <div class="target"></div>
    </div>
    <script>
        document.querySelector('.button1').addEventListener('click', () => {
            // <img> 라는 객체를 생성하고
            const img = document.createElement('img');

            // img 객체에 속성을 추가한다
            img.setAttribute('src', 'http://ggoreb.com/images/choco/1.jpg');

            // class 선택자 
            const target = document.querySelector('.target');
            target.appendChild(img);
        });
        document.querySelector('.button2').addEventListener('click', () => {     
            const images = document.querySelectorAll('.target img');
            images.forEach(img => img.remove());
        })
    </script>
</body>
```

- 키보드 이벤트

```HTML
<body>
    <h3>글자 수 : 0</h3>
    <input type="text" name="title" id="title">
</body>
<script>
    const h3 = document.querySelector('h3');
    const input = document.querySelector('input');

    // 키보드 이벤트
        // 눌렀던 키를 떨어질 때 실행 : keyup
        // 키가 입력되었을 때 실행 : keypress
        // 눌렀던 키를 떨어질 때 실행 : keyup
    input.addEventListener('keypress', function (event) {
        const length = input.value.length;
        h3.textContent = `글자 수 : ${length}`;
    });
</script>
```

- 각 항목의 선택값 출력하기


```JavaScript
const select = document.querySelector('select');
const checks = document.querySelectorAll('[type=checkbox]');
const radios = document.querySelectorAll('[type=radio]')
const button = document.querySelector('button')
button.addEventListener('click', () => {
    
    // 선택된 인덱스로 접근
    const index = select.options.selectedIndex;
    const sel = select.options[index].textContent;
    console.log(sel);
    
    // checkbox 
    // 객체 속성 접근으로 선택값 출력하기
    // console.dir(v) debugging
    radios.forEach((v) => {
        if (v.checked){
            //console.log(v.defaultValue);
            console.log(v.value);
        }
    });
});
// a 태그 링크막기
document.querySelector('a').addEventListener('click', (e) =>{
    e.preventDefault();
});
```

- 기본 이벤트 막기

`prventDefault`,`stopPropagation` : 기본적으로 콜백함수에 `event` 인자를 전달

```JavaScript
const imgs = document.querySelectorAll('img');
// 기본 이벤트 막기
imgs.forEach((img) => {
    // event 인자를 입력
    img.addEventListener('contextmenu', (event) => {
        event.preventDefault();
    });
});
```
