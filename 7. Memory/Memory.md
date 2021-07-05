# Memory

### 서로 다른 종류의 Strorage는 서로 다른 Access Time

# Non-Random Access Memory

### → Data의 위치에 따라 Access Time이 달라짐

1. Sequential : Data가 순차적으로 접근됨
2. Non-Sequential : Storage를 Block으로 나누어 접근
→ 결국 Block 내에서는 순차적인 접근
ex) HDD, CD-ROM

### → Non-Random Access는 Random Access에 비해
     10^5 ~ 10^8배 느린 Access Time

---

# Random Access Memory

## Dynamin Random Access Memory ( DRAM )

Data가 **주기적으로 Refresh**되어야 하기 때문에 → "Dynamic"

### 높은 Density ( 면적 대비 용량 ), 낮은 전력 소모 및 가격
→ Access Time이 SRAM보다 오래 걸림

## Static Random Access Memory ( SRAM )

Refresh하지 않아도, **전원만 공급된다면 Data가 영원히 유지** → "Static"

### 낮은 Density, 높은 전력 소모 및 가격
→ Access Time이 DRAM보다 2-10배 짧음
→ 고속의 Access가 필요한 App에서 많이 사용

---

# Locality

### → Program을든 특정 시간동안 상대적으로 적은 부분의 Address
     에 접근

## 90/10 Rule

→ **90%의 Access가 전체 Address 중 10%에서 이뤄짐
→ 실제로 유용하게 쓰이는 법칙**

## Temporal Locality ( 시간적 )

→ 특정 Data가 최근에 사용되었다면, **해당 Date가 곧 다시 사용될 가능성**이 높음

## Spatial Locality ( 공간적 )

→ 특정 Data가 최근에 사용되었다면, **그 주변 Data들이 곧 사용될 가능성**이 높음

---

# Memory Hierarchy Solution

![Memory%20f1321e02433e4bdba78aee45daa83452/_2021-06-25__3.28.06.png](Memory%20f1321e02433e4bdba78aee45daa83452/_2021-06-25__3.28.06.png)

### → 접근이 많은 것부터 Processor에 가까운 Memory에 배치