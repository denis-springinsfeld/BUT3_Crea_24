# API

## V1

```jsx
import { useEffect, useState } from "react";

import Card from "./components/Card";

export default function App() {
  const [data, setData] = useState({});
  const fetchNewAdvice = async () => {
    try {
      const response = await fetch("https://api.adviceslip.com/advice");
      const data = await response.json();
      setData(data);
      console.log(data);
    } catch (error) {
      console.error(error);
    }
  };

  useEffect(() => {
    fetchNewAdvice();
  }, []);

  return (
    <>
      {/*'.?' opératuer de chainage optionnel elle permet d'accéder à une propriété profodément imbriquée dans un objet, en évitant les erreurs si une propriété intermédiaire est null ou undefined*/}
      <p>{data?.slip?.id}</p>
      <p>{data?.slip?.advice}</p>
    </>
  );
}
```
App.jsx


## V2

```jsx
import { useEffect, useState } from "react";

export default function App() {
  const [state, setState] = useState({
    data: null,
    isLoading: true,
  });

  const fetchNewAdvice = async () => {
    try {
      const response = await fetch("https://api.adviceslip.com/advice");
      const data = await response.json();
      setState({ data: data, isLoading: false });
    } catch (error) {
      console.error(error);
    }
  };

  useEffect(() => {
    fetchNewAdvice();
  }, []);

  return (
    <>
      {/*'.?' opérateur de chainage optionnel il permet d'accéder à une propriété profodément imbriquée dans un objet, en évitant les erreurs si une propriété intermédiaire est null ou undefined*/}
      {state?.isLoading ? (
        <p>Loading...</p>
      ) : (
        <div>
          <p>{state?.data?.slip?.id}</p>
          <p>{state?.data?.slip?.advice}</p>
        </div>
      )}
    </>
  );
}
```
App.jsx
