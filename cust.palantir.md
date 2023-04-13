---
id: mfx9mmod8isg5dwnltt0oom
title: Palantir
desc: ""
updated: 1681405838707
created: 1675461426469
---

# Engagement with Palantir/Crisis24

- Wants to do a deeper dive
- They work with Crisis24
- Will demo their application
- Use cases unclear?

# Call with Chad on 4/13/23

- Showing a demo / presentation deck
- Chad was in the CIA for a couple decades
- "Dynamic Risk Library" - SW tool to enable clients to increase revenue (decrease losses), to yield strategic insights
- Sold as annual subscription license per user
- Custom Analytic Products (current and historic)
- Emerging Risk Products (future focused)
- Going to include Bloomberg Data
- And CIA Playbook
- Meritime Shipping Data

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

## Meeting with Crisis/Palantir - 4/7/23

- Chad Lesch
- Mike Gilbert / Topo1 platform engineer
- Thomas Lee / CTO of Topo1 by Crisis24 Platform
- Steve D'Adamo / Crisis24 - Horizon
- Cathy Gill / Crisis24 - Horizon

- Vik Trivikram
- Ismail Seyfi / IT

- Topo1
  - CEM space
  - Understand assets an organization has and threats
  - Natural disasters/weather events/...
  - Got interested based on Chad's poking
  - Mike Gilbert - question around the data sources
    - Asking how we sell data and in what different bundles

## Meeting with Crisis24/Palantir

- Chad Lesch - Crisis24
- Zach Romanow - Palantir
- Trivikram "Vik" Pathak

- Meandering discussion
- Zach has had access to PDC data via Ray for over 6 months now (from PDC tier)
- Very interested in historical data
  - Custom reports
  - Some layer Data
  - Population density/exposure/hazard brief data
- Interested in "Predictive Model" and "Estimated Import"
- Curious about coverage in other paths of the world
  - Mention Iran and Syria as two examples
- Recommended they get SaaS trial, and then get demo from Johnny to allow them to best review the available data

- Chad handed over to Matt Bradley (used to be at OnSolve)
