# Far-field

At the end of the near-field stage, a far-field motion takes place. Here, oil parcels move independently under 3D advection-diffusion driven by ocean currents. Another consistent characteristic is the vertical rising induced by oil buoyancy, which strongly depends on particle size—larger particles have greater buoyancy compared to smaller ones.

This project uses [OceanParcels](https://oceanparcels.org/), an open-source framework for Lagrangian ocean analysis. OceanParcels is developed and maintained by the OceanParcels team, and its source code is available at [github.com/OceanParcels/parcels](https://github.com/OceanParcels/parcels).


### Create parcels environment

    conda env create -n parcels environment.yml

### Preconfiguration of oil parcels

A representative sample of oil particles is here created. Given release and ambient conditions, a likely parcel-size distribution is built (on a log-normal assumption) and size-corresponding buoyant velocity is calculated from a drag-buoyancy balance _(Zheng and Yapa, 2000)_.

Just insert the initial conditions in _Init.yaml_ :
- oil density
- nozzle diameter
- release vertical velocity
- number of numerical oil 'parcels' 

and run _WbuoySize.ipynb_ to obtain PDF of oil parcels size and respective vertical buoyant velocity.

A typical size-PDF is

<center>
<img src="/size_distr_N2500.png" width="600">
</center>

with vertical buoyant velocity

<center>
<img src="/buoyant_velocities.png" width="600">
</center>



### Transport experiment

In _Init.yaml_ are also the settings for the transport experiment:

- initial lat and lon (from near-field end state)
- near-field plume dimension and intrusive depth (end of near-field)
- starting spill date and time (with respect to first available ocean data)
- total transport time (in hours)
- output time-interval for post-processing and visualization


Run _FarParcels.ipynb_ to do the following:

1 - Define output folder & select 3D ocean currents data ( on native C grid ) from a local directory, which defines a FieldSet, together with the sub-grid diffusion constants Kv and Kh

2 - Determine surface and boundary conditions

3 - Initialize the oil parcels (in number and position), assign each particle a buoyant velocity (depending on size PDF). Define a ParticleSet from the inherited class BuoyParticle

4 - Set simulation time periods and output intervals 

5 - RUN the transport simulation


### Visualization

Running _Visuals.ipynb_ you can see the particle transport in time from two perspectives:

- a Lat-Lon view with u-v intensity field, where parcels color represent depth

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


- a Depth view, with rising oil particles, where parcels color represents vertical velocity

<center>
<img src="/parcels.zarr/PLOTS/Depth_2012-09-01_N2500_00h00min.png" width="800">
<img src="/parcels.zarr/PLOTS/Depth_2012-09-01_N2500_00h15min.png" width="800">
<img src="/parcels.zarr/PLOTS/Depth_2012-09-01_N2500_00h30min.png" width="800">
<img src="/parcels.zarr/PLOTS/Depth_2012-09-01_N2500_01h00min.png" width="800">
<img src="/parcels.zarr/PLOTS/Depth_2012-09-01_N2500_02h00min.png" width="800">
<img src="/parcels.zarr/PLOTS/Depth_2012-09-01_N2500_02h00min.png" width="800">
  
</center>