# Facefusion

## [Installation](https://docs.facefusion.io/installation) on Windows

- Set proxy via [powershell](conda.md#^377d00)
- Initiate [conda](conda.md) environment
- Install with python 3.10: `conda create --name facefusion` python=3.10
- Install ffmpeg: `conda install -c conda-forge ffmpeg`
- Clone facefusion from github
### Using the installation script

- Set https and http proxy via [powershell](conda.md#^377d00)
- `conda create --name facefusion python=3.10`
- `conda activate facefusion`
- `conda install pip`
- `git clone --depth=1 <link>`
- `python install.py --skip-venv`
- `pip install httpx[socks]`
- `pip install pysocks`
- Install cudatoolkit 11.8 from official website
- Install cudnn 9.0 from official website
- `python run.py`

### cuda

- pytorch and conda vers are not as fast as nvidia native ones

### use conda envs

- `python install.py --skip-venv`
## MacOS

- Make venv inside conda env
- Then install.py

## Windows returned black screen

This issue can be fixed using `EXHAUSTIVE` rather than `DEFAULT` in `facefusion/facefusion/execution_helper.py`

``` python
def apply_execution_provider_options(execution_providers: List[str]) -> List[Any]:
    execution_providers_with_options : List[Any] = []

    for execution_provider in execution_providers:
        if execution_provider == 'CUDAExecutionProvider':
            execution_providers_with_options.append((execution_provider,
            {
                'cudnn_conv_algo_search': 'EXHAUSTIVE'
            }))
        else:
            execution_providers_with_options.append(execution_provider)
    return execution_providers_with_options
```

> Occurs with 1660 cards

## Usage

- Long videos take more time to post-process after the status bar is filled;