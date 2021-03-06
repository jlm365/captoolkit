![splash](splash.png)

# captoolkit - Cryosphere Altimetry Processing Toolkit

[![Language](https://img.shields.io/badge/python-3.6%2B-blue.svg)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://github.com/leiyangleon/autoRIFT/blob/master/LICENSE)
[![DOI](https://zenodo.org/badge/104787010.svg)](https://zenodo.org/badge/latestdoi/104787010)
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/fspaolo/captoolkit/master)  


#### Set of tools for processing and integrating satellite and airborne (radar and laser) altimetry data.

## Project leads

* [Fernando Paolo](https://science.jpl.nasa.gov/people/Serrano%20Paolo/) (paolofer@jpl.nasa.gov)
* [Johan Nilsson](https://science.jpl.nasa.gov/people/Nilsson/) (johan.nilsson@jpl.nasa.gov)
* [Alex Gardner](https://science.jpl.nasa.gov/people/AGardner/) (alex.s.gardner@jpl.nasa.gov)

Jet Propulsion Laboratory, California Institute of Technology

Development of the codebase was funded by the NASA Cryospheric Sciences program and the NASA MEaSUReS ITS_LIVE project through award to Alex Gardner.

## Contributors

- Tyler Sutterley (tsutterl@uw.edu) 

## Contribution

If you would like to contribute (your own code or modifications to existing ones) just create a [pull request](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/creating-a-pull-request) or send us an email, we will gladly add you as a contributor to the project.

## Install

    git clone https://github.com/fspaolo/captoolkit.git
    cd captoolkit
    python setup.py install

## Example

Read ICESat-2 Land Ice Height product (ATL06) in parallel and extract some variables using 4 cores (from the command line):

    readatl06.py -n 4 *.h5 

To see the input arguments of each program run:

    program.py -h

For more information check the header of each program.

## Notebooks

[Introduction to HDF5 data files](https://nbviewer.jupyter.org/github/fspaolo/captoolkit/blob/master/notebooks/intro-to-hdf5.ipynb)   
High-level overview of the HDF5 file structure and associated tools

[Reduction of ICESat-2 data files](https://nbviewer.jupyter.org/github/fspaolo/captoolkit/blob/master/notebooks/redu-is2-files.ipynb)  
Select (ATL06) files and variables of interest and write to a simpler structure
  
[Filtering and gridding elevation change data](https://nbviewer.jupyter.org/github/fspaolo/captoolkit/blob/master/notebooks/Gridding-rendered.ipynb)  
Interpolate and filter data to derive gridded products of elevation change

## Notes

This package is under heavy development, and new tools are being added as we finish testing them (many more utilities are coming).

Currently, the individual programs work as standalone command-line utilities or editable scripts. There is no need to install the package. You can simply run the python scripts as:

    python program.py -a arg1 -b arg2 /path/to/files/*.h5

## Tools

### Reading

* `readgeo.py` - Read Geosat and apply/remove corrections
* `readers.py` - Read ERS 1/2 (REAPER) and apply/remove corrections
* `readra2.py` - Read Envisat and apply/remove corrections
* `readgla12.py` - Read ICESat GLA12 Release 634 HDF5 and apply/remove corrections
* `readatl06.py` - Read ICESat-2 ATL06 HDF5 and select specific variables

### Correcting

* `corrapply.py` - Apply a set of specified corrections to a set of variables
* `corrslope.py` - Correct slope-induced errors using 'direct' or 'relocation' method 
* `corrscatt.py` - Correct radar altimetry height to correlation with waveform parameters
* `corrlaser.py` - Compute and apply corrections for ICESat Laser 2 and 3.

### Filtering

* `filtst.py` - Filter point-cloud data in space and time
* `filtmask.py` - Select scattered data using raster-mask, polygon or bounding box
* `filtnan.py` - Check for NaNs in a given 1D variable and remove the respective "rows"
* `filttrack.py` - Filter satellite tracks (segments) with along-track running window (**coming**)
* `filttrackwf.py` - Filter waveform tracks (segments) with along-track running window (**coming**)

### Differencing

* `xing.py` - Compute differences between two adjacent points (cal/val)
* `xover.py` - Compute crossover values at satellite orbit intersections

### Fitting

* `fittopo.py` - Detrend data with respect to modeled topography
* `fitsec.py` - Compute robust height changes using a surface-fit approach

### Interpolating

* `interpgaus.py` - Interpolate irregular data using Gaussian Kernel
* `interpmed.py` - Interpolate irregular data using a Median Kernel
* `interpkrig.py` - Interpolate irregular data using Kriging/Collocation

### Utilities

* `split.py` - Split large 1D HDF5 file(s) into smaller ones
* `merge.py` - Merge several HDF5 files into a single or multiple file(s)
* `mergetile.py` - Merge tiles from different missions keeping the original grid
* `tile.py` - Tile geographical (point) data to allow parallelization
* `join.py` - Join a set of geographical tiles (from individual files)
* `joingrd.py` - Join a set of geographical tiles (subgrids from individual files)
* `stackgrd.py` - Stack a set of 2D grids into a 3D cube using time information
* `sort.py` - Sort (in place) all 1D variables in HDF5 file(s)
* `dummy.py` - Add dummy variables as 1D arrays to HDF5 files(s)
* `hdf2txt.py` - Convert HDF5 (1D arrays) to ASCII tables (columns)
* `txt2hdf.py` - Convert (very large) ASCII tables to HDF5 (1D arrays)
* `query.py` - Query entire data base (tens of thousands of HDF5 files) (**coming**)

### Gaussian Processes 

* `ointerp/ointerp.py` - Optimal Interpolation/Gaussian Processes (**coming**)
* `ointerp/covx.py` - Calculate empirical spatial covariances from data (**coming**)
* `ointerp/covt.py` - Calculate empirical temporal covariances from data (**coming**)
* `ointerp/covfit.py` - Fit analytical model to empirical covariances (**coming**)

### IBE

* `ibe/corribe.py` - Compute and apply inverse barometer correction (IBE)
* `ibe/slp2ibe.py` - Convert ERA-Interim Sea-level pressure to IBE
* `ibe/geteraint.py` - Example python params to download ERA-Interim

### Tides

* `tide/corrtide.py` - Compute and apply ocean and load tides corrections
* `tide/calc_astrol_longitudes.py` - Computes the basic astronomical mean longitudes
* `tide/calc_delta_time.py` - Calculates difference between universal and dynamic time
* `tide/convert_xy_ll.py` - Convert lat/lon points to and from projected coordinates
* `tide/infer_minor_corrections.py` - Return corrections for 16 minor constituents
* `tide/load_constituent.py` - Loads parameters for a given tidal constituent
* `tide/load_nodal_corrections.py` - Load the nodal corrections for tidal constituents
* `tide/predict_tide_drift.py` - Predict tidal elevations using harmonic constants
* `tide/read_tide_model.py` - Extract tidal harmonic constants from OTIS tide models
* `tide/read_netcdf_model.py` - Extract tidal harmonic constants from netcdf models
* `tide/read_GOT_model.py` - Extract tidal harmonic constants from GSFC GOT models

### 2D Fields

* `gettopo.py` - Estimate slope, aspect and curvature from given DEM
* `getdem.py` - Regrid mean height field (DEM) from grid-1 onto grid-2 (**coming**)
* `getveloc.py` - Combine best 2D mean field from different velocities (**coming**)
* `vregrid.py` - Regrid velocity field onto height field (**coming**)
* `getmsl.py` - Calculate and extend MSL field for the ice shelves (**coming**)
* `mkmaskpy` - Compute ice shelf, basin and buffer raster masks (**coming**)

### 3D Fields 

* `cubefilt.py` - Filter slices (spatial) and individual time series (temporal) (**coming**)
* `cubefilt2.py` - Filter time series residuals w.r.t. a piece-wise poly fit (**coming**)
* `cubexcal.py` - Cross-calibrate several data cubes with same dimensions (**coming**)
* `cubeimau.py` - Filter and regrid IMAU Firn cube product (**coming**)
* `cubegsfc.py` - Filter and regrid GSFC Firn cube product (**coming**)
* `cubegemb.py` - Filter and regird JPL Firn and SMB cube products (**coming**)
* `cubesmb.py` - Filter and regrid RACMO and ERA5 SMB cube products (**coming**)
* `cubethick.py` - Compute time-variable Freeboard, Draft, and Thickness (**coming**)
* `cubediv.py` - Compute time-variable Flux Divergence, and associated products (**coming**)
* `cubemelt.py` - Compute time-variable basal melt rates and mass change (**coming**)
* `cuberegrid.py` - Remove spatial artifacts and regrid 3D fields (**coming**)

### Scripts

* `scripts/` - This folder contains supporting code (generic and specific) that we have used in our analyses. We provide these scripts **as is** in case you find them useful.

### Data

* `data/` - The data folder contains example data files for some of the tools. See respective headers.
