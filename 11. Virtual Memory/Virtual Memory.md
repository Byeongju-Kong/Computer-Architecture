# Virtual Memory

![Virtual%20Memory%2076912712b9b54f64a218a7b89f060544/_2021-06-25__5.01.22.png](Virtual%20Memory%2076912712b9b54f64a218a7b89f060544/_2021-06-25__5.01.22.png)

M-M를 Cache와 Disk Storage사이의 또 다른 Cache로 간주

프로그램을 **Page라는 단위로 쪼개 필요한 부분만 M-M에 올려**서 사용

![Virtual%20Memory%2076912712b9b54f64a218a7b89f060544/_2021-06-25__5.11.29.png](Virtual%20Memory%2076912712b9b54f64a218a7b89f060544/_2021-06-25__5.11.29.png)

### 프로그램은 Virtual Address로 되어있고 CPU도 Virtual Address 사용 Memory는 Physical Address

→ Memory에 대한 매 접근 마다 Virtual Address를 **Physical Address로 변환
     해야함**

![Virtual%20Memory%2076912712b9b54f64a218a7b89f060544/_2021-06-25__5.14.26.png](Virtual%20Memory%2076912712b9b54f64a218a7b89f060544/_2021-06-25__5.14.26.png)

MMU(Memory Management Unit)가 **M-M에 있는 Page Table을 Look-Up**하고 Virtual to Physical, Physical to Virtual로 변환해줌

→ Page Table엔 Virtual - Physical Address에 대한 정보가 있음

## Page Fault

Processor가 참조하려는 Virtual Address의 Data가 M-M에 없는 상황
→**OS가 새로운 Page를 Storage에서 불러오고 Page Table에 새 Entry를 추가**

---

# Caching Page Table ( TLB )

![Virtual%20Memory%2076912712b9b54f64a218a7b89f060544/_2021-06-25__5.32.02.png](Virtual%20Memory%2076912712b9b54f64a218a7b89f060544/_2021-06-25__5.32.02.png)

### TLB : translation Lookaside Buffer

→Page Table에 cache 개념을 적용한 것

### 모든 Physical Address 접근시, TLB 먼저 확인

→ Hit이 발생하면 TLB에서 바로 Physical Address 얻을 수 있음.
→ Miss라면 M-M의 Page Table 확인해야 함

### TLB와 M-M는 독립적인 장치이기 때문에 동시 접근이 가능

→ TLB에서 Miss가 발생하고 나서 Page Table을 Look-up하는 것이 아니라, 
    동시에 접근하는 것