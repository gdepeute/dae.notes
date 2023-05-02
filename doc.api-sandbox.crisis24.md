---
id: tvv9uvy133xemeu0kzaq6k3
title: Crisis24
desc: ""
updated: 1683055204123
created: 1683054386243
---

# API Sandbox Documentation for Crisis24

## Crisis24 POC

Crisis24 has requested access to the historical hazards and 5 layers for their POC effort:

Layers:

- Population Density (WMS)
  - https://api-sandbox.disasteraware.com/services/geowebcache_wms (LAYERS=pop_dens_2015)
- Earthquake Locations and Magnitude (ARCGIS)
  - https://api-sandbox.disasteraware.com/services/global/pdc_active_hazards/MapServer (layers=6)
- Earthquake Intensity Zones (ARCGIS)
  - https://api-sandbox.disasteraware.com/services/gloabl/pdc_hazard_zones/MapServer (layers=9)
- Earthquake Shaking Intensity - ShakeMap Model (ARCGIS)
  - https://api-sandbox.disasteraware.com/services/global/pdc_models/MapServer
- Tectonic Plate Boundaries (ARCGIS)
  - https://api-sandbox.disasteraware.com/services/global/pdc_hazard_zones/MapServer (layers=9)

## Palanir/Crisis24 SOW

- Desired Layers

  - Population Density
    - https://agsc.pdc.org/geowebcache/service/wms (LAYERS=pop_dens_2015)
  - Earthquake Locations and Magnitutude
    - https://apps.pdc.org/msf/rest/services/global/pdc_active_hazards/Mapserver (6: Recent_Earthquakes)
  - Earthquake Intensity Zones
    - https://org-disasteralert.pdc.org/msf/rest/services/global/pdc_hazard_zones/MapServer (9: Earthquake Intensity Zones)
  - ## Shaking Intensity (ShakeMap Model)
  - Tectonic Plate Boundaries
    - https://org-disasteralert.pdc.org/msf/rest/services/global/pdc_hazard_zones/MapServer (6: Tectonic Plate Boundaries)

- Need to configure mappings to 4 servers:
  - https://agsc.pdc.org/geowebcache/service/wms with query param "LAYERS=pop_dens_2015)
  - https://apps.pdc.org/msf/rest/services/global/pdc_active_hazards/Mapserver (id: 6)
  - https://org-disasteralert.pdc.org/msf/rest/services/global/pdc_hazard_zones/MapServer (id: 6 and 9)
  - https://apps.pdc.org/msf/rest/services/global/pdc_models/MapServer (id: 6)
