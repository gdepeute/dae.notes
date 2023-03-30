---
id: w8v5qudwwmj1x018wpy3qvu
title: API Proxy
desc: ""
updated: 1680200498108
created: 1679703138003
---

# Prototyping API gateway proxy via AWS API Gateway

- Adding Historical Hazards with existing query strings/parameters and new role
- Adding Layers with direct pass-thru with new role
- Need to experiment validating JWT role in API gateway

## Adding Historical Hazards

## Adding Layers with direct pass-thru

- Have prototyped 2 different types of layers (WMS and ARCGIS)
- It appears if layer url ends in "?", then a direct mapping can be implemented
- If the layer url does NOT end in "?", then assume that it could have multiple layers added, thus configure last stage as {proxy+}

## Layers and Protocols for initial implementation

In the initial list from Crisis24/Palantir, only ARCGIS and WMS map services requested

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
- Earthquakes Intensity Zones / PDC MapServer / ARCGIS / layer_id: Earthquake Intensity Zones
  - https://org-disasteralert.pdc.org/msf/rest/services/global/pdc_hazard_zones/MapServer
- Earthquakes Shaking Intensity / PDC Mapserver / ARCGIS / layer_id: Shaking Intensity (ShakeMap Model)
  - https://apps.pdc.org/msf/rest/services/global/pdc_models/MapServer
- Tornado (Warnings) / PDC AGS / ARCGIS / layer_id: US_Tornado_Warning
  - https://apps.pdc.org/msf/rest/services/global/pdc_active_hazards/MapServer
- Tornado (Watches) / PDC AGS / ARCGIS / layer_id: US_Tornado_Watch
  - https://apps.pdc.org/msf/rest/services/global/pdc_active_hazards/MapServer
- Tsunami (Watch and Warning Zones) / PDC AGS / ARCGIS / layer_id: Tsunami_Watch_and_Warning_Zones / auth: no
  - https://apps.pdc.org/msf/rest/services/global/pdc_models/MapServer
- Volcano Locations / PDC Mapserver / ARCGIS / layer_id: Volcano Locations
  - https://org-disasteralert.pdc.org/msf/rest/services/global/pdc_global_historical_hazards/MapServer
- Wildfire Locations (Hotspots) / PDC Mapserver / ARCGIS / layer_id: Wildfire Locations (Hotspots)
  - https://apps.pdc.org/msf/rest/services/global/pdc_active_hazards/MapServer
- Potential Large/Intense Wildfire / PDC AGS / ARCGIS / layer_id Potential Large/Intense Wildfires / auth: no
  - https://apps.pdc.org/msf/rest/services/global/pdc_active_hazards/MapServer
- Tectonic Plate Boundaries / PDC AGS / ARCGIS / layer_id: Tectonic Plate Boundaries
  - https://org-disasteralert.pdc.org/msf/rest/services/global/pdc_hazard_zones/MapServer
- Global Weather Observations (METAR) PDC AGS / ARCGIS / layer_id: Global Weather Observations (METAR)
  - https://apps.pdc.org/msf/rest/services/global/pdc_meteorology/MapServer
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

This yields this set of map services to be proxied - initial experiment using API gateway:

api.disasteraware.com/services/geowebcache_wms -> https://agsc.pdc.org/geowebcache/service/wms (S13)

- Land_Cove (L383), Railroads (L527), Shaded_Relief (L555), Topography_Bathymetry (L585), pop_desn_2015 (L817)
  api.disasteraware.com/services/global/pdc_active_hazards/MapServer -> https://apps.pdc.org/msf/rest/services/global/pdc_active_hazards/MapServer (S62/64)
- Storm_Positions (L574), Storm_Segments (L575), Storm_Winds (L576), US_Tornados_Warning (L611), US_Tornados_Watch (L612)
  api.disasteraware.com/services/global/pdc_global_infrastructure/MapServer -> https://apps.pdc.org/msf/rest/services/global/pdc_global_infrastructure/MapServer (S85)
  api.disasteraware.com/services/global/pdc_meteorology/MapServer -> https://apps.pdc.org/msf/rest/services/global/pdc_meteorology/MapServer (S128)
  api.disasteraware.com/services/global/pdc_models/MapServer -> https://apps.pdc.org/msf/rest/services/global/pdc_models/MapServer (S133)
  api.disasteraware.com/services/global/pdc_basemap/MapServer -> https://org-disasteralert.pdc.org/msf/rest/services/global/pdc_basemap/MapServer (S66)
  api.disasteraware.com/services/global/pdc_global_historical_hazards/MapServer -> https://org-disasteralert.pdc.org/msf/rest/services/global/pdc_global_historical_hazards/MapServer (S84)
  api.disasteraware.com/services/global/pdc_hazard_zones/MapServer -> https://org-disasteralert.pdc.org/msf/rest/services/global/pdc_hazard_zones/MapServer (S109)

