# Conda

> [Python](Python.md) package and environment manager

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