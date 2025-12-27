Here is the completely overhauled, high-end technical documentation for your repository. This is written in a professional "Software Documentation" style to make your GitHub profile stand out to recruiters and engineers.

---

# 🏗️ Concrete Mix Design Automation (ACI 211.1)

## 📌 Project Overview

This repository contains a specialized **Simulink model** designed to automate the procedural calculations of **ACI 211.1: Standard Practice for Selecting Proportions for Normal, Heavyweight, and Mass Concrete**.

By digitizing the traditional table-lookup and interpolation process, this tool provides a dynamic environment for Civil Engineers to perform rapid mix design, sensitivity analysis, and "what-if" scenarios for concrete performance.

---

##  Design Methodology & Logic

The model architecture follows the rigid mathematical sequence mandated by the **American Concrete Institute (ACI)**.

### The ACI 211.1 Workflow

The simulation processes data through a multi-stage logic gate:

1. **Water Demand Analysis:** Determines required  of water based on desired slump and nominal maximum aggregate size.
2. ** Efficiency Mapping:** Selects the optimal Water-Cement ratio based on the target 28-day compressive strength ().
3. **Volumetric Calculations:** Uses the **Absolute Volume Method** to calculate the displacement of each ingredient (Cement, Water, Coarse/Fine Aggregates, and Entrapped Air) to ensure exactly  of yield.

---

##  Simulink Model Architecture

The system is engineered for modularity and clarity, organized into three distinct functional zones:

### 1. Input Interface (Control Panel)

Nine `Constant` blocks allow for the real-time adjustment of:

* Target Strength () & Slump ()
* Aggregate Characteristics (Size, Fineness Modulus, Unit Weight)
* Specific Gravities (Cement, Water, Aggregates)

### 2. Computational Core (Logic Engine)

* **2-D Lookup Tables:** Digitized versions of ACI Tables 1, 2, and 3 for automated data retrieval.
* **Absolute Volume Subsystem:** A nested hierarchy of math blocks that calculate the residual volume available for fine aggregates, minimizing visual clutter on the main canvas.

### 3. Output Telemetry

Instantaneous feedback via `Display` blocks providing:

* **Water Content** ()
* **Cement Content** ()
* **Coarse Aggregate Mass** ()
* **Fine Aggregate Mass** ()

---

## 🧪 Model Verification (Sample Scenarios)

To ensure accuracy, the model was tested across three performance tiers using standard industry constants (SG: 3.15/2.65/2.70).

| Parameter | Scenario 1 (M25) | Scenario 2 (M35) | Scenario 3 (M45) |
| --- | --- | --- | --- |
| **Target Strength** | 25 MPa | 35 MPa | 45 MPa |
| **Slump** | 100 mm | 100 mm | 50 mm |
| **Water Content** | 205 kg/m³ | 205 kg/m³ | 190 kg/m³ |
| **Cement Content** | 315.4 kg/m³ | 394.2 kg/m³ | 452.4 kg/m³ |
| **Coarse Agg.** | 1024 kg/m³ | 1024 kg/m³ | 1024 kg/m³ |
| **Fine Agg.** | **778.1 kg/m³** | **690.6 kg/m³** | **658.5 kg/m³** |

### Execution Proof

<img width="1827" height="912" alt="Execution Screenshot" src="[https://github.com/user-attachments/assets/5c228b42-5e5e-4666-9a87-ea5e52b304e5](https://github.com/user-attachments/assets/5c228b42-5e5e-4666-9a87-ea5e52b304e5)" />

---

## 🚀 Getting Started

### Prerequisites

* **MATLAB R2023b** or newer
* **Simulink** Toolbox

### Installation

```bash
git clone https://github.com/Ahmad-Akram7/concrete-mix-design-simulink.git

```

### Usage

1. Open `Concrete_Mix_Design_Simulink_v9.slx`.
2. Input your laboratory parameters into the blue `Constant` blocks.
3. Click **Run (▶)**.
4. View your optimized mix proportions in the green `Display` blocks.

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](https://www.google.com/search?q=LICENSE) file for details.

---
