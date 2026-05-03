# 🐻 Zustand: React 상태 관리 라이브러리

Zustand는 독일어로 **'상태'**라는 뜻을 가진 라이브러리로, 단순하고 빠르며 확장 가능한 상태 관리 솔루션을 제공합니다.

---

### 1. Zustand가 필요한 이유

- **Prop Drilling 해결**: 컴포넌트 트리가 깊어질 때, 상태를 하위 컴포넌트로 전달하기 위해 중간 컴포넌트들이 불필요하게 props를 넘겨주는 문제를 방지합니다.
- **공통 상태 관리**: 로그인 정보, 테마 설정 등 여러 페이지나 서비스 전반에서 공통으로 사용되는 상태를 중앙에서 효율적으로 관리할 수 있습니다.
- **낮은 학습 곡선**: Redux에 비해 설정이 매우 간단하며, Boilerplate 코드가 적어 직관적인 개발이 가능합니다.

---

### 2. 설치 방법 (Installation)

터미널에서 아래 명령어를 입력하여 설치합니다.

```bash
npm install zustand
```

---

### 3. 기본 사용법 (Basic Usage)

#### ① 스토어(Store) 생성

`create` 함수를 사용하여 상태(State)와 이를 업데이트하는 함수(Action)를 정의합니다.

```javascript
import { create } from "zustand";

// 전역 상태 저장소 정의
export const useStore = create((set) => ({
  bears: 0, // 상태

  // 상태 업데이트 액션
  increasePopulation: () => set((state) => ({ bears: state.bears + 1 })),

  // 상태 초기화 액션
  removeAllBears: () => set({ bears: 0 }),

  // 특정 값으로 업데이트
  updateBears: (newBears) => set({ bears: newBears }),
}));
```

#### ② 컴포넌트에서 사용

생성한 `useStore` 훅을 컴포넌트 내부에서 호출하여 상태를 구독하고 액션을 사용합니다.

```javascript
import { useStore } from "./store"; // 스토어 임포트

function BearCounter() {
  const { bears, increasePopulation, removeAllBears } = useStore();

  return (
    <div>
      <h1>곰 마릿수: {bears}</h1>
      <button onClick={increasePopulation}>한 마리 추가</button>
      <button onClick={removeAllBears}>모두 삭제</button>
    </div>
  );
}
```

---

### 4. Zustand의 동작 원리 요약

1.  **Store**: `create` 함수로 만든 중앙 집중식 저장소입니다.
2.  **set**: 상태를 변경하는 함수로, 기존 상태를 인자로 받아 새로운 상태를 병합(Merge)합니다.
3.  **Subscribing**: 컴포넌트가 `useStore`를 호출하면 스토어의 상태 변화를 감시(Subscribe)하며, 관련 상태가 변경될 때만 자동으로 리렌더링됩니다.

---
