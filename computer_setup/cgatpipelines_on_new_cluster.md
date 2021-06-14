Installing cgat pipeline code on new cluster

1) Export conda envirnoment.yml file from old cluster using `conda --no-build`
2) On new cluster - download `miniconda3` in home -> follow workshop - reset channels so `conda-forge` is at top
3) Install mamba in `base` enviroment
4) create env from `yml` file using `mamba`

5) when source conda there is an issue with the system conda interfering
    - use sed to remove it from the path before source
    - then source conda
    - conda activate base
    - conda deactivate # otherwise will not prepend path correctly when change env
    # test by doing which python in different environments
    - conda activate base
    - conda activate environment_new (check python path - should now be ok)

    - need to put conda activate in if PS1 so that conda env will be inherited correctly
    when running pipelines

6)installing cgatcode 
- install cgatapps via conda mamba install to get all dependencies
- mamba remove --force cgatapps (just removes cgatapps)
- update cython conda install cython=0.29 to install cgatapps repo
- download cgatapps repo
- python setup.py develop
- download cgatflow
- python setup.py develop


- installed juptyer lab
- installed dataclasses
