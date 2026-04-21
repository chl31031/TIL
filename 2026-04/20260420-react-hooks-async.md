# React Hooks 및 자바스크립트 비동기 처리 (Async)

## 1. React Hooks
함수형 컴포넌트에서 상태 관리와 생명주기 기능을 사용할 수 있게 해주는 기능입니다.

### ① useEffect
* **역할**: 컴포넌트가 렌더링될 때마다 특정 작업(Side Effect)을 수행하도록 설정합니다.
* **의존성 배열**: 배열에 넣은 값이 바뀔 때만 실행됩니다. 빈 배열(`[]`)을 넣으면 마운트 시에만 딱 한 번 실행됩니다.

### ② useMemo & useCallback (성능 최적화)
* **useMemo**: 연산량이 많은 함수의 **반환값**을 메모리에 저장(캐싱)하여, 재랜더링 시 불필요한 재연산을 방지합니다.
* **useCallback**: 특정 **함수 자체**를 메모리에 저장합니다. 자식 컴포넌트에 함수를 props로 넘길 때 불필요한 함수 재생성을 막기 위해 사용합니다.

### ③ useRef
* **역할 1**: DOM 요소에 직접 접근할 때 사용합니다 (예: 포커스 주기).
* **역할 2**: 렌더링과 상관없이 유지되어야 하는 값을 저장할 때 사용합니다. 값이 바뀌어도 컴포넌트가 리렌더링되지 않습니다.

### ④ Custom Hook
* **정의**: 여러 컴포넌트에서 반복되는 로직을 `use-`로 시작하는 함수로 분리하여 재사용하는 방식입니다.

---

## 2. 자바스크립트 비동기 (Async)
자바스크립트가 오래 걸리는 작업(API 호출 등)을 기다리지 않고 다음 코드를 실행할 수 있게 하는 방식입니다.

### ① Intro (비동기의 필요성)
* 자바스크립트는 싱글 스레드 언어이므로, 한 번에 하나의 작업만 처리합니다.
* 네트워크 요청 같은 작업이 완료될 때까지 브라우저가 멈추는 것을 방지하기 위해 비동기 처리가 필수적입니다.

### ② Promise
* **개념**: 비동기 작업의 최종 완료 또는 실패를 나타내는 객체입니다.
* **상태**: 
    * `Pending`(대기): 작업 진행 중
    * `Fulfilled`(이행): 작업 성공 (`.then()`으로 결과 처리)
    * `Rejected`(거부): 작업 실패 (`.catch()`로 에러 처리)

### ③ Async / Await
* **특징**: Promise를 기반으로 하지만, 비동기 코드를 마치 동기 코드처럼 읽기 쉽고 간결하게 작성할 수 있게 해주는 문법 설탕(Syntactic sugar)입니다.
* **사용**: 함수 앞에 `async`를 붙이고, Promise를 반환하는 호출 앞에 `await`를 사용합니다.

---

## 💡 코드 예시 (Hooks & Async)

```javascript
// Custom Hook 예시
function useWindowWidth() {
  const [width, setWidth] = useState(window.innerWidth);
  useEffect(() => {
    const handleResize = () => setWidth(window.innerWidth);
    window.addEventListener('resize', handleResize);
    return () => window.removeEventListener('resize', handleResize);
  }, []);
  return width;
}

// Async-Await 예시
async function fetchData() {
  try {
    const response = await fetch('[https://api.example.com/data](https://api.example.com/data)');
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error("데이터 로드 실패:", error);
  }
}
```