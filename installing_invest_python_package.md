# Installing the InVEST python package

## Suggested method

**Pattern:**
```
conda create -y -n <name> python=<python version>
conda activate <name>
conda install -y -c conda-forge gdal=<gdal version>
pip install natcap.invest[ui]==<invest version>
```
Replace `<name>` with any name you'd like to give your environment.
Replace `<python version>` with a python version known to be compatible with the desired invest version.
Replace `<gdal version>` with a GDAL version known to be compatible with the desired invest version.
Replace `<invest version>` with the desired invest version.

Most of the time, it is not really necessary to specify the versions of `python`, `gdal`, and `natcap.invest`. If you do not specify a version, the latest version will be installed. Usually the latest versions are compatible with each other, but not always. Specifying versions that are known to work can prevent some problems. You can find the supported range of GDAL versions in the [requirements.txt](https://github.com/natcap/invest/blob/main/requirements.txt) (be sure to switch to the desired release tag in the dropdown).

This is not the only way to do it. There are other virtual environment tools and other ways to install GDAL. 

**Example for InVEST 3.9.1:**
```
conda create -y -n invest391 python=3.9.7
conda activate invest391
conda install -y -c conda-forge gdal=3.3.1
pip install natcap.invest[ui]==3.9.1
```

**Condensed into one line:**
```
conda create -y -c conda-forge -n invest391 python=3.9.7 gdal=3.3.1 && conda activate invest391 && pip install natcap.invest[ui]==3.9.1
```

## Details
Here is an explanation of what the commands are doing:
### 1. Create a brand-new environment with the correct python version.
   `conda create -y -n <name> python=<python version>`
   
   To be safe, you should **always install `invest` into a brand-new virtual environment**. This way you can be sure you have all the right versions of dependencies. Many issues with installing or using the `invest` package arise from dependency problems, and it's a lot easier to create a new environment than it is to fix an existing one.
   
### 2. Activate the brand-new environment just created.
   `conda activate <name>`

   If you run `conda list` after this, you'll see the specified python version is there along with around 15 other packages that are included with python by default. None of these are specific to invest. You're now in an isolated environment so you can control which versions of dependencies are available to invest.
   
### 3. Install GDAL before installing invest
   `conda install -y -c conda-forge gdal=<gdal version>`
  
   This is important because GDAL is not an ordinary python package. When you install the `natcap.invest` package in step 4, `pip` will also install all the dependencies of `natcap.invest`. When `pip` tries to install GDAL, you will get an error unless the underlying GDAL binaries are already installed. That's because the `gdal` package that `pip` would install is just a python wrapper that depends on the GDAL binaries. GDAL itself is not a python package and can't be installed with `pip`. Luckily, it can be installed with `conda`!
   
### 4. Install invest
   `pip install natcap.invest[ui]=<invest version>`
  
   `pip` will also install the correct versions of all dependencies of `natcap.invest`.
   
   The `[ui]` is a package extra. It tells `pip` to also install all the dependencies needed for the invest UI. Since sometimes we don't need to use the UI at all, the basic `natcap.invest` package does not include them. If you know you won't need the UI, you can leave them out: `pip install natcap.invest=<invest version>`. If you do try to use the UI without having installed the UI dependencies, you'll get an error.