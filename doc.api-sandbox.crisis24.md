---
id: tvv9uvy133xemeu0kzaq6k3
title: Crisis24
desc: ""
updated: 1689795866022
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
    - point
- Earthquake Intensity Zones (ARCGIS)
  - https://api-sandbox.disasteraware.com/services/gloabl/pdc_hazard_zones/MapServer (layers=8)
    - polygon
- Tectonic Plate Boundaries (ARCGIS)
  - https://api-sandbox.disasteraware.com/services/global/pdc_hazard_zones/MapServer (layers=5)
    - polyline
- Earthquake Shaking Intensity - ShakeMap Model (ARCGIS)
  - https://api-sandbox.disasteraware.com/services/global/pdc_models/MapServer (layers=6)
    - polygon

The credential created for Crisis24 (disasterawareingestion@crisis24.com) for this POC effort has been given access to only the resources listed above. Any request outside of that list will return an error.

## Basic API Usage

The basic API documentation resides at https://api-docs.disasteraware.com. For the Crisis24 POC, any time you see a reference to https://api.disasteraware.com, replace with https://api-sandbox.disasteraware.com.

As shown in the documentaiton, a authorization token MUST be submitted with every request to the API with the exception of the /authorize endpoint. The authorization tokens expire after 15 minutes, therefore make sure you are sending a valid token with your requests. If you need a new authorization token, please hit the /authorize endpoint again.

## Accessing Historical Hazards

The endpoint for fetching historical hazards: - https://api-sandbox.disasteraware.com/historical_hazards

You MUST supply a search term to this endpoint in order to limit the matches to be returned. There is a limit of 1000 matches which can be returned. This endpoint does NOT support paging.

In order to determine whether your request would return fewer than 1000 matches, it is recommended you use https://api-sandbox.disasteraware.com/hazards_count with the same exact search string, and if it's a valid search, it will return the number of matches in the response.

The search term models a SQL query. The fields which can be used in a query:

- status = 'E'
  - Search for expired hazards
- type_id
  - Hazard type: AVALANCE, TORNADO, WILDFIRE, ...
    - Example: type_id = 'AVALANCHE' OR type_id = 'WILDFIRE'
- category_id
  - Hazard category: EVENT, EXERCISE, OTHER, RESPONSE
- severity_id
  - Hazard severity: WARNING, WATCH, ADVISORY, INFORMATION
- hazard_name
  - Hazard Name
    - Example: UPPER(hazard_name) LIKE '%HAWAII%'
- comment_text
  - Any comment text associated with hazard
- create_date
  - Hazard creation date, typically used to check between range of dates:
    - Example: create_date >= to_date('2023-05-01 00:00:00', 'yyyy-mm-dd hh24:mi:ss') AND create_date <= to_date('2023-05-31 00:00:00', 'yyyy-mm-dd hh24:mi:ss')

Multi-field example. Searchs for expired WILDFIRE hazard of type EVENT, severity WARNING, created between 5/1/23 and 5/31/23 with "namefoo" (case insensitive) in the hazard_name and "commentfoo" (case insensitive) in the comment_text

```
https://api-sandbox.disasteraware.com/hazards_count?where=((category_id = 'EVENT')) AND (UPPER(comment_text) LIKE '%COMMENTFOO%') AND (create_date >= to_date('2023-05-01 00:00:00', 'yyyy-mm-dd hh24:mi:ss') AND create_date <= to_date('2023-05-31 00:00:00', 'yyyy-mm-dd hh24:mi:ss')) AND (UPPER(hazard_name) LIKE '%NAMEFOO%') AND ((severity_id = 'WARNING')) AND ((status = 'E')) AND ((type_id = 'WILDFIRE'))
```

## Accessing WMS Map Servers

Please refer to [WMS Reference](https://docs.geoserver.org/stable/en/user/services/wms/reference.html#operations) for details on how to query WMS map servcies.

## Accessing ARCGIS Map Servers

Please refer to [ARCGIS Map Service](https://developers.arcgis.com/rest/services-reference/enterprise/map-service.htm) for details on how to query ARCGIS map services.

## Crisis24 Test Tool

We've included a simple python3 test tool for all the resources Crisis24 is licensed to receive. This includes an example of all licensed resources, and can be used to verify your credentials.

Add the username/password for your `disasterawareingestion@crisis24.com` API account. That is the account we've applied the additional roles to control access to the resources above.
