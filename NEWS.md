rnoaa 0.5.2
===============

### NEW FEATURES

* New data source added: ARGO buoy data. See functions starting with `argo()` (#123)
for more, see http://www.argo.ucsd.edu/
* New data source added: CO-OPS tide and current data. See function `coops_search()` 
(#111) for idea from @fmichonneau (#124) for implementing @jsta See http://co-ops.nos.noaa.gov/api/
also (#126) (#128)

### MINOR IMPROVEMENTS

* `rgdal` moved to Suggests to make usage easier (#125)
* Changes to `ncdc_plot()` - made default brakes to just default to what
`ggplot2` does, but you can still pass in your own breaks (#131)

rnoaa 0.5.0
===============

### NEW FEATURES

* New data source added: NOAA Global Ensemble Forecast System (GEFS) data. 
See functions `gefs()`, `gefs_dimension_values()`, `gefs_dimensions()`, `gefs_latitudes()`, 
`gefs_longitudes()`, and `gefs_variables()` (#106) (#119)  thanks @potterzot - he's 
now an author too
* New data source added: NOAA Extended Reconstructed Sea Surface Temperature 
(ERSST) data. See function `ersst()` (#96)
* New function `isd_stations()` to get ISD station data.
* Added code of conduct to code repository

### MINOR IMPROVEMENTS

* Swapped `ncdf` package for `ncdf4` package. Windows binaries weren't 
availiable for `ncdf4` prior to now. (#117)
* Proper license info added for javascript modules used inside the
package (#116)
* Improvements to `isd()` function to do transformations of certain 
variables to give back data that makes more sense (#115)
* `leaflet`, `geojsonio`, and `lawn` added in Suggests, used in a few 
functions.
* Note added to `swdi()` function man page that the `nldn` dataset is 
available to military users only (#107)

### BUG FIXES

* Fix to `buoy()` function to accept character class inputs for the 
`buoyid` parameter. the error occurred because matching was not 
case-insensitive, now works regardless of case (#118)
* Fixes for new `ggplot2` version (#113)
* Built in `GET` request retries for `ghncd` functions as 
some URLs fail unpredictably (#110)

rnoaa 0.4.2
===============

### MINOR IMPROVEMENTS

* Explicitly import non-base R pkg functions, so importing from `utils`, `methods`, and `stats` (#103)
* All NCDC legacy API functions are now defunct. See `?rnoaa-defunct` for more information (#104)
* `radius` parameter removed from `ncdc_stations()` function (#102), was already removed internally within the function in the last version, now not in the function definition, see also (#98) and (#99)
* Dropped `plyr` and `data.table` from imports. `plyr::rbind.fill()` and `data.table::rbindlist()` replaced with `dplyr::bind_rows()`.

### BUG FIXES

* Fixed problem with `httr` `v1` where empty list not allowed to pass to
the `query` parameter in `GET` (#101)

rnoaa 0.4.0
===============

### NEW FEATURES

+ Gains a suite of new functions for working with NOAA GHCND data, including
`ghcnd()`, `ghcnd_clear_cache()`, `ghcnd_countries()`, `ghcnd_search()`, `ghcnd_splitvars()`
`ghcnd_states()`, `ghcnd_stations()`, and `ghcnd_version()` (#85) (#86) (#87) (#88) (#94)
+ New contributor Adam Erickson (@DougFirErickson)
+ All NOAA buoy functions put back into the package. They were previously
on a separate branch in the GitHub repository. (#37) (#71) (#100)

### MINOR IMPROVEMENTS

+ Minor adjustments to `isd()` functions, including better man file.
+ Cleaner package imports - importing mostly only functions used in dependencies.
+ Startup message gone.
+ `callopts` parameter changed to `...` in function `swdi()`.
+ More robust test suite.
+ `ncdc()` requires that users do their own paging - previously this was done internally (#77)
+ Many dependencies dropped, simplifying package: `RCurl`, `maptools`, `stringr`, `digest`.
A few new ones added: `dplyr`, `tidyr`.

### DEPRECATED AND DEFUNCT

+ All `erddap` functions now defunct - see the package [rerddap](https://github.com/ropensci/rerddap),
a general purpose R client for ERDDAP servers. (#51) (#73) (#90) (#95)
+ The `extent` function in `noaa_stations()` used to accept either a bounding
box or a point defined by lat/long. The lat/long option dropped as it required
two packages, one of which is a pain to install for many users (#98) (#99)

rnoaa 0.3.3
===============

### NEW FEATURES

+ New data source NOAA legacy API with ISD, daily, and ish data via function
`ncdc_legacy()`. (#54)
+ New function `isd()` to get ISD data from NOAA FTP server. (#76)
+ ERDDAP gridded data sets added. Now tabledap datasets are accessible via
`erddap_table()`, while gridded datasets are available via `erddap_grid()`. Helper
function `erddap_search()` was modified to search for either tabledap or griddap
datasets, and `erddap_info()` gets and prints summary information differently
for tabledap and griddap datasets. (#63)

### MINOR IMPROVEMENTS

+ `erddap_data()` defunct, now as functions `erddap_table()` and `erddap_grid()`, uses new
`store` parameter which takes a function, either `disk(path, overwrite)` to store
on disk or `memory()` to store in R memory.
+ `assertthat` library removed, replaced with `stopifnot()`

rnoaa 0.3.0
===============

### NEW FEATURES

+ New data source added (NOAA torndoes data) via function `tornadoes()`. (#56)
+ New data source added (NOAA storm data from IBTrACS) via functions
`storm_*()`. (#57)
+ New data source added (NOAA weather station metadata from HOMR) via functions
`homr_*()` (#59)
+ New vignettes for storm data and homr data.
+ Some functions in rnoaa now print data.frame outputs as `dplyr`-like outputs
with a summary of the data.frame, as appropriate.

### MINOR IMPROVEMENTS

+ Across all `ncdc_*` functions changed `callopts` parameter to `...`. This parameter
allow you to pass in options to `httr::GET` to modify curl requests. (#61)
+ A new helper function `check_key()` looks for one of two stored keys, as an
environment variable under the name `NOAA_KEY`, or an option variable under the name
`noaakey`. Environment variables can be set during session like `Sys.setenv(VAR = "...")`,
or stored long term in your `.Renviron` file. Option variables can be set during session
like `options(var = "...")`, or stored long term in your `.Rprofile` file.
+ `is.*` and `print.*` functions no longer have public man files, but can be seen via
`rnoaa:::` if needed.

rnoaa 0.2.0
===============

### NEW FEATURES

* New package imports: `sp`, `rgeos`, `assertthat`, `jsonlite`, and `ncdf4`, and new package Suggests: `knitr`, `taxize`
* Most function names changed. All `noaa*()` functions for NCDC data changed to `ncdc*()`. `noaa_buoy()` changed to `buoy()`. `noaa_seaice()` changed to `seaice()`. When you call the old versions an error is thrown, with a message pointing you to the new function name. See ?rnoaa-defunct.
* New vignettes: NCDC attributes, NCDC workflow, Seaice vignette, SWDI vignette, ERDDAP vignette, NOAA buoy vignette.
* New functions to interact with NOAA ERDDAP data: `erddap_info()`, `erddap_data()`, and `erddap_search()`.
* New functions to interact with NOAA buoy data: `buoy()`, including a number of helper functions.
* `ncdc()` now splits apart attributes. Previously, the attributes were returned as a single column, but now there is column for each attribute so data can be easily retrieved. Attribute columns differ for each different `datasetid`.
* `buoy()` function has been removed from the CRAN version of `rnoaa`. Install the version with `buoy()` and associated functions via `devtools::install_github("ropensci/rnoaa", ref="buoy")`

### MINOR IMPROVEMENTS

* `noaa_swdi()` (function changed to `swdi()`) gains new parameter `filepath` to specify path to write a file to if `format=kmz` or `format=shp`. Examples added for using `format=` csv, shp, and kmz.
* Now using internal version of `plyr::compact`.
* Added API response checker/handler to all functions to pass on helpful messages on server errors.
* `ncdc()` gains new parameter `includemetadata`. If TRUE, includes metadata, if not, does not, and response should be faster as does not take time to calculate metadata.
* `noaa_stations()` gains new parameter `radius`. If `extent` is a vector of length 4 (for a bounding box) then radius is ignored, but if you pass in two points to `extent`, it is interpreted as a point, and then `radius` is used as the distance upon which to construct a bounding box. `radius` default is 10 km.

### BUG FIXES

* `datasetid`, `startdate`, and `enddate` are often required parameters, and changes were made to help users with this.


rnoaa 0.1.0
===============

### NEW FEATURES

* Submitted to CRAN.


rnoaa 0.0.8
===============

### NEW FEATURES

* Wrote new functions for NOAA API v2.
* A working vignette now.


rnoaa 0.0.1
===============

### NEW FEATURES

* Wrappers for NOAA API v1 were written, not on CRAN at this point.
