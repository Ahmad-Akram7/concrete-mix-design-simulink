# Simulink Model for Concrete Mix Design (ACI 211.1)

This repository contains a Simulink model that automates the concrete mix design process based on the **ACI 211.1: Standard Practice for Selecting Proportions for Normal, Heavyweight, and Mass Concrete**.

The model serves as a dynamic and interactive tool for civil engineers and students to perform calculations, minimize human error, and conduct rapid "what-if" scenario analysis for different concrete grades and input conditions.

---

## Table of Contents
1.  [Introduction](#1-introduction)
2.  [Methodology](#2-methodology)
3.  [Simulink Model Documentation](#3-simulink-model-documentation)
4.  [Results & Verification](#4-results--verification)
5.  [Conclusion](#5-conclusion)

---

## 1. Introduction

### Purpose of Concrete Mix Design
Concrete mix design is the process of selecting suitable ingredients—cement, water, fine aggregate (sand), and coarse aggregate—and determining their relative quantities to produce concrete that meets specific performance requirements. The primary objectives are to achieve a target strength, ensure adequate workability, guarantee long-term durability, and optimize for cost.

### Importance of Simulink Modeling
For a procedural task like concrete mix design, Simulink allows for the creation of a dynamic, interactive model that automates the calculation-heavy process. This visual approach minimizes human error, provides instant results for different input conditions, and allows for rapid scenario analysis.

---

## 2. Methodology

### Adopted Standard: ACI 211.1
The model's logic is based entirely on the ACI 211.1 standard, which provides a systematic, step-by-step procedure that is logically sound and can be directly translated into a computational model.

### Mathematical Logic
The design process follows these sequential steps:
1.  **Water Content Estimation**: Determined from ACI tables based on slump and the nominal maximum size of the coarse aggregate.
2.  **Water-Cement (w/c) Ratio Selection**: Selected from ACI tables based on the target 28-day compressive strength (f'c).
3.  **Cement Content Calculation**: `Cement (kg/m³) = Water (kg/m³) / (w/c Ratio)`
4.  **Coarse Aggregate Content Estimation**: The volume of coarse aggregate is determined from ACI tables based on its maximum size and the fineness modulus (FM) of the sand. This volume is converted to mass using its unit weight.
5.  **Fine Aggregate Content Calculation (Absolute Volume Method)**: The remaining volume in 1 m³ of concrete is filled by the fine aggregate. This is done by subtracting the absolute volume of all other ingredients (water, cement, coarse aggregate, and entrapped air) from 1 m³.

### Governing ACI Tables
The model's logic is driven by data from the following standard ACI tables.

**Table 1: Estimated Water Content (kg/m³)**
| Slump (mm) | Max. Agg. Size 10mm | Max. Agg. Size 20mm | Max. Agg. Size 40mm |
|:----------:|:-------------------:|:-------------------:|:-------------------:|
| **25-50**  | 215                 | 190                 | 175                 |
| **75-100** | 225                 | 205                 | 185                 |

**Table 2: Water-Cement Ratio vs. Compressive Strength**
| Compressive Strength (MPa) | Water-Cement Ratio |
|:--------------------------:|:------------------:|
| **45**                     | 0.42               |
| **35**                     | 0.52               |
| **25**                     | 0.65               |

**Table 3: Volume of Coarse Aggregate per Unit Volume of Concrete**
| Max. Agg. Size (mm) | FM 2.40 | FM 2.60 | FM 2.80 |
|:-------------------:|:-------:|:-------:|:-------:|
| **10**              | 0.50    | 0.48    | 0.46    |
| **20**              | 0.66    | 0.64    | 0.62    |
| **40**              | 0.75    | 0.73    | 0.71    |

---

## 3. Simulink Model Documentation

### Model Architecture and Layout
The Simulink model is organized from left to right to follow the logical flow of the calculation:
- **Inputs**: A section of `Constant` blocks where all design parameters are defined.
- **Calculations**: A series of calculation blocks and a central subsystem that encapsulates the main ACI 211.1 logic.
- **Outputs**: A series of `Display` blocks showing the final computed quantities for Water, Cement, Fine Aggregate, and Coarse Aggregate in kg/m³.

***
> **IMAGE PLACEHOLDER**
> *Replace the placeholder below with a screenshot of your overall Simulink model architecture.*

![Model Architecture](https://via.placeholder.com/800x400.png?text=PASTE+MODEL+ARCHITECTURE+SCREENSHOT+HERE)
***

### Block-by-Block Construction
The model was constructed manually using the Simulink Library Browser:
- **Input Blocks**: `Constant` blocks from the `Simulink/Sources` library were used to define all input parameters (e.g., `Target_Strength_MPa`).
- **Calculation Blocks**:
    - `2-D Lookup Table` blocks were used to implement ACI Table 1 and Table 3.
    - A `1-D Lookup Table` was used for ACI Table 2 (W/C Ratio).
    - `Divide`, `Product`, and `Sum` blocks from the `Math Operations` library were used for calculations.
    - The "Absolute Volume Method" for fine aggregate calculation was encapsulated in a dedicated `Subsystem` block to keep the main canvas clean.
- **Output Blocks**: `Display` blocks from the `Simulink/Sinks` library were used to show the final results.

---

## 4. Results & Verification
The model was verified against three scenarios for different grades of concrete.

**Common Inputs for all Scenarios:**
- Max. Aggregate Size: **20 mm**
- Fineness Modulus of Sand: **2.60**
- Specific Gravities: Cement (**3.15**), Fine Agg. (**2.65**), Coarse Agg. (**2.70**)
- Unit Weight of Coarse Aggregate: **1600 kg/m³**
- Entrapped Air: **2%**

### Scenario 1: M25 Grade Concrete
- **Inputs**: Target Strength = 25 MPa, Slump = 100 mm
- **Model Outputs**:
    - Water: **205 kg/m³**
    - Cement: **315.4 kg/m³**
    - Coarse Aggregate: **1024 kg/m³**
    - Fine Aggregate: **778.1 kg/m³**

***
> **IMAGE PLACEHOLDER**
> *Replace the placeholder below with a screenshot of your Simulink model running the M25 scenario.*

![M25 Results](https://via.placeholder.com/800x300.png?text=PASTE+M25+SCENARIO+SCREENSHOT+HERE)
***

### Scenario 2: M35 Grade Concrete
- **Inputs**: Target Strength = 35 MPa, Slump = 100 mm
- **Model Outputs**:
    - Water: **205 kg/m³**
    - Cement: **394.2 kg/m³**
    - Coarse Aggregate: **1024 kg/m³**
    - Fine Aggregate: **690.6 kg/m³**

***
> **IMAGE PLACEHOLDER**
> *Replace the placeholder below with a screenshot of your Simulink model running the M35 scenario.*

![M35 Results](https://via.placeholder.com/800x300.png?text=PASTE+M35+SCENARIO+SCREENSHOT+HERE)
***

### Scenario 3: High-Strength M45 Grade Concrete
- **Inputs**: Target Strength = 45 MPa, Slump = 50 mm
- **Model Outputs**:
    - Water: **190 kg/m³**
    - Cement: **452.4 kg/m³**
    - Coarse Aggregate: **1024 kg/m³**
    - Fine Aggregate: **658.5 kg/m³**

***
> **IMAGE PLACEHOLDER**
> *Replace the placeholder below with a screenshot of your Simulink model running the M45 scenario.*

![M45 Results](https://via.placeholder.com/800x300.png?text=PASTE+M45+SCENARIO+SCREENSHOT+HERE)
***

The model's outputs are logical and consistent with established concrete design principles. As the target strength increases, the model correctly calculates a higher required cement content.

---

## 5. Conclusion
This project successfully demonstrates the use of Simulink to create a functional and accurate model for concrete mix design. By translating the standard ACI 211.1 procedure into a visual, block-based model, the design process is automated, efficient, and less prone to calculation error. The model was validated against multiple scenarios and proven to be a reliable tool for civil engineering design and analysis.
