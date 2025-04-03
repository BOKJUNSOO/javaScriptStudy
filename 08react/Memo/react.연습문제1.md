## Convert 문제

```jsx
import { useState } from 'react';
import './App.css';

const MinutesToHours = () => {
  const [condition , setCondition] = useState(false);
  const [minutes, setMinutes] = useState();
  const [hours, setHours] = useState();
  return (
    <div>
      <h3>Minutes To Hours</h3>
      <div>
        <label htmlFor="minutes">Minutes</label>
        <input type="number" id="minutes" placeholder="Minutes"
          disabled={condition}
          value={minutes}
          onChange={(e) => {
            const v = e.target.value;
            setMinutes(v);
            const new_hours = v/60;
            setHours(new_hours)
          }}/>
      </div>
      
      <div>
        <label htmlFor="hours">Hours</label>
        <input type="number" id="hours" placeholder="Hours"
          disabled={!condition}
          {/*해당 부분을 객체로 받는 것이 중요*/}
          value={hours}
          onChange={(e) =>{
            const w = e.target.value;
            setHours(w);
            const new_mintues = w*60;
            setMinutes(new_mintues);
          }} />
      </div>
      
      <button onClick={()=>{
        setHours(0);
        setMinutes(0);
      }}>Reset</button>
      
      <button onClick={()=>{
        const condition2 = !condition;
        setCondition(condition2);
      }}>Flip</button>
    </div>
  )
};

function App() {
  return (
    <div className="App">
      <MinutesToHours/>
    </div>
  );
}
export default App;
```