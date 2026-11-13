# 8-Bit Von Neumann Machine & ALU (Logisim-evolution)

A custom-built, educational **8-bit Arithmetic Logic Unit (ALU)** and processor architecture designed entirely from fundamental logic gates and modular blocks using **Logisim-evolution**. This project emphasizes manual datapath implementation, control signal management, and hardware-level signal routing without high-level library shortcuts.

---

## 🏗️ Architecture & Datapath Overview

The system features an 8-bit datapath governed by a robust selection mechanism, supporting core arithmetic, logical, comparison, and shifting operations. 

### 1. Basic Arithmetic Building Blocks
The arithmetic foundation starts from fundamental components and scales up to an 8-bit cascading architecture:
- **Half Adder:** Combines an AND gate for the carry and an XOR gate for the sum.
  
  ![Half Adder](half_adder.png)

- **Full Adder Implementation:** Integrates carry inputs and propagation logic.
  
  ![Full Adder](full_adder.png)

- **8-Bit Ripple Carry Adder:** Cascades individual adders from $z_0$ to $z_7$ to handle full byte arithmetic with a global `carry_out`.
  
  ![8-Bit Adder](8_bit_adder.png)

### 2. ALU Arithmetic & Control Routing
The core arithmetic unit combines XOR-based conditional inversion (for subtraction and increments/decrements) with an 8-bit adder and multiplexed carry routing.

![ALU Arithmetic Unit](alu_arithmetic.png)

### 3. Signal Integrity & Conflict Management
To prevent short-circuit errors (`E`) caused by conflicting direct outputs, controlled buffers and pull-resistors are utilized for safe tri-state bus management:
- **Signal Conflict Detection:** Direct wiring of conflicting logic states results in simulation errors.
  
  ![Signal Conflict](signal_conflict.png)

- **Controlled Buffer & Tri-State Isolation:** Using tri-state buffers and pull-up/pull-down resistors to cleanly gate data flow.
  
  ![Controlled Buffer Circuit](controlled_buffer.png)

### 4. Multiplexing & Signal Control
To avoid bus conflicts and manage multiple operation slots cleanly, multiplexer arrays and tri-state buffer configurations handle data flow and high-impedance ($Z$) states.

- **Multiplexer Routing:**
  
  ![Multiplexer Routing](multiplexer_array.png)

### 5. Relational Comparator Module
The relational comparison block evaluates operand conditions ($A = B$, $A > B$, $A < B$) independently before mapping them onto the datapath bus.

![Comparator Logic](comparator.png)

### 6. Top-Level ALU Overview
The complete integrated ALU schema combining all 16 operations via a 4-bit selection bus ($S_3, S_2, S_1, S_0$).

![Top-Level ALU](top_level_alu.png)

---

## ⚙️ Supported Operations (4-Bit Selection Bus / 16 Operations)

The ALU supports up to 16 core operations mapped via selection control lines ($S_3, S_2, S_1, S_0$):

### Arithmetic & Comparison Operations (`0` – `7`)
1. **`0000` ($0$):** $A + B$ (Addition)
2. **`0001` ($1$):** $A - B$ (Subtraction)
3. **`0010` ($2$):** $A++$ (Increment $A$)
4. **`0011` ($3$):** $A--$ (Decrement $A$)
5. **`0100` ($4$):** $A + B + C_{in}$ (Addition with Carry)
6. **`0101` ($5$):** $A - B - C_{in}$ (Subtraction with Borrow)
7. **`0110` ($6$):** $\text{NOT } A$ (Bitwise Inversion)
8. **`0111` ($7$):** $A \ge B$ (Relational Comparison)

### Logic, Shift & Control Operations (`8` – `F`)
9. **`1000` ($8$):** $A \text{ AND } B$ (Bitwise AND)
10. **`1001` ($9$):** $A \text{ OR } B$ (Bitwise OR)
11. **`1010` ($A$):** $A \text{ XOR } B$ (Bitwise XOR)
12. **`1011` ($B$):** $A \text{ NOR } B$ (Bitwise NOR)
13. **`1100` ($C$):** $A \ll 1$ (Shift Left with $C_{in}$ into $a_0$)
14. **`1101` ($D$):** $A \gg 1$ (Shift Right with $C_{in}$ into $a_7$)
15. **`1110` ($E$):** $A$ (Pass $A$ directly to output)
16. **`1111` ($F$):** $0$ (Clear / Force output to zero)

---

## 🚀 Getting Started

1. Download and install Logisim
2. Clone or download this repository to your local machine.
3. Open the main `.circ` project file within Logisim-evolution to explore sub-circuits, test the ALU interactive simulation using the hand tool, and inspect the register file integration.

---

## 🛠️ Next Steps in Development
- Implementing the Register File ($R_0, R_1$, Accumulator).
- Integrating Instruction Memory (RAM/ROM) for Von Neumann execution cycles.
- Developing the Control Unit (CU) instruction decoder.
