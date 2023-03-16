# useContext()

**useContext()** 는 React를 사용하는데 있어서 확장성(?)이 좋은 Hook 이다.&#x20;

대부분 컴포넌트간의 통신은 **props** 를 통해 데이터를 전달하게 되는데, (부모 -> 자식) 만약 거쳐야되는 컴포넌트들이 많아지게되면 소스자체가 굉장히 비효율적으로 바뀔수밖에 없다. 이때 **useContext()** 를 쓰게 되면 전역적으로 변수를 사용할 수 있어 비효율적인 코드 작성을 할 필요가 없다.

#### useContext()

우선 **createContext()** 를 선언해 전달할 데이터를 선언한다.



`createContext({`&#x20;

`loading : () => {}`

`useMemo(() => loading,[loading]);`

다음과 같이 **객체** 를 보낼때는 **useMemo()** Hook 을 이용해 리렌더링을 방지해줘야 한다. **useMemo()** 에 관한 내용은 다음글에 정리하도록 하겠다. **createContext()** 를 선언해주고 사용할 컴포넌트에 사용하면 된다.



`const contextTest() => {`&#x20;

&#x20;  `const [loading] = useContext(loading);`&#x20;

&#x20;  `return(`&#x20;

&#x20;     `<>`&#x20;

&#x20;     `<button onClick{() => loading((prev) => !prev)}> contextButton Test </button>`

&#x20;    `</>`&#x20;

&#x20;   `);`&#x20;

&#x20;`};`

`export default contextTest;`



만들어진 버튼을 클릭하면 loading 을 불러온다.

**Context** 는 React 가 버전에 따라서 많은 변경이 있어 공식문서에서도 사용을 지양해 대체인 **Redux** 를 이용했지만, 현재는 이와 같이 **createContext() , useContext()** 와 같이 정리가 잘 되어 활발히 활용되는 Hook 이다. 다만 , useContext() 를 쓸때 조심해야할 점이 있다면, Provider 에 제공한 value 가 달라지게 되면 useContext() 를 쓰는 모든 컴포넌트가 리렌더링이 된다. 이부분만 주의하면 충분히 활용도가 높은 Hook 이라 생각한다.