# liesel-install-jss

Make sure you have Conda, Miniconda, Mamba or Micromamba installed, then run:

```
conda env create -f environment.yml
conda activate liesel-install-jss
Rscript -e "remotes::install_github('liesel-devs/rliesel')"
quarto render test-install.qmd
```

Congratulations! If the file `test-install.html` was created and ends with the message "Liesel and RLiesel installed successfully", everything worked out as expected.
