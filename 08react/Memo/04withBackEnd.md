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
- 이렇게 최소 생성되는 작업을 `mount` 라고 한다.
  - `update` 는 의존성 배열로 작업
  - `unmount` 소멸은 콜맥함수 내에 `return() => {}` 를 추가로 작성하면 가능하다.

```jsx
const Clock = () => {
  const [hours, setHours] = useState("00");
  const [minutes, setMinutes] = useState("00");
  const [seconds, setSeconds] = useState("00");
  
  useEffect(()=>{ // return : 랜더링 끝난 후 useEffect 동작
    getClock();
    setInterval(getClock,1000); // 최초 한번만 동작하지만 여러번 동작하는것 처럼 보이게 함
  },[]); // 괄호내의 준 어떤 값이 변경되어야 useEffect 다시 호출

  function getClock() {
    const clock = document.querySelector('#clock');
    const date = new Date();
    const hours = String(date.getHours()).padStart(2, "0");
    setHours(hours);
    const minutes = String(date.getMinutes()).padStart(2, "0");
    setMinutes(minutes);
    const seconds = String(date.getSeconds()).padStart(2, "0");
    setSeconds(seconds);
    // 해당 부분은 DOM을 계속해서 조작하기 때문에 react 스럽지 못하다
    // state 와 setter 를 쓰는 것이 바람직함
    //clock.innerText = `${hours}:${minutes}:${seconds}`;
  }

  return (
    <h2 id="clock">{hours}:{minutes}:{seconds}</h2>
  );
}
```

### movie 예제
- `onChange` 이벤트 속성을 이용하여 입력받은 데이터를 `setter`로 저장
- 버튼 클릭시 `getData` 를 실행
  - `getData` 를 이용하여 `json`을 파싱하고 필요한 값들을 저장
  - 저장한 값을 출력

해당 코드를 빌드하면 검색을 한번 눌렀을때 api 호출을 하지만 바로 랜더링 해주지 않는 오류가 발생했다.

```jsx
import styles from './MovieList.module.css';
import {useState} from 'react';

const MovieList = () => {
  const [movieTitle, setMovieTitle] = useState("");
  const [movieScore, setMovieScore] = useState("");
  const [openDate, setOpenDate] = useState("");
  const [overview, setOverView] = useState("");
  const [results, setResults] = useState("");
  const [poseter, setPoster] = useState();
  const [searchTerm, setSearchTerm] = useState("");

  const getData = async (query) => {
    const url = `https://api.themoviedb.org/3/search/movie?api_key=cba95d401a14ab806ffc13a5052aab89&query=${query}`;
    const res = await fetch(url);
    const data = await res.json();

    setResults(data.results[0]);
    setMovieTitle(results.title);
    setMovieScore(results.vote_average);
    setOpenDate(results.release_date);
    setOverView(results.overview);
    setPoster(results.poster_path);
  }
}

export default MovieList;
```

수정된 코드는 다음과 같다
이는 비동기적으로 처리되는 부분에서 생긴 문제이다.
```jsx
const MovieList = () => {
  const [movieTitle, setMovieTitle] = useState("");
  const [movieScore, setMovieScore] = useState("");
  const [openDate, setOpenDate] = useState("");
  const [overview, setOverView] = useState("");
  //const [results, setResults] = useState("");
  const [poseter, setPoster] = useState();
  const [searchTerm, setSearchTerm] = useState("");

  const getData = async (query) => {
    const url = `https://api.themoviedb.org/3/search/movie?api_key=cba95d401a14ab806ffc13a5052aab89&query=${query}`;
    const res = await fetch(url);
    const data = await res.json();

    if (data.results.length > 0) {
      const movie = data.results[0]; // ✅ 상태 업데이트 전에 변수에 저장
      setResults(movie);
      setMovieTitle(movie.title);
      setMovieScore(movie.vote_average);
      setOpenDate(movie.release_date);
      setOverView(movie.overview);
      setPoster(movie.poster_path);
    }
  };
}
```

### Kakao map 예제

`kakao api`를 호출해서 `Marker` 객체등을 생성했다.
해당 과정에서 api에 맞게 사용하기위해 참고를 하는데 오타로 인한 디버깅이 쉽지 않다.

특정 위치의`위도 경도` `api`를 파싱

```jsx
import './App.css';
import { useEffect, useRef } from 'react';

const { kakao } = window;
let ref = null;

const MapContainer = () => {
  ref = useRef();
  useEffect(() => {
    const container = document.getElementById('myMap');
    const options = {
      center: new kakao.maps.LatLng(33.450701, 126.570667),
      level: 3
    };
    const map = new kakao.maps.Map(container, options);
    ref.current = map; // global reference 변수에 값 할당

    // 마커생성
    const markerPosition = new kakao.maps.LatLng(33.450701, 126.570667);
    const marker = new kakao.maps.Marker({
      position: markerPosition,
    });
    marker.setMap(ref.current);

    // API 호출
    async function getData() {
      const url = 'https://ggoreb.pythonanywhere.com/location/data/?page=1&count=50';
      const res = await fetch(url);
      const data = await res.json();
      
      // 실제 위도 경도 parsing
      const list = data.data;
      console.log(list);
      list.map((v) => {
        const lat = v.latitude;
        const lng = v.longitude;
        console.log(lat,lng);
        var markerPosition = new kakao.maps.LatLng(lat,lng)
        var marker = new kakao.maps.Marker({
          position: markerPosition
        });
        marker.setMap(ref.current);
      })
      
      // 마커생성
      var markerPosition = new kakao.maps.LatLng(33.450701, 126.570667);
      var marker = new kakao.maps.Marker({
        posittion: markerPosition
      });
      marker.setMap(ref.current);
    }
    getData();

  }, []);

  return (
    <div id='myMap' style={{
      width: '500px',
      height: '500px'
    }}></div>
  );
}

function App() {
  return (
    <>
      <h1>Kakao Map</h1>
      <MapContainer />
      <button onClick={() => {
        var moveLatLon = new kakao.maps.LatLng(33.452613, 126.570888);
        // global 변수 참조
        ref.current.setCenter(moveLatLon);
      }}>이동</button>
    </>
  );
}

export default App;
```