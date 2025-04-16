Far-Field Oil Parcel Transport
This repository simulates the far-field transport of oil parcels following an underwater release. After the near-field stage, oil parcels evolve independently under 3D advection-diffusion driven by ocean currents. A key factor influencing their movement is buoyancy-induced vertical rising, which varies with particle size—larger particles exhibit greater buoyancy compared to smaller ones.

This project builds upon the open-source framework OceanParcels, developed for Lagrangian ocean analysis.
🔗 Source code: github.com/OceanParcels/parcels

📦 Conda Environment Setup
To create the Conda environment used in this project:

bash
Copia
Modifica
conda env create -n parcels environment.yml
⚙️ Preconfiguration of Oil Parcels
A representative distribution of oil parcels is generated based on initial release and ambient conditions. Assuming a log-normal distribution, parcel sizes are sampled, and buoyant velocities are computed from a drag-buoyancy balance, following Zheng and Yapa (2000).

Edit the parameters in Init.yaml:

Oil density

Nozzle diameter

Initial vertical release velocity

Number of oil parcels

Then, run the notebook WbuoySize.ipynb to generate the PDF of parcel sizes and their corresponding vertical velocities.

Size Distribution (PDF)
<center> <img src="/size_distr_N2500.png" width="600"> </center>
Corresponding Buoyant Velocities
<center> <img src="/buoyant_velocities.png" width="600"> </center>
🌊 Transport Simulation
Transport settings are also defined in Init.yaml:

Initial latitude and longitude (from near-field output)

Near-field plume dimensions and intrusive depth

Start date/time relative to ocean data

Total simulation duration (in hours)

Output time interval

Run FarParcels.ipynb to execute the simulation. The steps include:

Define output paths and load 3D ocean current data (C-grid) as a FieldSet

Set sub-grid diffusion coefficients Kv and Kh

Apply surface and boundary conditions

Initialize the ParticleSet with custom buoyant velocity from the size distribution

Define simulation runtime and time steps

Run the Lagrangian transport simulation

🖼️ Visualization
Use Visuals.ipynb to explore particle transport through two perspectives:

1. Lat-Lon View
Oil parcel positions overlaid on horizontal current fields. Parcel color indicates depth.

<center> <div> <img src="/parcels.zarr/PLOTS/2012-09-01_N2500_00h00min.png" width="400"> <img src="/parcels.zarr/PLOTS/2012-09-01_N2500_00h15min.png" width="400"> </div> <div> <img src="/parcels.zarr/PLOTS/2012-09-01_N2500_00h30min.png" width="400"> <img src="/parcels.zarr/PLOTS/2012-09-01_N2500_01h00min.png" width="400"> </div> <div> <img src="/parcels.zarr/PLOTS/2012-09-01_N2500_02h00min.png" width="400"> <img src="/parcels.zarr/PLOTS/2012-09-01_N2500_10h00min.png" width="400"> </div> </center>
2. Depth View
Rising parcel profiles, where color represents vertical velocity.

<center> <div> <img src="/parcels.zarr/PLOTS/Depth_2012-09-01_N2500_00h00min.png" width="800"> <img src="/parcels.zarr/PLOTS/Depth_2012-09-01_N2500_00h15min.png" width="800"> </div> <div> <img src="/parcels.zarr/PLOTS/Depth_2012-09-01_N2500_00h30min.png" width="800"> <img src="/parcels.zarr/PLOTS/Depth_2012-09-01_N2500_01h00min.png" width="800"> </div> <div> <img src="/parcels.zarr/PLOTS/Depth_2012-09-01_N2500_02h00min.png" width="800"> <img src="/parcels.zarr/PLOTS/Depth_2012-09-01_N2500_02h00min.png" width="800"> </div> </center>