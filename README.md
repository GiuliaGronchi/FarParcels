# Far-field Oil Spill Modeling with OceanParcels

[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![OceanParcels](https://img.shields.io/badge/Powered%20by-OceanParcels-blue.svg)](https://oceanparcels.org/)

This project simulates the far-field transport of oil parcels using [OceanParcels](https://oceanparcels.org/). It models 3D advection-diffusion and buoyancy-driven vertical rise (dependent on particle size) after the near-field stage.


## Overview

This repository provides the necessary scripts and configuration files to:

1.  **Pre-configure oil parcels:** Generate a representative size distribution and calculate corresponding buoyant velocities based on initial release and ambient conditions.
2.  **Conduct transport experiments:** Simulate the advection and diffusion of oil parcels under the influence of ocean currents, incorporating buoyancy effects.
3.  **Visualize the results:** Display the temporal evolution of particle transport in both horizontal and vertical perspectives.

## Technology Stack

This project leverages the following open-source tools:

* **[OceanParcels](https://oceanparcels.org/):** A powerful Python framework designed for Lagrangian ocean analysis.
* **Python:** The primary programming language used for scripting and analysis.
* **[conda](https://conda.io/):** An open-source package management system for environment management.
* **YAML:** Used for configuration files.
* **Jupyter Notebook:** Provides an interactive environment for code execution and visualization.

## Setup and Installation

### Prerequisites

* **conda:** Ensure you have conda installed on your system. You can find installation instructions [here](https://conda.io/projects/conda/en/latest/user-guide/install/).

### Creating the Environment

To set up the necessary environment for this project, navigate to the repository directory in your terminal and run the following command:

    conda env create -n parcels environment.yml

This command will create a dedicated conda environment named `parcels` with all the required dependencies specified in the `environment.yml` file.

### Activating the Environment

Once the environment is created, activate it using:

    conda activate parcels

## Workflow

### 1. Pre-configuration of Oil Parcels

The `WbuoySize.ipynb` notebook handles the pre-configuration of oil parcels. It takes initial conditions defined in the `Init.yaml` file as input to generate a likely parcel-size distribution (assuming a log-normal distribution as from Branvik et al.,2013 and Li et al.,2017) and calculates the corresponding buoyant velocities based on the drag-buoyancy balance equation described by Zheng and Yapa (2000).

**Input parameters in `Init.yaml`:**

* `oil_density`: Density of the oil.
* `nozzle_diameter`: Diameter of the release nozzle.
* `release_vel`: Initial vertical velocity of the released oil.
* `npart`: Number of numerical oil parcels to simulate.

Execute the `WbuoySize.ipynb` notebook to produce the Probability Density Function (PDF) of oil parcel sizes and their respective vertical buoyant velocities. Example outputs are provided below:

**Typical Size Distribution PDF:**
<center>
<img src="/size_distr_N2500.png" width="600">
</center>

**Corresponding Vertical Buoyant Velocities:**

<center>
<img src="/buoyant_velocities.png" width="600">
</center>


### 2\. Transport Experiment

The `FarParcels.ipynb` notebook conducts the far-field transport simulation. The experiment settings are also defined in the `Init.yaml` file.

**Transport experiment settings in `Init.yaml`:**

  * `init_lat`: Initial latitude of the oil plume (obtained from the near-field end state).
  * `init_lon`: Initial longitude of the oil plume (obtained from the near-field end state).
  * `Dlat_plume`-`Dlon_plume`: Horizontal dimension of the near-field plume at the end state.
  * `init_depth`: Vertical intrusive depth of the near-field plume at the end state.
  * `release_delay`: Starting time of the spill simulation (relative to the first available ocean data).
  * `sim_runtime`: Total duration of the transport simulation in hours.
  * `output_dt`: Time interval (in hours) for saving simulation output for post-processing and visualization.

Run the `FarParcels.ipynb` notebook to perform the following steps:

1.  **Data Loading and FieldSet Definition:** Specify the output directory and load 3D ocean current data (on a native C grid) from a local directory. This data is used to create a `FieldSet` object in OceanParcels, which also includes sub-grid horizontal (`Kh`) and vertical (`Kv`) diffusion constants.
2.  **Boundary and Surface Conditions:** Define the conditions at the ocean surface and boundaries that will affect the movement of the oil parcels.
3.  **Parcel Initialization:** Initialize the oil parcels based on the specified number and initial positions. Each particle is assigned a buoyant velocity based on the size PDF generated in the pre-configuration step. A `ParticleSet` is created using a custom `BuoyParticle` class that inherits from the standard OceanParcels `Particle` class and includes the buoyant velocity attribute.
4.  **Simulation Setup:** Define the total simulation time and the frequency at which output data should be saved.
5.  **Simulation Execution:** Run the Lagrangian transport simulation using the defined `FieldSet`, `ParticleSet`, and simulation parameters.

### 3\. Visualization

The `Visuals.ipynb` notebook provides tools to visualize the results of the transport experiment. It generates plots showing the particle transport over time from two different perspectives:

  * **Lat-Lon View:** Displays the horizontal movement of particles on a map, with the background showing the intensity of ocean currents (u and v components). The color of each particle represents its depth.

    
    <center>
      <div>
        <img src="/parcels.zarr/PLOTS/2012-09-01_N2500_00h00min.png" width="400">
        <img src="/parcels.zarr/PLOTS/2012-09-01_N2500_00h15min.png" width="400">
      </div>
      <div>
        <img src="/parcels.zarr/PLOTS/2012-09-01_N2500_00h30min.png" width="400">
        <img src="/parcels.zarr/PLOTS/2012-09-01_N2500_01h00min.png" width="400">
      </div>
      <div>
        <img src="/parcels.zarr/PLOTS/2012-09-01_N2500_02h00min.png" width="400">
        <img src="/parcels.zarr/PLOTS/2012-09-01_N2500_10h00min.png" width="400">
      </div>
    </center>
    

  * **Depth View:** Illustrates the vertical movement of oil particles, showing their rise due to buoyancy. The color of each particle in this view represents its vertical velocity.

    
    <center>
    <img src="/parcels.zarr/PLOTS/Depth_2012-09-01_N2500_00h00min.png" width="800">
    <img src="/parcels.zarr/PLOTS/Depth_2012-09-01_N2500_00h15min.png" width="800">
    <img src="/parcels.zarr/PLOTS/Depth_2012-09-01_N2500_00h30min.png" width="800">
    <img src="/parcels.zarr/PLOTS/Depth_2012-09-01_N2500_01h00min.png" width="800">
    <img src="/parcels.zarr/PLOTS/Depth_2012-09-01_N2500_02h00min.png" width="800">
    <img src="/parcels.zarr/PLOTS/Depth_2012-09-01_N2500_02h00min.png" width="800">
    </center>
    

## License

This project is licensed under the [MIT License](https://opensource.org/licenses/MIT).

## Acknowledgements

We gratefully acknowledge the developers and maintainers of the [OceanParcels](https://oceanparcels.org/) framework for providing this invaluable tool for oceanographic research.
