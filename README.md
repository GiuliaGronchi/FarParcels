
## Far Parcels

At the end state of the near-field, a far-field motion takes place. Here, oil parcels are under 3D advection-diffusion by ocean currents and move independently. Another consistent characteristics is the vertical rising induced by oil buoyancy. This is very dependent on size, as larger particles have greater buoyancy with respect to smaller ones.

A representative sample of oil particles is here modelled. Given release and ambient conditions, a likely parcel-size distribution is built (on a log-normal assumption) and size-corresponding buoyant velocity is calculated from a drag-buoyancy balance.

Just insert the initial conditions of the Farfield simulation in _Init.yaml_ :

Input values:

- oil density
- nozzle diameter
- release vertical velocity
- number of numerical oil 'parcels' 

and run _WbuoySize.ipynb_ for this part.

In _Init.yaml_ we also have other settings:

- initial lat and lon (from near-field end state)
- near-field plume dimension and intrusive depth
- starting simulation time with respect to first ocean data
- total simulation time in hours
- output time-interval


Then, you can run _FarParcels.ipynb_ and see the following steps going on:

1 - define output folder & import ocean currents data ( on native C grid ) from local directory, which defines a FieldSet, together with the sub-grid diffusion constants Kv and Kh

2 - define buoyant velocity kernel, surface and boundary conditions kernels

3 - initialize parcels number , parcels position

4 - assign each particle a buoyant velocity, depending on size PDF built in w_buoy.csv

5 - define a ParticleSet from the inherit class BuoyParticle

6 - define simulation time periods and intervals 

7 - RUN the transport simulation


In _Visuals.ipynb_ you can visualize the particle transport from two different perspective.

- a Lat-Lon view, with ocean currents superposed, where depth is represented by particles color
- a Depth view, with rising oil particles, where color represents vertical velocity