
# mregions2

<!-- badges: start -->

[![Funding](https://img.shields.io/static/v1?label=powered+by&message=lifewatch.be&labelColor=1a4e8a&color=f15922)](https://lifewatch.be)
[![Status at rOpenSci Software Peer
Review](https://badges.ropensci.org/590_status.svg)](https://github.com/ropensci/software-review/issues/590)
[![R-CMD-check](https://github.com/lifewatch/mregions2/actions/workflows/R-CMD-check.yaml/badge.svg)](https://github.com/lifewatch/mregions2/actions/workflows/R-CMD-check.yaml)
[![pkgcheck](https://github.com/lifewatch/mregions2/workflows/pkgcheck/badge.svg)](https://github.com/lifewatch/mregions2/actions?query=workflow%3Apkgcheck)
[![Codecov test
coverage](https://codecov.io/gh/lifewatch/mregions2/branch/main/graph/badge.svg)](https://app.codecov.io/gh/lifewatch/mregions2?branch=main)
<!-- badges: end -->

mregions2 allows to access the [Marine Regions
Gazetteer](https://marineregions.org/gazetteer.php) and the [Marine
Regions Data Products](https://marineregions.org/sources.php) in R.

You can find detailed information in the articles online:

- [Introduction to
  mregions2](https://lifewatch.github.io/mregions2/articles/mregions2.html)
- [Why mregions and
  mregions2?](https://lifewatch.github.io/mregions2/articles/why_mregions2.html)
- [mregions2 as
  RDF](https://lifewatch.github.io/mregions2/articles/mregions2-rdf.html)

![](https://user-images.githubusercontent.com/54405067/156809171-1487bb9f-35af-4418-8e2f-93c24a59aad0.gif)

<sup>(Source: <https://www.vliz.be/en/news?p=show&id=8160>)</sup>

## Installation

You can install the development version of mregions2 from GitHub with:

``` r
# install.packages("devtools")
devtools::install_github("lifewatch/mregions2")
```

Load the library with

``` r
library(mregions2)
```

## Query the Marine Regions Gazetteer

The [Marine Regions Gazetteer](https://marineregions.org/gazetteer.php)
is a standard list of marine georeferenced place names.

> Gazetteer: a dictionary of geographical names.

<sup><https://www.thefreedictionary.com/gazetteer></sup>

You can search the Gazetteer in many ways:

Search by free text:

``` r
gaz_search("Belgian")
#> # A tibble: 9 × 14
#>   MRGID gazetteerSource       placeType preferredGazett… preferredGazett… status
#>   <int> <chr>                 <chr>     <chr>            <chr>            <chr> 
#> 1    14 "(2001). The Times c… Nation    Belgien          German           stand…
#> 2  2550 "ASFA thesaurus"      Coast     Belgian Coast    English          stand…
#> 3  2554 "ASFA thesaurus"      Coast     Belgian West Co… English          stand…
#> 4  3293 "Flanders Marine Ins… EEZ       Belgian Contine… English          stand…
#> 5  3293 "Flanders Marine Ins… EEZ       Belgian Exclusi… English          stand…
#> 6 24493 "Belgian Sea Fisheri… Historic… (Historical) fi… English          stand…
#> 7 26567 "VLIZ (2020). Inters… Marine R… Belgian part of… English          synon…
#> 8 49010 "Flanders Marine Ins… Territor… Belgian 12 NM    English          stand…
#> 9 49243 "Flanders Marine Ins… Contiguo… Belgian 24 NM    English          stand…
#> # … with 8 more variables: accepted <int>, latitude <dbl>, longitude <dbl>,
#> #   minLatitude <dbl>, minLongitude <dbl>, maxLatitude <dbl>,
#> #   maxLongitude <dbl>, precision <dbl>
```

Search by unique identifier. See `?MRGID`:

``` r
gaz_search(3293)
#> # A tibble: 1 × 14
#>   MRGID gazetteerSource    placeType latitude longitude minLatitude minLongitude
#>   <int> <chr>              <chr>        <dbl>     <dbl>       <dbl>        <dbl>
#> 1  3293 Flanders Marine I… EEZ           51.5      2.71        51.1         2.24
#> # … with 7 more variables: maxLatitude <dbl>, maxLongitude <dbl>,
#> #   precision <dbl>, preferredGazetteerName <chr>,
#> #   preferredGazetteerNameLang <chr>, status <chr>, accepted <int>
```

Search by location:

``` r
gaz_search(x = 2.927, y = 51.21551)
#> # A tibble: 50 × 14
#>    MRGID gazetteerSource          placeType minLatitude minLongitude maxLatitude
#>    <int> <chr>                    <chr>           <dbl>        <dbl>       <dbl>
#>  1    14 (2001). The Times compr… Nation           49.5         2.55        51.5
#>  2    14 (2001). The Times compr… Nation           49.5         2.55        51.5
#>  3    14 (2001). The Times compr… Nation           49.5         2.55        51.5
#>  4    14 (2001). The Times compr… Nation           49.5         2.55        51.5
#>  5    14 (2001). The Times compr… Nation           49.5         2.55        51.5
#>  6    14 (2001). The Times compr… Nation           49.5         2.55        51.5
#>  7    20 SAIL                     Province…        50.7         2.55        51.4
#>  8    20 SAIL                     Province…        50.7         2.55        51.4
#>  9    20 SAIL                     Province…        50.7         2.55        51.4
#> 10    20 SAIL                     Province…        50.7         2.55        51.4
#> # … with 40 more rows, and 8 more variables: maxLongitude <dbl>,
#> #   preferredGazetteerName <chr>, preferredGazetteerNameLang <chr>,
#> #   status <chr>, accepted <int>, latitude <dbl>, longitude <dbl>,
#> #   precision <dbl>
```

Search by place type:

``` r
gaz_search_by_type("EEZ")
#> # A tibble: 254 × 14
#>    MRGID gazetteerSource   placeType latitude longitude minLatitude minLongitude
#>    <int> <chr>             <chr>        <dbl>     <dbl>       <dbl>        <dbl>
#>  1  3293 Flanders Marine … EEZ           51.5      2.71        51.1         2.24
#>  2  5668 Flanders Marine … EEZ           53.6      4.19        51.0         2.54
#>  3  5669 Flanders Marine … EEZ           54.6      8.39        52.9         3.35
#>  4  5670 Flanders Marine … EEZ           40.9     19.1         39.6        18.3 
#>  5  5672 Flanders Marine … EEZ           42.9     29.2         42.0        27.4 
#>  6  5673 Flanders Marine … EEZ           43.4     15.7         41.6        13.0 
#>  7  5674 Flanders Marine … EEZ           56.1      9.25        54.4         3.25
#>  8  5675 Flanders Marine … EEZ           58.8     23.0         57.6        20.4 
#>  9  5676 Flanders Marine … EEZ           61.8     21.9         58.8        19.1 
#> 10  5677 Flanders Marine … EEZ           46.0     -1.97        41.2        -9.88
#> # … with 244 more rows, and 7 more variables: maxLatitude <dbl>,
#> #   maxLongitude <dbl>, precision <dbl>, preferredGazetteerName <chr>,
#> #   preferredGazetteerNameLang <chr>, status <chr>, accepted <int>
```

Search by authortative source:

``` r
gaz_search_by_source("Flanders Marine Institute (VLIZ)")
#> # A tibble: 23 × 13
#>    MRGID gazetteerSource           placeType latitude longitude preferredGazett…
#>    <int> <chr>                     <chr>        <dbl>     <dbl> <chr>           
#>  1 62642 Seys, J.; Pint, S.; Verv… Sampling…     51.3      3.16 SW-Blankenberge…
#>  2 62643 Seys, J.; Pint, S.; Verv… Sampling…     51.2      2.96 SW-Bredene-01   
#>  3 62644 Seys, J.; Pint, S.; Verv… Sampling…     51.3      3.26 SW-Duinbergen-01
#>  4 62645 Seys, J.; Pint, S.; Verv… Sampling…     51.3      3.00 SW-De Haan-Voss…
#>  5 62646 Seys, J.; Pint, S.; Verv… Sampling…     51.3      3.24 SW-Heist-01     
#>  6 62647 Seys, J.; Pint, S.; Verv… Sampling…     51.1      2.62 SW-Koksijde-01  
#>  7 62648 Seys, J.; Pint, S.; Verv… Sampling…     51.2      2.81 SW-Middelkerke-…
#>  8 62649 Seys, J.; Pint, S.; Verv… Sampling…     51.2      2.71 SW-Nieuwpoort-01
#>  9 62650 Seys, J.; Pint, S.; Verv… Sampling…     51.1      2.69 SW-Oostduinkerk…
#> 10 62651 Seys, J.; Pint, S.; Verv… Sampling…     51.2      2.94 SW-Oostende_Oos…
#> # … with 13 more rows, and 7 more variables: preferredGazetteerNameLang <chr>,
#> #   status <chr>, accepted <int>, minLatitude <dbl>, minLongitude <dbl>,
#> #   maxLatitude <dbl>, maxLongitude <dbl>
```

The list of place types and sources are available with `gaz_types()` and
`gaz_sources()` respectively.

You can add the geometry of the Gazetteer entries with `gaz_geometry()`:

``` r
# Get a record and turn into a sf object with geometry
gaz_search(3293) %>% gaz_geometry()
#> Simple feature collection with 1 feature and 14 fields
#> Geometry type: MULTIPOLYGON
#> Dimension:     XY
#> Bounding box:  xmin: 2.238333 ymin: 51.08931 xmax: 3.370403 ymax: 51.87611
#> Geodetic CRS:  WGS 84
#> # A tibble: 1 × 15
#>   MRGID gazetteerSource    placeType latitude longitude minLatitude minLongitude
#>   <int> <chr>              <chr>        <dbl>     <dbl>       <dbl>        <dbl>
#> 1  3293 Flanders Marine I… EEZ           51.5      2.71        51.1         2.24
#> # … with 8 more variables: maxLatitude <dbl>, maxLongitude <dbl>,
#> #   precision <dbl>, preferredGazetteerName <chr>,
#> #   preferredGazetteerNameLang <chr>, status <chr>, accepted <int>,
#> #   the_geom <MULTIPOLYGON [°]>

# Or get only the geometry 
gaz_geometry(3293, format = "sfc")
#> Geometry set for 1 feature 
#> Geometry type: MULTIPOLYGON
#> Dimension:     XY
#> Bounding box:  xmin: 2.238333 ymin: 51.08931 xmax: 3.370403 ymax: 51.87611
#> Geodetic CRS:  WGS 84
#> MULTIPOLYGON (((3.370403 51.36696, 3.369459 51....
```

The entries of the Marine Regions Gazetteer are organized
hierarchically. You can browse this hierarchy up and down with
`gaz_relations()`

``` r
# Get all relations
gaz_search(3293) %>% gaz_relations()
#> # A tibble: 31 × 14
#>    MRGID gazetteerSource   placeType latitude longitude minLatitude minLongitude
#>    <int> <chr>             <chr>        <dbl>     <dbl>       <dbl>        <dbl>
#>  1  3293 Flanders Marine … EEZ           51.5      2.71        51.1         2.24
#>  2  2419 ASFA thesaurus    Sandbank…     51.5      2.58        NA          NA   
#>  3  2420 ASFA thesaurus    Sandbank…     51.5      2.88        NA          NA   
#>  4  2421 ASFA thesaurus    Sandbank…     51.3      2.64        NA          NA   
#>  5    14 (2001). The Time… Nation        50.5      4.48        49.5         2.55
#>  6  2350 (1953). Limits o… IHO Sea …     56.4      2.74        51.0        -4.45
#>  7  4675 <NA>              Sandbank…     NA       NA           NA          NA   
#>  8  2550 ASFA thesaurus    Coast         51.2      2.91        51.1         2.54
#>  9 17401 Aphia             Wreck         51.4      2.32        NA          NA   
#> 10 17409 Aphia             Wreck         51.1      2.33        NA          NA   
#> # … with 21 more rows, and 7 more variables: maxLatitude <dbl>,
#> #   maxLongitude <dbl>, precision <dbl>, preferredGazetteerName <chr>,
#> #   preferredGazetteerNameLang <chr>, status <chr>, accepted <int>

# Or get the relations directly
gaz_relations(3293)
#> # A tibble: 31 × 14
#>    MRGID gazetteerSource   placeType latitude longitude minLatitude minLongitude
#>    <int> <chr>             <chr>        <dbl>     <dbl>       <dbl>        <dbl>
#>  1  3293 Flanders Marine … EEZ           51.5      2.71        51.1         2.24
#>  2  2419 ASFA thesaurus    Sandbank…     51.5      2.58        NA          NA   
#>  3  2420 ASFA thesaurus    Sandbank…     51.5      2.88        NA          NA   
#>  4  2421 ASFA thesaurus    Sandbank…     51.3      2.64        NA          NA   
#>  5    14 (2001). The Time… Nation        50.5      4.48        49.5         2.55
#>  6  2350 (1953). Limits o… IHO Sea …     56.4      2.74        51.0        -4.45
#>  7  4675 <NA>              Sandbank…     NA       NA           NA          NA   
#>  8  2550 ASFA thesaurus    Coast         51.2      2.91        51.1         2.54
#>  9 17401 Aphia             Wreck         51.4      2.32        NA          NA   
#> 10 17409 Aphia             Wreck         51.1      2.33        NA          NA   
#> # … with 21 more rows, and 7 more variables: maxLatitude <dbl>,
#> #   maxLongitude <dbl>, precision <dbl>, preferredGazetteerName <chr>,
#> #   preferredGazetteerNameLang <chr>, status <chr>, accepted <int>
```

## Marine Regions Data Products

In addition to the Marine Regions Gazetteer, the Marine Regions Team
creates and hosts geographical Data Products, being the most popular one
the [Marine Regions Maritime
Boundaries](https://marineregions.org/eez.php).

An overview of all available products can be consulted with `mrp_list`

``` r
mrp_list
#> # A tibble: 21 × 8
#>    title                   namespace layer license citation doi   imis  abstract
#>    <chr>                   <chr>     <chr> <chr>   <chr>    <chr> <chr> <chr>   
#>  1 Exclusive Economic Zon… MarineRe… eez   Creati… "Flande… http… http… "Versio…
#>  2 Maritime Boundaries (v… MarineRe… eez_… Creati… "Flande… http… http… "Versio…
#>  3 Territorial Seas (12 N… MarineRe… eez_… Creati… "Flande… http… http… "Versio…
#>  4 Contiguous Zones (24 N… MarineRe… eez_… Creati… "Flande… http… http… "Versio…
#>  5 Internal Waters (v3, w… MarineRe… eez_… Creati… "Flande… http… http… "Versio…
#>  6 Archipelagic Waters (v… MarineRe… eez_… Creati… "Flande… http… http… "Versio…
#>  7 High Seas (v1, world, … MarineRe… high… Creati… "Flande… http… http… "High S…
#>  8 Extended Continental S… MarineRe… ecs   Creati… "Flande… http… http… "This d…
#>  9 Extended Continental S… MarineRe… ecs_… Creati… "Flande… http… http… "This d…
#> 10 IHO Sea Areas (v3)      MarineRe… iho   Creati… "Flande… http… http… "World …
#> # … with 11 more rows
```

You can visualize the Marine Regions Data Products with `mrp_view()`. It
opens an interactive `leaflet::leaflet` viewer.

``` r
mrp_view("eez")
```

![](https://raw.githubusercontent.com/lifewatch/mregions2/main/man/figures/README-prod1-1.png)

Or you can download and read the data products into R with `mrp_get()`

``` r
mrp_get("eez")
```

You can specify the download path in the `path` argument:

``` r
mrp_get("eez", path = "path/to/data")
```

Get to know more in the [Get Started
vignette](https://lifewatch.github.io/mregions2/articles/mregions2.html).

## Citation

``` r
citation("mregions2")
#> To cite package 'mregions2' in publications use:
#> 
#>   Fernandez-Bejarano S, Pohl L (2023). _mregions2: Access Data from
#>   Marineregions.org: The Marine Regions Gazetteer and the Marine
#>   Regions Data Products_. <https://github.com/lifewatch/mregions2>.
#> 
#> A BibTeX entry for LaTeX users is
#> 
#>   @Manual{,
#>     title = {{mregions2}: Access Data from Marineregions.org: The Marine Regions Gazetteer and the Marine Regions Data Products},
#>     author = {Salvador Fernandez-Bejarano and Lotte Pohl},
#>     year = {2023},
#>     url = {https://github.com/lifewatch/mregions2},
#>   }
```

## License

MIT. See `LICENSE.md`

## Code of Conduct

Please note that the mregions2 project is released with a [Contributor
Code of
Conduct](https://lifewatch.github.io/mregions2/CODE_OF_CONDUCT.html). By
contributing to this project, you agree to abide by its terms.
