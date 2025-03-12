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

### Programmer Visible State
#### Memory
- array of storage locations indexed by an address

#### Registers
- Given special names in the ISA (as opposed to address)
- general vs. special purpose

#### Program Counter
- Memory address of the current instruction
다시 말해, 명렁어, 즉 프로그램은 programmer visible state의 값들을 어떻게 바꿔야 하는지 명시한다.

### General Instruction Classes
#### 산술 논리 연산 (예시: add, sub, and, or)
- 대체로 정수형 또는 실수형 명렁어로 분류될 수 있다.
1) 특정 위치에서 피연산자들을 가져온다.
2) 연산자들을 함수로 연산한다.
3) 특정 위치에 결과를 저장한다.
4) 다음 명렁어 위치로 pc를 업데이트한다.

#### Data movement operations (예시: move, load, store)
1) 특정 위치에서 피연산자들을 가져온다.
2) 특정 위치에 피연산자의 값들을 저장한다.
3) pc를 다음으로 옮긴다.

#### Control flow operations (예시: branch, jump)
1) 특정 위치에서 피연산자들을 가져온다.
2) branch 조건과 target address를 계산한다.
3) branch 조건이 참이면, pc를 target address로, 거짓이면, 다음 명령어로 업데이트한다.

### Atomicity of an Instruction
- 모든 명령어들은 소프트웨어 관점에서 완전히 실행되었거나, 아직 실행되었거나 둘중 하나이다.
- 다시 말해, 명령어에 의한, programmer visible state의 부분적인 업데이트는 관측되어서는 절대 안된다.
- 예시: semantics of a RISC-V instruction "ADDI x4, x5, 10"
    - GPR[x4] <- GPR[x5] + 10
    - PC <- PC + 4

### 초기의 ISA: EDSAC (1949)
- Single accumulator architecture

### Evolution of "Register" Architecture
- accumulator
- accumulator + address registers
- General-purpose registers

### Operand Sources?
- 피연산자의 개수
    - mondaic (예시: EDSAC)
    - dyadic (예시: IBM 360)
    - triadic (예시: MIPS)
- can ALU operands be in memory?
    - Yes (예시: x86/VAX/CISC)
    - No (예시: MIPS/RISC) -> load-store architecture
- How many different variations
    - a very few (예시: MIPS/RISC)
    - a lot (예시: x86)
    - everything goes (예시: VAX)

### Memory Addressing Modes
- absolute
    - immediate value를 주소로 사용.
- register indirect
    - GPR의 값을 주소로 사용.
- displaced of based
    - GPR+offset의 값을 주소로 사용.
- indexed
    - GPR[r_base]+GPR[r_index]의 값을 주소로 사용.
- memory indirect
    - M[GPR]의 값을 주소로 사용.
- auto inc/decrement
    - GPR[r_base]의 값을 주소로 사용하고, GPR[r_base]를 더하거나 뺀다.

### VAX-11: ISA in Mid-life Crisis
- 최초의 상업적인 32비트 머신.

### RISC (Reduced Instruction Set Computer)