# N-Way Set Associative  Cache

![N-Way%20Set%20Associative%20Cache%205bfb85204371401fbe901dd8ca9dd3c4/_2021-06-25__4.27.28.png](N-Way%20Set%20Associative%20Cache%205bfb85204371401fbe901dd8ca9dd3c4/_2021-06-25__4.27.28.png)

### 각 Index에 N개의 Entry가 할당됨

→ N개의 Directed Mapped Cache가 병렬적으로 동작

### Data를 찾을 때 해당 Index로 접근해 N번의 비교만 하면 됨

### N이 커지면 Hit Rate가 증가

→ 하지만, 너무 커지면 비교할 Entry가 많아져 Hit Time ⬆️

## Cache Block Replacement Policy - LRU

→ Least Recently Used로 **가장 최근에 사용되지 않은** Block 쫓아냄.

## Compulsory / Cold Start

### → Cache의 첫번째 접근엔, Conflict Miss가 무조건 발생

      Solution) Block Size를 늘리는 것
                      → 첫 접근에 최대한 많은 Data를 가져와 다음 번의 접근에서 Miss가 
                          뜰 확률을 낮춤

---

# Cache Write Policy

## Write - Through

→ Main Memory는 **Cache에 값을 쓸 때마다** Update됨
→ 단순하지만 느리고, **Memory Traffic을 증가시킴**
→ Cache의 Block Data를 쫓아낼 때, **단순 덮어쓰기**를 하면 됨

### Write Buffer for Write - Through

![N-Way%20Set%20Associative%20Cache%205bfb85204371401fbe901dd8ca9dd3c4/_2021-06-25__4.48.03.png](N-Way%20Set%20Associative%20Cache%205bfb85204371401fbe901dd8ca9dd3c4/_2021-06-25__4.48.03.png)

→ Processor가 data를 Cache와 Write Buffer에 쓰면
    Memory Controller가 **Buffer의 내용을 천천히 Memory에 Update**함

## Write - Back

→ Cache에 값을 쓸 때, Main Memory를 바로 Update하지 않고
    해당 Entry의 값과 MM의 **값이 다르다 것을 Dirty Bit로 Check해둠**
→ Cache의 Block Data를 쫓아낼 때, **MM에 Update를 해주고 덮어써야함**