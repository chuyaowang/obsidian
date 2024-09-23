# How to configure jupyter notebook

Install on base conda environment and use ipykernel to add other environments as kernels

Meaning:

``` bash
conda activate selenium
conda install ipykernel
ipython kernel install --user --name=selenium
conda deactivate
```

## irkernel

[irkernel](irkernel.md)

## nb_conda_kernels

https://github.com/anaconda/nb_conda_kernels
Easily use all [R](R.md) and [Python](Python.md) [conda](conda.md) environments as kernels.

## jupyverse

Used to start jupyter lab and access it remotely.

Single user use:
https://davidbrochart.github.io/jupyverse/usage/single_user/

``` sh
jupyverse --set auth.mode=noauth
```

## autostart

https://medium.com/analytics-vidhya/auto-start-jupyter-lab-on-machine-boot-e4f6b3296034
https://medium.com/@datamove/setup-jupyter-notebook-server-to-start-up-on-boot-and-use-different-conda-environments-147b091b9a5f

## Jupyter lab configurations

### starting folder

First run

``` sh
jupyter lab --generate-config
```

It will tell you where the config file is. Go open it. For it is at `~/.jupyter`

Find `c.ServerApp.root_dir` and set it to a directory of your choice.

Make sure to uncomment the line!

### Starting port

Similar as above, but change `c.ServerApp.port = 8080` or whatever number you like

### ip listened

`c.ServerApp.ip` defaults to localhost. Since I use port forwarding to forward my port to localhost on Ubuntu, it is ok I leave it at localhost. Otherwise change to 0.0.0.0 for remote access.


## Shutdown

Find all running servers
``` sh
jupyter lab list
```

Ctrl + C or 
``` sh
jupyter lab stop <port_number>
```

## Remove kernel

``` sh
jupyter kernelspec list
jupyter kernelspec uninstall unwanted-kernel
```

## Run jupyter lab

``` sh
jupyter lab --port=8080 --no-browser
```

## auto-complete

https://ericmjl.github.io/data-science-bootstrap-notes/turbocharge-jupyter-lab-using-language-servers/