# The R language

All R packages links to here.

## Where is R

``` r
R.home()
```

## Where are packages

``` r
.libPaths()
```

## Can't find a library

Sometimes R can't find a required library, like openssl. Download the source code and use this to install:

``` sh
R CMD INSTALL --configure-vars='INCLUDE_DIR=/opt/homebrew/Caskroom/miniconda/base/pkgs/openssl-3.2.1-h0d3ecfb_0/include LIB_DIR=/opt/homebrew/Caskroom/miniconda/base/pkgs/openssl-3.2.1-h0d3ecfb_0/lib' openssl_2.2.0.tar.gz
```

First find where the library is installed with:

``` sh
which openssl
```

or 

``` sh
whereis openssl
```

or find where [conda](conda.md) environment installs the library

## Look in directory

``` r
tempdir()
```

``` r
list.files()
```

## R and R packages from conda

https://medium.com/@tortuecookie/using-r-with-conda-80953395bfe6

Some new packages are not there. See below:
### Install github r package in conda

https://stackoverflow.com/questions/52061664/install-r-package-from-github-using-conda

``` sh
conda skeleton cran <github_url>
conda build --R=<my_r_version> r-<lower-case-package-name>
```