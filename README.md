# 🐍 Serpenti – Snake Game on PIC16F877A with GLCD

Serpenti is a classic Snake Game fully developed for the **PIC16F877A microcontroller**, integrated with a **128x64 Graphical LCD (GLCD)**, a **buzzer**, and **five tactile buttons**. Built using **CCS C**, this project showcases a complete real-time embedded system combining software and hardware in harmony.

> 🎮 Developed as a collaborative embedded systems project by [Eren Yurtcu](https://github.com/erenyurtcu) and [@berkinyl](https://github.com/berkinyl)

---

## 🎯 Project Objective

To develop an educational, real-time, and interactive game experience using:

- Low-level embedded C programming  
- Hardware control using GPIO (PORTB/PORTC)  
- Modular and efficient logic for constrained microcontrollers  
- Realistic Proteus simulation and breadboard implementation  

---

## 🧠 Features

✅ 10x10 Grid drawn dynamically using GLCD  
✅ Snake Movement via UP, DOWN, LEFT, RIGHT buttons  
✅ Game Reset using dedicated button  
✅ Difficulty Menu (Easy, Medium, Hard) with real-time visual selection  
✅ Score Tracking with real-time and session-based best score  
✅ Collision Detection: Wall and self-hit logic  
✅ Random Food Generation avoiding overlap with snake  
✅ Buzzer Feedback: Beeps for food, error melody for game over, victory tune  
✅ Victory Condition when snake reaches length 64  
✅ Screen transitions: Splash, Game Over, Victory, In-Game UI  
✅ Stable and responsive physical implementation  

---

## 🔌 Hardware Requirements

| Component         | Description                                      |
|------------------|--------------------------------------------------|
| Microcontroller   | PIC16F877A                                       |
| Display           | 128x64 GLCD (LGM12641BS1R)                       |
| Input             | 5 Tactile Push Buttons (UP, DOWN, LEFT, RIGHT, RESET) |
| Audio             | Active Buzzer with PNP Transistor driver         |
| Crystal Oscillator| 16 MHz with 22pF capacitors                      |
| Potentiometer     | 20kΩ for contrast adjustment                     |
| Breadboard + Wires| Standard prototyping setup                      |
| Power             | +5V Regulated Supply (USB-serial tested)         |

---

## 📌 Pin Mapping

| Component | Pin / Terminal | Connected To           | PIC Pin No | Description                                |
|-----------|----------------|------------------------|------------|--------------------------------------------|
| CRYSTAL   | Pin 1          | PIC16F877A – OSC1      | 13         | Crystal input (clock in)                   |
| CRYSTAL   | Pin 2          | PIC16F877A – OSC2      | 14         | Crystal output (clock out)                 |
| GLCD      | CS1            | RB0 / INT              | 33         | Chip Select 1                              |
| GLCD      | CS2            | RB1                    | 34         | Chip Select 2                              |
| GLCD      | DI (RS)        | RB2                    | 35         | Data/Instruction Select                    |
| GLCD      | RW             | RB4                    | 37         | Read/Write Control                         |
| GLCD      | E (EN)         | RB5                    | 38         | Enable Signal                              |
| GLCD      | RST            | RC0                    | 15         | Reset Signal                               |
| GLCD      | DB0            | RD0 / PSP0             | 19         | Data Bit 0                                 |
| GLCD      | DB1            | RD1 / PSP1             | 20         | Data Bit 1                                 |
| GLCD      | DB2            | RD2 / PSP2             | 21         | Data Bit 2                                 |
| GLCD      | DB3            | RD3 / PSP3             | 22         | Data Bit 3                                 |
| GLCD      | DB4            | RD4 / PSP4             | 27         | Data Bit 4                                 |
| GLCD      | DB5            | RD5 / PSP5             | 28         | Data Bit 5                                 |
| GLCD      | DB6            | RD6 / PSP6             | 29         | Data Bit 6                                 |
| GLCD      | DB7            | RD7 / PSP7             | 30         | Data Bit 7                                 |
| POT-HG    | Left (VCC)     | +5V Supply             | –          | Connected to +5V supply                    |
| POT-HG    | Middle (V0)    | LCD Pin 3              | –          | Contrast voltage input for GLCD           |
| POT-HG    | Right (VOUT)   | GND                    | –          | Ground reference                           |
| BUTTON    | UP             | RC1                    | 16         | Controls upward movement                   |
| BUTTON    | DOWN           | RC2                    | 17         | Controls downward movement                 |
| BUTTON    | RIGHT          | RC3                    | 18         | Controls right movement                    |
| BUTTON    | LEFT           | RC4                    | 23         | Controls left movement                     |
| BUTTON    | RESET          | RC5                    | 24         | Resets the system                          |
| BUZZER    | – Terminal     | PNP Emitter            | RB3        | Controlled via RB3 through PNP             |
| RESISTOR  | One end        | RB3                    | 36         | 100Ω to PNP base (current limiting)        |

---

## 🔩 Hardware Circuit Diagram

![Circuit Diagram](hardware/circuit_diagram.png)
  
---

## 🔧 Software & Tools

- CCS C Compiler  
- Proteus 8.0 or higher (for simulation)  
- GLCD Library (`glcd.c`)  
- Real-time embedded logic in modular C code  

---

## 🕹️ Game Logic Summary

### ➤ Snake Movement:
- Direction buttons mapped to `PORTC` pins (RC1 to RC4)  
- Movement restricted to grid bounds (10x10)  
- Snake grows when it eats food  

### ➤ Food Logic:
- Randomly generated on empty grid cells  
- Eating food:  
  - Increases score and snake length  
  - Triggers short beep  
  - Updates Best Score if needed  

### ➤ Game End:
- Game Over: Wall hit or self-collision → `"GAMEOVER !!!"` with error beeps  
- Victory: Reaching length 64 → `"YOU WON!"` + melody  

---

## ⚡ Circuit Overview

- **PORTD** → GLCD data lines  
- **PORTB** → GLCD control + Buzzer  
- **PORTC** → Button inputs  
- **RB3** → Controls buzzer via PNP transistor  
- **V0 (GLCD Contrast)** → Controlled via 20kΩ potentiometer  
- **Oscillator** → 16 MHz crystal + 22pF capacitors  

---

## 📦 Repository Contents

📄 **main.c** → Main game logic (snake, movement, GLCD drawing)  
📄 **main.h** → Header file for definitions and function declarations  
📄 **main.hex** → Compiled output ready to be flashed to PIC16F877A  
📄 **main.ccspjt** → CCS project file  
📄 **main.cof** → COF file for debugging in Proteus  
📄 **main.STA** → Compiler status file  
📄 **main.err** → Compilation error log (if any)  
📄 **main.lst** → Assembly listing file  
📄 **main.tre** → Symbol table (tree format)  
📄 **main.sym** → Compiler-generated symbol info  
📄 **main.esym** → Extended symbol file  
📄 **main.xsym** → Extra symbol information  
📁 **_history/** → Auto-generated backup history (by IDE or CCS)  
📄 **.gitattributes** → Git attributes (text encoding rules)  
