# Metabolic Kinetics & Steady-State Validator 

![PyScript](https://img.shields.io/badge/PyScript-black?style=flat-square&logo=python)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)
![Data Analysis](https://img.shields.io/badge/Data_Analysis-Pandas_|_SciPy-blue?style=flat-square)

An advanced browser-based analytical tool for processing Cardiopulmonary Exercise Testing (CPET) data. Designed for researchers, sports scientists, and exercise physiologists, this application automatically calculates Maximal Fat Oxidation (MFO), FatMax intensity, and models V̇O₂ kinetics during graded exercise testing.

## Key Features

* **100% Client-Side:** Built with [PyScript](https://pyscript.net/), all Python data analysis (Pandas, SciPy, Matplotlib) runs directly in your browser. No software installation, terminal usage, or backend server configuration is required.
* **FatMax & MFO Modeling:** Polynomial curve fitting to pinpoint the exact stage of maximal fat oxidation and the metabolic crossover point.
* **Lean Mass Adjustment:** Automatic calculation of MFO indexed to fat-free mass (MFOadjFFM), expressed in standardized units (`mg·kgFFM⁻¹·min⁻¹`).
* **V̇O₂ Kinetics:** Automatically evaluates and fits the best mathematical model (Linear vs. Mono-exponential) for the oxygen uptake response during each stage.
* **Data Quality Control:** Implements the Hampel filter for robust outlier imputation and calculates the Respiratory Exchange Ratio Coefficient of Variation (RER-CV%) to validate metabolic steady-state.
* **Export Results:** Download high-resolution charts (`.png`), subject-specific tabular data (`.csv`), and a comprehensive global cohort summary (`.csv`).

## Usage Instructions

1. **Access:** Clone this repository or simply download the `index.html` file.
2. **Run:** Open the `index.html` file in any modern web browser (Chrome, Firefox, Safari, Edge).
   > *Note: On the first load, PyScript will download the Python environment and necessary libraries. This may take a few seconds.*
3. **Upload Data:** Click "Select CPET Files" and choose one or multiple raw `.csv` files.
4. **Configuration:** Define the Stage Duration in seconds (Default: `180` seconds).
5. **Analyze:** Click the **"Analyze Cohort"** button.

## Required Data Format

The script processes raw `.csv` files (exported directly from your metabolic cart). The code includes an intelligent column cleaner, but files should ideally contain the following variables (order does not matter):

### Mandatory Columns:
* `TIME` (Time in seconds)
* `VO2` (Oxygen uptake in L/min)
* `VCO2` (Carbon dioxide production in L/min)
* `RER` (Respiratory Exchange Ratio)

### Optional (Highly Recommended) Columns:
* `HR`: Heart Rate in bpm.
* `Speed_mph` or `Speed_kmh`: Treadmill speed.
* `LeanMass` or `LM`: Lean mass in kg (required for MFOadjFFM calculation).

*The script automatically ignores columns containing the word "KG" (e.g., relative V̇O₂/kg) or "VE" to avoid conflicts, as it calculates absolute values internally.*

## Scientific Methodology

* **Substrate Oxidation:** Utilizes the stoichiometric equations by **Jeukendrup and Wallis (2005)** to calculate fat and carbohydrate oxidation rates (g/min).
* **Steady-State Window:** The algorithm extracts the final 60 seconds of each stage to average gas exchange data and calculate the RER-CV%. If the RER consistently exceeds 1.0, the data is truncated to prevent erroneous FatOx modeling.
* **V̇O₂ Kinetics:** Baseline values from the last 30 seconds of the previous stage are subtracted to accurately model the amplitude (A) of the oxygen uptake response to the new energy demand.

## Contributing

Contributions, issues, and pull requests are welcome. Feel free to fork this repository and improve the mathematical models or user interface!

## License

This project is licensed under the MIT License - see the `LICENSE` file for details. This tool is designed for scientific research and educational purposes.