# ☕ Java — 제어문(Control Flow) 및 배열(Array) 정리

## 1. 조건문 (Conditional Statements)

### ① if문 (if, Nested if)

조건식의 결과가 `true`일 때 실행됩니다. 중첩하여 사용할 수도 있습니다.

```java
// 기본 if문
if (num % 2 == 0) {
    System.out.println("입력한 숫자는 짝수입니다.");
}

// 중첩 if문 (양수이면서 짝수인 경우)
if (num > 0) {
    if (num % 2 == 0) {
        System.out.println("입력한 숫자는 양수이면서 짝수입니다.");
    }
}
```

### ② switch문 (Classic vs Modern)

정수, 문자, 문자열 등의 값에 따라 실행 지점을 결정합니다.

- **Classic Switch**: `break`가 없으면 다음 case까지 실행(fall-through)됩니다.
- **Modern Switch (Java 14+)**: 화살표(`->`)를 사용하며, 값을 직접 반환(yield)할 수 있어 간결합니다.

```java
// 향상된 switch문 예시
int modernResult = switch (op) {
    case '+' -> first + second;
    case '-' -> first - second;
    case '*' -> first * second;
    case '/' -> first / second;
    case '%' -> first % second;
    default -> {
        System.out.println("잘못 입력하셨습니다.");
        yield 0; // 복별한 로직 후 값 반환 시 yield 사용
    }
};
```

---

## 2. 반복문 (Looping Statements)

### ① for문

반복 횟수가 정해져 있을 때 주로 사용합니다. (예: 구구단 출력)

```java
for (int i = 2; i <= 9; i++) {
    System.out.println("---" + i + "단---");
    for (int j = 1; j <= 9; j++) {
        System.out.println(i + " * " + j + " = " + (i * j));
    }
}
```

### ② while문 vs do-while문

- **while**: 조건식을 먼저 검사하고 실행합니다. (0회 실행 가능)
- **do-while**: **무조건 1회는 실행**한 뒤 조건식을 검사합니다.

```java
// do-while 예시: 최소 한 번은 입력을 받음
do {
    System.out.println("문자열을 입력하세요('exit' 입력 시 종료) : ");
    str = sc.nextLine();
    System.out.println("입력한 문자열 : " + str);
} while (!str.equals("exit"));
```

---

## 3. 배열 (Array)

동일한 자료형을 연속된 메모리 공간에 저장하는 자료구조입니다.

- **특징**: `new` 연산자를 사용하여 **Heap 영역**에 할당됩니다.
- **인덱스**: 0부터 시작합니다.

```java
// 배열 선언 및 할당 (크기 5)
int[] score = new int[5];

// 인덱스를 이용한 값 대입
score[0] = 80;
score[1] = 90;
score[2] = 40;
score[3] = 10;
score[4] = 70;
```

---

## 💡 핵심 요약

1.  **조건문**: `switch` 문은 가독성이 좋지만 복잡한 범위 조건은 `if` 문이 유리합니다.
2.  **반복문**: 종료 조건이 명확하지 않을 때는 `while`을, 최소 1번의 실행이 보장되어야 하면 `do-while`을 선택합니다.
3.  **배열**: 배열의 크기는 한 번 지정하면 변경할 수 없으며, 인덱스 범위(`0` ~ `length-1`)를 넘지 않도록 주의해야 합니다.
