---
id: o9f6vx2d6lop53ox7bbmryn
title: Plf
desc: ""
updated: 1673312219834
created: 1673311998165
---

# Pacific Labour Facility

## Map Service Creation

- PLF sends updates approx every month to us.
- Jesse does some work to make sure it's consistent from the last verison
- Went we update, we remove all prior features, and create all new features
- When new file received from Jesse, open in Excel (if .xlsx), save as CSV into GIS_data/CSV
- Run the following:

  - ```
    pipenv run ./gis_tool.py -a -r -d csv -f ../GIS_data/CSV/<filename> -l "Pacific Labour Facility 031921" --security public -dae

    ```
