
# Elliptic Curve Cryptography (ECC) on FPGA

> A hardware implementation of secure and efficient public-key cryptography using Elliptic Curve ElGamal on a Spartan-7 FPGA.

---

## 📘 Abstract

This project presents the design and implementation of **Elliptic Curve Cryptography (ECC)** using **Field-Programmable Gate Arrays (FPGA)** to accelerate cryptographic operations. Traditional ECC software implementations are computationally intensive, especially for embedded and IoT devices. By leveraging the **parallelism and customizability of FPGA hardware**, we optimize ECC components such as modular arithmetic and scalar multiplication.

---

## 📌 Key Features

- 🔐 Implementation of ECC primitives in Verilog
- 💡 Two modular addition approaches:
  - **Repeated Subtraction**
  - **Shift-and-Subtract (Long Division-style)**
- 🔧 Deployed on **Spartan-7 FPGA (XC7S50CSGA324-1)** using the Boolean Board
- 🧠 Focused on ElGamal encryption using ECC
- ✅ Verified using ModelSim simulation and Vivado synthesis

---

## 🧠 Concepts Covered

### 🔸 What is ECC?

ECC is a form of **asymmetric cryptography** based on the algebraic structure of elliptic curves over finite fields. It offers:

- Strong security with shorter key lengths
- Reduced computational load
- Efficient memory and energy usage

ECC security relies on the **Elliptic Curve Discrete Logarithm Problem (ECDLP)**, which is computationally infeasible to reverse.

### 🔸 ElGamal Encryption using ECC

ECC is combined with the **ElGamal public-key scheme**:

- **Public Parameters**: `(E, p, G, n)`
- **Private Key**: `d ∈ [1, n-1]`
- **Public Key**: `Q = dG`

**Encryption:**
```
C1 = kG
C2 = Pm + kQ
```

**Decryption:**
```
Pm = C2 - dC1
```

Where `Pm` is the encoded message point on the curve.

---

## ⚙️ Hardware Implementation

### 🧱 FPGA Board: Boolean Board

- **Family**: Spartan-7
- **Part**: XC7S50CSGA324-1
- **Resources**:
  - 52,160 logic cells
  - 32,600 LUTs
  - 120 DSP slices
  - 2.7 Mb block RAM

### 🔧 Modular Addition - Two Methods

#### 1. Repeated Subtraction (Simple but Inefficient)
```verilog
while (sum >= m)
    sum = sum - m;
```

- Easy to implement but slow when `m` is small compared to `a + b`

#### 2. Shift-and-Subtract (Efficient Division-like)
```verilog
temp = (out << 1) | next_bit;
if (temp >= m) temp = temp - m;
```
![Adder Diagram](images/Long_division_1.png)
![Adder Diagram](images/Long_division_2.png)

- Performs in **constant number of steps** based on bit width, not input size
- Better suited for **real-time cryptographic operations**

📎 **I/O Constraint Files** are available at:  
👉 [github.com/Sunny1619/ECC_on_FPGA](https://github.com/Sunny1619/ECC_on_FPGA)

---

## 🔭 Future Work

- 🧩 Implement complete ECC-ElGamal system in hardware:
  - Scalar multiplication
  - Modular multiplication/inversion
  - Point addition/doubling (affine/projective)
- 🧪 Performance evaluation (latency, area, power)
- 🔐 Mitigation of side-channel attacks
- ⚙️ Integration into real-time cryptographic pipelines

---

## 👨‍🎓 Authors

- Sunny Kumar Pandit (CSE/22105/959)   
👨‍🏫 Supervised by: **Dr. Soumen Pandit**, IIIT Kalyani

---

## 🎓 Institution

**Indian Institute of Information Technology Kalyani**  
West Bengal – 741235, India

---

## 📄 License

This work is part of an academic research project and is intended for educational and research purposes. Contributions are welcome!

---

## 🔗 References

- [Wikipedia: Elliptic Curve Cryptography](https://en.wikipedia.org/wiki/Elliptic-curve_cryptography)
- [RareSkills: ECC Point Addition Explained](https://www.rareskills.io/post/elliptic-curve-addition)
- [YouTube: ECC Explained](https://www.youtube.com/watch?v=XmygBPb7DPM)
