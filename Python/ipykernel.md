# ipykernel

Install in [conda](conda.md) environment to use it in [jupyter](jupyter.md) notebook

When you have multiple kernels, install each kernel manually [here](https://ipython.readthedocs.io/en/stable/install/kernel_install.html)

``` sh
/path/to/kernel/env/bin/python -m ipykernel install --prefix=/path/to/jupyter/env --name 'python-my-env'
```

`/path/to/kernel/env/bin/python`: should be the python in your environment
`/path/to/jupyter/env`: should point to your base environment! `/opt/miniconda`! The kernel will be installed to `/opt/miniconda/share/jupyter/kernels/`
`--name`: set a different name. Kernels with the same name overwrite each other! The actual files are separate, but Jupyter only sees the last installed kernel in the kernels with the same name.