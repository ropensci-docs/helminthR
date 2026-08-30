# Clean helminth parasite occurrence data

Given the data or a subset of the helminth interaction data (see
\`loadData()\`), perform various cleaning functions on the data,
including validation of species names, run taxize on hosts (again, as
there are already host and parasite taxonomic variables as part of this
data.frame , and remove records only to genus level.

## Usage

``` r
cleanData(data, speciesOnly = FALSE, validateHosts = FALSE)
```

## Arguments

- data:

  helminth interaction data

- speciesOnly:

  boolean flag to remove host and parasite species where data are only
  available at genus level (default = FALSE)

- validateHosts:

  boolean flag to check host species names against Catalogue of Life
  information and output taxonomic information (default = FALSE)

## Value

data.frame with cleaned data

## Details

Use `data(locations)` for a list of possible locations.

## Author

Tad Dallas
