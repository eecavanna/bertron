# NMDC

This directory contains information about retrieving geographical location information about biosamples in the NMDC database.

## Contents

Here's a diagram depicting the relationships between the NMDC database and the files in this directory.

```mermaid
flowchart LR
    subgraph NMDC Infrastructure
        nmdc_db[("NMDC<br>Database")]
        nmdc_api["NMDC<br>API"]
        nmdc_db -.-> nmdc_api
        nmdc_api --> nmdc_db
    end
    
    notebook[["get_nmdc_biosample_geo_data.ipynb"]]
    notebook -- Biosample metadata<br>requests --> nmdc_api
    notebook -- Biosample metadata --> csv_file
    nmdc_api -. Biosample metadata .-> notebook
    csv_file[("lat_lons_by_biosample_id.csv")]
```

## References

- [Using Python to access the NMDC API](https://docs.microbiomedata.org/runtime/nb/api_access_via_python/)
- [NMDC Schema documentation page about the `Biosample` schema class](https://microbiomedata.github.io/nmdc-schema/Biosample/)
- [NMDC Schema documentation page about the `lat_lon` schema slot](https://microbiomedata.github.io/nmdc-schema/lat_lon/)
