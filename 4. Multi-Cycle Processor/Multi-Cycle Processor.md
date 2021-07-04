# Multi-Cycle Processor

---

# Multi - Cycle Processor를 사용하는 이유

## Single-Cycle Processor

### 장점

- 한 Cycle에 하나의 Instruction
- 회로와 Clock을 단순화시킬 수 있다 → 모든 명령어들은 1의 CPI를 가진다.

### 단점

- 서로 다른 명령어를 수행하는데 걸리는 시간을 다르다. 따라서 연산을 위한 Unit들과 Memory를 비효율적으로 사용한다.
- Clock Cycle Time이 가장 시간이 오래 걸리는 경로에 의해 정해진다.( Memory 접근 명령어 )

## Multi-Cycle Processor

### 구현 방법

- 각 명령어를 여러 개의 Step들로 나눈다.
- 각 step이 한 Clock Cycle에 동작하도록 한다.
- 서로 다른 명령어는 서로 다른 CPI를 갖는다.

### 구조의 변화

- 각 Step을 나누기 위해 추가적인 Register를 사용한다.

### 장점

- Clock Cycle Time이 짧아진다.
- 단순한 명령어들은 짧은 시간 안에 처리할 수 있다.
- 계산을 위해 사용되는 Unit들이 하나의 Instruction의 각 Step에서 사용될 수 있다.(Unit의 효율 상승)

### 단점

- Step을 나누기 위해서 추가적인 Register를 사용해야 한다. (비용적인 측면인 듯 하다.)
- Design, 분석, 그리고 최적화 하기 위해 고려해야 할 Timing Path들이 많아진다.

---

# Multi-Cycle Division

1. Instruction Fetch ( Instruction Memory )
명령어를 패치 시킨다.
2. Instruction Decode and Operand Fetch ( Register )
명령어를 해독하고 각 bit의 값들을 Register에 배치시킨다
3. Execute ( ALU Unit etc. )
명령어 실행
4. Store result ( Memory or Register )
결과 값을 저장한다.
5. next Instruction
다음 명령어를 위한 준비

## Finite State Machine

- Control Signal이 더 이상 Decoded 명령어에 의해서만 정해지지 않기 때문에 각 step에 따른 다른 Control Signal이 필요하다.

---

# Multi-Cycle Processor uses only one Memory, ALU

- 같은 Clock Cycle 동안 여러 Step이 실행이 되는데, Memory를 하나를 둠으로써, 한 Clock Cycle에 Memory에 두번 접근하는 것을 구조적으로 방지한다.
- 산술/논리 연사, Memory 주소 계산, 다음 명령어를 계산하는데 하나의 ALU만 사용한다.

---

# Multi-Cycle의 Steps

![Multi-Cycle%20Processor%20034ac03ff18c46139e49b1ba66688d8c/_2021-04-28__5.23.09.png](Multi-Cycle%20Processor%20034ac03ff18c46139e49b1ba66688d8c/_2021-04-28__5.23.09.png)

![Multi-Cycle%20Processor%20034ac03ff18c46139e49b1ba66688d8c/_2021-04-28__5.24.03.png](Multi-Cycle%20Processor%20034ac03ff18c46139e49b1ba66688d8c/_2021-04-28__5.24.03.png)