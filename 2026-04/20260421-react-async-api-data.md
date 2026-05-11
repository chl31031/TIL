# React 비동기 API 호출 및 Date 컴포넌트 처리

## 1. API 호출과 비동기 데이터 처리
React 컴포넌트 내에서 외부 API 데이터를 가져올 때는 `useEffect`와 `async/await`를 조합하여 사용합니다.

### ① 비동기 호출 패턴
* **마운트 시 호출**: 컴포넌트가 나타날 때 데이터를 가져오려면 의존성 배열을 빈 배열(`[]`)로 설정합니다.
* **로딩 및 에러 상태 관리**: 비동기 통신은 시간이 걸리거나 실패할 수 있으므로 `loading`과 `error` 상태를 별도로 관리하는 것이 사용자 경험(UX) 측면에서 좋습니다.

### ② 데이터 흐름
1. `useState`로 데이터, 로딩, 에러 상태 초기화
2. `useEffect` 내부에서 `async` 함수 정의 및 호출
3. `try...catch`문을 사용하여 에러 핸들링
4. 데이터 수신 완료 시 상태 업데이트 및 UI 렌더링

---

## 2. Date 컴포넌트 및 날짜 데이터 처리
서버에서 받아오는 날짜 데이터는 보통 ISO 형식(`2026-04-21T06:00:00Z`)이거나 타임스탬프 형태입니다. 이를 사용자 친화적인 형식으로 변환하여 화면에 보여주는 컴포넌트 구조가 중요합니다.

### ① 자바스크립트 Date 객체 주요 메서드
* `new Date(ISO_String)`: 문자열을 날짜 객체로 변환
* `toLocaleDateString()`: 로컬 환경에 맞는 날짜 형식 반환 (예: 2026. 4. 21.)
* `getFullYear()`, `getMonth() + 1`, `getDate()`: 개별 날짜 요소 추출

### ② 컴포넌트화 전략
* 날짜를 보여주는 로직이 반복된다면 별도의 `DateFormatter` 컴포넌트를 만들어 유지보수를 용이하게 합니다.

---

## 💡 통합 코드 예시

```javascript
import React, { useState, useEffect } from 'react';

// 1. 날짜 포맷팅 컴포넌트
const DateDisplay = ({ dateString }) => {
  const date = new Date(dateString);
  const formattedDate = date.toLocaleDateString('ko-KR', {
    year: 'numeric',
    month: 'long',
    day: 'numeric',
  });
  return <span>{formattedDate}</span>;
};

// 2. API 호출 메인 컴포넌트
function PostList() {
  const [posts, setPosts] = useState([]);
  const [isLoading, setIsLoading] = useState(true);

  useEffect(() => {
    const fetchPosts = async () => {
      try {
        const response = await fetch('[https://api.example.com/posts](https://api.example.com/posts)');
        const data = await response.json();
        setPosts(data);
      } catch (error) {
        console.error("API 호출 실패:", error);
      } finally {
        setIsLoading(false);
      }
    };

    fetchPosts();
  }, []);

  if (isLoading) return <div>로딩 중...</div>;

  return (
    <ul>
      {posts.map(post => (
        <li key={post.id}>
          <h3>{post.title}</h3>
          {/* 비동기로 받아온 날짜 데이터를 컴포넌트에 전달 */}
          <DateDisplay dateString={post.createdAt} />
        </li>
      ))}
    </ul>
  );
}
```

---

## 3. 핵심 요약
* **API 호출**: `useEffect` 안에서 비동기 로직을 처리하며, 불변성을 지켜 상태를 업데이트한다.
* **Date 처리**: 서버의 원본 데이터(Raw Data)를 UI 전용 컴포넌트(Formatter)를 통해 변환하여 가독성을 높인다.
* **비동기 상태**: `pending`(로딩), `fulfilled`(성공), `rejected`(실패) 각 단계에 맞는 UI 대응이 필요하다.
```