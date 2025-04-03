# form submit

`form`을 작성하고 submit 할때 입력한 정보를 alret 해주는 어플리케이션

- 삼항연산자로 랜더링 여부를 구현했다.
- 비밀번호 부분에서는 입력받은 `e` 의 `e.target.value` 자체가 우리가 아는 `string` 객체로 처리가 가능하게 된다. (주의)
- 마지막 `submit`하는 부분에서 `form`의 `onSubmit` 속성과 `button` 의 `onClick` 을 이용해 구현했다
```jsx
import './App.css';
import {useState} from 'react';
const App = () => {
  const [agree,setIsagree] = useState(false);
  const [user_id,setId] = useState("");
  const [email,setEmail] = useState("");
  const [phoneNumber, setPhoneNumber] = useState("");
  const [address,setAddress] = useState("");

  const [password,setPw] = useState("default");
  const [password_a,setPw_a] = useState("defalut");
  
  const handleSubmit = (e) => {
    e.preventDefault();
    alert(`아이디: ${user_id}\n비밀번호: ${password}\n이메일: ${email}\n전화번호: ${phoneNumber}\n주소: ${address}`);
  };
  
  return (
    <div className="container">
      <h2>회원 가입</h2>
      
      <div className="form-group">
          <input
            type="checkbox"
            id="agree"
            onClick={()=>{
              setIsagree(!agree); // 초깃값이 false
            }}
          />
          <label className='agree' htmlFor="agree">이용약관에 모두 동의합니다</label>
      </div>
      {/*삼항 연산자로 해당 부분 조건부 랜더링*/}
      {
        agree
        ? <form onSubmit={handleSubmit}>  
        <div>
          <div className="form-group">
            <label htmlFor="userId">사용자 아이디</label>
            <input
              type="text"
              id="userId"
              name="userId"
              required
              onChange={(e) =>{
                setId(e.target.value);
              }}
            />
          </div>

          <div className="form-group">
            <label htmlFor="password">비밀번호</label>
            <input
              type="password"
              id="password"
              name="password"
              required
              onChange={(e)=>{
                setPw(e.target.value);
              }}
            />
          </div>

          <div className="form-group">
            <label htmlFor="confirmPassword">비밀번호 확인</label>
            <input
              type="password"
              id="confirmPassword"
              name="confirmPassword"
              required
              onChange={(e)=>{
                setPw_a(e.target.value); // 해당 라인에서 처리
              }}
            />
            
            {
              password==password_a?
              null
              :<label id="pw-match" className="pw-match">비밀번호가 일치해야 됩니다.</label> 
            }
          </div>

          <div className="form-group">
            <label htmlFor="email">이메일</label>
            <input
              type="email"
              id="email"
              name="email"
              required
              onChange={(e) =>{
                setEmail(e.target.value);
              }}
            />
          </div>

          <div className="form-group">
            <label htmlFor="phoneNumber">전화번호</label>
            <input
              type="tel"
              id="phoneNumber"
              name="phoneNumber"
              required
              onChange={(e) =>{
                setPhoneNumber(e.target.value);
              }}
            />
          </div>

          <div className="form-group">
            <label htmlFor="address">주소</label>
            <input
              type="text"
              id="address"
              name="address"
              required
              onChange={(e) =>{
                setAddress(e.target.value);
              }}
            />
          </div>

          <button type="submit" onClick={handleSubmit}>제출</button>
        </div>
        </form>: 
        null
      }
      
    </div>
  );
};

export default App;
```