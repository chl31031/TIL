# JavaScript DOM 선택 및 조작 마스터

### 1. DOM 요소 선택 (Selection)
가장 현대적이고 권장되는 방식은 `querySelector` 시리즈를 사용하는 것입니다.

* **`querySelector(selector)`**: CSS 선택자와 일치하는 **첫 번째 요소** 하나만 반환합니다.
* **`querySelectorAll(selector)`**: 일치하는 모든 요소를 **고정된 `NodeList`**로 반환합니다. `forEach`를 바로 사용할 수 있어 편리합니다.
* **주의: Live Object 문제**:
    * `getElementsByClassName`, `getElementsByTagName` 등이 반환하는 `HTMLCollection`은 노드의 변화를 실시간으로 반영하는 '살아있는' 객체입니다. 
    * 반복문 도중 요소의 클래스를 바꾸면 리스트의 인덱스가 꼬이는 버그가 발생할 수 있습니다.
    * **해결책**: `[...$collection]` 처럼 스프레드 문법을 사용해 **진짜 배열로 변환** 후 작업하세요.

---

### 2. 텍스트 조작 (Text Manipulation)
| 속성 | 특징 | 비고 |
| :--- | :--- | :--- |
| **`textContent`** | 요소 내의 모든 자식 텍스트를 가져오거나 변경. | **가장 권장 (안전/빠름)** |
| `innerText` | CSS 스타일이 반영된(눈에 보이는) 텍스트만 취급. | 성능이 다소 느림 |
| `nodeValue` | 텍스트 노드 자체의 값. 요소 노드에서 쓰려면 자식으로 들어가야 함. | 번거로움 |

---

### 3. DOM 생성 및 노드 조작 (Remodeling)
HTML 구조를 변경하는 세 가지 주요 시나리오입니다.

### ① `innerHTML` (전체 교체)
- 내부를 새로운 HTML 문자열로 싹 갈아엎을 때 사용합니다.
- **위험성**: 사용자 입력을 그대로 넣을 경우 **XSS(교차 사이트 스크립팅) 공격**에 노출될 수 있습니다.

### ② `insertAdjacentHTML` (특정 위치 삽입)
- 기존 내용을 유지하면서 원하는 위치(`beforebegin`, `afterbegin`, `beforeend`, `afterend`)에 요소를 끼워 넣습니다.

### ③ `createElement` & `appendChild` (정석 조립)
- `document.createElement('li')`로 요소를 만들고 `textContent`를 부여한 뒤 `appendChild`로 조립합니다.
- **최적화**: 여러 요소를 한 번에 추가할 때는 `document.createDocumentFragment()`라는 임시 바구니를 사용하여 **DOM 접근 횟수**를 줄이는 것이 성능에 좋습니다.

---

### 4. 어트리뷰트(Attribute) vs 프로퍼티(Property)
- **Attribute**: HTML 파일에 기록된 **초기 설정값**. (`getAttribute`로 접근)
- **Property**: 자바스크립트 엔진이 관리하는 **실시간 최신 상태**. (객체 점 표기법으로 접근)
- **실무 팁**: 사용자가 입력한 최신 값을 가져올 때는 반드시 **`.value` 프로퍼티**를 사용해야 합니다.
- **Data Attribute**: `data-board-id`처럼 작성하고 JS에서 `.dataset.boardId`로 읽어와 커스텀 데이터를 관리합니다.

---

### 5. CSS 조작 (Style & Class)
1.  **`element.style`**: 인라인 스타일을 직접 수정합니다. (예: `$box.style.backgroundColor = 'red'`)
2.  **`element.classList`**: 클래스를 제어하는 가장 깔끔한 방법입니다.
    - `.add('className')`: 추가
    - `.remove('className')`: 삭제
    - `.toggle('className')`: 있으면 제거, 없으면 추가
    - `.contains('className')`: 확인 (true/false)
