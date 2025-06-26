# Far-field: Subsurface Oil Spill Simulation

[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![OceanParcels](https://img.shields.io/badge/Powered%20by-OceanParcels-blue.svg)](https://oceanparcels.org/)

This repository contains a Python-based framework for simulating the **far-field transport** of oil parcels following a subsurface release event.  
The model uses [OceanParcels](https://oceanparcels.org/) to simulate 3D Lagrangian advection-diffusion dynamics and buoyancy-driven vertical rise, based on particle size distributions generated during the pre-processing phase.

---

## Overview

This repository provides tools and scripts to:

1. **Preprocess oil parcel properties**  
   Generate a size distribution and assign buoyant rise velocities based on physical conditions at the end of the near-field stage.
   
2. **Run far-field simulations**  
   Perform 3D advection-diffusion modeling of oil parcels under ocean current and buoyancy influence.
   
3. **Visualize transport behavior**  
   Analyze the horizontal and vertical evolution of particles over time.

---

## Setup and Installation

### Prerequisites

Ensure that **conda** is installed. Instructions can be found [here](https://conda.io/projects/conda/en/latest/user-guide/install/).

### Create the Conda Environment

Navigate to the repository folder and run:

```bash
conda env create -n parcels environment.yml
```

This will create a conda environment named `parcels` with all required dependencies.

### Activate the Environment

```bash
conda activate parcels
```

---

## Workflow

### 1. Preprocess Oil Parcels

The `WbuoySize.ipynb` notebook generates a size distribution and calculates vertical velocities for each parcel based on input parameters in `Init.yaml`. The model uses a log-normal distribution (Branvik et al., 2013; Li et al., 2017) and buoyancy-drag physics (Zheng & Yapa, 2000).

**Key parameters in `Init.yaml`:**

- `oil_density`: Oil density (kg/m³)  
- `nozzle_diameter`: Release nozzle diameter (m)  
- `release_vel`: Initial release velocity (m/s)  
- `npart`: Number of particles to simulate  

#### Example Outputs

**Oil Parcel Size Distribution:**

<img src="/size_distr_N2500.png" alt="Size distribution" width="500"/>

**Buoyant Velocity Distribution:**

<img src="/buoyant_velocities.png" alt="Buoyant velocities" width="500"/>

---

### 2. Far-field Transport Simulation

The `FarParcels.ipynb` notebook performs the Lagrangian simulation using OceanParcels. Configuration is controlled via `Init.yaml`.

**Simulation settings in `Init.yaml`:**

- `init_lat`, `init_lon`: Release coordinates  
- `Dlat_plume`, `Dlon_plume`: Horizontal extent of the plume  
- `init_depth`: Release depth  
- `release_delay`: Time offset from first ocean data  
- `sim_runtime`: Simulation duration (hours)  
- `output_dt`: Output interval (hours)

**Steps performed:**

1. **Load ocean data** and create a `FieldSet` object from native C-grid 3D currents (and optional `Kh`, `Kv` diffusivity fields)  
2. **Initialize parcels** with buoyant velocities and starting positions using a custom `BuoyParticle` class  
3. **Run simulation** with user-defined time span and output frequency  
4. **Store results** for visualization and post-processing

---

### 3. Visualization

The `Visuals.ipynb` notebook creates 2D and 3D plots of the simulation output.

#### Horizontal Transport – Lat/Lon Map

Color denotes particle depth; background shows ocean current velocity (u, v).

<img src="/parcels.zarr/PLOTS/OUT2012-09-01_N2500_10h00min.png" alt="Horizontal map" width="400"/>

**Time-lapse:**

<div>
  <img src="/parcels.zarr/PLOTS/2012-09-01_N2500_00h00min.png" width="300"/>
  <img src="/parcels.zarr/PLOTS/2012-09-01_N2500_00h15min.png" width="300"/>
  <img src="/parcels.zarr/PLOTS/2012-09-01_N2500_00h30min.png" width="300"/>
  <img src="/parcels.zarr/PLOTS/2012-09-01_N2500_01h00min.png" width="300"/>
  <img src="/parcels.zarr/PLOTS/2012-09-01_N2500_02h00min.png" width="300"/>
  <img src="/parcels.zarr/PLOTS/2012-09-01_N2500_10h00min.png" width="300"/>
</div>

---

#### Vertical Transport – Depth View

Particles are colored by vertical velocity.

<div>
  <img src="/parcels.zarr/PLOTS/Depth_2012-09-01_N2500_00h00min.png" width="500"/>
  <img src="/parcels.zarr/PLOTS/Depth_2012-09-01_N2500_00h15min.png" width="500"/>
  <img src="/parcels.zarr/PLOTS/Depth_2012-09-01_N2500_00h30min.png" width="500"/>
  <img src="/parcels.zarr/PLOTS/Depth_2012-09-01_N2500_01h00min.png" width="500"/>
  <img src="/parcels.zarr/PLOTS/Depth_2012-09-01_N2500_02h00min.png" width="500"/>
  <img src="/parcels.zarr/PLOTS/Depth_2012-09-01_N2500_10h00min.png" width="500"/>
</div>

---

## License

This project is licensed under the [MIT License](https://opensource.org/licenses/MIT).


