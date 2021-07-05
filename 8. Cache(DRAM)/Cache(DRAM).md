# Cache ( DRAM )

### DRAM과 Processor사이의 Buffer로 사용되는 중간 Storage

### Locality를 활용

→ 가장 **저렴한 Memory**를 사용하면서 가장 **빠른 Access Speed**를 뽑는게 목표

### Compute System은 여러 단계의 Cache 사용

## Upper vs Lower

### Upper Cache → Processor에 가까운 Memory

### Lower Cache → Processor에서 먼 Memory

---

# Memory Hierarchy Terminology

## Block

→ **서로 다른 계층의 Storage 사이**에서 주고 받는 **Data의 단위**

## Entry

→ Cache를 **여러 개의 공간으로 쪼개는 단위**

## Hit

→ 접근하려는 Data가 해당 Level에 존재하는 경우

→ Hit Rate : 해당 Level에 Data가 존재하는 비율

→ Hit Time : 해당 Level의 Data에 접근하는데 걸리는 시간

## Miss

→ 접급하려는 Data가 해당 Level에 존재하지 않는 경우

→ Miss Rate : 1 - Hit Rate

→ Miss Penalty : Data를 Lower Level에서 불러오는 시간
                             + Upper Level에 Data를 저장하는 시간

💡 Miss가 떴어도, 해당 Data를 사용한 것이기 때문에, Upper Cache에 올려줘서
    해당 Data의 다음 접근을 수월하게 해줘야하기 때문

### Conflict Miss

→ **참조하려는 Entry에 찾는 Date가 없어서** 발생하는 Miss

### Capacity Miss

→ **Cache가 꽉차서 발생**하는 Miss

### Hit Time은 Miss Penalty보다 훨씬 짧다

### Access Time = Hit Time * Hit Rate 
                              + Miss Rate * Miss Penalty

---

## Exploting Locality in Cache

### Spatial Locality

→ 연속적인 Word Data 여러 개를 **하나의 Block으로 묶어 Upper Level로 이동**

### Temporal Locality

→ 가장 최근에 접근된 **Data를 Upper Level에 저장**

→ 특정 Level의 Cache 공간이 다 차도, **FIFO의 방식으로 공간을 마련**

---

## Splitting Caches

### Cache를 Data Cache와 Instruction Cache로 분리

→ 쪼개진 Cache는 Size가 작아져 **Miss Rate** ⬆️
→ 하지만, 분리된 두 개의 Cache에 **동시접근**이 가능하기 때문에 전체 성능은
    Unified Cache보다 **Splitted Caches가 더 좋음**