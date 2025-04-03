# Conda

> [Python](Python.md) package and environment manager
> [Common commands](https://developer.aliyun.com/article/1267271)

## Add conda to PATH on Windows

- Add `D:\miniconda3\condabin\` to path variable
- Run `conda init` in powershell
- Re-open powershell

## Windows proxy

> [!code] Powershell Proxy Setting
> 
`$env:http_proxy="socks5://127.0.0.1:33211"`
`$env:https_proxy="socks5://127.0.0.1:33211"`
`$env:http_proxy="http://127.0.0.1:33210"`
`$env:https_proxy="http://127.0.0.1:33210"`

^377d00
### Install pysocks for socks support

`pip install pysocks`

## Add channels

``` sh
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge 
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/
conda config --show channels
```
## Create environment

`conda create -n "name" pip`
## Update conda

`conda update -n base -c defaults conda`

## Update python in the current env

`conda update python`

## List packages

`conda list`

## List envs

`conda env list`

## Remove envs

`conda remove --name name --all`

## Use with pip

`conda install pip`
Then do other pip installations

## Create requirements.txt

``` sh
conda list -e > requirements.txt
```

Use

``` sh
conda install --file requirements.txt
```

## conda clean

clean cache and unused package. 
resolves `ValueError: unsupported format character 'T' (0x54) at index 1787` error

``` sh
conda clean --all -y
```

## conda build

Build R packages from github

### Install conda build

``` sh
conda activate base
conda install conda-build
```

### Build skeleton

``` sh
conda skeleton cran https://github.com/cole-trapnell-lab/cicero-release
```

### Build package

``` sh
conda-build r-fansi
```
### Convert to other platforms

https://docs.conda.io/projects/conda-build/en/latest/user-guide/tutorials/build-pkgs.html#converting-a-package-for-use-on-all-platforms

## .condarc

- add or remove channels
- located at `~`
- `conda config --show channels` to show all channels