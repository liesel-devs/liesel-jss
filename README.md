# liesel-jss

This repository contains detailed installation instructions for Liesel and RLiesel as well as the supplementary material for the manuscript "Liesel: A Probabilistic Programming Framework for Developing Semi-Parametric Regression Models and Custom Bayesian Inference Algorithms" by Hannes Riebl, Paul F.V. Wiemann, and Thomas Kneib. Following this README, you should be able to replicate the running example and the case studies from the manuscript.

## Installation

Liesel runs natively on Linux and macOS. On Windows, installing Liesel natively is possible but more complicated. We therefore recommend using the Windows Subsystem for Linux (WSL) to run Liesel on Windows.

### Installing WSL (only on Windows)

- Open the Windows Command Prompt in administrator mode by right-clicking and selecting "Run as administrator".
- Run `wsl --install -d Ubuntu`.
- Reboot your computer.
- Follow the instructions to set a user name and password.

For details, see [the official WSL installation instructions](https://learn.microsoft.com/en-us/windows/wsl/install).

### Installing Conda

The easiest way to install Liesel is via Conda (or Miniconda, or Mamba, or Micromamba). If you don't have any Conda variant on your system yet, we recommend installing Micromamba:

- Open a Bash shell or WSL.
- Run `"${SHELL}" <(curl -L micro.mamba.pm/install.sh)`.
- Answer the questions by pressing enter.
- Run `source ~/.bashrc`.
- Run `alias conda=micromamba`.

For details, see [the official Micromamba installation instructions](https://mamba.readthedocs.io/en/latest/installation/micromamba-installation.html).

### Installing Liesel

Clone this repository and create a Conda environment with Liesel and RLiesel installed:

```sh
git clone https://github.com/liesel-devs/liesel-jss.git
cd liesel-jss
conda env create -f environment.yml
conda activate liesel-jss
Rscript -e "remotes::install_github('liesel-devs/rliesel@v0.0.3', upgrade = FALSE)"
```

Check if Liesel and RLiesel are installed and working:

```sh
quarto render test-install.qmd
```

Don't worry if you see a few messages and warnings on your console, for example about JAX falling back to CPU or Liesel not being able to update certain nodes during initialization. The warnings about nodes not being updated are due to the fact that RLiesel constructs the model step by step, and some quantities cannot be computed before the model is complete. At the end, when RLiesel is finished, the returned model is fully functional and can be sampled with MCMC.

Verify that the file test-install.html was created and ends with the message "Liesel and RLiesel installed successfully". On Windows, you may find the file by opening the File Explorer, then clicking on Linux in the sidebar, then on Ubuntu, home, your user name, liesel-jss and test-install.html.

### Installing Liesel natively on Windows (without WSL, not recommended)

Installing Liesel natively on Windows is possible but incompatible with Conda. Instead, you need to perform the following steps manually:

- Install Python.
- Install Liesel.
- Optionally, install the [pygraphviz](https://pygraphviz.github.io/) package.
- Install R.
- Install RLiesel.
- Install [Quarto](https://quarto.org/).
- Make sure the [reticulate](https://rstudio.github.io/reticulate/) package uses the right version of Python (or the right virtual environment) and finds the Liesel package when running through Quarto.

## Supplementary material

The instructions above install Liesel and RLiesel from PyPI and GitHub, but the source code is included in the supplementary material for documentation purposes (liesel-0.3.3.zip and rliesel-0.0.3.zip).

The running example and the case studies use [Quarto](https://quarto.org/), a publishing system that allows for a seamless integration of Python and R code as well as the corresponding documentation and renders the computation results (tables and figures) to high-quality PDF or HTML documents.

### Running example: Bayesian regression

Make sure you're still in the liesel-jss directory and have the liesel-jss environment activated (see [above](#installing-liesel)), then execute the running example as follows:

```sh
quarto render supplement/1-running-example/example.qmd
```

The results are stored in the file supplement/1-running-example/example.html.

### Case study: Sampling schemes

The case study on sampling schemes requires some additional R packages:

```sh
conda install r-dplyr r-forcats r-stringr r-tidyr
Rscript -e "remotes::install_cran('SemiPar', upgrade = FALSE)"
```

Now, run the case study as follows:

```sh
quarto render supplement/2-case-study-sampling/case-study.qmd
```

*Note*: This case study was conducted with the environment variable `XLA_FLAGS=--xla_cpu_use_thunk_runtime=false` set to mitigate a performance regression caused by the new XLA backend for CPUs. We anticipate this issue will be resolved in a future update. For more details, see [this issue](https://github.com/liesel-devs/liesel/issues/242).

The results are stored in the file supplement/2-case-study-sampling/case-study.html.

### Case study: Species counts

The case study on species counts requires a git submodule, an additional Python package and a few more R packages:

```sh
git submodule update --init
pip install supplement/3-case-study-species
conda install r-dplyr r-lubridate r-patchwork r-purrr r-readr r-sf r-stringr r-tidyr
```

To replicate a part of the real-world application of Riebl, Glatthorn, and Kneib (2023), run the following command (this may take about an hour to finish!):

```sh
quarto render supplement/3-case-study-species/paper/application/rtg-2300.qmd \
    -P taxon:col -P distribution:negbin
```

The command estimates the multi-species count model (MSCM) for the taxon of collembolas with a negative binomial count distribution, including the predictor specification, the derived quantities and the MCMC scheme outlined in the JSS manuscript.

You may find the results in the directory supplement/3-case-study-species/paper/application.
