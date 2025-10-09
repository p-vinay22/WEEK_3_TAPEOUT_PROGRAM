# ⚙️ BabySoC – Gate Level Simulation (GLS)

with the **new iverilog command integrated**, all paths corrected to **vinay/vin**, and clear placeholders for your images 🖼️.
This version is **GitHub-ready**, visually neat, and consistent with your earlier BabySoC reports.

---

# ⚙️ BabySoC – Gate Level Simulation (GLS)

## 🧩 Post-Synthesis Simulation Report

---

## 🎯 **Purpose of GLS**

Gate-Level Simulation (GLS) is performed **after synthesis** to verify that the **design’s functionality** is maintained when converted from RTL (Register Transfer Level) to a **gate-level netlist**.

Unlike RTL simulation, GLS operates at the **netlist level**, including **actual gates, cells, and timing delays**.

---

## 🔍 **Key Aspects of GLS for BabySoC**

### ⏱️ 1. Verification with Timing Information

* GLS uses **Standard Delay Format (SDF)** files to ensure **timing correctness**.
* It validates that the SoC behaves as expected **under real-world timing constraints**.

### 🧠 2. Design Validation Post-Synthesis

* Confirms that **logical behavior** is maintained after synthesis.
* Ensures the design is **free from metastability and glitches**.

### 🧰 3. Simulation Tools Used

* **Synthesis Tool:** Yosys
* **Simulation Tool:** Icarus Verilog
* **Waveform Viewer:** GTKWave

### 💡 4. Why GLS is Important for BabySoC

BabySoC integrates multiple blocks — **RISC-V Processor, PLL, DAC, Clock Gate**, etc.
GLS ensures that:
✅ Each module interacts correctly.
✅ Timing and logic integrity are preserved in the synthesized design.

---

## 🧪 **Step-by-Step GLS Flow**

---

### 🧩 **Step 1: Load the Top-Level Design and Supporting Modules**

Launch **Yosys**:

```bash
yosys
```

Inside the Yosys shell, run:

```bash
read_verilog /home/vinay/vin/VSDBabySoC/src/module/vsdbabysoc.v
read_verilog -I /home/vinay/vin/VSDBabySoC/src/include /home/vinay/vin/src/module/rvmyth.v
read_verilog -I /home/vinay/vin/VSDBabySoC/src/include /home/vinay/vin/src/module/clk_gate.v
```

📸 Yosys 
<img width="829" height="604" alt="image" src="https://github.com/user-attachments/assets/bc08100f-8f41-4b1c-be1a-cd3ef223bbfc" />

 ### Top-Level Design and Supporting Modules

<img width="829" height="604" alt="image" src="https://github.com/user-attachments/assets/0eaddfa6-ff62-4389-9634-b8e2c4de315f" />
<img width="829" height="604" alt="image" src="https://github.com/user-attachments/assets/425ed175-8db3-47b4-bad9-c9b34aca72d7" />
<img width="829" height="604" alt="image" src="https://github.com/user-attachments/assets/5e9b3246-3904-4006-afc8-f28cedc4fe87" />

---

### 📚 **Step 2: Load Liberty Files for Synthesis**

