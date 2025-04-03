## 백엔드 통신

### `fetch() with Ajax code`
설계된 API를 프론트엔트에 호출하는 방법에는 여러가지가 있다.

그중 비동기로 작동되는 `fetch` 방법이 존재하는데 다음과 같이 작동할 수 있다.

`fetch` 는 비동기 방식으로 작동하기 때문에 요청에 대한 응답을 변수에 저장하는 과정에서 오류가 발생할 수 있다.(해당 함수의 호출을 기다리지 않고 다음 코드가 실행된다.)

따라서 호출에 대한 응답을 모두 기다린다는 의미의 `await` 키워드를 작성하여 해결할 수 있는데, 이 방식에는 `async` 키워드를 함수에 함께 작성해주어야 한다.

하지만 컴포넌트에는 `async`를 붙히지 않으므로(랜더링 과정에서 문제가 생긴다.) 새로운 함수를 정의하여 아래와 같이 사용할 수 있다.

```jsx
function App() {
  
  // response 레퍼변수에 담기
  // fetch 는 비동기 방식으로 동작 하므로 await 사용 
  // await 사용하려면 async 키워드 필요 
  // 그러나 컴포넌트에는 사용해선 안됨! 따라서 함수 하나 정의하기 or Axios 라이브러리 사용 가능
  const getData = async() => {
    const url ='http://ggoreb.com/api/toc.jsp';
    const res = await fetch(url);
    const data = await res.json(); // response의 속성중 json이 존재한다.
  };
  getData();
  return (<Component/>)
}
```

### `useEffect`

한번만 호출

```jsx
function App() {
  const [toc,setToc] = useState([]);

  const getData = async() => {
    const url ='http://ggoreb.com/api/toc.jsp';
    const res = await fetch(url);
    const data = await res.json();
    setToc(data);
  };
  
  // 한번 호출하고 객체 저장
  useEffect(() => {
    getData()
  },[]);

  return (
    // useEffect + setter로 가져온 리스트를 작성
    // 리스트 값 출력 => map + 콜백함수
    toc.map((v)=>{
      return <h3>{v.title}</h3>
    })
  )
}
```

### api 호출을 통한 복합문제 (weather)

- `react 컴포넌트`의 리턴값이 먼저 실행되어야 내부의 코드가 실행된다.
- **`useEffect`는 랜더링이 모두 된 이후에 동작한다!**

```jsx
import {useEffect,useState} from 'react';
import logo from './logo.svg';
import './App.css';

//component
const Clock = () => {
  useEffect(()=>{ // return : 랜더링 끝난 후 useEffect 동작
    getClock();
    setInterval(getClock,1000); // 최초 한번만 동작하지만 여러번 동작하는것 처럼 보이게 함
  },[]); // 괄호내의 준 어떤 값이 변경되어야 useEffect 다시 호출

  function getClock() {
    const clock = document.querySelector('#clock');
    const date = new Date();
    const hours = String(date.getHours()).padStart(2, "0");
    const minutes = String(date.getMinutes()).padStart(2, "0");
    const seconds = String(date.getSeconds()).padStart(2, "0");
    clock.innerText = `${hours}:${minutes}:${seconds}`;
  }

  return (
    <h2 id="clock">00:00:00</h2>
  );
}

```