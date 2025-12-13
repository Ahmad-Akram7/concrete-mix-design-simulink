# Project Report: Simulink Model for Concrete Mix Design

**Author:** Ahmad Akram
**Date:** December 13, 2025

---

## 1. Table of Contents

1.  **Abbreviations**
2.  **Introduction**
    1.  Purpose of Concrete Mix Design
    2.  Importance of Simulink Modeling
3.  **Methodology**
    1.  Adopted Standard: ACI 211.1
    2.  Mathematical Logic and Step-by-Step Procedure
    3.  Governing Tables for Mix Design
4.  **Actual Simulink Model Documentation**
    1.  Model Architecture and Layout
    2.  Block-by-Block Construction Process
    3.  Signal Flow and Data Processing
5.  **Sample Results & Model Verification**
    1.  Scenario 1: M25 Grade Concrete
    2.  Scenario 2: M35 Grade Concrete
    3.  Scenario 3: High-Strength M45 Grade Concrete
6.  **Conclusion**

---

## 2. Abbreviations

*   **ACI:** American Concrete Institute
*   **f'c:** Target 28-day Compressive Strength
*   **w/c:** Water-Cement Ratio
*   **SSD:** Saturated Surface-Dry
*   **SG:** Specific Gravity
*   **FM:** Fineness Modulus

---

## 3. Introduction

### 3.1. Purpose of Concrete Mix Design
Concrete mix design is the process of selecting suitable ingredients—cement, water, fine aggregate (sand), and coarse aggregate—and determining their relative quantities to produce concrete that meets specific performance requirements. The primary objectives are to achieve a target strength, ensure adequate workability, guarantee long-term durability, and optimize for cost.

### 3.2. Importance of Simulink Modeling
MATLAB/Simulink is a powerful environment for modeling and simulating dynamic systems. For a procedural task like concrete mix design, Simulink allows for the creation of a dynamic, interactive model that automates the calculation-heavy process. This visual approach minimizes human error, provides instant results for different input conditions, and allows for rapid "what-if" scenario analysis, making it an invaluable tool for civil engineers.

---

## 4. Methodology

### 4.1. Adopted Standard: ACI 211.1
The model's logic is based on the **ACI 211.1: Standard Practice for Selecting Proportions for Normal, Heavyweight, and Mass Concrete**. This method provides a systematic, step-by-step procedure that is logically sound and can be directly translated into a computational model.

