---
id: tvv9uvy133xemeu0kzaq6k3
title: Crisis24
desc: ""
updated: 1689796411161
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

```#!/usr/bin/env python3
import requests
import json
import argparse

API_PATH = "https://api-sandbox.disasteraware.com"
API_USERNAME = "disasterawareingestion@crisis24.com"
API_PASSWORD = "<REPLACE_WITH_PASSWORD>"

WHERE = "((status = 'E')) AND (create_date >= to_date('2023-03-01 00:00:00', 'yyyy-mm-dd hh24:mi:ss') AND create_date <= to_date('2023-03-02 00:00:00', 'yyyy-mm-dd hh24:mi:ss'))"

hazards_paths = [API_PATH + "/hazards/active"]

historical_hazards_paths = [
    API_PATH + "/hazards_count?where=" + WHERE,
    API_PATH + "/historical_hazards?where=" + WHERE,
]

"""

Crisis24 Layers:

  - (WMS) API_PATH + /services/geowebcache_wms - layer_name: pop_dens_2015
  - (ARCGIS) API_PATH + /services/global/pdc_active_hazards/Mapserver - layer_id: 6 (Recent_Earthquakes)
  - (ARCGIS) API_PATH + /services/global/pdc_hazard_zones/MapServer - layer id: 5 (Tectonic Plate Boundaries), layer_id: 8 (Earthquake Intensity Zones)
  - (ARCGIS) API_PATH + /services/global/pdc_models/MapServer - layer_id: 6 (Shaking Intensity (ShakeMap Model))

"""

map_service_paths = [
    API_PATH
    + "/services/geowebcache_wms?service=wms&version=1.1.1&request=GetCapabilities",
    API_PATH
    + "/services/geowebcache_wms?service=wms&version=1.1.1&request=GetCapabilities&LAYERS=pop_dens_2015",
    API_PATH
    + "/services/geowebcache_wms?LAYERS=pop_dens_2015&format=image/png&version=1.1.1&service=WMS&TRANSPARENT=true&request=GetMap&bboxSR=102100&SRS=EPSG:102100&WIDTH=256&HEIGHT=256&BBOX=5009377.0857,15028128.50729,10018754.17139,20037509.91734&STYLES=",
    API_PATH + "/services/global/pdc_active_hazards/MapServer?f=json",
    API_PATH + "/services/global/pdc_active_hazards/MapServer/6?f=json",
    API_PATH
    + "/services/global/pdc_active_hazards/MapServer/6/query?f=json&geometryType=esriGeometryEnvelope&outSR=4326&returnGeometry=true&geometry=%7B%22xmin%22%3A15028131.25709%2C%22ymin%22%3A-20048966.10401%2C%22xmax%22%3A20037508.34279%2C%22ymax%22%3A-5621521.48619%2C%22spatialReference%22%3A%7B%22wkid%22%3A3857%7D%7D&outFields=*",
    API_PATH + "/services/global/pdc_hazard_zones/MapServer?f=json",
    API_PATH + "/services/global/pdc_hazard_zones/MapServer/5?f=json",
    API_PATH
    + '/services/global/pdc_hazard_zones/MapServer/5/query?f=json&geometryType=esriGeometryEnvelope&outSR=4326&returnGeometry=true&geometry={"xmin":-10018754.17139,"ymin":5621521.48619,"xmax":-5009377.0857,"ymax":20048966.10401,"spatialReference":{"wkid":3857}}&outFields=*',
    API_PATH
    + '/services/global/pdc_hazard_zones/MapServer/5/query?f=json&geometryType=esriGeometryEnvelope&outSR=4326&returnGeometry=true&geometry={"xmin":-10018754.17139,"ymin":-5621521.48619,"xmax":-5009377.0857,"ymax":0,"spatialReference":{"wkid":3857}}&outFields=*',
    API_PATH + "/services/global/pdc_hazard_zones/MapServer/8?f=json",
    API_PATH
    + "/services/global/pdc_hazard_zones/MapServer/export?format=png32&bboxSR=3857&SRS=EPSG:3857&version=10.04&BBOX=-16280475.52852,3757032.52065,-15028131.25709,5009377.37034&layers=show:8&size=256,256&transparent=true&f=image&dpi=96&imageSR=3857",
    API_PATH + "/services/global/pdc_models/MapServer?f=json",
    API_PATH + "/services/global/pdc_models/MapServer/6?f=json",
    API_PATH
    + "/services/global/pdc_models/MapServer/export?format=png32&bboxSR=3857&SRS=EPSG:3857&version=10.04&BBOX=-13775786.98567,3757032.52065,-12523442.71424,5009377.37034&layers=show:6&size=256,256&transparent=true&f=image&dpi=96&imageSR=3857",
]

crisis24_paths = hazards_paths + historical_hazards_paths + map_service_paths


def add_arguments(parser):
    parser.add_argument(
        "-r",
        dest="show_response",
        action="store_true",
        help="Show responses",
    )


def main():
    parser = argparse.ArgumentParser()
    add_arguments(parser)
    args = parser.parse_args()

    # Get token
    response = requests.post(
        API_PATH + "/authorize",
        json={"username": API_USERNAME, "password": API_PASSWORD},
    )
    if response.status_code == 200:
        token = json.loads(response.text)["accessToken"]
        print("Success - API Token:", token)

    for path in crisis24_paths:
        print("Executing:", path)
        response = requests.get(path, headers={"Authorization": "Bearer " + token})
        if response.status_code == 200:
            if response.text[0] == "{" or response.text[0] == "[":
                print(
                    "Success - JSON",
                    json.dumps(response.json(), indent=4) if args.show_response else "",
                )
            elif "<?xml" in response.text:
                print("Success - XML", response.text if args.show_response else "")
            elif "PNG" in response.text[1:4]:
                print("Success - PNG")
            else:
                print("Success - UNKNOWN", response.text if args.show_response else ""),
        else:
            print("Error", response.status_code, response.text)

        cont = input("Next?")
        print("")


if __name__ == "__main__":
    main()
```
