# SimpleCalculator
Simple Calculator using react js
import { useState } from "react";
function App() {
  const [calc ,setCalc]=useState("");
  const [result,setResult]=useState("");
  const ops=['/','*','+','-','.'];
  
  #for restricting the illegal use of opertars simultaniously
  const updateCalc=value=>{
    if( ops.includes(value) && calc === '' || 
        ops.includes(value) && ops.includes(calc.slice(-1))
        )
    {
      return;
    }
    setCalc(calc+value);
    if (!ops.includes(value)){
      setResult(eval(calc+value).toString())
    }
  }

# for adding 1-9 button in calculator at once using for loop instead of giving the same tags 10 times 
  const createDigits=()=>{
    const digits=[];
    for(let i=1;i<10;i++)
    {
      digits.push(
        <button onClick={()=>updateCalc(i.toString())
         } key={i}>{i}</button>
      )
    }
    return digits;
  }
  
  #for calculating the result of the operations 
const calculate=()=>{
  setCalc(eval(calc).toString());
}

for deleting the previous digit or for clearing the result
const deleteLast = () => {
     if (calc ==''){
       return;
      } 

     const value = calc.slice(0, -1);
     setCalc(value);
}

  return (
    <div className="App">
       <div className="calculator">
       
   
       <div className="display">
         {result?<span>{result}</span>:''}&nbsp;
         {calc||"0"}
        
       </div>
       <div className="operators">
         <button onClick={()=>updateCalc('/')}>/</button>
         <button onClick={()=>updateCalc('*')}>*</button>
         <button onClick={()=>updateCalc('+')}>+</button>
         <button onClick={()=>updateCalc('-')}>-</button>
     
       
       <button onClick={deleteLast}>DEL</button>
       </div>
       <div className="digits">
         {createDigits()}
         <button onClick={()=>updateCalc('0')}>0</button>
         <button onClick={()=>updateCalc('.')}>.</button>
         <button onClick={calculate}>=</button>
       </div>


       </div>
    </div>
  );
}

export default App;
