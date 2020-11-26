## Summary

The SYD PYpline -> asteroseismic SYD pipeline ([Huber et al. 2009](https://ui.adsabs.harvard.edu/abs/2009CoAst.160...74H/abstract)) originally written in IDL translated into python

The pipeline works in two major parts:
1) findex: automatically finds power excess due to solar-like oscillations using a frequency resolved collapsed autocorrelation function
2) fitbg: perform a fit to the granulation background and measures the frequency of maximum power (nu_max), the large frequency separation (Delta_nu) and oscillation amplitude

## File Overview

### Files/
- todo.txt: File containing IDs of stars to be processed 
- data/: Directory containing data to be processed. File format: ID_LC.txt (lightcurve: days versus fractional flux) and ID_PS.txt (power spectrum: muHz versus ppm^2 muHz^-1). 
- params_findex.txt: input parameters for findex module (detailed documentation coming)
- params_fitbg.txt: input parameters fot fitbg module (detailed documentation coming)
- star_info.csv: basic information on stars to be processed. If no estimate of numax is provided, the stellar parameters are used to calculate as estimate
- results/target/: Directory containing result plots and files for each target

### Code
- functions.py : models, distributions, ffts, smoothing functions are all in this file
- SYD.py : initiates SYD through main
- scrape_output.py : grabs each individual target's results and concatenates results into a single csv in Files/ for each submodulel (i.e. findex.csv and globalpars.csv)

Documentation and code under construction.

## Example

To run example code clone/download the repository and then do:
- python SYD.py
To combine the results:
- python scrape_output.py

This will run the pipeline on the two stars specified in the todo.txt file (KIC1435467 and KIC2309595), one star at a time first using the findex module followed by the fitbg module. If you'd like to skip findex (e.g. useful for a handful of high S/N stars where you can visually estimate nu_max and thus specify it manually in star_info.csv), set findex = False in SYD.py. 

Note: for multiple targets in todo.txt, the text and plot outputs are supressed. To override this default and see the output in real time, simply run this command instead:
- python SYD.py -i
