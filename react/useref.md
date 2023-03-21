# useRef()

**useRef()는 current 속성을 가지고 있는 객체를 반환하는데, 인자로 넘어온 초기값을 할당한다.**

**current 속성은 값이 바뀌어도 랜더링이 되지 않는 특징을 가지고 있다.**

사용하는 방법은 다음과 같다.

```tsx
const test = useRef(null);

function testFuc() {
	test.current?.method()
}
```

test 에 **useRef(null)** 을 선언후, **testFuc()에 current 속성안 객체를 선언**한다.

사용빈도는 낮은 Hook 함수이지만, ( 용도가 극히 제한적 ) DOM 노드나 React Element 에 직접 접근하기 위해서는 사용하는 Hook 함수이기에 알아두면 좋을거 같다.
