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

## Remove conda environment

### 🔹 Removing a Conda Environment

1. **List environments**
    
    ```bash
    conda env list
    ```
    
2. **Deactivate current env**
    
    ```bash
    conda deactivate
    ```
    
3. **Remove environment completely**
    
    ```bash
    conda remove --name ENV_NAME --all
    ```
    
    - Deletes the environment and all its packages.
    - If created with a custom path:
        
        ```bash
        conda remove -p /path/to/env --all
        ```
        

---

### 🔹 Cleaning Up Conda Caches

Conda stores package tarballs and unused packages in a shared cache (`pkgs/`), which can grow large.

- **Remove unused packages**
    
    ```bash
    conda clean -p
    ```
    
- **Remove tarballs**
    
    ```bash
    conda clean -t
    ```
    
- **Full cleanup (safe default)**
    
    ```bash
    conda clean -a -y
    ```
    
    Removes: unused packages, tarballs, index cache, logs.
- ⚠️ Avoid `-f` unless you want to force‑remove _all_ caches (can break environments).

---

### 🔹 Checking Disk Usage per Environment (with Sorting)

#### Linux / macOS

```bash
du -sh ~/miniconda3/envs/* | sort -h
```

- `du -sh` → show size of each environment folder
- `sort -h` → sort by human‑readable size (smallest → largest)

To see **largest first**:

```bash
du -sh ~/miniconda3/envs/* | sort -hr
```

#### Windows (PowerShell)

```powershell
Get-ChildItem "C:\Users\<username>\Anaconda3\envs" |
  ForEach-Object {
    $size = (Get-ChildItem $_.FullName -Recurse | Measure-Object Length -Sum).Sum / 1MB
    [PSCustomObject]@{Env=$_.Name; SizeMB=[math]::Round($size,2)}
  } | Sort-Object SizeMB -Descending
```

- Lists each environment with its size in MB
- Sorted from largest to smallest

---

### ✅ Workflow Recap

1. **Check env sizes** (sorted)
    - Linux/macOS: `du -sh ~/miniconda3/envs/* | sort -hr`
    - Windows: PowerShell snippet above
2. **Delete environment**
    
    ```bash
    conda remove --name myenv --all
    ```
    
3. **Clean caches**
    
    ```bash
    conda clean -a -y
    ```
    