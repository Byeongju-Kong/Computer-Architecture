# Machine Language

## Register를 사용하는 이유

- 연산을 위해서 필수적으로 저장공간이 필요하다. 하지만, 메모리는 용량이 크기 때문에 Register라는 것을 사용한다.

## Register의 용량을 늘릴 수 없는 이유

- 기본적으로 용량을 늘리려면 물리적인 크기도 늘어나야한다. 
Register는 Processor안에 들어가는 장치로 Register가 커지면 Processor도 같이 커져야하기 때문이다.
- **Register가 커진다면 원하는 데이터가 있는 공간에 접근하는데 시간이 더 걸리기 때문이다.**

## 메모리 속 배열에 접근하는 방법

- Base Address + offset을 통해 접근을 한다.
- 배열의 첫번째 주소 + 첫번째 주소에서 얼만큼 떨어져있는가

## Offset 계산 방법

arr[i]에 접근하는 방법

( int배열 arr의 Base Address : $s0, 배열의 index [i] : $s1 ) 이라고 가정

1. Offset값 계산
arr배열 속 값들의 Primitive 타입은 Integer - 4Byte이기 때문에
add 연산을 통해 i값을 4배 시켜준다.

add $t0 $s1 $s1
add $t1 $t0 $t0     → $t1에는 4*i의 값이 저장된다.

2. Base Address + Offset 
add 연산으로 Base Address와 Offset을 더해준다.

add $t2 $s0 $t1   → $t2에는 arr[i]의 주소가 저장된다.

## Calling Convention

함수 호출 시에, Caller와 Callee가 데이터 값에 대한 처리를 어떻게 할 지에 대한 규약

### MIPS 에는 Caller Save, Callee Save, Hybrid Save가 있다.

## Caller와 Callee의 관계 예시

Caller : main 함수

Callee : 새로 정의된 함수 A

→ main함수에서 A함수를 호출하면 두 함수는 Caller와 Callee의 관계

## Caller Save

함수 호출 시, back-up needed Register의 백업을 Caller가 처리하는 방법

### Caller Save가 효율적인 경우

- Caller에서 $s0~$s2의 레지스터를 변수를 위한 공간으로 사용한다
- Callee에서 $s0~$s5의 레지스터를 변수를 위한 공간으로 사용한다

→ 백업 해야 할 레지스터는 $s0~$s2이다. 하지만 이를 Callee에서 Back-up한다면 $s0~$s5을 백업해야
    스택메모리에 6번 접근해야한다.
    하지만 Caller에서 Back-up을 한다면 $s0~$s2, 세 번의 스택메모리 접근만으로 Back-up을 완료가능하다.

## Callee Save

함수 호출 시, back-up needed Register의 백업을 Callee가 처리하는 방법

### Callee Save가 효율적인 경우

- Caller에서 $s0~$s5의 레지스터를 변수를 위한 공간으로 사용한다
- Callee에서 $s0~$s2의 레지스터를 변수를 위한 공간으로 사용한다

→ 백업 해야 할 레지스터는 $s0~$s2이다. 하지만 이를 Caller에서 Back-up한다면 $s0~$s5을 백업해야해서     

스택메모리에 6번 접근해야한다.

하지만 Callee에서 Back-up을 한다면 $s0~$s2, 세 번의 스택메모리 접근만으로 Back-up을 완료할 수 있다.

## Hybrid Save

함수 호출 시, Back-up needed Register의 백업을 Caller와 Callee가 나누어서 하는 경우

### Hybrid Save를 사용하는 이유

Caller의 입장에서는 어떤 레지스터가 permanent하게 필요하지 않다면 stack에 저장할 필요가 없고
Callee의 입장에서는 어떤 레지스터를 modify하지 않을 것이라면 stack에 저장할 필요가 없다.

→ $t0과 같은 temporary한 레지스터는 임시적인 공간으로 지속적으로 필요할 가능성이 적으므로 Caller가 
    save를 하고 $s0와 같은 permanent한 레지스터는 Caller에서 Permanent하게 필요할 가능성이 
    높은데, Callee가 해당 레지스터의 값을 modify한다면 save를 하는 것이 스택 메모리에 덜 접근을 할 수 있어 
    효율적이다.