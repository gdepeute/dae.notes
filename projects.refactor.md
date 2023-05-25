---
id: kv4e0wfu43ayzjt9k08qb7a
title: Refactor
desc: ""
updated: 1685051323449
created: 1685050966915
---

# Refactoring Asset Tracking and other tools

- Goal, replace EVERYTHING on atpoc with refactored code
- Once refactoring complete, move repos into DisasterAWARE repos
- Current status

  - [x] Main refactoring of DAE_AT_utils (combines DAE_bag_of_tricks, ATN_bag_of_tricks)
  - [x] Main refacoring of GIS_utils (from GIS_bag_of_tricks)
  - [x] Main refactoring of GIS_cli (broke down gis_tool.py into several subcomponents)
  - [x] Main refactoring of GEN_utils (generic pieces)
  - [x] Creation of DAE_AT (renamed and changed from DAE_AT_tools)
  - [x] Refactoring of AT_config (now in DAE_AT, was AT_poc previously)

- Individual components
  - DAE_AT
    - [x] dae_hazards.py refactored
    - [x]
