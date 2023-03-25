---
id: w8v5qudwwmj1x018wpy3qvu
title: Mapproxy
desc: ""
updated: 1679704405592
created: 1679703138003
---

# MapProxy experimentation

## Layers and Protocols for initial implementation

- Population Density / PDC GeoWebCache / WMS / layer_id: pip_dens_2015 / auth: yes
  - https://agsc.pdc.org/geowebcache/service/wms
- Airport / PDC Mapserver / ARCGIS / layer_id: large_airports / auth: yes
  - https://apps.pdc.org/msf/rest/services/global/pdc_global_infrastructure/MapServer
- Airport Density / PDC Mapserver / ARCGIS / layer_id: airport_density
  - https://org-disasteralert.pdc.org/msf/rest/services/global/pdc_basemap/MapServer
- Hospitals (Infra) / PDC Mapserver / ARCGIS / layer_id: Hospitals / auth: yes
  - https://apps.pdc.org/msf/rest/services/global/pdc_global_infrastructure/MapServer
- Ports (Infra) / PDC Map Server / ARCGIS / layer_id: Large Ports / auth_yes
  - https://apps.pdc.org/msf/rest/services/global/pdc_global_infrastructure/MapServer
- Earthquakes Locations and Magnitude / PDC Mapserver / ARCGIS / layer_id: Recent_Earthquakes / auth: no
  - https://apps.pdc.org/msf/rest/services/global/pdc_active_hazards/Mapserver
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
- Historical Earthquakes / PDC Mapserver / ARCGIS / layer_id: Historical Earthquakes
  - https://org-disasteralert.pdc.org/msf/rest/services/global/pdc_global_historical_hazards/MapServer
- Historical Tsunami Events / PDC Mapserver / ARCGIS / layer_id: Historical Tsunami Events
  - https://org-disasteralert.pdc.org/msf/rest/services/global/pdc_global_historical_hazards/MapServer
- Historical Cyclone Tracks 2014-2021 / PDC Mapserver / ARCGIS / layer_id: Historical Cyclone Tracks - <year>
  https://org-disasteralert.pdc.org/msf/rest/services/global/pdc_global_historical_hazards/MapServer
- Historical Large Fires
- Historical Large Floods / PDC Mapserver / ARCGIS / layer_id: Flood Incidents (NASA)
  - https://org-disasteralert.pdc.org/msf/rest/services/global/pdc_global_historical_hazards/MapServer
- Historical Volcanic Eruptions
  - https://org-disasteralert.pdc.org/msf/rest/services/global/pdc_global_historical_hazards/MapServer
- Historical Landslide - NO MATCH
- Historical Avalanche - NO MATCH
- Historical Winterstore - NO MATCH
- Rainfall?

Unclear what they are requesting here. We have some Rainfall accumulation layers, and some animated forecast and potential layers. BUT there are also a bunch of the Rainfall layers are TAOS layers. Need to clarify what exactly they want and that TAOS is off the table.
