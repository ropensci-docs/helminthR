# Introduction to the helminthR package

This is an introduction to the `helminthR` package, whicih allows for
the programmatic access to the London Natural History Museum’s helminth
parasite database ([available
here](https://www.nhm.ac.uk/research-curation/scientific-resources/taxonomy-systematics/host-parasites/index.html)).
This database represents the largest known database of host-helminth
interactions, containing host-helminth occurrence records for over 350
locations, including aquatic, marine, and terrestrial locations.

See software note in *Ecography* ([available
here](https://onlinelibrary.wiley.com/doi/10.1111/ecog.02131))

### Installation

From GitHub

``` r


# install.packages("devtools")
devtools::install_github("rOpenSci/helminthR")
library("helminthR")
```

From CRAN

``` r


install.packages("helminthR")
```

## Package functionality

The package allows for the acquisition of host-helminth interaction
records based on host name (genus or species), parasite name (genus,
species, or group), and/or location (accepted region name as provided in
`data(locations)`. Parasite groups include “Acanthocephalans”,
“Cestodes”, “Monogeans”, “Nematodes”, “Trematodes”, or “Turbs” (short
for Turbellarians). The user can further define host species as occuring

1.  “In the wild”
2.  “Zoo captivity”
3.  “Domesticated”
4.  “Experimental”
5.  “Commercial source”
6.  “Accidental infestation”

by inputting the corresponding number above in the `hostState` argument.

The package itself has two base functions; `loadData` and `cleanData`

### `loadData()`

This function loads the data. The data were previously served by the
London Natural History Museum, so this package programmatically accessed
them via API queries. The data have been archived, and this package
ships with a zipped copy of the current release of the data.

``` r

data <- loadData()
```

### `cleanData()`

There are numerous records that the end user may want to remove before
analyzing the data. For instance, `(Deer)` is a valid host species
listed, as is `(duck)`. We can clean the data to remove these records
and others not identified to species-level, as well as use `taxize` to
access taxonomic data on hosts using the
[`cleanData()`](https://docs.ropensci.org/helminthR/reference/cleanData.md)
function.

``` r

data2 <- cleanData(data)
```

### `data(locations)`

A data file containing all the location names that can be queried, along
with putative latitude and longitude coordinates for the centroid of
each location can be found in `data(locations)`. Note that this will
replace any object in the global environment named `locations`. These
names can be used to subset the existing data product (see
[`loadData()`](https://docs.ropensci.org/helminthR/reference/loadData.md)).
Below, I look at host-parasite associations recorded in France.

``` r


france <- data[which(data$country == 'France'), ]
dim(france)
head(france)
```

### plotting host-helminth networks

Below, I provide an example of code for plotting the bipartite network
of host-helminth interactions found in the state of Montana.

``` r


g <- igraph::graph_from_biadjacency_matrix(table(
  france$hostScientificName, 
  france$parasiteScientificName)
)
igraph::V(g)$name <- NA
igraph::E(g)$color <- 'black'

plot(g, 
    vertex.color=c("black","dodgerblue")[igraph::V(g)$type+1],
    vertex.size=5
)
```
