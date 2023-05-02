---
id: tvv9uvy133xemeu0kzaq6k3
title: Crisis24
desc: ""
updated: 1683055708785
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
  - https://api-sandbox.disasteraware.com/services/global/pdc_models/MapServer (layers=6)
- Tectonic Plate Boundaries (ARCGIS)
  - https://api-sandbox.disasteraware.com/services/global/pdc_hazard_zones/MapServer (layers=9)

The credential created for Crisis24 for this POC effort has been given access to only the resources listed above. Any request outside of that list will return in error.

## Accessing WMS Map Servers

Please refer to [WMS Reference](https://docs.geoserver.org/stable/en/user/services/wms/reference.html#operations) for details on how to query WMS map servcies.

## Accessing ARCGIS Map Servers

Please refer to [ARCGIS Map Service](https://developers.arcgis.com/rest/services-reference/enterprise/map-service.htm) for details on how to query ARCGIS map services.
