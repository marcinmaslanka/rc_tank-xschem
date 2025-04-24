# 🛠️ RC Low-Pass Filter (RC Tank) Simulation in Xschem

This project demonstrates how to build and simulate a simple **RC low-pass filter** ("RC Tank") in **Xschem**, using **custom Verilog-A models** for the resistor and capacitor.

---
## 🔧 Step-by-Step Instructions

### 1. Create Verilog-A Models

#### `res.va`

#### `cap.va`

In the working directory run the following instruction for a resistor and the capacitor separately:
```bash
/foss/designs/SKY/rc_tpf > openvaf rc_lowpass.va
Finished building rc_lowpass.va in 0.11s
```

## 📁 Project Structure

2. Setup Xschem
Open Xschem.

Make a new symbols for a resistor and capacitor. Set the Properties as depicted hier:

![Screenshot From 2025-04-24 13-56-26](https://github.com/user-attachments/assets/d39fa4a8-915d-4707-86ae-985bf6650351)


Add a new schematic file: rc_tank.sch.

Place the following components:

Voltage source (set to PULSE(0 1.8 0 100n 100n 50m 100m) for test)

`res_model.sym` and `cap.sym`

GND

Net labels: in, out, and vss

Connect as follows:

css
Vin → [my_resistor] → out → [my_capacitor] → GND


3. Set Simulation Parameters
Add a .control block or a separate .spice file with simulation commands like:

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

![Screenshot From 2025-04-24 14-01-26](https://github.com/user-attachments/assets/1c81aebb-df99-407e-822a-08178891a0b6)


4. Run Simulation

Netlist and Run

## 📈 Expected Output
The output voltage (V(out)) should show a low-pass behavior, smoothing out the sharp edges of the input pulse signal depending on the RC time constant.

## 🧠 Concepts Covered
Basic RC filter behavior

Use of custom Verilog-A models

Time-domain simulation with .tran

## ✅ Requirements
Xschem

Ngspice

---


