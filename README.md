
## Far Parcels

In the near-field region, oil spills behave collectively as a plume until they reach a deep buoyant level in the water column. In the far-field region, oil parcels resulting from the disintegration of a deep oil spill are advected and diffused by ocean currents. Moreover, they move vertically within the water column due to the buoyancy of oil in water.

This script, based on OceanParcels libraries and repositories, performs the following:

1 - define output folder & import ocean currents data ( on native C grid ) from local directory, which defines a FieldSet, together with the sub-grid diffusion constants Kv and Kh

2 - define buoyant velocity kernel, surface and boundary conditions kernels

3 - initialize parcels number , parcels position

4 - assign each particle a buoyant velocity, depending on size PDF built in w_buoy.csv

5 - define a ParticleSet from the inherit class BuoyParticle

6 - define simulation time periods and intervals and RUN the transport simulation