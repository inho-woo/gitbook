# ⚡ React 관련 개념정리

### 🟡 리액트 <a href="#undefined" id="undefined"></a>

> 리액트를 쓰는 이유는 아래와 같은 특징들로 설명해볼 수 있다.

#### 📍 Javascript + XML <a href="#javascript-xml" id="javascript-xml"></a>

* 자바스크립트에 HTML 태그를 끼얹은 문법\
  HTML 태그 안에선 중괄호 `({})`를 사용해서 JS를 쓸 수 있다.
* 써보면 굉장히 편리하다.

```null
const apple = "사과"
const title = <h1>{apple} 드실분?</h1>
```

***

#### 📍 컴포넌트 <a href="#undefined" id="undefined"></a>

* 화면을 이루는 '요소'로 여러 곳에서 **재사용 가능한 UI 코드 조각**이다.
* 개발하다가 특정 부분에서 버그가 일어나면 그 컴포넌트만 수정하여 사용할 수 있다.\
  그래서 코드의 재사용성과 유지보수성을 증가시켜준다.
* 리액트 데이터의 흐름은 **단방향**으로 이뤄진다. 즉, 부모에서 자식으로 한방향으로만 데이터를 props를 사용하여 공유해줄 수 있다.

**Props**

* 프로퍼티의 줄임말이고 **부모 컴포넌트에서 -> 자식 컴포넌트**로 데이터를 전달해주는 개념이다.
* 자식 컴포넌트에서 전달 받은 props는 읽기 전용이고 Props를 전달해준 **최상위 부모 컴포넌트만** props를 변경할 수 있다.

**State**

* 컴포넌트의 상태를 나타내고 동적인 데이터를 다룰 때 사용한다.
* useState 함수로 상태를 추가할 수 있다.
* `const [상태명, 상태변경함수명] = useState(초기값);`

***

#### 📍 제어 컴포넌트 vs 비제어 컴포넌트 <a href="#vs" id="vs"></a>

리액트는 두 가지 방식으로 form의 입력을 처리한다.\
바로 제어 컴포넌트와 비제어 컴포넌트로 나눌 수 있는데

**🔥 (1) 제어 컴포넌트**

* 사용자가 제어 컴포넌트에 데이터를 입력하면 변경 이벤트 핸들러가 호출되고 코드가 **업데이트된 값으로 다시 렌더링**이 된다. 대표적으로 form에 `value` 값을 `useState`로 관리해서 데이터를 최신화 하는 것이다.

```null
const [inputValue, setInputValue] = useState('');

return (
 <input value={inputValue} onChange={(e) => setInputValue(e.target.value) />
)
```

이런식으로 텍스트 입력을 할 때마다 onChange의 콜백 호출에 따라서 form의 상태가 계속 즉각으로 렌더링 되는 것을 **제어 컴포넌트**라고 한다.

**활용 예)**

* form의 유효성 검사할 때 (아이디나 비밀번호 체크시)
* form에 데이터 값에 따라 버튼 상태를 disabled로 표시

\


**🔥 (2) 비제어 컴포넌트**

* 사용자가 폼 필드에 데이터를 입력하면 업데이트된 정보가 리액트에서 별도 처리할 필요 없이 엘리먼트에 반영된다.\
  제어 컴포넌트는 useState로 관리하지만 비제어 컴포넌트는 ref로 관리한다.

```null
const inputRef = useRef();

return (
<input ref={inputRef} value="hello" />
)
```

이처럼 ref를 활용해 입력 폼의 상태를 접근할 수 있다. button을 클릭할 때 ref를 통해 값을 얻을 수 있다.

**활용 예)**

* 불필요한 렌더링을 줄이고, 버튼을 클릭하여 제출할 때 값이 필요할 경우에 사용

***

#### 📍 이벤트 <a href="#undefined" id="undefined"></a>

사용자 이벤트(클릭, 스크롤 등) 다루기

* 일반 자바스크립트 이벤트 목록과 동일하지만 중간을 대문자로 쓰면 된다.
* onclick -> onClick
* onsubmit -> onSubmit

***

#### SPA (Single Page Application) <a href="#spa-single-page-application" id="spa-single-page-application"></a>

사용자가 한 페이지의 머무르면서 새로운 페이지로 바뀔 때 마다 필요한 정보만 추가적으로 받아와 **부분적으로 업데이트**한다.

* 첫 화면 로딩 시간이 다소 길다는 점이 있다.
* 라우팅에 따라 다른 뷰를 보여줄 수 있다.

***

#### 📍 가상 돔(Virtual DOM) <a href="#virtual-dom" id="virtual-dom"></a>

