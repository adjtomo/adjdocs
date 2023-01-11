# An (ongoing) Inversion Walkthrough for northern Alaska

## Motivation
As I step into my own inversion project for northern Alaska, I'd like to keep track of all my steps in a sort of diagrammatic walkthrough.
This would be something like a flowchart with each of the tasks I had to complete (from data gathering to model updates), and the packages or code snippets I used to create them. 

It is currently difficult to determine which package should be used where, and how all the adjTomo suite is meant to work in conjunction, so my hope is that a real world example, and the documentation that falls out of it, can providesUsers a point of reference when using the suite for their own research.

For now I will list the steps that I have taken or will take, and the package used to tackle it. I hope in the future each of these tasks has a set of hyperlinks to docs pages or code snippets that show exactly how these things happened. 

## Tasks

### A. Run a Forward Simulation

#### 1. Decide study region, determine domain boundaries [manually]
- Our original proposal was to study northeastern Alaska so this decision was previously made
- I use a bounding box tool to determine the geographic extent of the region in question (e.g., https://boundingbox.klokantech.com/)
>__Boundary Note:__ Try to add some buffer boundary so that events and stations are not right on the edge of your mesh. 
    I'm not sure there is an accepted value, but I try to add a few wavelengths.

#### 2. Generate hexahedral mesh [meshfem3D]
- Due to the scale of the problem (continental) we choose to use SPECFEM3D_GLOBE 
- We use the SPECFEM internal mesher (Meshfem3D) to generate our truncated one chunk mesh
- ETOPO4 is used for topography (already available in SPECFEM3D_GLOBE)

#### 3. Choose velocity model [specfem3d_globe]
- At the moment I have chosen to use a model present in the software (Crust2.0 + S20RTS with ETOPO4 topography)
- In the future we may choose more heterogeneous/complex 3D models of our study region

#### 4. Determine example source, generate CMTSOLUTION [[PySEP](https://github.com/adjtomo/pysep)]
- We need an appropriate earthquake to run a simulation
- The [Kaktovic earthquake](https://earthquake.usgs.gov/earthquakes/eventpage/ak20076877#moment-tensor) comes to mind as a large event in the region. Perhaps too large to use a point source approximation, but aftershocks should be reasonable
- Searching through the [GCMT catalogue](https://www.globalcmt.org/), I find an appropriate event of M5.1 (201808121602B)
- I can directly copy-paste the CMTSOLUTION from their website, or use PySEP to grab it for me given an origin time. This will be useful in the future when grabbing an entire catalog of earthquakes

```python
from pysep.utils.mt import get_gcmt_moment_tensors
cat = get_gcmt_moment_tensors(origintime="2018-08-12T16:02:09", magnitude=5.1)
cat.write('CMTSOLUTION_201808121602B',format="CMTSOLUTION")
```

#### 5. Gather stations in the region [[PySEP](https://github.com/adjtomo/pysep)]
- Now I need a STATIONS file for SPECFEM, defining existing broadband seismic stations in this region  
- We can use ObsPy to gather station information from IRIS and PySEP to write them out into the STATIONS format expected by SPECFEM
- https://github.com/adjtomo/pysep/wiki/6.-Cookbook#create-stations-file-for-specfem

#### 6. Run simulation

- Now we can run meshfem and specfem to generate synthetic seismograms
- Visualize the mesh and model using ParaView
- Make adjustments to mesh, model or receivers based on the result of this example forward simulation  

### B. Set Up Inversion

#### 1. Gather catalog of moment tensors [[PySEP](https://github.com/adjtomo/pysep) + ObsPy]

- We can use PySEP to gather moment tensors for our specified region

```python
from obspy import UTCDateTime, Catalog
from obspy.clients.fdsn import Client
from pysep.utils.mt import get_usgs_moment_tensor, get_gcmt_moment_tensor

c = Client("IRIS")
cat = c.get_events(starttime=UTCDateTime("2000-01-01"),
                   endtime=UTCDateTime("2022-12-31"),
                   minmagnitude=4.0, maxmagnitude=6.0,
                   minlatitude=66., maxlatitude=71.,
                   minlongitude=-168., maxlongitude=-140.,
                   maxdepth=60., orderby="magnitude-asc",
                   includeallorigins=False, 
                   includeallmagnitudes=False,
                   )

# This recovers 90 USGS moment tensors
usgs_cat = Catalog()
for event in cat:
    mt = get_usgs_moment_tensor(event)
    if mt:
        usgs_cat.extend(mt)

for event in cat_w_mt:         
    tag = event.preferred_origin().resource_id.id.split("/")[3]                 
    if hasattr(event, "focal_mechanisms") and event.focal_mechanisms:           
        try:                                                                    
            event.write(f"CMTSOLUTION_{tag}", format="CMTSOLUTION")             
        except Exception as e:                                                  
            continue      

# This recovers 30 GCMT moment tensors
gcmt_cat = Catalog()
for event in cat:
    mt = get_gcmt_moment_tensor(event)
    gcmt_cat.extend(mt)

for event in gcmt_cat:                                                          
    tag = event.resource_id.id.split("/")[2]                                    
    try:                                                                        
        event.write(f"CMTSOLUTION_{tag}", format="CMTSOLUTION")                 
    except Exception:                                                           
        continue    
```

#### 2. (Optional) Visualize moment tensors [[based_alaska](https://github.com/bch0w/based_alaska)]

- Using the collected QUAKEML and STATIONS file, Based Alaska can plot a basemap using PyGMT
![nalaska_map](https://user-images.githubusercontent.com/23055374/206031355-ffb2cc75-096b-4abb-bc32-09f0a8b6ac08.png)



