# React-Debounce-Snippet
Code snippet on how to create custom denounce hook in react.

[![Edit how-to-use-debounce](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/how-to-use-debounce-zdfym?fontsize=14&hidenavigation=1&theme=dark)

```js
import "./styles.css";
import React, { useEffect, useRef, useState } from "react";

const useDebounce = (value, delay = 500) => {
  const [debouncedValue, setDebouncedValue] = useState();
  const timer = useRef(null);
  useEffect(() => {
    timer.current = setTimeout(() => {
      setDebouncedValue(value);
    }, delay);
    return () => clearTimeout(timer.current);
  }, [value, delay]);

  return debouncedValue;
};



export default function App() {
  const [text, setText] = React.useState("Text input - Empty");
  const debouncedText = useDebounce(text);

  const handleChange = (event) => {
    const {
      target: { value }
    } = event;
    const cleanValue = value?.trim() || "Text input - Empty";
    setText(cleanValue);
  };

  return (
    <div className="App">
      <h1>Hello CodeSandbox</h1>
      <h2>Start editing to see some magic happen!</h2>
      <input type="text" onChange={handleChange} />
      <h3>{debouncedText}</h3>
    </div>
  );
}

```
