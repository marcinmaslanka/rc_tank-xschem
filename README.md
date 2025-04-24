# 🛠️ RC Low-Pass Filter (RC Tank) Simulation in Xschem

This project demonstrates how to build and simulate a simple **RC low-pass filter** ("RC Tank") in **Xschem**, using **custom Verilog-A models** for the resistor and capacitor.

---

## 🔧 Step-by-Step Instructions

### 1. Create Verilog-A Models

Prepare your Verilog-A model files for the resistor and capacitor:

- `res.va`
- `cap.va`

Then, compile each model using `openvaf` (for example in your project directory):

```bash
/foss/designs/SKY/rc_tpf > openvaf res.va
Finished building res.va in 0.11s

/foss/designs/SKY/rc_tpf > openvaf cap.va
Finished building cap.va in 0.09s
```

2. Set Up Xschem
Open Xschem.

Create symbols for both res.va and cap.va.

Set their properties similar to the following:

![Screenshot From 2025-04-24 13-56-26](https://github.com/user-attachments/assets/25a0cf1c-a7fb-4a2d-9d9c-cb86a8e25ee0)


Create a new schematic file: rc_tank.sch.

Place the following components in the schematic:

Voltage source with waveform: PULSE(0 1.8 0 100n 100n 50m 100m)

res_model.sym (symbol for resistor)

cap.sym (symbol for capacitor)

GND

Net labels: in, out, and vss

Wire the components like this:

```css
Vin → [resistor] → out → [capacitor] → GND
```

3. Set Simulation Parameters
Add a simulation control block to the schematic or to an external .spice file:

```spice
.options savecurrents

.control
  save all
  op
  remzerovec
  write tb_rc.raw
  tran 10u 500m
  set appendwrite
  remzerovec
  write tb_rc.raw
.endc
```
Visual reference:

![Screenshot From 2025-04-24 14-01-26](https://github.com/user-attachments/assets/0ba7c560-228e-490b-881c-ba548baa97fb)


4. Run Simulation
In Xschem, click "Netlist and Run" to launch the simulation.
Then open the resulting .raw file in GTKWave or the waveform viewer.

## 📈 Expected Output
The output voltage V(out) will show typical low-pass behavior, smoothing the sharp edges of the input pulse. The shape depends on the RC time constant.

## 🧠 Concepts Covered
RC low-pass filter behavior

Use of custom Verilog-A models

Time-domain simulation with .tran

Netlist-based analog simulation flow

## ✅ Requirements
Xschem

Ngspice

GTKWave

openvaf from IIC-OSIC-TOOLS

## 🗂️ Project Structure (Example)
```bash
rc_tank/
├── cap.va              # Verilog-A model of capacitor
├── res.va              # Verilog-A model of resistor
├── rc_tank.sch         # Xschem schematic
├── rc_tank.sym         # Optional top-level symbol
├── testbench.spice     # Simulation commands
├── tb_rc.raw           # Simulation result file
└── README.md           # This file
```

---


