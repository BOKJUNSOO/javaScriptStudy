## Hook

`클래스 컴포넌트`에서 지원되는 생명주기 관련 기능을 `함수 컴포넌트`에서도 사용할 수 있게 지원해주는 기술이다.


- 원래 존재하는 기능에 갈고리를 거는 것처럼 `끼어들어 실행`
- `Hook` 함수들은 모두 `use`로 시작한다.

### `useState`
- 컴포넌트의 상태를 관리하기 위해 사용
- 배열 형태의 반환 값을 가지며, 
  `첫번째 요소`는 현재의 상태값, `두번째 요소`에는 `setter`가 위치한다.

핵심은 `onClick`을 이용하여 `state`를 갱신할 때마다 `header` `만` 다시 랜더링 된다는 것을 유의하자.

```jsx
import {useState} from 'react';
function Header(props) {
    const [count,setCount] = useState(1)
    
    function click(e) {
        alert(e.target.innerText);
    }

    return (
        <header>
            <h1 onClick={click}>{props.title}</h1>
            <p onClick={() => { // 클릭할때마다 header가 다시 렌더링
                setCount(count+1);
            }}>{props.desc} {count}</p>
        </header>
    );
}
export default Header;
```
---
### `useEffect`
아래와같은 상황이 컴포넌트를 사용하면서 발생할 수 있다.

```jsx
const 서버데이터 =[]; // <== 랜더링을 새로하면 받은 데이터 초기화

const [serverData, setServerData] = useState(); // 서버 데이터를 받아올 때마다 랜더링? stackOverFlow
```


이때 `useEffect` 훅을 사용한다면 초기 랜더링을 제외하고 

어떤 컴포넌트가 리 랜더링 되어도 해당 블록 내에서 `useEffect` 내의 함수를 실행시키지 않는다.

사용 시에는 함수를 랩핑하는 방식으로 사용한다

**이때 `의존성 배열` 에 `[]`를 작성해 놓으면 되고, 변수에 의존**


```jsx
console.log('header');

// useEffect(함수, 의존성 배열)
useEffect(()=>{
    console.log('처음에만 실행!');
},[])

// useEffect도 여러번 사용이 가능하다. 
useEffect(()=>{
    console.log('count가 바뀔때 실행');
},[count]) // count라는 변수를 감시한다
```

실행흐름 - `life cycle`

- 처음 컴포넌트가 생성될 때 `mount`
- 어떠한 변수`state`가 변경될 때 `update`
- 컴포넌트가 소멸될때 `unmount`
- `setInterval` (polling)

```jsx
//App.js
function App() {
  const [hide, setHide] = useState(false);
  return (
    // 컴포넌트를 App 함수 내에서 실행
    // title 인자로 WEB을 전달
    <div className="App">
      <button onClick={() => {
        setHide(true);
      }}>숨기기</button>
      {/*삼항 연산으로 Header 숨기기*/}
      {
        hide ? //if 문을 못쓰므로 삼항연산자로 처리
        null :
        <Header {...headerProp}/>
      }
    </div>
  );
}
export default App;

//Header.js
import {useState, useEffect} from 'react';
function Header(props) {
    const [count,setCount] = useState(1)

    // useEffect(함수, 의존성 배열)
    useEffect(()=>{
        console.log('처음에만 실행!');
        return() => {
            console.log('header 소멸');
        }
    },[])

    function click(e) {
        alert(e.target.innerText);
    }

    return (
        <header>
            <h1 onClick={click}>{props.title}</h1>
            <p onClick={() => { // 클릭할때마다 header가 다시 렌더링
                setCount(count+1);
            }}>{props.desc} {count}</p>
        </header>
    );
}
export default Header;
```
### `useMemo`

- `값`을 기억 (의존성 배열의 변수 값이 변하지 않으면 현 상태를 유지)
  
- `Memorized value`를 리턴하는 Hook 이다.

### React.memo
- `컴포넌트 기억`을 위해 사용한다.(재생성x)
```jsx
// Parent의 state가 바뀌면서 Child 새로고침
const Child = (props) => {
  console.log(`🔁 Child 렌더링 ${props.value}`);
  return <h2>Child</h2>;
};

// Parent의 state가 바뀌면서 Child 새로고침되어야 하지만
// React.memo의 사용으로 새로고침되지 않음 (props가 바뀌지 않는 한)
const Child = React.memo((props) => {
  console.log(`🔁 Child 렌더링 ${props.value}`);
  return <h2>Child</h2>;
});
```

- `useCallback` : `함수를 기억`하는 기능이 있다
```jsx
// Parent의 state가 바뀌면서 Child 새로고침
// handleClick 함수 항상 다시 생성
const Child = (props) => {
  console.log(`🔁 Child 렌더링 ${props.value}`);

  const handleClick = () => console.log('자식 버튼 클릭');
  useEffect(() => {
    console.log('handleClick 새로 생성');
  }, [handleClick]);
  
  return (
    <div>
      <h2>Child</h2>
      <button onClick={handleClick}>자식 버튼</button>
    </div>
  );
};


// Parent의 state가 바뀌면서 Child 새로고침
// useCallback 사용으로 handleClick 함수 다시 생성하지 않음
const Child = (props) => {
  console.log(`🔁 Child 렌더링 ${props.value}`);

  const handleClick = useCallback(() => console.log('자식 버튼 클릭'), []);
  useEffect(() => {
    console.log('handleClick 새로 생성');
  }, [handleClick]);
  
  return (
    <div>
      <h2>Child</h2>
      <button onClick={handleClick}>자식 버튼</button>
    </div>
  );
};
```
(결론) `useMemo`,`useCallback`을 함께 쓰는 것이 효율적

---

`useRef`
- 컴포넌트의 특정 상태에 직접 접근할 수 있는 객체
- 컴포넌트 단위로 값을 직접 저장하거나 변경 가능
- `state`와 다르게 값을 변경하더라도 다시 랜더링 되지 않음
- `document.querySelector()`를 이용하여 `DOM 요소`에 접근