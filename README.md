# liesel-install-jss

Make sure you have Conda, Miniconda, Mamba or Micromamba installed. If you don't have any Conda variant on your system yet, we recommend Micromamba (see [the installation instructions](https://mamba.readthedocs.io/en/latest/installation/micromamba-installation.html)). Run these commands to create a Conda environment with Liesel and RLiesel installed:

```
# if you're using mamba, create an alias like this:
# alias conda=mamba
# or on powershell:
# New-Alias -Name conda -Value mamba

# if you're using micromamba, create an alias like this:
# alias conda=micromamba
# or on powershell:
# New-Alias -Name conda -Value micromamba

conda env create -f environment.yml
conda activate liesel-install-jss
Rscript -e "remotes::install_github('liesel-devs/rliesel@v0.0.2')"
```

Now you can check if Liesel and RLiesel are installed and working with this command:

```
quarto render test-install.qmd
```

Congratulations! If the file `test-install.html` was created and ends with the message "Liesel and RLiesel installed successfully", everything worked out as expected.