```bash
read_liberty -lib /home/vinay/vin/VSDBabySoC/src/lib/avsdpll.lib
read_liberty -lib /home/vinay/vin/VSDBabySoC/src/lib/avsddac.lib
read_liberty -lib /home/vinay/vin/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
### 📸 Liberty Files
<img width="829" height="604" alt="image" src="https://github.com/user-attachments/assets/55c87bf7-7c9e-46d0-af02-62ed774d231e" />
<img width="829" height="604" alt="image" src="https://github.com/user-attachments/assets/c375c7ec-5079-48a6-9ee9-2f8812d6b6eb" />
<img width="829" height="604" alt="image" src="https://github.com/user-attachments/assets/3633e42f-9486-4c96-8547-97633640e4d0" />

---

### ⚙️ **Step 3: Run Synthesis Targeting `vsdbabysoc`**

```bash
synth -top vsdbabysoc
```

### 📸 Synthesis output
<img width="821" height="370" alt="image" src="https://github.com/user-attachments/assets/adaf91a1-e134-4011-9f3e-6e87fd4d38cf" />
<img width="842" height="607" alt="image" src="https://github.com/user-attachments/assets/e389d954-5956-4305-893c-7fbb874bdbe8" />
<img width="842" height="607" alt="image" src="https://github.com/user-attachments/assets/1a6808d1-ca38-4e52-a87c-dee04c412d10" />
<img width="587" height="352" alt="image" src="https://github.com/user-attachments/assets/bc6bc41e-9bf0-45dc-8e64-e919dd99377f" />
<img width="692" height="832" alt="image" src="https://github.com/user-attachments/assets/fc881ba4-5c5b-406a-a7d6-985a151dcd50" />
<img width="826" height="402" alt="image" src="https://github.com/user-attachments/assets/631b66c6-e9cb-4fca-994a-78d1b023cf37" />

---

### 🔁 **Step 4: Map D Flip-Flops to Standard Cells**

```bash
dfflibmap -liberty /home/vinay/vin/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```

### 📸 DFF MAPPING OUTPUT
<img width="1097" height="896" alt="image" src="https://github.com/user-attachments/assets/9ef23fc3-bbb9-4aac-b529-358265e830a2" />

---

### ⚡ **Step 5: Optimization and Technology Mapping**

```bash
opt
abc -liberty /home/vinay/vin/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib -script +strash;scorr;ifraig;retime;{D};strash;dch,-f;map,-M,1,{D}
```

### 📸 Technology Mapping Logs
<img width="713" height="863" alt="image" src="https://github.com/user-attachments/assets/6b7abb4d-99f9-49c7-a9dc-8334632662a8" />
<img width="713" height="308" alt="image" src="https://github.com/user-attachments/assets/f1a7e017-6b9f-4282-8bf9-8f8ca1b36aea" />
<img width="905" height="999" alt="image" src="https://github.com/user-attachments/assets/397a64cc-4dd7-483b-932b-1eb7bcf50b61" />

---

### 🧹 **Step 6: Clean-Up and Renaming**

```bash
flatten
setundef -zero
clean -purge
rename -enumerate
```

### 📸 Cleanup Process
<img width="915" height="321" alt="image" src="https://github.com/user-attachments/assets/5307213a-901a-4640-9731-284a683ddbd4" />

---

### 📊 **Step 7: Check Statistics**

```bash
stat
```

### 📸 Yosys Statistics Output
<img width="632" height="887" alt="image" src="https://github.com/user-attachments/assets/b6e3d3e1-7ca4-453b-ac5a-b2a161bdf869" />
<img width="627" height="651" alt="image" src="https://github.com/user-attachments/assets/f450ee74-97de-427f-ac56-19a0454d086e" />

---

### 📝 **Step 8: Write the Synthesized Netlist**

```bash
write_verilog -noattr /home/vinay/vin/VSDBabySoC/output/post_synth_sim/vsdbabysoc.synth.v
```

### 📸 Netlist Generation Completed
<img width="1025" height="221" alt="image" src="https://github.com/user-attachments/assets/a13ec53f-a58a-4b7e-b5d5-25bef7944943" />

---

## 🎬 **Post-Synthesis Simulation and Waveform Analysis**

---

### 🧩 **Step 1: Compile the Testbench**

Run the following command to compile the **post-synthesis simulation** with GLS models:

```bash
iverilog -o /home/vinay/vin/VSDBabySoC/output/post_synth_sim/post_synth_sim.out \
-DPOST_SYNTH_SIM -DFUNCTIONAL -DUNIT_DELAY=#1 \
-I/home/vinay/vin/VSDBabySoC/src/gls_model \
-I/home/vinay/vin/VSDBabySoC/src/include \
-I/home/vinay/vin/VSDBabySoC/src/module \
/home/vinay/vin/VSDBabySoC/src/gls_model/primitives.v \
/home/vinay/vin/VSDBabySoC/src/gls_model/sky130_fd_sc_hd.v \
/home/vinay/vin/VSDBabySoC/src/module/testbench.v
```
### 📂 **Step 2: Navigate to the Output Directory**

```bash
cd output/post_synth_sim/
```

---

### ▶️ **Step 3: Run the Simulation**

```bash
./post_synth_sim.out
```
### 🌈 **Step 4: View the Waveforms in GTKWave**

```bash
gtkwave post_synth_sim.vcd
```

### 📸 Compiling the testbench,Navigate to output directory,GTKwave Results 

<img width="1600" height="900" alt="image" src="https://github.com/user-attachments/assets/55961c01-5a98-41b0-bc64-19545a60db79" />


---

## ✅ **Outcome**

* Successfully performed **Gate-Level Simulation** for BabySoC.
* Verified **functional correctness** and **timing integrity** post-synthesis.
* Generated and analyzed waveforms in **GTKWave** to validate real hardware-like behavior.

---

## 🏁 **Summary**

| Stage              | Description             | Tool Used      |
| :----------------- | :---------------------- | :------------- |
| RTL to Netlist     | Synthesis of design     | Yosys          |
| Netlist Simulation | Functional + Timing GLS | Icarus Verilog |
| Waveform Analysis  | Output visualization    | GTKWave        |

---

Would you like me to now add the 📂 **Directory Structure** and ⚠️ **Common Errors & Fixes** section next — similar to your earlier Week 2 and Week 3 reports — so it looks complete for submission?
