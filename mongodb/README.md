# Geospatial Data Tools for MongoDB

This repository contains two Python utilities for working with geospatial data in MongoDB:

1. `geo_importer.py` - Imports geospatial data from various sources into MongoDB
2. `geo_query.py` - Queries and visualizes geospatial data from MongoDB

## Prerequisites

- Python 3.6+
- MongoDB (running locally or accessible remotely)
- Required Python packages:
  ```
  pip install pymongo pandas folium
  ```
  
For processing large files, additional memory may be required.

## geo_importer.py

This tool imports geospatial data from multiple sources into a MongoDB database using a standardized schema.

### Supported Data Sources

- **EMSL** - Project location data (`latlon_project_ids.json`)
- **ESSDIVE** - ESS-DIVE package data (`ess_dive_packages.csv`)
- **NMDC** - NMDC biosample data (`nmdc_biosample_geo_coordinates.csv`)
- **JGI-Biosamples** - JGI GOLD biosample data (`jgi_gold_biosample_geo.csv`)
- **JGI-Organism** - JGI GOLD organism data (`jgi_gold_organism_geo.csv`)

### Data Schema

All data sources are imported into a consistent schema:

```json
{
  "dataset_id": "original_id_from_source",
  "system_name": "SYSTEM_NAME",  // One of: EMSL, ESSDIVE, NMDC, JGI-Biosamples, JGI-Organism
  "coordinates": {
    "type": "Point",
    "coordinates": [longitude, latitude]  // GeoJSON format
  },
  "metadata": {
    // Source-specific metadata (preserved from original data)
  }
}
```

### Usage

```bash
# Basic usage
python geo_importer.py --data-dir /path/to/data/directory

# Clear the collection before importing
python geo_importer.py --data-dir /path/to/data --clear-collection

# Skip large JGI GOLD files (useful for testing)
python geo_importer.py --data-dir /path/to/data --skip-large-files

# Specify a different MongoDB connection
python geo_importer.py --data-dir /path/to/data --mongodb-uri mongodb://username:password@hostname:port/database
```

## geo_query.py

This tool provides query and visualization capabilities for geospatial data stored in MongoDB.

### Features

- Get database statistics
- Query by system name or dataset ID
- Perform geospatial queries (bounding box, proximity)
- Generate interactive maps with Folium
- Export results to CSV or JSON
- Create summary reports

### Usage Examples

**Get database statistics:**
```bash
python geo_query.py --action stats
```

**Query by system name:**
```bash
python geo_query.py --action system --system-name ESSDIVE --format map --output essdive_locations
```

**Find points within a geographic region:**
```bash
python geo_query.py --action box --west -140 --east -60 --north 60 --south 20 --format map
```

**Find points near a location:**
```bash
python geo_query.py --action nearby --lat 37.8764 --lng -122.2608 --distance 50000
```

**Create separate maps for each system type:**
```bash
python geo_query.py --action all --format csv --output system_maps
```

### Output Formats

- **JSON** - Raw data in JSON format (default)
- **CSV** - Tabular data in CSV format
- **Map** - Interactive HTML map using Folium

## Common Query Examples

1. **Find all EMSL points in Alaska:**
   ```bash
   python geo_query.py --action box --west -180 --east -130 --north 72 --south 55 --system-name EMSL --format map --output alaska_emsl
   ```

2. **Export all JGI-Biosamples data to CSV:**
   ```bash
   python geo_query.py --action system --system-name JGI-Biosamples --format csv --output jgi_biosamples_data
   ```

3. **Find NMDC samples within 100km of Los Alamos:**
   ```bash
   python geo_query.py --action nearby --lat 35.8800 --lng -106.3031 --distance 100000 --system-name NMDC --format map --output los_alamos_nmdc
   ```

4. **Generate individual maps for each system type:**
   ```bash
   python geo_query.py --action all --output system_maps
   ```

## Limitations and Considerations

- Very large geospatial datasets can be memory-intensive
- The `--limit` parameter (default: 1000) can be used to restrict result sizes
- For very large JGI datasets, the `--skip-large-files` option can be used during testing
- MongoDB geospatial indexes are created automatically during import

## License

[Add your license information here]

## Contact

[Add your contact information here]