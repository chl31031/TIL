# React 기초 핵심 정리

### 1. React 개요 및 패러다임 변화
* **Before React (명령형 프로그래밍)**: 데이터가 변경될 때마다 개발자가 직접 DOM 요소에 접근하여(`document.getElementById` 등) 화면을 어떻게(How) 바꿀지 일일이 명령해야 했음.
* **After React (선언형 프로그래밍)**: 상태(State)를 정의하고 화면이 무엇(What)처럼 보여야 할지 선언하면, React가 변경된 부분만 감지하여 효율적으로 업데이트함.

---

### 2. 컴포넌트 (Component)
UI를 구성하는 재사용 가능한 독립적인 단위입니다.
* **명명 규칙**: 컴포넌트 이름의 첫 글자는 반드시 **대문자**로 시작해야 함 (소문자는 일반 HTML 태그로 인식됨).

#### ① 클래스형 컴포넌트 (Class Component)
* 초기 React의 표준 방식으로, `React.Component`를 상속받음.
* `render()` 메서드가 필수이며, 그 안에서 JSX를 반환함.
* 형태 예시:
```
  class Welcome extends React.Component {
    render() {
      return <h1>Hello, {this.props.name}</h1>;
    }
  }
```
#### ② 함수형 컴포넌트 (Functional Component)
* 현대 React 개발의 표준. 구조가 간결하고 Hook을 사용하여 상태 관리가 용이함.
* 형태 예시:
```
  function Welcome(props) {
    return <h1>Hello, {props.name}</h1>;
  }
```
---

### 3. JSX (JavaScript XML)
* 자바스크립트 코드 내에서 HTML과 유사한 마크업을 작성할 수 있게 해주는 문법 확장임.
* 브라우저 실행 전 Babel을 통해 일반 자바스크립트 객체로 변환됨.
* 자바스크립트 표현식을 사용할 때는 중괄호 `{ }`를 사용함.

---

### 4. Props (Properties)
* 부모 컴포넌트가 자식 컴포넌트에게 전달하는 **읽기 전용(Immutable)** 데이터.
* 컴포넌트 내부에서 수정할 수 없으며, 상위에서 하위로만 흐르는 단방향 데이터 흐름을 형성함.

#### propTypes
* 컴포넌트로 전달되는 Props의 타입을 사전에 검증하여 안정성을 높이는 도구.
* 예상치 못한 타입이 들어올 경우 콘솔 에러를 통해 개발자에게 알림.

---

### 5. State와 Event
#### State
* 컴포넌트 내부에서 관리되는 **동적인 데이터(상태)**.
* State의 값이 변경되면 React는 해당 컴포넌트를 자동으로 리렌더링하여 화면을 갱신함.

#### Event
* React의 이벤트는 카멜 케이스(camelCase)를 사용함 (예: `onClick`, `onChange`).
* HTML과 달리 이벤트 핸들러로 함수 그 자체를 전달함.
* 예: `<button onClick={handleClick}>클릭</button>`

* 핵심 요약

| 구분 | Props | State |
| :--- | :--- | :--- |
| **관리 주체** | 부모 컴포넌트 (외부) | 해당 컴포넌트 (내부) |
| **변경 가능성** | 불가능 (읽기 전용) | 가능 (상태 업데이트 시) |
| **역할** | 데이터 전달 및 설정 | 컴포넌트의 동적 상태 관리 |