# FORCeS ECS

*Combining emergent constraints produced by the FORCeS project using the [Bretherton and Caldwell (2020)](https://doi.org/10.1175/JCLI-D-19-0911.1) [BC2020] method.*

## Requirements

- Python 3
- Python packages:

    ```sh
    pip3 install numpy scipy matplotlib pymc ds-format pst-format
    ```
- GNU parallel (optional)

## Commands

The commands are to be run from the command line.

### bin/model

```
Run a PyMC model for multivariate emergent constraint (EC) calculation.

Usage: model INPUT... OUTPUT

Arguments:

  INPUT   Input directory with data.csv and obs.csv for an EC.
  OUTPUT  Output file (NetCDF).

Examples:

  Read all constraints in the directory input and write the output to data/all.nc.

  bin/model input/merged/* data/multivar/merged.nc

  Calculate univariate distributions.

  parallel bin/model {} data/merged/{/}.nc ::: input/merged/*
```

### bin/plot\_pdf

```
Plot conditional probability density function of emergent constraints (EC).

Usage: plot_pdf INPUT... OUTPUT [OPTIONS]

Arguments:

  INPUT   Input file - the output of model (NetCDF).
  OUTPUT  Output plot (PDF).

Options:

  xlim: { MIN MAX }  x-axis limits.
  ylim: { MIN MAX }  y-axis limits.

Examples:

  Plot probability density functions of all ECs in merged.

  bin/plot_pdf data/multivar/merged.nc data/merged/*.nc plot/pdf/merged.pdf
```

### bin/plot\_scatter

```
Plot a scatter plots with model x-axis and y-axis values for all combinations of constraints and the y-axis.

Usage: plot_scatter INPUT OUTPUT

Arguments:

  INPUT   Input file - output of model (NetCDF).
  OUTPUT  Output plot (PDF).

Examples:

  Plot scatter plots of the multivariate simulation.

  bin/plot_scatter data/multivar/merged.nc plot/scatter/merged.pdf
```

### bin/process\_schlund\_ec

```
Process Schlund et al. (2020) emergent constraint (EC) input data.

Usage: process_schlund_ec DATA OBS META OUTPUT

Arguments:

  DATA    Input file with data for all ECs (CSV).
  OBS     Input file with observation constraints or all ECs (CSV).
  META    Input file with metadata (CSV).
  OUTPUT  Output directory. In the output directory, a new directory for each EC is created.

Examples:

  Process input data in input/schlund2020/cmip{5,6,5+6}.

  bin/process_schlund_ec input/schlund2020/cmip5.csv input/schlund2020/{obs,meta}.csv input/schlund2020/cmip5/
  bin/process_schlund_ec input/schlund2020/cmip6.csv input/schlund2020/{obs,meta}.csv input/schlund2020/cmip6/
  bin/process_schlund_ec input/schlund2020/cmip5+6.csv input/schlund2020/{obs,meta}.csv input/schlund2020/cmip5+6/
```

## Input data

The input data are stored in `input`. These include the model EC x-axis values, ECS, observations x-axis value and standard deviation and EC metadata (title, x-axis label and units). The input data are split into the following groups:

- `bretherton2020`: The credible and other ECs analysed by BC2020.
- `forces`: FORCeS ECs.
- `merged`: BC2020 and [Schlund et al. (2020)](https://doi.org/10.5194/esd-11-1233-2020) [S2020] ECs together. The same ECs from BC2020 and S2020 are merged together, so that they contain all of the CMIP3, CMIP5 and CMIP6 models available.
- `schlund2020`: ECs from S2020 separately for CMIP5, CMIP6 and CMIP5+6 models. Subdirectories ending in `_sel` contain the same models as the related directory without `_sel`, but excluding the `sherwood2014_D` and `sherwood2014_S` ECs because they cause a convergence issue in the simulation when all three sherwood2014 ECs are included.

## License

This software is distributed under the MIT license. See [LICENSE.md](LICENSE.md).
