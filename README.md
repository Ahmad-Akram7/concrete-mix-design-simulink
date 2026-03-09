<div align="center">

<img src="https://img.shields.io/badge/MATLAB-Simulink-0076A8?style=for-the-badge&logo=mathworks&logoColor=white"/>
<img src="https://img.shields.io/badge/Standard-ACI%20211.1-FF6B35?style=for-the-badge"/>
<img src="https://img.shields.io/badge/Domain-Civil%20Engineering-2E8B57?style=for-the-badge"/>
<img src="https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge"/>

<br><br>

# 🏗️ Concrete Mix Design — Simulink Model
### *ACI 211.1 | Automated, Visual, and Blazing Fast*

**Stop doing mix design by hand. Let Simulink do the math.**

[📖 Read the Docs](#-methodology) · [🚀 Get Started](#-getting-started) · [🤝 Contribute](#-contributing) · [⭐ Star this repo](#)

<br>

---

</div>

## 🔥 Why This Project?

If you've ever sat down with ACI 211.1 and a calculator, you know the pain — cross-referencing tables, computing volumes, recalculating everything when one input changes. This model eliminates all of that.

Built in **MATLAB Simulink**, this tool automates the full ACI 211.1 concrete mix design workflow in a clean, block-based visual environment. Change a single input — slump, target strength, aggregate size — and every downstream value updates *instantly*.

```
💡 Designed for civil engineering students, researchers, and practicing engineers
   who want fast, reliable, and reproducible concrete mix designs.
```

---

## ✨ Key Features

- ⚡ **Instant recalculation** — Tweak any input and all outputs update in real time
- 📐 **Full ACI 211.1 compliance** — Water content, w/c ratio, and aggregate volumes sourced directly from ACI tables
- 🧱 **3 validated concrete grades** — M25, M35, and M45 scenarios included out of the box
- 🔬 **Absolute Volume Method** — Fine aggregate calculation encapsulated in a dedicated subsystem
- 🧩 **Modular architecture** — Clean, readable block layout organized left-to-right
- 📊 **2-D Lookup Tables** — ACI table data baked directly into the model, no external files needed
- 🎓 **Perfect for learning** — Ideal for coursework, labs, and understanding how mix design actually works

---

## 📸 Model Architecture

> *The model is organized left-to-right: Inputs → ACI Logic (Lookup Tables + Subsystems) → Outputs*

***
<img width="916" height="493" alt="image" src="https://github.com/user-attachments/assets/e6281e29-0630-4295-98f7-e7adf1398e6d" />

***

---

## 🚀 Getting Started

### Prerequisites

- MATLAB R2020b or later
- Simulink (base package)

### Installation

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/concrete-mix-design-simulink.git

# Open MATLAB and navigate to the project folder
cd concrete-mix-design-simulink
```

### Running the Model

```matlab
% Open the model
open('ConcreteMixDesign.slx')

% Set your inputs in the Constant blocks:
%   - Target_Strength_MPa  (e.g., 25, 35, 45)
%   - Slump_mm             (e.g., 50 or 100)
%   - Max_Agg_Size_mm      (10, 20, or 40)
%   - Fineness_Modulus     (2.40, 2.60, or 2.80)

% Hit Run (Ctrl+T) — results appear in the Display blocks instantly
```

---

## 📐 Methodology

The model implements the full **ACI 211.1** procedure as a sequential calculation chain:

```
Target Strength → w/c Ratio → Cement Content
Slump + Agg. Size → Water Content ↗
Agg. Size + FM → Coarse Agg. Volume → Coarse Agg. Mass
Absolute Volume Method → Fine Aggregate Mass
```

### Governing ACI Tables

**Table 1 — Estimated Water Content (kg/m³)**
| Slump (mm) | 10 mm Aggregate | 20 mm Aggregate | 40 mm Aggregate |
|:----------:|:---------------:|:---------------:|:---------------:|
| 25 – 50    | 215             | 190             | 175             |
| 75 – 100   | 225             | 205             | 185             |

**Table 2 — Water-Cement Ratio vs. Compressive Strength**
| f'c (MPa) | w/c Ratio |
|:---------:|:---------:|
| 45        | 0.42      |
| 35        | 0.52      |
| 25        | 0.65      |

**Table 3 — Volume of Coarse Aggregate per m³ of Concrete**
| Max. Agg. Size | FM 2.40 | FM 2.60 | FM 2.80 |
|:--------------:|:-------:|:-------:|:-------:|
| 10 mm          | 0.50    | 0.48    | 0.46    |
| 20 mm          | 0.66    | 0.64    | 0.62    |
| 40 mm          | 0.75    | 0.73    | 0.71    |

**Cement content** is derived as:

$$C = \frac{W}{(w/c)}$$

**Fine aggregate** fills the remaining volume after subtracting water, cement, coarse aggregate, and 2% entrapped air from 1 m³.

---

## 📊 Results & Verification

All three scenarios share these common inputs:

| Parameter | Value |
|-----------|-------|
| Max. Aggregate Size | 20 mm |
| Fineness Modulus | 2.60 |
| SG — Cement | 3.15 |
| SG — Fine Aggregate | 2.65 |
| SG — Coarse Aggregate | 2.70 |
| Unit Weight (CA) | 1600 kg/m³ |
| Entrapped Air | 2% |

---

### 🟢 Scenario 1 — M25 Grade Concrete
**Inputs:** Target Strength = 25 MPa · Slump = 100 mm

| Component | Result |
|-----------|--------|
| 💧 Water | **205 kg/m³** |
| 🏭 Cement | **315.4 kg/m³** |
| 🪨 Coarse Aggregate | **1024 kg/m³** |
| 🏖️ Fine Aggregate | **778.1 kg/m³** |

***
<img width="1000" height="666" alt="image" src="https://github.com/user-attachments/assets/97276999-6485-434c-910f-ebf324e17f58" />
***
---

### 🟡 Scenario 2 — M35 Grade Concrete
**Inputs:** Target Strength = 35 MPa · Slump = 100 mm

| Component | Result |
|-----------|--------|
| 💧 Water | **205 kg/m³** |
| 🏭 Cement | **394.2 kg/m³** |
| 🪨 Coarse Aggregate | **1024 kg/m³** |
| 🏖️ Fine Aggregate | **690.6 kg/m³** |

***
<img width="975" height="453" alt="image" src="https://github.com/user-attachments/assets/c6598107-9d36-463c-9083-88cfaf0b3c31" />
***

---

### 🔴 Scenario 3 — M45 High-Strength Concrete
**Inputs:** Target Strength = 45 MPa · Slump = 50 mm

| Component | Result |
|-----------|--------|
| 💧 Water | **190 kg/m³** |
| 🏭 Cement | **452.4 kg/m³** |
| 🪨 Coarse Aggregate | **1024 kg/m³** |
| 🏖️ Fine Aggregate | **658.5 kg/m³** |

***
<img width="975" height="431" alt="image" src="https://github.com/user-attachments/assets/c04e1620-a441-40d1-8d7b-c8f96bb7df59" />
***

> **Validation note:** As target strength increases, cement content rises and fine aggregate decreases — exactly as ACI 211.1 predicts. ✅

---

## 🏛️ Simulink Block Architecture

| Block Type | Library | Purpose |
|-----------|---------|---------|
| `Constant` | Sources | All design input parameters |
| `2-D Lookup Table` | Lookup Tables | ACI Tables 1 & 3 |
| `1-D Lookup Table` | Lookup Tables | ACI Table 2 (w/c ratio) |
| `Divide` / `Product` | Math Operations | Cement & mass calculations |
| `Sum` | Math Operations | Absolute volume summation |
| `Subsystem` | Ports & Subsystems | Encapsulates fine aggregate logic |
| `Display` | Sinks | Output: Water, Cement, CA, FA |

---

## 🤝 Contributing

Contributions are what make open source great. Here are some ideas to get you started:

- 🔧 **Extend aggregate sizes** — Add support for 12.5 mm or 63 mm aggregates
- 💨 **Add air-entrained concrete** — Implement the ACI 211.1 air-entrained water tables
- 📈 **Add a dashboard scope** — Real-time plotting of proportions as inputs change
- 🌍 **Metric/Imperial toggle** — Auto-convert between SI and US customary units
- 🧪 **Additional standards** — IS 10262, BS 8500, or EN 206 mix design logic
- 📄 **Report export** — Generate a PDF mix design summary from the Simulink outputs

### How to Contribute

```bash
# 1. Fork the repo
# 2. Create your feature branch
git checkout -b feature/air-entrained-concrete

# 3. Commit your changes
git commit -m "Add air-entrained water content tables"

# 4. Push and open a Pull Request
git push origin feature/air-entrained-concrete
```

Please open an **Issue** first for major changes so we can discuss the approach.

---

## 📚 References

- **ACI 211.1-91** — *Standard Practice for Selecting Proportions for Normal, Heavyweight, and Mass Concrete*. American Concrete Institute.
- MathWorks Simulink Documentation — [mathworks.com/products/simulink](https://www.mathworks.com/products/simulink.html)

---

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.

---

<div align="center">

**If this project saved you time, please consider giving it a ⭐**

*Built with ❤️ for the civil engineering community*

</div>
