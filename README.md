# Perovskite Automated Synthesis System

This project enables autonomous synthesis of perovskite ink formulations using a Raspberry Pi–based system integrated with:

- 🧪 Pipette and Vial Handling
- 🌡️ Hotplate and Spin Coater
- 📸 Live Spectrometer Readings (via Ossila)
- 🧠 Machine Learning (Random Forest) Bandgap Prediction
- 📊 Efficiency Estimation using Shockley-Queisser Limit
- 💻 Python + CustomTkinter GUI for real-time control and monitoring

It combines robotics, GUI automation, and AI-driven feedback to streamline perovskite material discovery and analysis.

## Core Features
- Automated ink mixing, dispensing, and heating
- Real-time spectral analysis and visualization
- Bandgap and efficiency prediction using ML models
- GUI interface for full lab control and data collection
- Export to CSV, visualization tools, and optimization routines

## Tools & Libraries
- `scikit-learn`, `seaborn`, `matplotlib`, `pandas`, `customtkinter`
- Hardware interfacing via `gpiozero` and serial communication

## Usage
### 1. Starting the Program
Run the `start.sh` script to launch the system.

> ⚠️ **Note:** The script will pull the latest files from GitHub (except the `persistent/` folder). If you’ve made local changes, they may be overwritten. You can:
- Edit `start.sh` to point to your own fork
- Push your edits to that fork to reflect updates

---

### 2. Building Procedures

Procedures are defined in a `.yaml` file under a `Procedure:` list. Each step corresponds to a machine action (like pipetting, moving, heating, measuring, etc.).

You can:
- **Write by hand** in a `.yaml` file
- **Use the built-in Procedure Builder** GUI:
  - **Dropdown:** Select step type
  - **Add/Insert Step:** Add to list or insert before selected
  - **Vary Step:** Interpolate between steps in loops
  - **Export:** Save a complete `.yaml` file
  - **Import:** Load a `.yaml` file with valid steps
  - **Quick Run:** Test-run without full export

---

### 3. Executing a Procedure

In the GUI:
- **Import:** Load a `.yaml` procedure
- **Start:** Begin execution
- **Pause:** Waits after current step
- **Stop:** Ends after current step
- **Kill:** Emergency shutdown (resets control board; requires full restart)

---

### 4. Locations System

Use the **Locations screen** to define named coordinates (e.g., vial carousel, hotplate, tip rack).  
The `move_to_location` command uses these and **raises the toolhead** first to avoid collisions.

> Updating coordinates in the UI updates movement live without needing restart.

---

### 5. Creating New Custom Moves

To define your own movement commands:
- Edit `moves.py`
- Add your function in the `Dispatcher` class
- Type all parameters so the GUI knows what input fields to show
- Register the move in the `move_dict` inside `__init__`

Your move will now show up in the procedure builder.

## 🧠 ML Details

Bandgap is predicted using Random Forest Regression trained on experimental spectral data.  
Efficiency is calculated using the Shockley-Queisser limit, adjusted for additive modifiers like Zn, Br, FA, EA, etc.

Plots include:
- Bandgap prediction accuracy
- Efficiency distribution
- Actual vs predicted bandgap
- Residuals and feature importances

---

## 📦 Requirements

- Python 3.8+
- Raspberry Pi OS with GPIO and Serial support
- Libraries: `pandas`, `numpy`, `matplotlib`, `seaborn`, `customtkinter`, `scikit-learn`, `category_encoders`, `bayesian-optimization`, etc.

---
## 🤝 Acknowledgements

Originally developed by our Team ECE515 @Binghamton University.

All machine learning code, spectrometer integration, and GUI frame development were built and extended by **Steve Roshan Surendra Kumar** as part of **Team 515** for advanced ML-driven optimization, autonomous spectral control, and user-friendly GUI enhancements.


