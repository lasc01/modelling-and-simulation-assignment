# Modelling and Simulation Assignment

This repository contains the implementation of a discrete event simulation for container transport operations for Chifeng Gold, performed as part of the Modelling & Simulation assignment at the National College of Ireland. The goal is to model the transportation of containers from the Chifeng mine to Hamburg via Chifeng terminal, Tianjin port, and shipping route; optimize resource allocation; and evaluate system performance under different scenarios.

## Overview

Chifeng Gold exports 2,000 forty-foot equivalent unit (FEU) containers per month. Containers are transported from the mine to the Chifeng rail terminal by trucks, loaded onto a daily scheduled train to Tianjin, and shipped biweekly to Hamburg. Key operational constraints include limited truck and crane capacities, finite buffer storage, train capacity (106 FEUs per day), and ship capacity (1,000 FEUs per voyage). This project uses SimPy to develop a discrete-event simulation to analyze resource requirements, throughput, and system robustness.

## Project Structure

- `src/` – Reusable Python modules for simulation logic and parameters.
- `notebooks/` – Jupyter notebooks for each step of the assignment:
  - `step3_initial_verification.ipynb` – Small-scale simulation to verify model logic with 3 containers, 1 truck, and 1 crane over one day.
  - `step4_scaling_and_stats.ipynb` – Scaling the model to handle up to 106 containers per day and analyzing resource requirements through simulation and calculations.
  - `step5_month_variability.ipynb` – Month-long simulation combining steady and variable demand scenarios.
- `report/` – LaTeX sources and compiled PDF of the final report.
- `figures/` – Images and plots used in the report.
- `data/` – Input and output data sets (if any).
- `docs/` – Additional documentation.
- `README.md` – This file.
- `LICENSE` – MIT License.
- `requirements.txt` – Python dependencies list.
- `environment.yml` – Conda environment specification.
- `Makefile` – Helper commands for running notebooks and building the report.

## Steps Summary

### Step 1 – Entities, Activities, and Events
Identify the key entities (containers, trucks, cranes, trains, ships), activities (transportation, loading, unloading), and events (arrivals, departures, load completions) in the system.

### Step 2 – Model Description
Develop graphical representations (activity cycle diagram and event graph) and mathematical formulations. Define throughput, resource capacities, and flow constraints using equations for truck and crane capacities, train limits, buffer sizes, and steady-state relations.

### Step 3 – Initial Simulation and Verification
Build an initial SimPy model to simulate 3 containers using a single truck and crane over one day. Verify sequential resource usage and ensure all containers are loaded onto the train before the scheduled departure. Use round-trip truck time of 1.5 hours and crane handling time of 0.5 hours to balance realism with simplicity.

### Step 4 – Scaling the Simulation Model
Scale the simulation to handle up to 106 containers per day (the train capacity). Determine the minimum number of trucks and cranes required using theoretical calculations and simulation experiments. Results indicate that 9 trucks and 3 cranes are necessary to meet daily throughput, and that buffer capacity should be at least 110 FEUs to handle peak queues. The train capacity of 106 FEUs per day acts as the primary bottleneck.

### Step 5 – Month-long Simulation and Variability
Extend the scaled model to simulate a full month (30 days) with both steady and variable daily demands. Use a normal distribution (mean 91 FEUs, standard deviation 15) to capture variability. Analyze throughput, resource utilization, queue lengths, and system robustness. Results show truck utilization around 91.67%, crane utilization about 68.75%, and average truck waiting times of approximately 10.79 hours, indicating trucks as the limiting resource during peak demand. Buffer occupancy can exceed 110 FEUs on high-demand days, suggesting the need for increased storage or dynamic management.

## Results and Recommendations

- **Resource Requirements**: At least 9 trucks and 3 cranes are required to meet the daily throughput of 106 FEUs. Buffer capacity of at least 110 FEUs is recommended to accommodate peak queues.
- **Throughput Constraints**: Train capacity of 106 FEUs per day limits throughput. Adding more trucks or cranes beyond the required numbers does not increase throughput but can reduce waiting times.
- **Utilization and Waiting Times**: In variable demand scenarios, trucks are heavily utilized (~91.67%) while cranes operate at moderate utilization (~68.75%). Average truck waiting times around 10.79 hours highlight the need for adequate truck resources.
- **Buffer Occupancy**: Buffer levels occasionally exceed the recommended 110 FEUs, particularly during demand surges. Consider increasing buffer space or implementing dynamic scheduling to mitigate congestion.
- **Operational Recommendations**: Expand the truck fleet or optimize dispatching to reduce wait times, maintain current crane capacity, and increase buffer storage to handle surges. Regularly monitor system performance and adjust resources as needed.

## Getting Started

To reproduce the simulation and explore the project:

1. **Clone the repository**
   ```bash
   git clone https://github.com/lasc01/modelling-and-simulation-assignment.git
   cd modelling-and-simulation-assignment
   ```

2. **Install dependencies** (using virtualenv):
   ```bash
   python -m venv .venv
   source .venv/bin/activate  # On Windows use .venv\\Scripts\\activate
   pip install -r requirements.txt
   ```
   or using Conda:
   ```bash
   conda env create -f environment.yml
   conda activate chifeng-sim
   ```

3. **Run the simulation notebooks**:
   ```bash
   jupyter notebook
   ```
   Open the notebook corresponding to the step you wish to explore. Each notebook is preconfigured to run simulations and generate plots.

4. **Build the report** (optional):
   ```bash
   make build-report
   ```
   This will compile the LaTeX report into a PDF in the `report/` folder.

## Contributing

Contributions are welcome! Please fork this repository and submit a pull request. For major changes, open an issue first to discuss your proposed modifications.

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.

## References

- J. Banks, J. S. Carson, B. L. Nelson, and D. M. Nicol, *Discrete-Event System Simulation*, 5th Edition, Pearson, 2010.
- B. K. Choi and D. Kang, *Modeling and Simulation of Discrete Event Systems*, Wiley, 2013.
- A. M. Law, *Simulation Modeling and Analysis*, 5th Edition, McGraw-Hill, 2014.
- L. G. Birta and G. Arbez, *Modelling and Simulation*, 3rd Edition, Springer, 2019.
- C. Horn, "Modelling and Simulation Lecture Notes," National College of Ireland, 2025.
