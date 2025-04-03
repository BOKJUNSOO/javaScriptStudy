## 이벤트 핸들링

#### react 문법
이벤트 발생시 특정 함수 실행

- `HTML` DOM 이벤트
```HTML
<button onclick="activate()">
    Activate
</button>
<script>
    function activate() {

    }
</script>
```
`react` 이벤트에서 문법은 조금 차이가 있다
- onclick -> on**C**lick
- 함수명이 문자열에서 `{함수(변수)}`
```jsx
<button onClick={activate}>
    Activate
</button>
```

#### 함수 컴포넌트

- 화살표 함수 사용
```jsx
function Toggle(props) {
    const [isToggleOn, setIsToggleOn] = useState(true);

    const handleClick = () => {
        setIsToggleOn(!isToggleOn);
    }
    return (
        <button onClick={handleClick}>
            {isToggleOn? '켜짐':'꺼짐'}
        </button>
    );
}
```

#### Arguments 전달하기

- 이벤트 정보 전달

인자를 객체로서 받아들이는 방법
```jsx
<input 
    type='number'
    value = {inputData} // global 하게 사용
    onChange={(e)=>{
    const arg = e.target.value
    console.log(arg);
}}>
</input>
```

## 조건부 렌더링

어떠한 조건에 따라 렌더링이 달라지는 것

(ex) true: 버튼 보이기, false: 버튼 숨기기
```jsx
<button
    disabled={true}>
</button>
```

- 컴포넌트를 변수처럼 다루는 것
```jsx
function LoginControl(props) {
  const [isLoggedIn, setIsLoggedIn] = useState(false);
  const handleLoginClick = () => setIsLoggedIn(true);
  const handleLogoutClick = () => setIsLoggedIn(false);
  let button;
  if (isLoggedIn) button = <LogoutButton onClick={handleLogoutClick} />;
  else button = <LoginButton onClick={handleLoginClick} />;
  return (
    <div>
      <Greeting isLoggedIn={isLoggedIn} />
      {button}
    </div>
  );
}
```

#### 인라인 조건

if문과 동일한 효과를 내기 위해 && 논리 연산자 사용

```jsx
function LoginControl(props){
    return (
        <div>
            {
                data.map((v) => {
                    v.suer ? <h2>v.user.name</h2> : <h2>정보없음</h2>

                    // 삼항 연산자와 비슷하게 쓰일 수 있다
                    // v.user가 참이라면
                    v.user && <h2>v.user.name</h2>
                })
            }
        </div>
    );
}
```

## 폼

폼이란 `HTML` 파일을 서버로 보내기위한 형식이다.

`form 관련 태그`
- `<input>` : 사용자 입력을 받는 제어 컴포넌트(value 속성을 작성해 둔다면 남아있도록 구현가능)

    
- `<textarea>` : 여러줄로 입력받기 위한 태그
- `<select>` : 


