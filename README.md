
# Far-field

At the end state of the near-field, a far-field motion takes place. Here, oil parcels are under 3D advection-diffusion by ocean currents and move independently. Another consistent characteristics is the vertical rising induced by oil buoyancy. This is very dependent on size, as larger particles have greater buoyancy with respect to smaller ones.

### Preconfiguration of oil parcels

A representative sample of oil particles is here modelled. Given release and ambient conditions, a likely parcel-size distribution is built (on a log-normal assumption) and size-corresponding buoyant velocity is calculated from a drag-buoyancy balance.

Just insert the initial conditions of the Farfield simulation in _Init.yaml_ :

Input values:

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





### Transport experiment

In _Init.yaml_ we also the settings for the transport experiment:

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


In _Visuals.ipynb_ you can visualize the particle transport in time from two perspectives:

- a Lat-Lon view with u-v intensity field, where parcels color represent depth

<center>
<img src="/parcels.zarr/PLOTS/2012-09-01_N2500_00h15min.png" width="600">
</center>


- a Depth view, with rising oil particles, where parcels color represents vertical velocity

<center>
<img src="/parcels.zarr/PLOTS/Depth_2012-09-01_N2500_00h15min.png" width="600">
</center>