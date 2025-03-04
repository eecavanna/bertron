# Map

## Overview

This web page displays all samples from all projects on a single map.

By default, the entire world map is visible.
You can click the `+`/`-` buttons on the map to zoom in/out. Samples are grouped into clusters, where the cluster color
indicates whether there is a small, medium, or large number of samples in that cluster, regardless of sample origin or
type.

The `index.html` file, itself, is about 8 KB in size. When a web browser loads the file and runs the JavaScript scripts
within it, the web browser will fetch an additional 1.5 MB of gzipped resources from GitHub (about 8.5 MB when unzipped).

## Technologies

This web page is built upon the following technologies:

- [Leaflet](https://leafletjs.com/) - to show the map
- [Leaflet.markercluster](https://github.com/Leaflet/Leaflet.markercluster) - to show map markers as clusters  
- [PapaParse](https://github.com/mholt/PapaParse) - to fetch and parse CSV files
- [Prettier](https://prettier.io) - to format our source code
- [Bootstrap 5](https://getbootstrap.com/) - to style the web page elements other than the map

> Note: I have not reviewed the licenses of those technologies. 

## Development

### Code format

We use Prettier to format the code in this directory. You can format it by running:

```shell
npx prettier index.html --write
```

### Project structure

I opted to keep the HTML, CSS, and JavaScript in a single file to facilitate rapid development. This was implemented as a PoC. If building upon this past a certain point, I'd recommend separating the HTML, CSS, and JavaScript into separate files, using a package manager to manage dependencies, etc. 