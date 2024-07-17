# How to configure jupyter notebook

Install on base conda environment and use ipykernel to add other environments as kernels

Meaning:

``` bash
conda activate selenium
pip install ipykernel
ipython kernel install --user --name=selenium
conda deactivate
```