## Full List of Service URLs from Enterprise as of 03/28/23

https://agsc.pdc.org/geowebcache/service/wms?
https://apps.pdc.org/dynamic_data_ha/gfs_data/gfs/
https://apps.pdc.org/msf-img/rest/services/global/pdc_global_aerosol_optical_thickness_dyn/ImageServer
https://apps.pdc.org/msf-img/rest/services/global/pdc_global_carbon_monoxide_concentration_dyn/ImageServer
https://apps.pdc.org/msf-img/rest/services/global/pdc_global_day_population_dyn/ImageServer
https://apps.pdc.org/msf-img/rest/services/global/pdc_global_daynight_dyn/ImageServer
https://apps.pdc.org/msf-img/rest/services/global/pdc_global_land_surface_temperature_anomaly_day_dyn/ImageServer
https://apps.pdc.org/msf-img/rest/services/global/pdc_global_nightlights_dyn/ImageServer
https://apps.pdc.org/msf-img/rest/services/global/pdc_global_sea_surface_temperature_dyn/ImageServer
https://apps.pdc.org/msf-img/rest/services/global/pdc_global_snow_cover_dyn/ImageServer
https://apps.pdc.org/msf-img/rest/services/global/pdc_global_tropical_cyclone_heat_potential_dyn/ImageServer
https://apps.pdc.org/msf-img/rest/services/global/pdc_global_waveheight_000_dyn/ImageServer
https://apps.pdc.org/msf-img/rest/services/global/pdc_global_waveheight_003_dyn/ImageServer
https://apps.pdc.org/msf-img/rest/services/global/pdc_global_waveheight_006_dyn/ImageServer
https://apps.pdc.org/msf-img/rest/services/global/pdc_global_waveheight_009_dyn/ImageServer
https://apps.pdc.org/msf-img/rest/services/global/pdc_global_waveheight_012_dyn/ImageServer
https://apps.pdc.org/msf-img/rest/services/global/pdc_global_waveheight_015_dyn/ImageServer
https://apps.pdc.org/msf-img/rest/services/global/pdc_global_waveheight_018_dyn/ImageServer
https://apps.pdc.org/msf-img/rest/services/global/pdc_global_waveheight_021_dyn/ImageServer
https://apps.pdc.org/msf-img/rest/services/global/pdc_global_waveheight_024_dyn/ImageServer
https://apps.pdc.org/msf-img/rest/services/global/pdc_global_waveheight_027_dyn/ImageServer
https://apps.pdc.org/msf-img/rest/services/global/pdc_global_waveheight_030_dyn/ImageServer
https://apps.pdc.org/msf-img/rest/services/global/pdc_global_waveheight_033_dyn/ImageServer
https://apps.pdc.org/msf-img/rest/services/global/pdc_global_waveheight_036_dyn/ImageServer
https://apps.pdc.org/msf-img/rest/services/global/pdc_global_waveheight_039_dyn/ImageServer
https://apps.pdc.org/msf-img/rest/services/global/pdc_global_waveheight_042_dyn/ImageServer
https://apps.pdc.org/msf-img/rest/services/global/pdc_global_waveheight_045_dyn/ImageServer
https://apps.pdc.org/msf-img/rest/services/global/pdc_global_waveheight_048_dyn/ImageServer
https://apps.pdc.org/msf/rest/services/global/pdc_active_hazards/MapServer
https://apps.pdc.org/msf/rest/services/global/pdc_cpc_tc_formation/MapServer
https://apps.pdc.org/msf/rest/services/global/pdc_geopioneer/MapServer
https://apps.pdc.org/msf/rest/services/global/pdc_global_demography/MapServer
https://apps.pdc.org/msf/rest/services/global/pdc_global_flooding/MapServer
https://apps.pdc.org/msf/rest/services/global/pdc_global_hazards/MapServer
https://apps.pdc.org/msf/rest/services/global/pdc_global_infrastructure/MapServer
https://apps.pdc.org/msf/rest/services/global/pdc_global_weather_outlook/MapServer
https://apps.pdc.org/msf/rest/services/global/pdc_meteorology/MapServer
https://apps.pdc.org/msf/rest/services/global/pdc_meteorology_dyn/MapServer
https://apps.pdc.org/msf/rest/services/global/pdc_meteorology_ocean/MapServer
https://apps.pdc.org/msf/rest/services/global/pdc_models/MapServer
https://apps.pdc.org/msf/rest/services/global/pdc_smart_alerts/MapServer
https://apps.pdc.org/msf/rest/services/global/pdc_tropical_cyclone_models/MapServer
https://apps.pdc.org/msf/rest/services/north_america/pdc_can_hazard/MapServer
https://apps.pdc.org/msf/rest/services/north_america/pdc_usa_rva/MapServer
https://apps.pdc.org/msf/rest/services/response/pdc_coronavirus_response_2020_alternate/MapServer
https://apps.pdc.org/msf/rest/services/response/pdc_haiti_eq_2021_response/MapServer
https://apps.pdc.org/msf/rest/services/response/pdc_tc_ida_response_2021/MapServer
https://apps.pdc.org/msf/rest/services/rva/PDC_Risk_Capacity_AGS/MapServer
https://apps.pdc.org/msf/rest/services/rva/PDC_Risk_Hazard_Exposure_AGS/MapServer
https://apps.pdc.org/msf/rest/services/rva/PDC_Risk_Vulnerability_AGS/MapServer
https://disasteraware.pdc.org/msf/rest/services/biosurveillance/pdc_biosurveillance/MapServer
https://disasteraware.pdc.org/msf/rest/services/emops/pdc_emops/MapServer
https://disasteraware.pdc.org/msf/rest/services/global/pdc_risk_platform/MapServer
https://disasteraware.pdc.org/msf/rest/services/response/pdc_cdc_coronavirus_2019/MapServer
https://geoserver.pdc.org/geoserver/gwc/service/wms?
https://geoservernn.pdc.org/geoserver/gwc/service/wms?
https://gis.fema.gov/arcgis/rest/services/Partner/FAA_Major_Airport_Delay_Status/FeatureServer/
https://imageryuploader.geoplatform.gov/arcgis/rest/services/ImageEvents/MapServer
https://mapservices.weather.noaa.gov/eventdriven/rest/services/WWA/watch_warn_adv/MapServer
https://mapservices.weather.noaa.gov/eventdriven/rest/services/water/ahps_riv_gauges/MapServer
https://mapservices.weather.noaa.gov/vector/rest/services/outlooks/SPC_wx_outlks/MapServer
https://nowcoast.noaa.gov/arcgis/rest/services/nowcoast/radar_meteo_imagery_nexrad_time/MapServer
https://nowcoast.noaa.gov/arcgis/rest/services/nowcoast/sat_meteo_emulated_imagery_lightningstrikedensity_goes_time/MapServer
https://nowcoast.noaa.gov/arcgis/rest/services/nowcoast/wwa_meteoceanhydro_shortduration_hazards_warnings_time/MapServer
https://org-disasteralert.pdc.org/msf/rest/services/global/pdc_basemap/MapServer
https://org-disasteralert.pdc.org/msf/rest/services/global/pdc_global_historical_hazards/MapServer
https://org-disasteralert.pdc.org/msf/rest/services/global/pdc_hazard_zones/MapServer
https://org-disasteralert.pdc.org/msf/rest/services/north_america/pdc_slosh_al_tx/MapServer
https://org-disasteralert.pdc.org/msf/rest/services/north_america/pdc_slosh_me_ga/MapServer
https://org-disasteralert.pdc.org/msf/rest/services/north_america/pdc_usa/MapServer
https://org-disasteralert.pdc.org/msf/rest/services/north_america/pdc_usa_infrastructure/MapServer
https://org-disasteralert.pdc.org/msf/rest/services/response/pdc_hurricane_harvey_response/MapServer
https://org-disasteralert.pdc.org/msf/rest/services/response/pdc_hurricane_laura_response_2020/MapServer
https://org-disasteralert.pdc.org/msf/rest/services/response/pdc_hurricane_sally_response2020/MapServer
https://org-disasteralert.pdc.org/msf/rest/services/response/pdc_response_2011_japan_tsunami/MapServer
https://org-disasteralert.pdc.org/msf/rest/services/response/pdc_tc_dorian_response_sep19/MapServer
https://org-disasteralert.pdc.org/msf/rest/services/response/pdc_tc_yutu_response_2018/MapServer
https://org-disasteralert.pdc.org/msf/rest/services/response/pdc_turkey_syria_eqM7_8_2023_response/MapServer
https://osm.gs.mil/tiles/default/
https://osm.gs.mil/tiles/humanitarian/
https://sentry.pdc.org/spoe_proxy/spoe/SPOEID011/public/NFHL/MapServer
https://sentry.pdc.org/spoe_proxy/spoe/SPOEID020/NSS/FEMA_NSS/MapServer
https://sentry.pdc.org/spoe_proxy/spoe/SPOEID031/nowcoast/forecast_meteoceanhydro_sfc_ndfd_qpf6hrs_offsets/MapServer/WMSServer?
https://sentry.pdc.org/spoe_proxy/spoe/SPOEID031/nowcoast/forecast_meteoceanhydro_sfc_ndfd_signwaveht_offsets/MapServer/WMSServer?
https://sentry.pdc.org/spoe_proxy/spoe/SPOEID031/nowcoast/forecast_meteoceanhydro_sfc_ndfd_time/MapServer/WMSServer?
https://sentry.pdc.org/spoe_proxy/spoe/SPOEID031/nowcoast/forecast_meteoceanhydro_sfc_ndfd_windspeed_offsets/MapServer/WMSServer?
https://sentry.pdc.org/spoe_proxy/spoe/SPOEID032/RNC/NOAA_RNC/MapServer
https://sentry.pdc.org/spoe_proxy/spoe/SPOEID035/wms/ncep_global/NCEP_Global_Atmospheric_Model_best.ncd?
https://sentry.pdc.org/spoe_proxy/spoe/SPOEID035/wms/scud_pac?
https://sentry.pdc.org/spoe_proxy/spoe/SPOEID054/haiti_earthquake_202108/EOS_RS_202108_DPM_Haiti_earthquake_v0_5_tif/ImageServer
https://server.arcgisonline.com/arcgis/rest/services/Canvas/World_Dark_Gray_Base/MapServer
https://server.arcgisonline.com/arcgis/rest/services/Canvas/World_Dark_Gray_Reference/MapServer
https://server.arcgisonline.com/arcgis/rest/services/Canvas/World_Light_Gray_Base/MapServer
https://server.arcgisonline.com/arcgis/rest/services/Canvas/World_Light_Gray_Reference/MapServer
https://server.arcgisonline.com/arcgis/rest/services/Ocean/World_Ocean_Base/MapServer
https://server.arcgisonline.com/arcgis/rest/services/World_Imagery/MapServer
https://server.arcgisonline.com/arcgis/rest/services/World_Street_Map/MapServer
https://services-enterprise.disasteraware.com/enterprise/spoe/SPOEID053/NRT/landslide_nowcast/ImageServer
https://services-enterprise.disasteraware.com/hp_srv/
https://services.arcgis.com/8ZpVMShClf8U8dae/arcgis/rest/services/TestingLocations_public2/FeatureServer
https://services.arcgis.com/BLN4oKB0N1YSgvY8/ArcGIS/rest/services/Power_Outages_(View)/FeatureServer
https://services.arcgis.com/XG15cJAlne2vxtgt/ArcGIS/rest/services/Waze_Traffic_Alerts_Public/FeatureServer
https://services.arcgis.com/XG15cJAlne2vxtgt/ArcGIS/rest/services/Waze_Traffic_Jams_Public/FeatureServer
https://services.arcgis.com/XG15cJAlne2vxtgt/arcgis/rest/services/POST_5KM_Event_Run/FeatureServer
https://services.arcgis.com/XG15cJAlne2vxtgt/arcgis/rest/services/POST_5KM_Laura_20200826_1522/FeatureServer
https://services.arcgis.com/cJ9YHowT8TU7DUyn/ArcGIS/rest/services/Air%20Now%20Current%20Monitor%20Data%20Public/FeatureServer
https://services3.arcgis.com/t6lYS2Pmd8iVx1fy/ArcGIS/rest/services/COVID_Airline_Information_V2/FeatureServer
https://services3.arcgis.com/t6lYS2Pmd8iVx1fy/ArcGIS/rest/services/COVID_Travel_Restrictions_V2/FeatureServer
https://services9.arcgis.com/MFFJOIIWq14qbgCA/ArcGIS/rest/services/Nippe_Water_Women_Sites/FeatureServer
https://services9.arcgis.com/RHVPKKiFTONKtxq3/arcgis/rest/services/NDFD_SnowFall_v1/FeatureServer
https://services9.arcgis.com/RHVPKKiFTONKtxq3/arcgis/rest/services/USA_Wildfires_v1/FeatureServer
https://unosatgis.cern.ch/rapidmapping/rest/services/EQ20230206SYR/Analysis/MapServer
https://unosatgis.cern.ch/rapidmapping/rest/services/EQ20230206SYR/Analysis_Copernicus/FeatureServer
https://unosatgis.cern.ch/undpv1/rest/services/EQ20210814HTI/DamageAssessment_EQ20210814HTI/MapServer
