# 🌐 DOM 요소 선택 및 조작 기초 

### 1. DOM(Document Object Model) 개요
* 브라우저는 HTML 문서를 로드한 후, 각 태그를 객체화하여 트리 형태의 구조로 만듭니다.
* 자바스크립트는 이 DOM 트리를 통해 HTML의 구조, 스타일, 내용을 동적으로 변경할 수 있습니다.

---

### 2. 핵심 요소 선택자
과거에는 `getElementById`나 `getElementsByClassName`을 사용했으나, 현대 자바스크립트에서는 CSS 선택자를 그대로 사용하는 방식을 권장합니다.

#### ① `document.querySelector('selector')`
* **특징**: 제공한 CSS 선택자와 일치하는 **첫 번째 요소 하나**만 반환합니다.
* **활용**: ID 선택자(`#apple`)나 특정 클래스의 첫 번째 요소를 잡을 때 유용합니다.

#### ② `document.querySelectorAll('selector')`
* **특징**: 선택자와 일치하는 **모든 요소**를 찾아 **NodeList**라는 유사 배열 형태로 반환합니다.
* **활용**: 여러 요소에 공통된 스타일을 적용하거나 반복문(`forEach`)을 돌릴 때 필수적입니다.
