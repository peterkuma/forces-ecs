# FORCeS ECS

*Combining emergent constraints produced by the FORCeS project using the Bretherton and Caldwell (2020) method.*

## Requirements

- Python 3
- Python packages:

    ```sh
    pip3 install numpy matplotlib pymc ds-format
    ```

## Commands

### bin/model

```
Run a PyMC model for multivariate emergent constraint (EC) calculation.

Usage: model INPUT... OUTPUT

Arguments:

  INPUT   Input directory with data.csv and obs.csv for an EC.
  OUTPUT  Output file (NetCDF).

Examples:

  Read all constraints in the directory input and write the output to data/all.nc.

  bin/model input/* data/all.nc
```