* DOM을 추상화한 가상의 객체이다.\
  ![](https://velog.velcdn.com/images/leemember/post/724b0be2-9cf2-42d6-9f51-3ad018a88116/image.png)

일반적인 브라우저 렌더링 과정으로는\
1\. **HTML 파싱 -> DOM 객체 생성 -> CSS 파싱 -> 스타일 규칙 생성**\
2\. 위의 과정을 합쳐 실제로 웹 브라우저에 보여줘야 할 **'render tree'** 를 만든다.\
3\. 이 렌더 트리 기준으로 레이아웃을 배치하고 **Paint**의 작업을 한다.

이 과정에서 변경될 구성 요소가 바뀌면 **전체가 렌더링**이 되는데 매우 비효율적이라고 볼 수 있다.\
그래서 리액트를 사용하는 이유중 하나가 바로 **Virtual DOM** 이다.\
Virtual DOM은 기존 DOM과 변경될 Virtual DOM의 차이를 판단하고 **변경된 구성요소만 찾아** **그부분만 렌더링**이 된다.

#### 📍 diffing 알고리즘 <a href="#diffing" id="diffing"></a>

위에 설명한 Virtual DOM과 관련이 크다.\
변경된 부분만 감지해서 바뀐 부분만 업데이트 하는 방식을 취하게 되는데 이 변경된 부분을 감지하는 것을 diffing Algorihm 이라고 한다.\
일반적인 트리 구조의 비교는 O(n^3)의 시간이 소요된다고 한다. 하지만 리액트는 이러한 diffing 알고리즘으로 인해 O(n)의 시간에 해결하고 있다.

#### 📍 key를 사용하는 이유 <a href="#key" id="key"></a>

이것 또한 Virtual DOM과 diffing 알고리즘과 연관이 있다.\
하나의 JSX 태그는 자바스크립트 객체로 구성되는데 이 객체에는 해당 객체가 Virtual DOM의 요소임을 확인해주는 심볼값과 각각의 **Virtual DOM를 고유하게 구분하는 key 값**이 들어가게 된다.

그래서 `map` 을 사용했을 때, 해당 리스트에 고유한 key값을 넣어줘야한다. 리액트는 이 **key들의 비교를 통해 리스트의 요소가 추가되거나 삭제되었을 때 상태를 빠르게 감지하고 반영**할 수 있다.

쉽게 말해 엘리먼트 혹은 **컴포넌트의 변화를 감지하기 위함이고 이는 효율적인 DOM 사용으로 귀결**된다.

***

#### 📍 Hooks <a href="#hooks" id="hooks"></a>

**useState**

* 컴포넌트의 상태를 관리할 수 있다.\
  상태에 따라 즉각적으로 다른 화면들을 출력해준다. (= 렌더링)

**useEffect**

* 렌더링 이후에 실행할 코드를 만들어준다.
* 사이드 이펙트를 감지하는 함수, 감시대상이 변하면 콜백을 실행한다.

```null
useEffect(감시 대상이 변하면 동작 할 콜백, [감시대상])
```

클래스 컴포넌트 시절에는 아래와 같은 함수로 useEffect 역할을 했는데, 이것도 기술면접 때 useEffect와 연관시켜 질문이 빈번하게 나오기 때문에 정리해봤다.

> **componentDidMount**: 컴포넌트를 만들고, 첫 렌더링을 다 마친 후 실행.\
> **componentDidUpdate**: 리렌더링을 완료한 후 실행. 즉 render()가 업데이트될 때마다 실행\
> **compoenntWillUnMount**: 컴포넌트를 DOM에서 제거할 때 실행.

**위 개념들이 useEffect로 어떻게 쓰이는지 ?**

* Component가 Mount 되었을 때(나타날 때) = `componentDidMount`
* deps부분을 생략한다면 해당 컴포넌트가 렌더링 될 때마다 useEffect가 실행된다.

```null
  useEffect(() => {
    console.log("렌더링 될때마다 실행");
  });
```

* 만약 맨 처음 렌더링 될 때 한 번만 실행하고 싶다면 deps위치에 빈 배열을 넣자

```null
useEffect(() => {
    console.log("맨 처음 렌더링될 때 한 번만 실행");
  },[]);
```

* Component가 Update 되었을 때(props, state 변경) = `componentDidUpdate`

```null
  useEffect(() => {
    console.log("name이라는 값이 업데이트 될 때만 실행");
  },[name]);
```

* Component가 사라질 때 & Update 되기 직전에 = `compoenntWillUnMount`
* 언마운트 될 때만 cleanUp 함수를 실행시키고 싶다면 deps에 빈배열을 넣으면 된다.
* 특정 값이 업데이트 되기 직전에 cleanup 함수를 실행시키고 싶다면 deps에 해당 값을 넣어주면 된다.

```null
  useEffect(() => {
    console.log("hello");
    return () => {
      console.log("cleanUp 함수");
    };
  });
```

**🔥 유의사항**

* useEffect는 첫 렌더링 후 실행된다.
* 최초에 한 번은 무조건 실행된다.

**useRef**

* 컴포넌트나 HTML의 DOM의 요소를 ref로 관리할 수 있다.

**useMemo & useCallback**

* 의존성 배열에 적힌 값이 변할 때만 값, 함수를 다시 정의할 수 있다.
* 주로 **렌더링 성능을 최적화해야 하는 상황**에 사용한다.
* 렌더링마다 새롭게 함수가 추가되는 것을 방지하고 감시 대상이 변하지 않는 이상 함수를 새롭게 생성하지 않는다.

```null
  useCallback(콜백, [의존성])

  // 렌더링마다 매번 새롭게 생성됨
  const foo = () => {} 
  
  // 매번 새롭게 생성되지 않는다.
  const foo2 = useCallback(() => {}, []) 
  
   // a 값이 바뀌지 않는 이상 매번 새롭게 생성되지 않는다.
  const foo3 = useCallback(() => {}, [a]) 
  
```

***

### 🟡 상태관리 <a href="#undefined" id="undefined"></a>

> 상태관리는 직접 사용해보고 알게된 특징들과 나의 생각들을 같이 정리 해봤습니다.

![](https://velog.velcdn.com/images/leemember/post/f0fc3ada-9afc-4601-a533-e60b366b225f/image.png)

`npm trends`라는 사이트에서 Redux와 Mobx, 그리고 Recoil의 동향을 파악해봤는데 여전히 Redux가 압도적이긴하다. 아무래도 리덕스가 가장 오래전에 나왔기 때문에 옛날에 만들어진 프로젝트들을 현재까지 운영하고 개발하려면 리덕스를 알아야되니 그렇다고 본다. 개인적으로 나는 recoil 찬양

#### 📍 Redux <a href="#redux" id="redux"></a>

![](https://user-images.githubusercontent.com/71499150/158109697-d9fedc8c-524f-4342-a680-1c8253b7bd2b.png)

action, dispatch, reducer, store가 있다.

* **action** : action은 상태(state)를 바꾸는 방식이다. 반드시 type필드가 있어야 한다.
* **dispatch** : action을 발생시키는 것으로 action 객체를 파라미터로 받는다.
* **reducer** : 변화를 일으키는 함수로 action의 결과로 상태를 어떤 식으로 바꿀지 구체적으로 정의하는 부분
* **store** : 리덕스를 적용하기 위한 **중앙 저장소** 이며, **단 한 개**만 가질 수 있다.\
  상태를 읽을 때는 getState() 상태를 바꿀 때는 dispatch()를 호출한다.
* 데이터 흐름을 **단방향**으로 흐르게 한다.
* 상태를 전역적으로 관리하기 때문에 어느 컴포넌트에 상태를 둬야할지 고민할 필요가 없게 한다.
* 상태관리에서 불변성 유지가 매우 중요하다.\
  Spread 방식(...) 보다 좀더 깔끔하게 처리하기 위해서는 **immer.js 라이브러리**를 사용하여 불변성 유지를 해줄 수 있다.
* **flux 아키텍처**를 따른다.\
  🔥 flux 구조란 ? 단방향 데이터 흐름을 가지는 구조.\
  새로운 데이터를 넣으면 처음부터 다시 시작되는 방식으로 설계되어있다.
* 데이터 흐름은 **dispatch -> store -> view** 순서이다. view에서 입력이 발생하면 액션을 통해 디스패치로 향하게 된다.
* 비동기 처리시 redux-saga나 redux-thunk같은 **미들웨어가 필수**이다.
* 여러 라이브러리를 함께 사용하게 되니 **러닝커브가 높은 편**
* 액션 하나 추가하는데 작성이 필요한 부분이 많고 컴포넌트와 스토어를 연결하는 필수적인 부분들이 있어서 **코드량이 상대적으로 많아진다.**

**불변성을 유지하는 이유 ?**

* 사이드 이펙트를 방지하여 프로그래밍 구조의 단순성을 지킨다.\
  원본 데이터가 변경될 경우, 원본 데이터를 참조하고 있는 다른 객체에서 예상치 못한 오류가 발생할 수도 있기 때문이다.

\


#### 📍 Mobx <a href="#mobx" id="mobx"></a>

* 리덕스와 다르게 스토어에 제한이 없다. 여러개여도 상관 없음.\
  observable을 기본적으로 사용한다.
* 절대적으로 필요한 경우에만 state를 변경한다.
* 객체 지향적이다. OOP 를 따름. 그래서 서버 개발자들에게 친숙한 아키텍쳐를 제공할 수 있다. 특히 자바 스프링과 유사하다.
* 리덕스의 보일러플레이트 코드가 사라지고 데코레이터를통해 깔끔한 코드 작성이 가능하다.
* 보일러 플레이트란 ? 반복적으로 사용되는 부분을 재사용하는 것을 의미
* State의 불변성 유지를 위해 노력하지 않아도 된다. 리덕스와 비교했을 때 리덕스에서는 state의 불변성 유지를 위해 여러 라이브러리(immer)를 사용하기도 하는데, mobx에서는 그러지 않아도 된다.

\


#### 📍 Recoil <a href="#recoil" id="recoil"></a>

* 페이스북에서 만든 상태관리 라이브러리
* 가장 리액트스럽다. 리액트 hooks의 느낌으로 친숙하게 작업할 수 있음\
  러닝커브가 굉장히 낮다.
* 초기 세팅이 정말 간편하고 recoil 라이브러리 외에 따로 설치해야 될 것들이 없어서 좋다.
* atom, selector 기능만 알고있다면 구현 쌉가능
* 이것도 mobx 처럼 자유로워서 협업자들과 룰 정해서 작업해야한다.
* 디버깅 도구 지원이 미미하다.
* 직관적이고 단순한 편이다.

\


#### 📍 React-query <a href="#react-query" id="react-query"></a>

* 데이터 페칭 툴
* 로딩 및 오류 상태 관리 (데이터가 로딩되었을 때와 오류 발생시 사용자에게 알려준다)
* 리액트 쿼리 개발자 도구를 통해 쿼리에 무슨 일이 일어났는지 추적이 가능하다.
* 블로그 게시물에 Pagination 기능을 써서 리액트 쿼리에서 어떻게 작업하는 지 알 수 있다
* Pagination 에 프리패칭(Prefetching)을 수행할 수 있다.\
  _프리패칭(Prefetching)이란 ?_ 다음 페이지를 미리 가져오면 사용자가 다음 페이지를 클릭 할 때 데이터를 즉시 가져오기 때문에 매끄럽게 처리되도록 할 수 있다.

***

### 🟡 프레임워크 Nextjs <a href="#nextjs" id="nextjs"></a>

#### 📍Next에서 제공해주는 기능들 <a href="#next" id="next"></a>

* 코드를 고치는대로 변경되는 `핫 리로딩`이 탑재되어있다.
* `pages/product/[slug]` 라는 표기로 다이나믹하게 path를 변경할 수 있었다.
* 손쉬운 배포 시스템 Vercel 제공
* 프론트엔드에 필요한 간단한 API 구성
* SEO 검색 엔진 최적화 (사용자들이 훨씬 더 쉽게 웹서비스를 찾아갈 수 있도록)
* 코드 분할 (코드 스플리팅) 으로 하여금 렌더링 속도가 빠르다.
* 파일 기반 구조 `/pages/main`
* pre-fetching

\


#### 📍SEO(검색 엔진 최적화) <a href="#seo" id="seo"></a>

**검색 결과 상위에 노출**될 수 있도록 하는 작업을 말한다.

\


#### 📍SSR (서버 사이드 렌더링) <a href="#ssr" id="ssr"></a>

* **서버가 데이터를 가져와서 그린다.**

**장점**

* 구글, 네이버, 다음 등의 검색 엔진이 우리가 만든 웹 애플리케이션의 페이지를 원활하게 수집해준다.\
  ✔ 따라서 웹 서비스의 검색 엔진 최적화를 위해서라면 서버 사이드 렌더링을 구현 해주는 것이 좋다.
* 초기 렌더링 성능을 개선할 수 있다.\
  예를들면, SSR이 구현되지 않은 웹 페이지에 사용자가 방문하면, JS가 로딩되고 실행될 때 까지 사용자는 **비어 있는 페이지를 보며 대기**해야한다.\
  여기에 API까지 호출해야 한다면 사용자의 대기 시간은 더더욱 길어진다.\
  반면 서버 사이드 렌더링을 구현한 웹 페이지라면 JS 파일 다운로드가 완료되지 않은 시점에서도 HTML상에 **사용자가 볼 수 있는 콘텐츠**가 있기 때문에 **대기 시간이 최소화되고, 이로 인해 사용자 경험도 향상**된다.

**단점**

* SSR은 결국 원래 브라우저가 해야 할 일을 서버가 대신 처리하는 것이므로 서버 리소스가 사용된다.
* 수많은 사용자가 동시에 웹 페이지에 접속하면 서버에 과부하가 생김.\
  ✔ **해결방안** : 사용자가 많은 서비스라면 캐싱과 로드 밸런싱을 통해 성능을 최적화 해줘야한다.
* 개발이 어려워 질 수 있다.\
  SSR을 하면 프로젝트의 구조가 좀 더 복잡해질 수 있고, 데이터 미리 불러오는 `프리패칭과 코드 스플리팅` 의 호환 등 고려해야 할 사항이 더 많아지기 때문이다.
* SSR을 담당하는 함수 : getServerSideProps
* 첫 페이지의 로딩시간이 CSR에 비해 짧다.\
  이미 렌더링된 페이지를 서버에서 받아서 화면을 구성하기 때문이다.
* SEO 측면에서도 유리하다.\
  검색엔진이 크롤링을 할 때 서버에 이미 하드코딩된 html 파일이 있기 때문에 검색엔진이 이 페이지가 어떤 역할을 하는지 파악하는데 용이하다.
* SSR은 서버 부하가 일어나니 필요에 따라 SSG와 ISR을 적절하게 쓰면 좋다.

\


#### 📍CSR (Client Side Render) <a href="#csr-client-side-render" id="csr-client-side-render"></a>

* **클라이언트가 데이터를 가져와서 그린다.**
* 처음 로딩시 js파일의 용량이 클수록 로딩시간이 길다.\
  하지만 초기에 로딩이 되고나면 페이지 간 이동 시 매우 빠른 속도로 전환되고, 페이지 이동 시 새로고침되는 현상도 사라진다.

\


#### 📍SSG (Statice-Site Generation) <a href="#ssg-statice-site-generation" id="ssg-statice-site-generation"></a>

* 정적인 사이트를 생성한다 : 정적인 사이트를 데이터를 가져와서 그려준다.\
  SSG을 담당하는 함수로는 `getStaticProps`라는 함수가 있다.\
  언제쓰이나 ? 블로그 같이 정적일 수 있는 것들을 이것을 사용한다.

\


#### 📍ISR (Incremental Static Regeneration) <a href="#isr-incremental-static-regeneration" id="isr-incremental-static-regeneration"></a>

* 증분 정적 사이트를 재생성 한다. (특정 주기로) 정적인 사이트에 데이터를 가져와서 다시 그려준다.\
  이걸 담당하는 함수는 `getStaticProps` 라는 함수다.\
  값을 리턴하면서 동작한다.

***

### 🟡 환경세팅 <a href="#undefined" id="undefined"></a>

#### 📍Webpack <a href="#webpack" id="webpack"></a>

* 웹팩이란 최신 프런트엔드 프레임워크에서 가장 많이 사용되는 모듈 번들러(Module Bundler)입니다. **모듈 번들러란** 웹 애플리케이션을 구성하는 자원(HTML, CSS, Javscript, Images 등)을 모두 각각의 모듈로 보고 이를 조합해서 병합된 하나의 결과물을 만드는 도구를 의미합니다

**사용하는 이유**

1. 파일 단위의 자바스크립트 모듈 관리의 필요성
2. 웹 개발 작업 자동화 도구
3. 웹 애플리케이션의 빠른 로딩 속도와 높은 성능

#### 📍Pritter <a href="#pritter" id="pritter"></a>

**협업을 하게 될 때, 일관성 있는 코드 스타일은 정말 중요**하다.\
그래서 일관성 있는 코드 스타일 규칙만 설정해주면 알아서 자동으로 그 규칙에 맞게 **코드들을 정리**해준다.

#### 📍Babel <a href="#babel" id="babel"></a>

* **최신 문법을 브라우저가 이해할 수 있는 자바스크립트로 통역**
* 브라우저는 JSX를 이해하지 못한다.\
  그러니 바벨이라는 통역사로 **JSX -> Javascript**

#### 📍Eslint <a href="#eslint" id="eslint"></a>

ESLint가 코드 퀄리티를 일관적으로 유지\
문법 에러를 잡아주거나 더 좋은 코드 구현 방식을 사용하도록 해준다.

> 참고자료\
> [https://velopert.com/3236](https://velopert.com/3236)\
> [https://yeoulcoding.me/147](https://yeoulcoding.me/147)\
> [https://velog.io/@velopert/react-hooks](https://velog.io/@velopert/react-hooks)\
> [https://hsp0418.tistory.com/17](https://hsp0418.tistory.com/171)\
>
