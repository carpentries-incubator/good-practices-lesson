---
title: Setup
---

## Software Setup

::::::::::::::::::::::::::::::::::::::: discussion

### Details

1. Git is required for this lesson. Please follow [this link](https://carpentries-incubator.github.io/collaborative-git-and-github-lesson/) for detailed setup instructions. 
2. Additionally you want to install [Miniconda](https://docs.anaconda.com/miniconda/) and dependencies.
There are different ways of installing it, we describe below a quick command line install. If you are not comfortable with it, please refer to [this installation](https://docs.anaconda.com/miniconda/install/#installing-miniconda) using graphical installer.

Note: Of course, you can use `venv` and `pip`, but those will not be covered here.

:::::::::::::::::::::::::::::::::::::::::::::::::::

:::tab
### Windows

When using Windows PowerShell run the following.
These three commands quickly and quietly download the latest 64-bit Windows installer, rename it to a shorter file name, perform a silent install, and then delete the installer:

```bash
wget "https://repo.anaconda.com/miniconda/Miniconda3-latest-Windows-x86_64.exe" -outfile ".\miniconda.exe"
Start-Process -FilePath ".\miniconda.exe" -ArgumentList "/S" -Wait
del .\miniconda.exe
```

### Mac

These four commands download the latest macOS installer (for your chosen chip architecture), rename it to a shorter file name, perform a silent install, and then delete the installer.

```bash
mkdir -p ~/miniconda3
curl https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-x86_64.sh -o ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm ~/miniconda3/miniconda.sh
```
Note, for Apple Silicon you replace `x86_64` with `arm64`.

### Linux

```bash
mkdir -p ~/miniconda3
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm ~/miniconda3/miniconda.sh
```
:::

After installing, close and reopen your terminal application or refresh it by running the following command:

```bash
source ~/miniconda3/bin/activate
```

Create a conda environment and install `pytest`.

```bash
conda create --name myenv
conda activate myenv
conda install pytest
```

You should now have a conda environment with pytest in it. Verify the environment:

```bash
python --version
pytest --version
```

which should return something like:

```output
Python 3.13.1
pytest 8.3.4
```

To deactivate the environment, run

```bash
conda deactivate
```