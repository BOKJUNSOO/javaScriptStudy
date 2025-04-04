## 컴포넌트간 변수 전달

서로다른 컴포넌트 사이에서는 해당 블록에 존재하는 변수를
다른 변수로 전달하는 것이 어렵다.`reducks` 사용하면 가능하긴함.

그러므로 `하위컴포넌트의 값을 먼저 상위 컴포넌트로 보내고`

상위컴포넌트에서 받은 값을 `props`로 하위 컴포넌트에 전달한다.

```jsx
import './App.css';
import styles from './App.module.css';
import {useState} from 'react';

function Title() {
  return (
    <div className='title'>
      <h1>가위 바위 보 게임</h1>
    </div>
  );
}
function Scissors(props) {
  return (
    <div className={styles.control} 
          onClick={()=>{
            // click 이벤트시 인자로 받은 props의 속성 함수 실행
            props.send(0);
          }}>
      <img src='http://ggoreb.com/images/react/scissors.png' />
    </div>
  );
}
function Rock(props) {
  return (
    <div className={styles.control} 
         onClick={() =>{
          props.send(1);
         }}>
      <img src='http://ggoreb.com/images/react/rock.png' />
    </div>
  );
}
function Paper(props) {
  return (
    <div className={styles.control}
          onClick={()=>{
            props.send(2);
          }}>
      <img src='http://ggoreb.com/images/react/paper.png' />
    </div>
  );
}
function Result(props) {
  return (
    <div className='result'>
    
      <h1>Com:{props.result.컴퓨터}</h1>
      <h1>Player:{props.result.플레이어}</h1>
      <h1>{props.result.결과}</h1>
    </div>
  );
}
function App() {
  const [result , setResult] = useState({}); // useState 결과 저장
  const send = (value) => {
    const com = parseInt(Math.random() *3);
    if (value+1 ==com) {
      setResult({
        컴퓨터:com,
        플레이어:value,
        결과:'com 승리'
      })
    } else if(com == value) {
      setResult({
        컴퓨터:com,
        플레이어:value,
        결과:'무승부'
      })
    } else {
      setResult({
        컴퓨터:com,
        플레이어:value,
        결과:'player 승리'
      })
    }
  }
  return (
    <div className="App">
      <Title />
      <Scissors send={send}/>
      <Rock send={send}/>
      <Paper send={send}/>
      <Result result={result}/>
    </div>
  );
}

export default App;
```