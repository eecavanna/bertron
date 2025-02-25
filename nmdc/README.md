# NMDC

This directory contains information about retrieving the geographical origin coordinates of biosamples in the NMDC database.

```mermaid
flowchart LR
    get_nmdc_biosample_geo_data.ipynb -- Dumps biosample metadata to --> lat_lons_by_biosample_id.csv
    get_nmdc_biosample_geo_data.ipynb -- Fetches biosample metadata from --> NMDC_API["NMDC API"]
    NMDC_API["NMDC API"] -.- NMDC_DB["NMDC Database"]
```

## References

- [Using Python to access the NMDC API](https://docs.microbiomedata.org/runtime/nb/api_access_via_python/)
- [NMDC Schema documentation page about the `Biosample` schema class](https://microbiomedata.github.io/nmdc-schema/Biosample/)
- [NMDC Schema documentation page about the `lat_lon` schema slot](https://microbiomedata.github.io/nmdc-schema/lat_lon/)
