# ipykernel

Install in [conda](conda.md) environment to use it in [jupyter](jupyter.md) notebook

When you have multiple kernels, install each kernel manually [here](https://ipython.readthedocs.io/en/stable/install/kernel_install.html)

``` sh
/path/to/kernel/env/bin/python -m ipykernel install --sys-prefix --name 'python-my-env'
```

`/path/to/kernel/env/bin/python`: should be the python in your environment
- run `whereis python` after activating the environment to find it
`--name`: set a different name. Kernels with the same name overwrite each other! The actual files are separate, but Jupyter only sees the last installed kernel in the kernels with the same name.

## Find kernel installation location

``` python
from jupyter_client.kernelspec import KernelSpecManager
ksm = KernelSpecManager()
print(ksm.find_kernel_specs())
```

to see where the current interpreter is:

``` python
import sys
print(sys.executable)
```