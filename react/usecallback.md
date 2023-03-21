# useCallback()

**useCallblack()** 은 함수를 메모이제이션 하기위해 사용하는 Hook 이다.

첫번째로 넘어오는 함수를 두번째 인자로 넘어온 값이 변경 될때가지 저장해놓고 사용하게 해준다.

```tsx
const plusQuiz = () ⇒  a + b;
```

예를 들어 plusQuiz 는 렌더링될따마다 함수를 새로 선언하게 되는데 여기서 useCallbaclk() 을 사용하게 되면

```tsx
const add = useCallback(() ⇒ a + b , [ a + b ]);
```

이러한 방식으로 사용하게 되고 a,b 값이 **동일하면** 다음 랜더링때 이 함수를 재사용을 하게 해준다.

이렇다보니 소스코드에서 useCallback() 을 남발을 하는 경우가 있었다.

하지만, 무분별하게 사용하게 되면 코드가 복잡해지거나, 유지보수 측면에서는 어렵기 때문에