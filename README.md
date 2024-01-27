# Batching_In_React

Q.1:- Your task is to explain why the console.log shows the older value of count


import React from 'react';

function App() {
  
  const [count, setCount] = React.useState(0);

  const handleClick = () => {
    setCount(count + 1);
    console.log(count); // You will see the older value of count in console
  };

  return (
    <div>
      <p>Button is clicked {count} times</p>
      <button onClick={handleClick}>Click Me</button>
    </div>
  );
}

export default App;

When i click on button the button clicked 1 time but in console we saw 0 because
useState is async in nature and when we click on button the entire block of code get
re-render and on that point the value of count is still 0. So, its printed as 0
and after that it will increase by one after some delay in mili-seconds.




1.Solution:- ---------------------------------------


If we want to log the updated value of count in console we can create a hook using Usestate which
captures that my button is clicked or not. if my button is clicked so after that i'll make it true
and in using UseEffect i can console the value of count if buttoncliked is true if i dont take
useState hook then useEffect function renders in page loading and directly logs the initial value
of count which is 0

import React, { useEffect } from 'react';

function App() {
  
  const [count, setCount] = React.useState(0);
  const [buttonClicked, setButtonClicked] = React.useState(false);

  const handleClick = () => {
    setCount(count + 1);
    setButtonClicked(true);
  };

  useEffect(() => {
    if (buttonClicked) {
      console.log(count);
    }
  }, [buttonClicked, count]);

  return (
    <div>
      <p>Button is clicked {count} times</p>
      <button onClick={handleClick}>Click Me</button>
    </div>
  );
}

export default App;

----------------------------------------------------------------------------------------------------



Q.2:- Your task is to explain why count value is not updated to 3 as expected

import React from 'react'
function App() {
const [count, setCount] = React.useState(0);
const handleClick = () => {
setCount(count + 1);
setCount(count + 1);
setCount(count + 1);
console.log(count);
};
return (
<div>
    <p>Button is clicked {count} times</p>
    <button onClick={handleClick}>Click Me</button>
</div>
);
}

export default App

In this code setCount calls do not result in the count being 3 beacuse when we click the button and
handleclick function got call the initial value of count is 0 and in next line we increase it by 1
now its become 0+1 = 1 but when we enter in next line the value is count still reflects to 0 because
it takes the value when we enters in the starting fase of function initial value and not considered
the value which is got updated inside that function on that execution.


2.Solution -------------------------------------------


Ans:- For getting the expected output of 3 we can use callback functions here. A callback function is a function Which takes another function as an argument inside that function. So if we will update the value of count inside call back we got the updated value as expected. This ensures that each update is applied sequentially and accurately, respecting React's asynchronous state update mechanism.


import React from 'react'

// Your task is to explain why count value is not updated to 3 as expected
function App() {
const [count, setCount] = React.useState(0);
const handleClick = () => {
setCount((pcount) => pcount + 1 );
setCount((pcount) => pcount + 1 );
setCount((pcount) => pcount + 1 );
};
return (
<div>
    <p>Button is clicked {count} times</p>
    <button onClick={handleClick}>Click Me</button>
</div>
);
}

export default App

