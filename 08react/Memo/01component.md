## 리액트 컴포넌트

### 리액트 어플리케이션

컴포넌트 작성 >> `App.js` 구조화 >> `index.js` 랜더링 >> `index.html`

이는 합성함수라고 생각하면 이해하기 편하다

### Function Component

리액트 컴포넌트는 일련의 규칙을 따른다.
- 함수처럼 작성하되 첫글자는 무조건 대문자로 작성한다.
  - 상위 컴포넌트의 태그 역시 대문자로 작성한다

- `return` 값으로 `html`을 작성한다

  - `하나의 컴포넌트는 **반드시** 하나의 부모태그`로 감싸 사용한다(여러개를 반환하지 못한다!)

```JavaScript
// 컴포넌트 파일
function Header() {
    return (
        <header>
            hello world!
        </header>
    );
}
```
작성한 컴포넌트를 `App.js` 에서 import 해와 사용한다
```JavaScript
//App.js
function App(){
    return(
    // 컴포넌트를 App 함수 내에서 실행한다
    <div className='App'>
        <Header></Header>
    </div>
    );
}
```

### Props
Props는 엘리먼트가 생성될 때 전달되는 값이다.

리액트 컴포넌트의 `prop` 를 인자로 제출하고 `리액트 엘리먼트`를 리턴 받는 방식을 사용한다.

`prop`의 특징은 다음과 같다
- 읽기전용 (Read-Only)
- 엘리먼트가 생성된 이후 `Props`는 변경 불가 하다
- 값을 변경하면 컴포넌트를 사용하여 새로운 앨리먼트를 생성한다

`Props`는 다음과 같이 사용한다
- **키와 값으로 이루어진 형태**로 컴포넌트에 전달한다
- 이는 자바스크립트의 `객체`에 해당한다

#### 상위컴포넌트에서 하위컴포넌트 
핵심은 상위 컴포넌트인 `App`의 인자가 객체 형식으로 하위 컴포넌트에 전달을 한다는 것이다.

하위 컴포넌트는 객체로서 인자를 받고 키-벨류 형식의 접근방법을 사용한다

이때 `jsx` 에서 `{}` 중괄호를 사용해줘야 `JavaScript` 문법 사용이 가능해져 `read` 가 가능하다
```JavaScript
import logo from './logo.svg';
//import './App.css';

// 컴포넌트 코드 작성
// 첫글자는 반드시 대문자
function Header(props) {
  console.log(props) //props 는 js 객체이다
  return (
  // jsx 내에서 js를 사용하려면 중괄호를 사용해야 한다
  <header>
    <h1>{props.title}</h1>
    {props['desc']}
  </header>
  );
}

function Nav(props) {
  // return이 없으면 컴포넌트가 아니다
  return(
    <nav>
      <ul>
        <li><a href={props.link1}>HTML</a></li>
        <li><a href={props.link2}>CSS</a></li>
        <li><a href={props['link3']}>JavaScript</a></li>
      </ul>
    </nav>
  );
}

function App() {
  return (
    // 컴포넌트를 App 함수 내에서 실행
    // title 인자로 WEB을 전달
    <div className="App">
      <Header title='WEB' desc ='World Wide Web!'></Header>
      <Nav link1='1.html' link2='2.html' link3 ='3.html'></Nav>
    </div>
  );
}

export default App;
```

#### nested object (스프레드 연산자)


- `App` 컴포넌트
- `comment` 컴포넌트

`comment` 컴포넌르를 확인해보면 `props`로 주어진 객체가 `nested` 한것으로 확인이 된다.(props-> author속성 -> avatarUrl 속성)

nested 한 객체를 인자로 입력할때 스프레드 연산자를 사용할 수 있다.



```jsx
const headerProps = {
  title:"WEB",
  desc:"World wide Web!"
};
// nested obj
const commentProps = {
  author:{
    'avatarUrl':'A',
    'name': 'b'
  }
};

function Comment(props) {
  return (
    <div className="comment">
      <div className="user-info">
        <img className="avatar"
          src={props.author.avatarUrl}
          alt={props.author.name}
        />
        <div className="user-info-name">
          {props.author.name}
        </div>
      </div>
      <div className="comment-text">
        {props.text}
      </div>
      <div className="comment-date">
        {props.date}
      </div>
    </div>
  );
}

function App() {
  return (
    // 컴포넌트를 App 함수 내에서 실행
    // title 인자로 WEB을 전달
    <div className="App">
      {/* 스프레드 연산자 사용 */}
      <Header {...headerProps}></Header>
      <Nav link1='1.html' link2='2.html' link3 ='3.html'></Nav>
      {/*컴포넌트에서 nested한 객체를 참조하려 하므로*/
      /*컴포넌트에 전달할 인자의 형태를 미리 정해주어야 에러가 발생되지 않는다.*/}
      <Comment {...commentProps}></Comment>

      <Avatar user={
        {
          'avatarUrl':'a',
          'name':'b'
        }
      }>
      </Avatar>
    </div>
  );
}
```

