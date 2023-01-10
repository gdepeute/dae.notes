---
id: pg3mz2bh425s1dv49hwq9wj
title: Shell
desc: ""
updated: 1673313342743
created: 1673312630295
---

# Shell Oil

- Key Folks

  - Andrea McAlister - Senior IT Process Analyst
  - Karmeneita - PM?
  - Leigh Frazer
    - Wade Vrtis - was going to help with SFTP of SAID asset data to us on regular basis (weekly)
  - Mark Honkaanen - Moogsoft Dude

- Proposed
  - Automation of asset map service updates
    - Shell would push via SFTP asset updated from SAID database to us regularly
    - Open on their side in terms of getting all the assets in one place, they aren't organized very well
    - Originally we were told assets were in ServiceNow, they were going to push them into their SAID database
    - More recently Andrea said data quality and ownership are an issue
    - We would write a quick tool (leverage gis_tool) to watch the SFTP, pull the data in and update the map service
  - Pushing of Entry/Exit events to Moogsoft
    - Using their asset map service, leverage the asset tracking system to determine entry/exit events
    - Push individual entry/exit events to Shell via a webhook which will then ingest data into Moogsoft
    - Open questions regarding "Configuration Items" and "Assignment Groups" of the assets
      - Note: assets go down to individual servers, routers, ...
- Calls
  - 8/11/22 - Large Shell workshop - 2 hours
    - Three WAN tiers
      - Tier 1 - 500km
      - Tier 2 - 225km
      - Tier 3 - 50km
    - Cyclone most used hazard
    - Need to define alert levels which might change for different groups at Shell
  - 10/5/22
    - Wade and Mark were on call
    - Able to discuss implementation details a bit
    - All actions on their side
  - 1/5/23
    - Dud meeting, neither Wade or Mark showed up
    - Andrea suggested they were "busy" and everything going to push
