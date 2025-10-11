# 🕒 Week 3 – Post-Synthesis GLS & STA Fundamentals

## 1. Purpose of STA 🔍
- **Static Timing Analysis (STA)**: Verify **timing correctness** without running full simulations.  
- Ensures **data reaches flip-flops/latches on time** ⏱️.  
- Detects **setup ⏱️ and hold ⏳ violations** that may break functionality.

---

## 2. Key Concepts ⚡

### Clock ⏰
- Acts as the **timing reference** for sequential circuits  
- **Primary clocks:** External inputs  
- **Derived clocks:** Generated internally (dividers/multipliers)  
- Parameters: period, duty cycle, skew, jitter

### Data Path ➡️
- Path connecting sequential elements (FFs/latches)  
- **Critical path:** Longest delay → determines max operating frequency  
- **Short path:** Shortest delay → may cause hold violations  

---

## 3. Timing Checks ✅❌

### Setup Time ⏱️
- Data must arrive **before clock edge**  
- **Violation:** Data arrives late  
- **Slack:** `Slack = Tclk – (Tdata + Tsetup)`  
- Positive slack ✅ → timing met  
- Negative slack ❌ → violation  

### Hold Time ⏳
- Data must remain **stable after clock edge**  
- **Violation:** Data changes too early  
- **Slack:** `Slack = Tdata – Thold`  
- Positive slack ✅ → timing met  
- Negative slack ❌ → violation  

---

## 4. Slack 💡
- **Definition:** Margin by which timing requirements are met  
- Positive slack ✅ → OK, Negative slack ❌ → Violation  
- Helps **prioritize critical paths for optimization**

---

## 5. Path-Based Analysis 🛣️
- Evaluates **all timing paths** between sequential elements  
- **Longest path:** Setup check  
- **Shortest path:** Hold check  
- Essential for **timing optimization**

---

## 6. Practical Steps in OpenSTA 🖥️
1. Load **post-synthesis netlist & SDC constraints**  
2. Define **clock(s)**  
3. Run **`report_timing`**  
4. Analyze **slack & violations**  
5. Optimize **logic or constraints** if needed
