---
id: tvv9uvy133xemeu0kzaq6k3
title: Crisis24
desc: ""
updated: 1683058951796
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

## Basic API Usage

The basic API documentation resides at https://api-docs.disasteraware.com. For the Crisis24 POC, any time you see a reference to https://api.disasteraware.com, replace with https://api-sandbox.disasteraware.com.

As shown in the documentaiton, a authorization token MUST be submitted with every request to the API with the exception of the /authorize endpoint. The authorization tokens expire after 15 minutes, therefore make sure you are sending a valid token with your requests. If you need a new authorization token, please hit the /authorize endpoint again.

## Accessing Historical Hazards

The endpoint for fetching historical hazards: - https://api-sandbox.disasteraware.com/historical_hazards

You MUST supply search terms to this endpoint in order to limit the responses to be returned. There is a limit of 1000 matches which will be returned. This endpoint does NOT support paging.

In order to determine whether your request would return fewer than 1000 matches, it is recommended you use https://api-sandbox.disasteraware.com/hazards_count with the same exact search string, and if it's a valid search, it will return the number of matches in the response.

The search term loosely models a SQL-like query. The fields which can be used in a query:

- status = 'E'
  - Search for expired hazards
-

```
https://services-enterprise.disasteraware.com/hp_srv/services/hazards/t/json/get_hazards_count?app_ids=1342,18&where=((category_id = 'EVENT' OR category_id = 'OTHER')) AND (UPPER(comment_text) LIKE '%COMMENTFOO%') AND
```

## Accessing WMS Map Servers

Please refer to [WMS Reference](https://docs.geoserver.org/stable/en/user/services/wms/reference.html#operations) for details on how to query WMS map servcies.

## Accessing ARCGIS Map Servers

Please refer to [ARCGIS Map Service](https://developers.arcgis.com/rest/services-reference/enterprise/map-service.htm) for details on how to query ARCGIS map services.
