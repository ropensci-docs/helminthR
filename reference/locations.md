# Table of geographic location names, and associated coordinates

Lists geographic locations and the corresponding latitude and longitude
coordinates of the country's centroid. The georeferencing was performed
dynamically using the Google Maps API, but they have since restricted
access. The data on locations is now provided in this data file called
`locations` – `data(locations)` – and is based on an earlier usage of
`ggmap`. The geographic coordinates may not be accurate, and users
should check for accuracy (and feel free to file an issue or PR on
Github with corrections).

## Usage

``` r
data(locations)
```

## Format

- Location:

  Name of geographic location

- Latitude:

  Latitude of location centroid

- Longitude:

  Longitude of location centroid

## References

Gibson, D. I., Bray, R. A., & Harris, E. A. (Compilers) (2005).
Host-Parasite Database of the Natural History Museum, London.
