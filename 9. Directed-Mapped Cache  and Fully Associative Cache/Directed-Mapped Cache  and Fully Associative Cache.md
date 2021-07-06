# Directed-Mapped Cache 
and Fully Associative Cache

# Directed Mapped Cache

![Directed-Mapped%20Cache%20and%20Fully%20Associative%20Cache%20fd5c73bc4e134287b748dd128ef0b422/_2021-06-25__3.57.44.png](Directed-Mapped%20Cache%20and%20Fully%20Associative%20Cache%20fd5c73bc4e134287b748dd128ef0b422/_2021-06-25__3.57.44.png)

### 각 Memory Block은 하나의 Single Cache Block에 Mapping

→ 어떤 Index의 Entry에 Mapping 될지는
    **Memory Address % Cache Block의 수**
    ex) 위의 그림에서, 000의 Entry에는 메모리주소가 0, 8, 16 등의 Data가
          Mapping 된다.

## Finding a Block

### Tag

→ 어떤 Index의 Block Data가 내가 찾는 Date인지 식별하기 위한 Bit

→ 메모리 주소의 상위 Bit 몇 개로 Tag를 사용

![Directed-Mapped%20Cache%20and%20Fully%20Associative%20Cache%20fd5c73bc4e134287b748dd128ef0b422/_2021-06-25__4.06.38.png](Directed-Mapped%20Cache%20and%20Fully%20Associative%20Cache%20fd5c73bc4e134287b748dd128ef0b422/_2021-06-25__4.06.38.png)

Directed Mapped Cache, Block Size - 4 Byte, Cache Size - 4KB

→ index의 개수 : Cache Size / Block Size = 4KB / 4B = 1024

### 메모리 주소의 마지막 2bit - Word 내에서 원하는 Byte 찾는 bit

### 다음 10bit는 Index와의 Mapping을 위한 bit

### 나머지 20bit가 Tag로 사용될 수 있음

## Limits of Directed Mapped Cache

→ **하나의 Index에 하나의 Block Data만 대응**되기 때문에 **Conflict Miss** 발생   
     확률이 높음

---

# Fully Associative Cache

Conflict Miss를 없애기 위해 **Cache의 Index의 개념 삭제**

![Directed-Mapped%20Cache%20and%20Fully%20Associative%20Cache%20fd5c73bc4e134287b748dd128ef0b422/_2021-06-25__4.22.34.png](Directed-Mapped%20Cache%20and%20Fully%20Associative%20Cache%20fd5c73bc4e134287b748dd128ef0b422/_2021-06-25__4.22.34.png)

### → Capacity Miss만 발생함

### → 모든 Entry의 Tag를 비교해야하므로, Access Time ⬆️