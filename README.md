## 컴포넌트 최적화

### useState

- useState 사용하여 state를 선언하고 초기값을 주입할 때 함수실행문을 사용하면 리렌더링 될 때마다 함수가 호출됨
- 그러나 실행문 없이 함수 자체를 파라미터로 주입하면 초기에만 호출됨 useState(getInitData)

### 성능체크

- 성능 체크는 크롬 개발자도구의 Performance 탭의 녹화기능을 활용하여 체크

### 컴포넌트 리렌더링 발생

- 전달 받은 props가 변경될 때
- 자신의 state가 변경될 때
- 부모의 컴포넌트가 리렌더링 될 때
- forceUpdate 함수가 실행 될 때

```
일반적으로 부모 컴포넌트에서 state를 관리하므로 리렌더링이 불필요한 자식 컴포넌트까지 리렌더링이 일어남
```

### React.memo

- 함수형 컴포넌트에서는 컴포넌트의 props가 변경되지 않았을시 React.memo를 이용해 리렌더링을 방지
- 클래스형 컴포넌트에서는 shouldComponentUpdate 라이프 사이클에서 제어

### state 제어 함수 재생성 방지

- onRemove, onToggle 등의 state를 컨트롤 하는 함수 들이 재생성을 방지하여 불필요한 함수 재생성을 막는다

1. useState의 함수형 업데이트

- useCallback 하에서 set함수를 호출하고 useCallback의 디펜던시를 제거.

```js
const onRemove = useCallback((id) => {
  setTodos((todos) => todos.filter((todo) => todo.id !== id));
}, []);
setTodo;
```

2. useReducer

- useState의 함수형 업데이트 대신 사용할 수 있음.
- useReducer를 사용할 경우 상태 업데이트 로직을 컴포넌트 바깥에 둘 수 있음

### 리스트 관련 컴포넌트를 작성할 떄는 리스트 아이템과 리스트 컴포넌트 모두 최적화 필요

### react-virtualized 사용

- react-virtualized를 사용하면 화면에 보이지 않는 컴포넌트는 크기하게끔 할 수 있음
- react-virtualized의 List 컴포넌트를 사용할 때에는 해당 리스트의 전체 크기와 각 항목의 높이, 각 항목에 대한 렌더링 함수, 리스트로 보여질 데이터 배열을 전달해주어야 함

### 보여줄 항목이 100개가 넘고, 업데이트가 자주 발생한다면 최적화가 필수
