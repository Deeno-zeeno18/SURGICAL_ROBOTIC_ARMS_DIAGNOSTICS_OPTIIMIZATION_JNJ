# Surgical Robotic Arm: Diagnostics and Design Optimization

Virtual work experience project based on the **Johnson & Johnson MedTech Robotics & Control Engineering** job simulation (Forage). The work is in two parts: diagnosing delayed responses in a surgical robotic arm, then proposing design changes to improve its responsiveness and durability.

**Author:** Zelden Nii-Okai Okai

> This is a self-paced simulation task, not real employment. The starter notebooks and report templates come from the Forage simulation. My own work is the measurements, analysis, written reports, design proposal and figures described below.

---

## Task 1: Control System Diagnostics

**Scenario:** A customer ticket reported delayed response times in a surgical robotic arm, with the `rotate_joint` command flagged as the problem.

**What I did**
- Measured response times for `move_arm`, `rotate_joint` and `adjust_grip` using the provided `check_response_time` function.
- Compared each measurement with its expected value and recorded the differences.
- Wrote a hypothesis for the cause of the delay (a blocking wait or redundant calculation in the `rotate_joint` code path).
- Applied the notebook's simulated optimization step and documented its limits.
- Wrote a structured diagnostic report using the provided template.

**Results**

| Command | Expected (s) | Initial (s) | Optimized (s) |
|---|---|---|---|
| `move_arm` | 0.10 | 0.101 | 0.08 |
| `rotate_joint` | 0.18 | 0.15 | 0.12 |
| `adjust_grip` | 0.09 | 0.05 | 0.04 |

**Key findings**
- `rotate_joint` was the slowest command and was close to the reported 0.18 s delay, so it remained the priority for investigation.
- `move_arm` and `adjust_grip` were within expected values; the 0.001 s gap on `move_arm` is within timing noise.
- The "optimized" times come from a fixed 20% improvement factor, not a code change. They show what a fix might achieve, not that one has been achieved.
- The root cause was not identified. Next steps are repeated measurements, inspecting the `rotate_joint` code for blocking waits or redundant calculations, making a real code change, and re-measuring.

---

## Task 2: Design Optimization

**Scenario:** Propose design modifications that improve the arm's response time and durability, using a provided simulation notebook.

**What I did**
- Ran the simulation with several efficiency factors (for example 0.2, 0.325, 0.5, 0.8, 0.85) and reinforcement factors (for example 0.40, 0.625, 0.742, 0.75, 0.90).
- Recorded the results for the headline case and compared original and modified metrics.
- Wrote a design proposal covering the problem statement, proposed modifications, simulation results, annotated visuals, expected outcomes and a conclusion.
- Created two annotated figures for the proposal.

**Results (efficiency factor 0.325, reinforcement factor 0.625)**

| Metric | Original | Modified |
|---|---|---|
| Response time | 0.20 s | 0.135 s (32.5% reduction) |
| Durability score | 75 | 121.88 |

**Key findings**
- The efficiency factor reduced response time by exactly the factor entered, so the result shows the effect of an assumed improvement, not a measured one.
- The durability score exceeded the notebook's 100-point scale, so the reinforcement factors need realistic justification.
- The two factors are independent in the model, so the simulation cannot show a trade-off between speed and durability. In a real design, added reinforcement could add mass and slow response, so this needs physical testing.
- Sensor feedback delay was not simulated. Sensor realignment is recommended in the proposal as a hypothesis to test.

---

## Repository contents

| File | Description |
|---|---|
| `Control_System_Diagnostics_Notebook.ipynb` | Task 1 notebook with my measurements, hypothesis and ROBOTICS_DIAGNOSTICS_REPORT.pdf` | Task 1 diagnostic report |
| `Robotic_Arm_Design_Simulation.ipynb` | Task 2 notebook with simulation runs and observations |
| `Design_Optimization_Proposal.pdf` | Task 2 design proposal |
| `design_proposal.tex` | LaTeX source for the proposal |
| `sensor_misalignment_vs_realignment.png` | Illustrative diagram (not measured data) |
| `actuator_upgrade_impact.png` | Simulation results chart (modelled values) |

---

## Skills demonstrated

**Engineering and analysis**
- Diagnosing performance problems in control software: baseline measurement, comparison against specifications, and hypothesis formation
- Latency and response-time analysis, including recognizing timing noise versus a real discrepancy
- Parametric simulation and sensitivity testing across a range of input factors
- Identifying the limits of a model, including the difference between modelled and measured results and assumptions hidden in simplified functions
- Design optimization thinking: actuator strain, sensor alignment, and the trade-off between responsiveness and durability
- Root cause analysis planning and defining validation steps (repeated trials, prototype testing)

**Programming and tools**
- Python: the `time` module for timing, NumPy for numerical work, and Matplotlib for plotting
- Jupyter Notebook workflow for running, documenting and iterating on experiments
- Data visualization: annotated bar charts and an explanatory diagram
- Git and GitHub for version control and publishing project work

**Communication**
- Technical report writing using structured templates (executive summary, issue description, findings, conclusion)
- Writing a design proposal with justification, expected outcomes and clearly stated limitations
- Documenting troubleshooting steps and recommending next steps
- LaTeX and Overleaf for formatted documents with tables, figures and consistent layout
- Reporting honestly: separating observed results from assumptions and simulated values

---

## How to run

1. Open the `.ipynb` files in Jupyter Notebook, JupyterLab or Google Colab.
2. Install the dependencies if needed: `pip install numpy matplotlib`.
3. Run the cells in order. The Task 2 notebook will ask you to enter an efficiency factor and a reinforcement factor (both between 0 and 1).
4. To rebuild the proposal PDF, upload `design_proposal.tex` and the two PNG files to Overleaf and compile.

## Next steps

- Replace the simulated 20% improvement factor in Task 1 with a real code change to `rotate_joint`, then re-measure and compare.
- Add repeated trials and report averages for each command.
- Extend the Task 2 simulation to model sensor feedback delay, and add a cap on the durability score.
- Test whether added reinforcement slows response, to check for a trade-off.
