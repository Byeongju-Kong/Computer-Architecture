# ISA and Performance

# Instruction Set Architecture

- 명령어 집합 구조라는 뜻으로, Hardware가 기계어에 따른 동작을 수행할 때, ISA를 통해 기계어를 해석하고 그에 맞는 동작을 수행하도록 하는 API이다.
- Example)
MIPS Architecture에서는 High-Level코드가 32개의 bit로 구성되어 이 32개의 bit를 통해서 Processor가 어떤 일을 수행하도록 하는데, 이 32개의 bit를 어떻게 구성시킬 것인지, 이 구성된 bit들이 Hardware에서 어떻게 동작되도록 할 것인지에 대한 약속이다.

# Assembly Language

- High-Level Code와 기계어 사이의 추상적인 레이어
- bit로 구성된 명령어를 개발자가 보다 쉽게 이해하기 위해 표현하는 방식이다.

---

# Performance

- 1 / Execution Time

## Clock Cycle Time

- 한 Clock Cycle을 수행하는데 걸리는 시간

## Clock Rate

- 시간 단위동안 몇 번의 Clock Cycle을 수행할 수 있는지( 보통 1second의 단위 )
Clock Rate = 1 / Clock Cycle Time

## Execution Time

- Clock Cycle Counts * Clock Cycle Time
- Clock Cycle Counts / Clock Rate
- ( 각 Instruction이 필요로 하는 Clock Cycle의 개수 * 해당 Instruction의 개수 )의 합 * Clock Cycle Time
Ex) ALU 명령어는 3Clock Cycle이 필요하고 명령어 개수는 4개 → ALU는 총 12개의 Clock Cycle
- CPI * Instruction Count * Clock Cycle Time

## CPI ( Clock cycles Per Instruction )

- ( 각 명령어가 차지하는 비율 * 각 명령어의 Clock Cycle 필요수 )들의 합
- CPI * Instruction count = 전체 Clock Cycle counts

## 벤치마크

- 하드웨어(프로세서)의 성능을 평가하는 지표

## Amdahl's Law(암달의 법칙)

어떤 명령어의 수행시간을 짧게 줄여 전체 실행시간을 줄이려고 할 때, 적용해야 하는 규칙

### Execution Time After Improvement

- Extime(new) = Extime(old) * ( 1- enhanced portion + enhanced portion / Speedup )
- Ex ) Extime이 3초인 10%의 ALU 연산을 2배 빨리 했다.
Extime(new) = 3 * (0.9 + 0.1/2) = 3 * 0.95 = 2.85

### - 전체 Instruction중에 많은 부분을 차지하는 Instruction의 성능을 향상 시켜야 한다.

## MIPS

- Million Instructions per second → 1초에 몇 백만개의 명령어 수행 가능한지
- MIPS는 명령어 마다 다른 Clock Cycle을 가진다는 것을 인지하지 못한다.