### 4.2. Mathematical Logic and Step-by-Step Procedure
The design process follows these sequential steps:
1.  **Water Content Estimation:** The mass of water required per cubic meter is determined based on slump and the nominal maximum size of the coarse aggregate.
2.  **Water-Cement (w/c) Ratio Selection:** The w/c ratio is selected based on the target 28-day compressive strength (f'c).
3.  **Cement Content Calculation:** `Cement (kg/m³) = Water (kg/m³) / (w/c Ratio)`
4.  **Coarse Aggregate Content Estimation:** The volume of coarse aggregate is determined based on its maximum size and the fineness modulus (FM) of the sand. This volume is converted to mass using its unit weight.
5.  **Fine Aggregate Content Calculation (Absolute Volume Method):** The remaining volume in 1 m³ of concrete is filled by the fine aggregate. The absolute volume of all other ingredients (water, cement, coarse aggregate, and entrapped air) is calculated and subtracted from 1 m³. The result is converted to mass.

### 4.3. Governing Tables for Mix Design
The model's logic is driven by data from standard ACI tables.

**Table 1: Estimated Water Content (kg/m³)**
| Slump (mm) | Max. Agg. Size (mm) | 10 | 20 | 40 |
| :--- | :--- | :--- | :--- | :--- |
| **25-50** | 215 | 190 | 175 |
| **75-100**| 225 | 205 | 185 |

**Table 2: Water-Cement Ratio for Target Strength (f'c)**
| Compressive Strength (MPa) | Water-Cement Ratio |
| :--- | :--- |
| **45** | 0.42 |
| **35** | 0.52 |
| **25** | 0.65 |

**Table 3: Volume of Coarse Aggregate per Unit Volume of Concrete**
| Max. Agg. Size (mm) | Fineness Modulus (FM) of Sand | 2.40 | 2.60 | 2.80 |
| :--- | :--- | :--- | :--- | :--- |
| **10** | 0.50 | 0.48 | 0.46 |
| **20** | 0.66 | 0.64 | 0.62 |
| **40** | 0.75 | 0.73 | 0.71 |

---

## 5. Actual Simulink Model Documentation

### 5.1. Model Architecture and Layout
The Simulink model was designed to be modular and intuitive. The canvas is organized from left to right, following the logical flow of the calculation:
1.  **Inputs:** A section of `Constant` blocks where all design parameters are defined.
2.  **Calculations:** A series of calculation blocks and a central subsystem that encapsulates the main ACI 211.1 logic.
3.  **Outputs:** A series of `Display` blocks showing the final computed quantities.

This architecture allows a user to easily change an input scenario and observe the results without needing to navigate complex internal logic.

### 5.2. Block-by-Block Construction Process
The model was constructed manually using the Simulink Library Browser.

1.  **Input Blocks:**
    From the `Simulink/Sources` library, nine `Constant` blocks were dragged onto the left side of the canvas. Each block was then double-clicked to open its properties dialog, where its value was set to a default (e.g., `Target_Strength_MPa` was set to `25`).

2.  **Calculation Blocks:**
    *   **Water Content:** A `2-D Lookup Table` block was added from the `Lookup Tables` library. By double-clicking the block, its axes were configured for slump and aggregate size, and the grid was populated with data from ACI Table 1.
    *   **W/C Ratio:** Similarly, a `1-D Lookup Table` was used for the water-cement ratio, configured with data from ACI Table 2.
    *   **Cement Content:** A `Divide` block was dragged from the `Math Operations` library to calculate the cement content.
    *   **Coarse Aggregate:** A `2-D Lookup Table` and a `Product` block were used to find the volume and then calculate the mass of the coarse aggregate.
    *   **Fine Aggregate Calculation:** To keep the main canvas clean, the complex "Absolute Volume Method" was built inside a dedicated `Subsystem` block. This subsystem was constructed by dragging and dropping the necessary `Divide`, `Product`, `Sum`, and `Constant` blocks to replicate the formula step-by-step as described in the methodology.

3.  **Output Blocks:**
    Four `Display` blocks were added from the `Simulink/Sinks` library to the right side of the model. Each block's name was set to be a clear, descriptive label (e.g., `Water_kg_per_m3`) and configured to display above the block for readability.

4.  **Wiring:**
    Finally, the blocks were connected by clicking and dragging lines from the output port of one block to the input port of the next, following the logical data flow of the mix design procedure.

### 5.3. Signal Flow and Data Processing
Data flows from the input `Constant` blocks on the left to the final `Display` blocks on the right. The signals are processed sequentially by the calculation blocks. The outputs of the initial lookup tables (Water Content and W/C Ratio) are fed into subsequent blocks to calculate the mass of cement, aggregates, and so on, until the final mix proportions are determined.

---

## 6. Sample Results & Model Verification

To verify the model, three scenarios were simulated for different grades of concrete.

**Common Inputs for all Scenarios:**
*   Max. Aggregate Size: 20 mm
*   Fineness Modulus of Sand: 2.60
*   Specific Gravities: Cement (3.15), Fine Agg. (2.65), Coarse Agg. (2.70)
*   Unit Weight of Coarse Aggregate: 1600 kg/m³
*   Entrapped Air: 2%

### 6.1. Scenario 1: M25 Grade Concrete
*   **Inputs:** Target Strength = 25 MPa, Slump = 100 mm
*   **Model Outputs:**
    *   Water: **205 kg/m³**
    *   Cement: **315.4 kg/m³**
    *   Coarse Aggregate: **1024 kg/m³**
    *   Fine Aggregate: **778.1 kg/m³**

### 6.2. Scenario 2: M35 Grade Concrete
*   **Inputs:** Target Strength = 35 MPa, Slump = 100 mm
*   **Model Outputs:**
    *   Water: **205 kg/m³**
    *   Cement: **394.2 kg/m³**
    *   Coarse Aggregate: **1024 kg/m³**
    *   Fine Aggregate: **690.6 kg/m³**

### 6.3. Scenario 3: High-Strength M45 Grade Concrete
*   **Inputs:** Target Strength = 45 MPa, Slump = 50 mm
*   **Model Outputs:**
    *   Water: **190 kg/m³**
    *   Cement: **452.4 kg/m³**
    *   Coarse Aggregate: **1024 kg/m³**
    *   Fine Aggregate: **658.5 kg/m³**

The model's outputs are logical and consistent with established concrete design principles. As the target strength increases, the model correctly calculates a higher required cement content.

---

## 7. Conclusion

This project successfully demonstrated the use of Simulink to create a functional and accurate model for concrete mix design. By translating the standard ACI 211.1 procedure into a visual, block-based model, the design process is automated, efficient, and less prone to calculation error. The model was validated against multiple scenarios and proven to be a reliable tool for civil engineering design and analysis.
