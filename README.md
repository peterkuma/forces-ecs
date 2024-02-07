# FORCeS ECS

*Combining emergent constraints produced by the FORCeS project using the Bretherton and Caldwell (2020) method.*

## Requirements

- Python 3
- Python packages:

    ```sh
    pip3 install numpy matplotlib pymc ds-format pst-format
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

  bin/model input/* data/multivar.nc

  Calculate univariate distributions.

  parallel bin/model {} data/univar/{/}.nc ::: input/*
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

  Plot probability density functions of all ECs.

  bin/plot_pdf data/multivar.nc data/univar/*.nc plot/pdfs.pdf
```

### bin/plot\_scatter

```
Plot a scatter plots with model x-axis and y-axis values for all combinations of constraints and the y-axis.

Usage: plot_scatter INPUT OUTPUT

Arguments:

  INPUT   Input file - output of model (NetCDF).
  OUTPUT  Output plot (PDF).
```

## License

This software is distributed under the MIT license. See [LICENSE.md](LICENSE.md).
