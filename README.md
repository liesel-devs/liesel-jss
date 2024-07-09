# liesel-install-jss

Liesel runs natively on Linux and macOS. On Windows, installing Liesel natively is possible but more complicated. We therefore recommend using the Windows Subsystem for Linux (WSL) to run Liesel on Windows.

## Installing WSL on Windows

- Open the Windows Command Prompt in **administrator** mode by right-clicking and selecting "Run as administrator".
- Run `wsl --install`.
- Reboot your computer.
- Follow the instructions to set a user name and password.

For details, see [the official WSL installation instructions](https://learn.microsoft.com/en-us/windows/wsl/install).

## Installing Conda

The easiest way to install Liesel is via Conda (or Miniconda, or Mamba, or Micromamba). If you don't have any Conda variant on your system yet, we recommend installing Micromamba:

- Open a Bash shell or WSL.
- Run `"${SHELL}" <(curl -L micro.mamba.pm/install.sh)`.
- Answer the questions by pressing enter.
- Run `source ~/.bashrc`.
- Run `alias conda=micromamba`.

For details, see [the official Micromamba installation instructions](https://mamba.readthedocs.io/en/latest/installation/micromamba-installation.html).

## Installing Liesel

Clone this repository and create a Conda environment with Liesel and RLiesel installed:

```
git clone https://github.com/hriebl/liesel-install-jss.git
cd liesel-install-jss
conda env create -f environment.yml
conda activate liesel-install-jss
Rscript -e "remotes::install_github('liesel-devs/rliesel@v0.0.2')"
```

Check if Liesel and RLiesel are installed and working:

```
quarto render test-install.qmd
```

Congratulations! If the file test-install.html was created and ends with the message "Liesel and RLiesel installed successfully", everything worked out as expected. On Windows, you may find the file by opening the File Explorer, then clicking on Linux in the sidebar, then on Ubuntu, home, your user name, liesel-install-jss and test-install.html.
