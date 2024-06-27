# liesel-install-jss

Make sure you have Conda, Mamba or Micromamba installed, then run:

```
conda env create -f environment.yml

# alternatively, if the first environment does not work, try:
# conda env create -f environment-fix.yml

conda activate liesel-install-jss
Rscript -e "remotes::install_github('liesel-devs/rliesel')"
quarto render test-install.qmd
```
