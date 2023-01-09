### This details how to add your own code folders that are underdevelopment to your conda python path

You should not use PYTHONPATH variable with conda python installs as they can lead to the wrong versions of packages being used.
Instead you can have a .pth file in your conda site.packages directory that will add
to your path

see: http://evantilton.com/guides/anacondapythonpath/

- have to do this for each env
- in python do:

```
import sys
print(sys.path)
```

- This will show you where the conda env site packages file is (e.g. `/home/c/cgeorge/conda/obds_conda/envs/cgat-f-2020/lib/python3.6/site-packages`)
- in this location add a file called `.pth` e.g. `my_code_repos.pth` (You can do this using `conda develop`)
- for each repo add the path to a separate line in that file
- save file and reactivate conda env and test its worked using `print(sys.path)`

Should also be able to do it using `conda develop` from `conda-build` package (need to install conda build first into conda base env) 
https://docs.conda.io/projects/conda-build/en/latest/resources/commands/conda-develop.html?highlight=conda-develop

1. Make sure you have conda installed
2. Install conda-build (library for creating conda packages) in your base environment
