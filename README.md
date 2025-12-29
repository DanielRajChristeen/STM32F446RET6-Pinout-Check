# **STM32F446RET6 – Pinout Check (Register-Level)**

A **bare-metal GPIO pin verification project** for the STM32F446RET6, written using **direct register access** — no STM32CubeMX, no HAL pin configuration, no abstraction layers.

This project is designed to **validate MCU pin connectivity at the hardware level** by configuring GPIO registers manually and toggling pins for physical verification (LED / multimeter / logic probe).

---

## 🎯 Project Objective

Before writing complex firmware, every embedded engineer must answer one simple question:

> **“Are my pins wired correctly?”**

This repository solves exactly that problem using:

* **Direct register manipulation**
* **Full control over GPIO configuration**
* **Zero auto-generated code**

Think of this as a **power-on self-test** for STM32F446RET6 pin integrity.

---

## 🧠 Why Register-Level Coding?

This project intentionally avoids CubeMX and HAL because:

* ✔️ You **learn how the MCU actually works**
* ✔️ No hidden code generation
* ✔️ No pin configuration magic
* ✔️ Perfect for debugging schematics and PCBs
* ✔️ Faster execution, zero overhead

If you understand this repo, you understand **real embedded systems**.

---

## 🧰 What This Project Does

* Enables GPIO peripheral clocks using `RCC`
* Configures GPIO pins via:

  * `MODER`
  * `OTYPER`
  * `OSPEEDR`
  * `PUPDR`
* Toggles pins directly using:

  * `ODR` (Output Data Register)
* Helps visually confirm pin behavior using LEDs or probes

---

## 📁 Repository Structure

```
STM32F446RET6-Pinout-Check/
├── Core/
│   ├── Src/
│   │   └── main.c            # Register-level GPIO logic
│   ├── Inc/
│       └── main.h
├── Drivers/
│   └── CMSIS/                # Core & device headers
├── startup_stm32f446xx.s     # Startup file
├── STM32F446RETx_FLASH.ld    # Linker script
├── .cproject
├── .project
└── README.md
```

> 💡 **No `.ioc` file is used for pin configuration**
> All pin settings are written manually in C.

---

## 🔌 Hardware Requirements

* STM32F446RET6 (Nucleo or custom board)
* LEDs + resistors **or**
* Multimeter / logic analyzer
* ST-LINK (onboard or external)

---

## 🚀 Getting Started

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/DanielRajChristeen/STM32F446RET6-Pinout-Check.git
```

---

### 2️⃣ Open in STM32CubeIDE

* File → Open Projects from File System
* Select the cloned directory

---

### 3️⃣ Understand the Core Flow (main.c)

At a high level, the firmware does:

1. Enable GPIO clock
2. Set pin mode as output
3. Toggle pin state
4. Observe hardware response

Example (conceptual):

```c
RCC->AHB1ENR |= RCC_AHB1ENR_GPIOAEN;
GPIOA->MODER |= (1U << (5 * 2));
GPIOA->ODR ^= (1U << 5);
```

This is **raw MCU control** — exactly how datasheets intend it.

---

### 4️⃣ Build & Flash

* Click **Build**
* Click **Debug / Run**
* Observe LEDs or pin voltage changes

---

## 🧪 How to Use This for Pin Checking

1. Connect an LED (with resistor) to a target pin
2. Modify the pin number in code
3. Re-flash
4. Confirm LED toggles
5. Repeat for other pins

This process verifies:

* GPIO routing
* Board layout
* MCU health
* Schematic correctness

---

## 📘 Who Should Use This Repo?

* 🔰 Beginners learning STM32 internals
* 🧑‍💻 Embedded engineers debugging boards
* 🧠 Anyone transitioning from HAL → Register coding
* 🛠 Engineers validating new PCB designs

---

## 📈 Learning Outcomes

After working with this project, you will understand:

* GPIO registers in STM32
* Clock enabling via RCC
* Bare-metal firmware flow
* Startup + linker basics
* Why abstraction layers exist (and when not to use them)

---

## 📝 License

This project is licensed under the **MIT License**.

```
MIT License

Copyright (c) 2025 Daniel Raj Christeen

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND.
```

---

Have a Great Developing Ahead!
