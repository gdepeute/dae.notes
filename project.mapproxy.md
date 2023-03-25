---
id: w8v5qudwwmj1x018wpy3qvu
title: Mapproxy
desc: ""
updated: 1679703558660
created: 1679703138003
---

# MapProxy experimentation

## Layers and Protocols for initial implementation

- Population Density / PDC GeoWebCache / WMS / layer_id: pip_dens_2015 / auth: yes
- Airport
- Airport Density
- Hospitals (Infra)
- Ports (Infra)
- Earthquakes Locations and Magnitude
- Earthquakes Intensity ones
- Earthquakes Shaking Intensity
- Tornado (Warnings)
- Tornado (Watches)
- Tsunami (Watch and Warning Zones)
- Volcano Locations
- Wildfire Locations (Hotspots)
- Potential Large/Intense Wildfire
- Tectonic Plate Boundaries
- Global Weather Observations (METAR)

· Global Weather (METAR) including forecasts

I believe this exactly matches the existing layer “Global Weather Observations (METAR)” in the Observations and Forecasts/Surface folder
· Historical Data at a global level (going back till 2010 if possible)

o Historical Earthquakes with details

I believe this exactly matches the existing layer “Historical Earthquakes” in the Earthquakes folder

o Historical Tsunami and Cyclones with path and details

I believe this exactly matches the existing layers “Historical Tsunami Events, Historical Cyclone Tracks 2014-2021” in the Tsunami and Cyclone folders

o Historical Wildfires, path and details

I believe this exactly matches the existing layer “Historical Large Fires” in the Wildfire folder

o Historical Floods

I believe this exactly matches the existing layer “Historical Large Floods” in the Flood folder

o Historical Landslide with Landslide frequency, exposure, etc.

I don’t believe we currently have this data/layers

o Historical Winterstorm / Avalanches with forecasts

I don’t believe we currently have this data/layers

o Historical Volcanic eruptions and locations

I believe this exactly matches the existing layer “Historical Volcanic Eruptions” in the Volcanos folder

· Rainfall

Unclear what they are requesting here. We have some Rainfall accumulation layers, and some animated forecast and potential layers. BUT there are also a bunch of the Rainfall layers are TAOS layers. Need to clarify what exactly they want and that TAOS is off the table.
