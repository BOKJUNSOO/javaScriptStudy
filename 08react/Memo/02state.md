## State

`State`는 

`react`에서는 버튼 상태가 변경되거나 이벤트가 발생하면 `HTML`의 어떤 값을 변경시키는 것이 아니라 `필요한 부분만` 리랜더링 된다.
즉 컴포넌트가 다시 실행되는 것인데,

컴포넌트 내의 변수를 단순히 `let`으로 설정한다면 컴포넌트가 다시 호출되어 `상태가 초기화` 되게 된다.

이때 적용할 수 있는 것이 `state`이다. 이는 컴포넌트가 자체적으로 가지는 데이터로 변경 가능한 데이터이다.

```jsx
import { useState } from 'react';
// setState는 state에 접근할 수 있는 전용셋터이다.
const [state, setState] = useState('Initializar');
const [list, setList] = useState(['HTML','CSS','JavaScript']);
```


- `state`를 변경하면 해당 `state`와 관련된 컴포넌트는 다시 렌더링 된다.

- `state`에 저장된 값은 해당 컴포넌트가 다시 랜더링 되어도 계속 기억된다.

- 이에 어떤 이벤트를 발생시켰을때 값을 기억할 요구가 있을때 사용한다.

### useState

`useState` 함수가 제공하는 상태 변수와 업데이트 함수를 사용한다

리액트는 하위 컴포넌트가 변경되면 해당 부분만 수정

- `let`으로 선언한 변수와 `state` 의 차이를 확인
```jsx
import {useState} from 'react';
function Nav(props) {
    const [count, setCount] = useState(0); // 값 초기화
    let count2 = 0;
    console.log("Nav 생성");
    return(
        <nav>
            <button onClick={() => {
                count2++;
                setCount(count+1);
            }}>증가{count} {count2}</button>
        </nav>
    );
}

export default Nav;
```
### 이벤트 처리

`state` 는 상태를 저장하고 있기 때문에 해당 부분을 사용하는 컴포넌트만 다시 랜더링 된다는 장점이 있고,

이점을 살려 어떤 이벤트를 처리하는 것에 이점이 있다.

#### 추가 기능

`Props`라 하면 상위 컴포넌트`App` 으로부터 인자를 받아 하위 컴포넌트에 파라미터처럼 전달을 하는 역할이다.
하지만 하위 컴포넌트로 부터 인자를 직접 입력받는 경우도 있을 것이다.
#### 삭제 기능
#### 수정 기능

#### 
```jsx
// 콜백함수를 외부에 정의
// 다시 클릭하면 지워지도록 구현
const handleClick = (e) => {
  e.target.style.backgroundColor = 'beige';
  e.target.style.textDecoration = 'underline';
}
function Footer(props) {
  return (
    <footer>
      {
        props.footers.map((v, i) => {
          return <h5 key={i} onClick={handleClick}>{v}</h5>
        })
      }
    </footer>
  );
}
export default Footer;
```