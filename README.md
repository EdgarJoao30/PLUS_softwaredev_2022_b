# Basics of Software Development lecture [@PLUS](https://www.plus.ac.at/)

## Creating a Python environment
We can use conda to create and manage Python environments. For this, we have to install Anaconda or Miniconda, follow the official [documentation](https://www.anaconda.com/products/distribution) to make the installation. 

The intended use of this environment will be the geospatial analysis, conveniently, [Prof. Qiusheng Wu](https://wetlands.io/) has recently released the
[geospatial](https://geospatial.gishub.org/installation/) Python package that puts together many packages for spatial analysis, spatial data manipulation, and visualization. 

Following the documentation of the geospatial package we can create a Python environment using conda and mamba with the code bellow.

```
conda create -n geo python=3.9
conda activate geo
conda install -c conda-forge mamba
mamba install -c conda-forge geospatial
```

## Exporting the enviroment
The main feature of creating a virtual environment is that you can also share the configuration details of such environment so anyone can replicate it. This can be easily done with the code bellow.

```
conda env export --name geo > environment.yml
```

While testing the export and create from file (See bellow) features on different Operating Systems (OS), we noticed that even though the export function claims to be OS independent, there were some inconsistencies on the package dependencies between different versions been available on different OS.

To solve this issue we added the --no-builds parameter to the previous code. This reduced considerably the amount of packages affected by the `ResolvePackageNotFound` error, but not completely.

```
conda env export --no-builds > environment.yml
```

## Create an environment based on a file
We can create and environment from a `.yml` file with the following command.

```
conda env create --file environment.yml
```

To prevent the remaining packages to throw the `ResolvePackageNotFound` error, we had to modify the `.yml` file by specifying that those packages should be installed from `pip` as shown bellow.

```
  - pip:
    - wincertstore=0.2
```
