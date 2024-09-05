# irkernel

Use R in Jupyter notebook

https://github.com/IRkernel/IRkernel
[jupyter](jupyter.md)
[R](R.md)

## install to a specific name and path

``` r
IRkernel::installspec(name = 'ir33', displayname = 'R 3.3', predix='/opt/miniconda3',verbose=TRUE)
```

The prefix determines where to install the kernel. Make it the same for every kernel.

Run `jupyter kernelspec` to see where is the base environment kernel is.

## With renv

renv does not work outside the folder it is installed in. If you have a project and use renv, everything renv uses is in `project/renv/`. If you install irkernel, but edits a notebook outside `project/`, Jupyter will FAIL to connect to the kernel because the outside directory has no renv!

Create [File Links](File%20Links.md) to mitigate this problem. Using absolute paths!
```bash
ln -s /your/renv_folder/directory/ /your/notebook/directory/
ln -s /your/.Rprofile/directory/ /your/notebook/directory/
```

