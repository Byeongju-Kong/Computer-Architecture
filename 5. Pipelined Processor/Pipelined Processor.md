# Pipelined Processor

# Pipelined Processor란?

![Pipelined%20Processor%20d123d040990c471a85dfbe51639078a1/_2021-06-24__3.59.08.png](Pipelined%20Processor%20d123d040990c471a85dfbe51639078a1/_2021-06-24__3.59.08.png)

![Pipelined%20Processor%20d123d040990c471a85dfbe51639078a1/_2021-06-24__4.05.09.png](Pipelined%20Processor%20d123d040990c471a85dfbe51639078a1/_2021-06-24__4.05.09.png)

### 한 명령어의 수행이 끝나야 다음 명령어의 수행을 할 수 있는 Sequential과 다르게
**한 Cycle에 여러 가지 명령어가 수행될 수 있도록 하는 것**

장점

→ 여러 가지 Unit들의 사용률을 향상 시킴

→ Performance가 향상됨

단점

→ 하드웨어 구성 및 Control Logic이 복잡해짐

→ Hazard가 발생

![Pipelined%20Processor%20d123d040990c471a85dfbe51639078a1/_2021-06-24__4.02.31.png](Pipelined%20Processor%20d123d040990c471a85dfbe51639078a1/_2021-06-24__4.02.31.png)

### 다음과 같이 한 명령어를 다음과 같은 기준으로 5개의 Stage로 구분

### 따라서, Stage를 구분하는 Stage Register가 추가적으로 필요

ex) Add명령어의 WB 단계에서 Register에 값을 Write하려고 하는데, 어떤 Register에 Write를 해야하는지에    
      대한 정보를 알아야 하기 때문 or 명령어의 Stage에 따른 Control Signal들을 참고하기 위해 필요
      

---

# Hazard

### 다음 명령어가 바로 Pipeline에서 실행되지 못하는 현상

## Structure Hazard

### 두개 이상의 명령어가 한 Cycle에서 같은 Source를 사용하고 있는 경우

![Pipelined%20Processor%20d123d040990c471a85dfbe51639078a1/_2021-06-24__4.08.56.png](Pipelined%20Processor%20d123d040990c471a85dfbe51639078a1/_2021-06-24__4.08.56.png)

한 Cycle에서 WB Stage가 동시에 두개가 실행됨

하지만 **Register의 Write Port는 1개**기 때문에, 두 명령어의 WB중 하나는 실행되지 않을 수 있음

### Solution 1) **Stall을 사용**하여 add 명령어의 4번째 Stage에서는 do nothing을 시킴.

![Pipelined%20Processor%20d123d040990c471a85dfbe51639078a1/_2021-06-24__4.12.11.png](Pipelined%20Processor%20d123d040990c471a85dfbe51639078a1/_2021-06-24__4.12.11.png)

### Solution 2) Register의 Write Port를 두개 사용

## Data Hazard

### 명령어의 순서에 따라 특정 Data의 Read-Write 순서가 바뀌는 상황

![Pipelined%20Processor%20d123d040990c471a85dfbe51639078a1/_2021-06-24__4.15.08.png](Pipelined%20Processor%20d123d040990c471a85dfbe51639078a1/_2021-06-24__4.15.08.png)

ADD의 명령어가 $1에 WB하기 전에 SUB 명령어가 $1을 RF/ID에서 Read한다.

→ ADD 명령어를 통해 **최신화되지 않은 $1의 값**이 SUB 명령어에서 **Read**된다.

### Data Hazard Solution 1) Stall

![Pipelined%20Processor%20d123d040990c471a85dfbe51639078a1/_2021-06-24__4.18.11.png](Pipelined%20Processor%20d123d040990c471a85dfbe51639078a1/_2021-06-24__4.18.11.png)

→ Stall을 삽입해 Do nothing을 시키고 앞선 명령어의 **WB Stage가 실행된 후** 다음 명령어의 **Read가 실행**되도록 한다.

→ **3 Clock Cycle을 낭비**하는 셈

### Data Hazard Solution 2) Change Clock Cycle

한 Cycle을 **두개의 Half Cycle**로 나누는 방법

![Pipelined%20Processor%20d123d040990c471a85dfbe51639078a1/_2021-06-24__4.21.33.png](Pipelined%20Processor%20d123d040990c471a85dfbe51639078a1/_2021-06-24__4.21.33.png)

