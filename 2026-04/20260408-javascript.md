# 🟨 JavaScript 기초 및 개요


### 1. JS 개요 및 환경 구축
* **정의**: 웹 브라우저에서 동작하는 유일한 프로그래밍 언어. (HTML/CSS는 마크업/스타일 문서)
* **특징**: 동적 타입 언어(런타임 결정), 인터프리터 언어.
* **Node.js**: 브라우저 외부 실행 환경. `node -v` 및 `npm -v`로 설치 확인 완료.
---

### 2. 변수와 상수 (ES5 vs ES6)
* **Strict Mode**: `"use strict";` 사용으로 안전한 코드 작성 유도.

| 특징 | `var` (ES5) | `let` (ES6) | `const` (ES6) |
| :--- | :--- | :--- | :--- |
| **스코프** | 함수 레벨 | 블록 레벨 | 블록 레벨 |
| **재선언** | ✅ 가능 | ❌ 불가능 | ❌ 불가능 |
| **재할당** | ✅ 가능 | ✅ 가능 | ❌ 불가능 |
| **호이스팅** | 선언 + 초기화 | 선언만 (TDZ 발생) | 선언만 (TDZ 발생) |

> **Note:** `const`는 선언과 동시에 반드시 값을 할당(초기화)해야 합니다.
---
### 3. 데이터 타입과 템플릿 리터럴
* **원시 타입**: `number`, `string`, `boolean`, `null`, `undefined`, `symbol` (Immutable)
* **템플릿 리터럴**: 백틱(`` ` ``)과 `${}`를 이용한 간결한 문자열 결합.
---
### 4. 타입 변환 (Type Conversion)
* **명시적 변환**: 개발자가 의도적으로 함수를 호출 (`Number()`, `String()`).
* **암묵적 변환**: JS 엔진이 문맥에 따라 자동 변환 (예: `1 + '2' = '12'`).
---
### 5. 연산자 (Operators)
* **비교**: `==`(동등, 타입 무시) vs `===`(일치, 타입 포함 - **권장**).
* **최신 연산자**: 
    * `?.` (옵셔널 체이닝): null/undefined 에러 방지.
    * `??` (null 병합): null/undefined일 때만 기본값 할당.
---
### 6. 제어문 (Control Flow)
프로그램의 실행 흐름을 조건이나 반복에 따라 제어하는 핵심 문법입니다.

#### ① 조건문 (Conditional Statements)
상태에 따라 다른 코드를 실행할 때 사용합니다.
* **`if...else`**
    * **구조:**
    ```javascript
    if (조건식) {
        조건식이 true인 경우 실행구문;
    } else {
        조건식이 false인 경우 실행구문;
        }
    ```

* **`if...else if...else` (범위와 논리)**
    * 여러 조건을 처리할 때 사용.
    * **구조**:
        ```javascript
        if (score >= 90) {
            console.log("A 등급");
        } else if (score >= 80) {
            console.log("B 등급");
        } else {
            console.log("C 등급");
        }
        ```
        
* **`switch` (값의 매칭)** 
    * 하나의 변수에 대해 여러 경우를 처리
    * **구조**:
        ```javascript
        switch (browser) {
            case 'Chrome':
                console.log('크롬입니다.');
                break;
            case 'Safari':
                console.log('사파리입니다.');
                break;
            default:
                console.log('지원하지 않는 브라우저입니다.');
        }
        ```
    #### 💡 제어 보조 키워드
    * **`break`**: 루프를 완전히 중단하고 탈출합니다.

#### ② 반복문 (Loop Statements)
동일한 작업을 자동화할 때 사용합니다.

* **`for` (횟수 중심)**
    * 반복 횟수가 명확할 때 사용.
    * **구조**:
        ```javascript
        for (초기화; 조건식; 증감식) {
            반복 실행할 코드;
        }
        ```
---
최종 수정일: 2026-04-08