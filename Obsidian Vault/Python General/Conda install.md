# Conda install
#conda #install #dependencies


# Openpyxl
[github - openpyxl](https://github.com/conda-forge/openpyxl-feedstock)

Installing `openpyxl` from the `conda-forge` channel can be achieved by adding `conda-forge` to your channels. Once the `conda-forge` channel has been enabled, `openpyxl` can be installed.

```shell
conda config --add channels conda-forge
conda config --set channel_priority strict
conda install openpyxl
```