→ CC5의 **앞 Half**에서 SUB 명령어의 **WB**이 실행되도록함
     CC5의 **뒤 Half**에서 AND 명령어의 **RF**가 실행되도록 함.

→ 하지만 **여전히 2 Clock Cycle을 Stall** 시켜야 함

### Data Hazard Solution 3) Forwarding

필요한 Data를 Data를 **필요로 하는 Unit으로 직접 전달해주는 방법**

![Pipelined%20Processor%20d123d040990c471a85dfbe51639078a1/_2021-06-24__4.28.50.png](Pipelined%20Processor%20d123d040990c471a85dfbe51639078a1/_2021-06-24__4.28.50.png)

→ EX단계 실행 후, EX/MEM Register에 있는 Data의 계산된 값을 필요로 하는 Unit으로 직접 전달해줌

![Pipelined%20Processor%20d123d040990c471a85dfbe51639078a1/_2021-06-24__4.33.14.png](Pipelined%20Processor%20d123d040990c471a85dfbe51639078a1/_2021-06-24__4.33.14.png)

→ 위의 그림과 같은 Forwarding Unit이 추가적으로 필요함.

→ Forward를 해야한다면 Forwarding Unit이 Mux 값을 Control하는 Logic인 것으로 보임

### Fowarding의 Limitation

LW 명령어에 의해 발생

![Pipelined%20Processor%20d123d040990c471a85dfbe51639078a1/_2021-06-24__4.39.27.png](Pipelined%20Processor%20d123d040990c471a85dfbe51639078a1/_2021-06-24__4.39.27.png)

→ LW의 MEM과 AND의 EX가 같은 Cycle에 있어 Forwarding이 될 것이라고 예상하지만
    Memory에 접근하는 **LW는 수행 시간이 길어 Clock Cycle의 후반부에 수행이 완료**됨
    하지만 **EX는 Clock Cycle의 전반부에 수행되기 때문에 Forwarding 불가능**

solution of Fowarding의 Limitation)
→ 어쩔 수 없이 한 Cycle의 Stall을 사용해야 한다.

### Solution 4) Compiler

![Pipelined%20Processor%20d123d040990c471a85dfbe51639078a1/_2021-06-24__4.42.48.png](Pipelined%20Processor%20d123d040990c471a85dfbe51639078a1/_2021-06-24__4.42.48.png)

→ Compiler가 Hazard가 발생할 것 같다고 인지되는 **명령어들의 순서를 변경**해줌

## Control Hazard

### **주로 Branch에 의해서 발생
Branch가 Taken 된다면 뒤따라오던 명령어 3개는 무용지물
→ 3 Clock Cycle의 낭비 초래**

![Pipelined%20Processor%20d123d040990c471a85dfbe51639078a1/_2021-06-24__4.44.29.png](Pipelined%20Processor%20d123d040990c471a85dfbe51639078a1/_2021-06-24__4.44.29.png)

### Control Hazard Solution 1) Stall

→ Branch에 해당하는 명령어의 결과를 알기 전까지 뒤의 명령어들을 Stall 시킴

### Control Hazard Solution 2) Prediction

→ 결과가 **Taken일지 Not-Taken일지 예측**하는 것

→ Taken인지 Not-Taken인지에 대한 **과거의 결과를 저장해두는 Table**을 활용

### Control Hazard Solution 3) Comparator

→ RF/ID Stage에서 Comparator라는 Unit으로 비교

→ Penalty를 1 Clock Cycle로 줄일 수 있음

→ 구현하기가 굉장히 어려움

**1bit Branch - Prediction**

![Pipelined%20Processor%20d123d040990c471a85dfbe51639078a1/_2021-06-24__4.49.17.png](Pipelined%20Processor%20d123d040990c471a85dfbe51639078a1/_2021-06-24__4.49.17.png)

→ Taken으로 예상하다가 Not-Taken 발생하면 Not-Taken으로 예상, 다시 Taken 발생하면 Taken 예상

**2bit Branch - Prediction**

![Pipelined%20Processor%20d123d040990c471a85dfbe51639078a1/_2021-06-24__4.50.52.png](Pipelined%20Processor%20d123d040990c471a85dfbe51639078a1/_2021-06-24__4.50.52.png)

연속 두번으로 예상과 다른 결과가 발생해야 예상하는 값이 바뀜.