##### 모듈화 

`App.js`에 모든 컴포넌트를 작성하면 관리가 쉽지 않고 코드 가독성도 매우 떨어질 것이다. 

이에 `Header` 라는 컴포넌트를 작성할 `Header.js` 스크립트를 생성하여 관리한다
```jsx
function Header(props) {
    console.log(props);

    return (
        <header>
            <h1>
                {props.title}
            </h1>
            {props.desc}
        </header>
    );
}
export const headerProps ={
    'title':'introduce',
    'desc':'hi2'
}
export default Header;
```
`App.js` 스크립트에서 `import` 하는 방식으로 컴포넌트를 관리할 수 있을 것같다.

이때 따로 인스턴스화의 과정이 필요 없다는 점에 유의하자
```jsx
// 컴포넌트 import
import Header from './Header';
// 컴포넌트에 넘겨줄 인자
import { headerProps } from './Header';

function App() {
  return (
    <div className='App'>
      <Header {...headerProp}/>
    </div>
  );
}
```

### `App`의 list 데이터를 `Nav` 목록으로 전달
- `Nav` 컴포넌트

아래의 코드중 `props.list` 로 접근하는 것 역시 위에서 언급한 속성접근과 문법이 같음을 알 수 있다.
```jsx
function Nav(props) {
    return(
        <nav>
            <ul>
                {   // 자바스크립트 문법 쓸때는 중괄호 내부에 작성!
                    props.list.map((item, index) => {
                        return <li><a href={`${index+1}.html`}>{item}</a></li>
                    })
                }
            </ul>
        </nav>
    );
}

export default Nav;
```
- `App` 컴포넌트
```jsx
import './App.css';
import Nav from './Nav';

function App() {
  const list = [
    'HTML','CSS','JavaScript'
  ]
  return (
    <div className="App"> 
      <Nav list={list}></Nav>
    </div>
  );
}

export default App;
```

- 연습문제

```jsx
import logo from './logo.svg';
//import './App.css';
import Header from './Header';
import Footer from './Footer';
import Section from './Section';
import Article from './Article';
import Nav from './Nav';

function App() {
  const list = [
    'HTML','CSS','JavaScript'
  ]
  const sections = [
    '사용되는 숫자는 0에서 9까지 서로 다른 숫자이다.',
    '숫자는 맞지만 위치가 틀렸을 때는 볼.',
    '숫자와 위치가 전부 맞으면 스트라이크.',
    '숫자와 위치가 전부 틀리면 아웃. "틀렸다"는 게 중요하다.',
    '물론 무엇이 볼이고 스트라이크인지는 알려주지 않는다.'
  ]
  const footerArr = [
    '. 830 - 들어맞는 숫자가 아예 없으므로 아웃. 이때부터 0, 3, 8이 후보에서 빠지므로 남는 숫자는 1, 2, 4, 5, 6, 7, 9다.',
    '. 659 - 6이 있지만 위치가 다르므로 1볼. 게임 상으로는 어떤 숫자가 맞는지 모르기 때문에 가장 난감하다.',
    '. 264 - 2가 있고 위치가 맞으며, 6이 있지만 위치가 다르므로 1스트라이크 1볼.',
    '. 126 - 숫자는 전부 맞지만 위치는 6만 맞고 나머지 둘은 다르므로 1스트라이크 2볼.',
    '. 216 - 전부 맞으므로 승리.'
  ]

  return (
    <div className="App"> {/*className 속성 적용시 App.css 의 내용이 모두 적용*/}
      <Header className="App-header"></Header>
      <Section sections={sections}></Section>
      <Article></Article>
      <Footer list={footerArr}></Footer>
      {/*<Nav list={list}></Nav>*/}
    </div>
  );
}

export default App;
```
컴포넌트 내부에서 map 객체를 이용할 레퍼런스 변수명은 app에서 결정된다
```jsx
//Section 컴포넌트
function Section(props) {
    return(
        <section>
            {   // App에서 전달되는 속성명을 명시
                props.sections.map((v,i) => {
                    return <h4 key={i}>{v}</h4>
                })
            }
        </section> 
    );
}
export default Section;
//Footer 컴포넌트
function Footer(props) {
    return(
    <div>
        <h5>
            {   // Footer의 경우 list로 래퍼변수명을 초기화함
                props.list.map((item,index) => { //list.map(callbackft)
                    return <h4>{index+item}</h4> // 리턴이 jsx 이므로 `{}` 를 활용하여 문법 사용
                })
            }
        </h5>
        
    </div>
    );
}

export default Footer;
```