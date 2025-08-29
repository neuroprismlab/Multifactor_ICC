# Generalizability Theory ICC toolbox

Calculate ICC coefficients extended to include multiple sources of error (i.e., facets) under Generalizability Theory and perform Decision Studies.

## Getting Started

### Prerequisites

Matlab (tested with Matlab 2018b).

### Usage

### 1. Create data and factor table variables.

*factor table*: n_observations x n_factors, with entries representing levels for each factor. Used directly by anovan.
Simple example: For two subjects (first column) and two scanners (second column):
ftbl = 
[1 1
1 2
2 1
2 2]
For example, the first column could represent subjects and the second scanners.

*roi data*: n_observations cell array where each cell is a 1-, 2- or 3-d matrix.
Simple example: For two brain regions:
roi_data=
{[0.1,0.2]}
{[0.5,0.7]}
{[0.2,0.3]}
{[0.2, 0.5]}

Alternatively, the *load\_reliability\_data* script could be used to automatically create a factor table from the filenames. However, this was originally developed for custom analyses. This can be changed for your data or data can be loaded manually (try "help load\_reliability\_data" for more info on the format).

### 2. Run reliability analysis.

Calculate ICCs with:

[icc_summary, var_comp_mean, selected_stats] = calc_roi_iccs(roi_data, factor_tbl, 'all')

More information about output:

*icc_summary* contains average Decision Studies across regions, single-measure ICCs for each region, and a truncated Decision Study for each region. Headings are 'DStudy_Gmean','DStudy_Dmean','first_Gmap (n_s=1,n_d=1)','first_Dmap (n_s=1,n_d=1)','detailed G','detailed D'.
var_comp_mean contains the mean variance components across all regions.

Alternatively, the *run\_reliability* script could be used to perform some optional filtering and significance masking (not recommended, but used for some custom analyses).

### 3. Interpretation.

Under construction - TODO
Generally recommend to use D coefficient (absolute) rather than G coefficient (relative)
Decision study reflects 6 levels, even if that is beyond what is collected (will extrapolate)
For decision study, note which axis is which facet


### References:

Noble, S., Spann, M. N., Tokoglu, F., Shen, X., Constable, R. T., & Scheinost, D. (2017). Influences on the test–retest reliability of functional connectivity MRI and its relationship with behavioral utility. Cerebral Cortex, 27(11), 5415-5429.

Noble, S., Scheinost, D., Finn, E. S., Shen, X., Papademetris, X., McEwen, S. C., ... & Mirzakhanian, H. (2017). Multisite reliability of MR-based functional connectivity. Neuroimage, 146, 959-970.

Webb, N.M., Shavelson, R.J. and Haertel, E.H., 2006. Reliability coefficients and generalizability theory. Handbook of statistics, 26, pp.81-124.
