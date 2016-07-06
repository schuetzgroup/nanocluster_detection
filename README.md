# clustermask_analysis
Matlab m-file supplements to Nature Methods article  
Baumgart et al., 2016: http://www.nature.com/nmeth/journal/vaop/ncurrent/pdf/nmeth.3897.pdf  
DOI: http://dx.doi.org/10.1038/nmeth.3897

published online 13 June 2016

## Article
***Varying label density allows artifact-free analysis of membrane-protein nanoclusters***  
Florian Baumgart, Andreas M Arnold, Konrad Leskovar, Kaj Staszek, Martin Fölser, Julian Weghuber, Hannes Stockinger, Gerhard J Schütz

### Abstract
We present a method to robustly discriminate clustered from randomly distributed molecules detected with techniques based on single-molecule localization microscopy, such as PALM and STORM.
The approach is based on deliberate variation of labeling density, such as titration of fluorescent antibody, combined with quantitative cluster analysis, and it thereby circumvents the problem of cluster artifacts generated by overcounting of blinking fluorophores.
The method was used to analyze nanocluster formation in resting and activated immune cells.

### Instructions to use Matlab Code:
1. Copy program files (*.m and *.fig) into a separate folder and add the path to the Matlab search paths using:  
pathtool -> Add Folder -> Save

2. Copy files containing superresolution images (*.csv) into a separate folder. Example files are included for random and clustered simulated data. Molecules were assumed to be observed seven times on average (exponentially distributed). Clusters were simulated at 3 μm-² and 75 nm radius. See Methods for more details.

3. Execute clustermask_createset.m
Note: The GUI is optimized for Matlab release 2015b.

4. Press Open Folder to select the folder that contains  the example files for analysis.

5. Adjust the following parameters if needed (or use default values):  

  - ***ROI size (pixel):***  
    size of recorded image
  - ***Pixelsize (in nm):***  
    camera pixel size
  - ***Gridsize (pixel):***  
    number of pixels used for binary mask
  - ***resulting pixelsize:***  
    here the effective pixel size of binary masks is automatically calculated from the given parameters (ROI size, Pixelsize, Gridsize).  It is recommended to keep this value significantly below the localization precision.
  - ***Sig for gaussians (nm):***  
    standard deviation of Gaussians used to represent localizations
  - ***Cut gauss at x times sig:***  
    radius at which Gaussians are set to zero
  - ***use same cellroi for all:***  
    check box to use the same ROI for all files
  - ***Figure parameter:***  
    check boxes to specify output figure parameters
  - ***TH1 - TH6:***  
    defines thresholds; set to 0 to skip 
  - ***Settings rho vs eta plot:***  
    check boxes to specify output plots;  edit parameters for reference curve


6. Hit Process Files to start the analysis. First a dialog window will open to specify ROIs for analysis. When ROIs for all files have been drawn, the program will start to analyze the files in the specified folder. The user can also mark the checkbox “use same cellroi for all”, in order to reuse the same ROI for all files in the chosen folder.

7. Results are saved in result.m, which contains the following output variables:  

  - ***num_locs:***  
    array containing the calculated number of localizations outside (#out) and inside (#in) of apparent clusters. Different thresholds are grouped pair-wise (#out, #in) in the order specified in no_locs_legend  
  - ***num_locs_legend:***  
    specifies the order of the columns in the variable num_locs  
  - ***clust_area:***  
    calculated clustered area (Ain)  
  - ***cell_area:***  
    area of the ROI drawn in the dialog window (A)  
  - ***files:***  
    file names of analyzed files  
  - ***eta:*** 
    array containing the values for relative clustered area (rows correspond to selected files; columns correspond to selected thresholds)  
  - ***rho:***  
    array containing values for localization density inside clusters (rows correspond to selected files; columns correspond to selected thresholds)  
  - ***fit:***  
    struct containing the fitted parameters for all thresholds  

8. Output graphs show the normalized ρ/η plot including the reference curve for randomly distributed data (red). Data are plotted as blue circles. Results from example files will be comparable to Figure 1.