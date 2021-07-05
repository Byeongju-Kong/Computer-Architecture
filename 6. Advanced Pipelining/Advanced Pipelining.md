# Advanced Pipelining

### Instruction Level Parallelism (ILP)라고 부르는
명령어들의 Parallelism을 활용

# Superpipelining

![Advanced%20Pipelining%204b0ef5d94eda4d089673d2752bdb5451/_2021-06-25__2.48.57.png](Advanced%20Pipelining%204b0ef5d94eda4d089673d2752bdb5451/_2021-06-25__2.48.57.png)

### Clock Frequency를 높이는데 목적이 있음
→ 과거엔 Clock Frequency가 높으면 좋은 것이라는 인식때문

### Stage의 수가 더 많아지므로, 그에 따른 추가적인 Stage Register 필요

### Hazard Issue가 더 복잡해짐

# Super-Scalar

![Advanced%20Pipelining%204b0ef5d94eda4d089673d2752bdb5451/_2021-06-25__2.57.04.png](Advanced%20Pipelining%204b0ef5d94eda4d089673d2752bdb5451/_2021-06-25__2.57.04.png)

### 여러 개의 명령어를 동시에 불러와 실행

### 병렬 실행을 위해 n배의 Function Unit이 필요

### Register와 Memory에 더 많은 Port가 필요