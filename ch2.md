# Chapter 2: Instruction Set Architecture
[목차](index.md)<br><br>

### 컴퓨터가 하는 일을 어떻게 나타낼까?
#### Architecture (ISA) level
- 자동차: 운전 매뉴얼과 사용법
    - 운전하기 위해서는 자동차 메카닉이 될 필요는 없다.
- 컴퓨터: 명렁어 집합 매뉴얼 (예시: Intel x86-64, Arm v8, RISC-V)
    - 컴퓨터를 사용하기 위해서 회로 디자이너가 될 필요는 없다.

#### Microarchitecture (implementation) level
- 자동차의 디자인에는 전기 및 기계적 구성 요소가 있다.
- 컴퓨터의 설계에는 datapath 및 control logic unit 구성 요소가 있다.

#### circuit level
- 자동차: metal sheets, cranks, shafts, gears, ...
- 컴퓨터, 게이트, 와이어, 반도체, 트랜지스터, ...

### Stored Program (von Neumann) Architecture
- stored-program architecture
    - 명령어는 선형 메모리에 들어 있다.
        - 명렁어와 데이터는 메모리에 있다.
    - 명렁어는 데이터처럼 수정될 수 있다.
        - 둘다 0과 1로 구성되어 있다.

- Sequential instruction processing
    - Program Counter는 현재 명령어의 위치를 가리킨다.
    - 명령어는 메모리에서 가져와서 실행된다.
    - program counter is advanced (according to instruction)
    - 반복한다.

### von Neumann vs. Dataflow
폰 노이만 구조
- 프로그램의 순서?
- 저장소 위치?

Dataflow: 명령어가 dataflow depenced에 의해 정렬되어 있다.
- 각 명령어는 누가 결과를 받아야 되는지 명시되어 있다.
- 명령어는 모든 피연산자들을 받았을때면 언제든지 실행될 수 있다.

## Instruction Set Architecture (ISA) "User's manual for the computer"
### ISA에는 무엇이 명시되어 있고, 결정되어 있는가?
- Data Types
    - Encoding and representation
- Memory Model
- Program Visible State
    - General registers
    - Memory space
    - program counter
    - processor status
- Instruction Set
    - instructions and formats
    - addressing modes
    - data structures
- System Model
    - States
    - Privilege
    - Interrupts
    - IO
- External Interfaces
    - IO
    - Management