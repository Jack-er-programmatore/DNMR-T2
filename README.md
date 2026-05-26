# DNMR-T2

This repository contains a modified version of **DNMR** with an added **T2 fitting tab**.

The original **DNMR** software was developed by **Davis Garrad**.  
Original repository: https://github.com/Davis-Garrad/DNMR

The **T2 extension** was implemented by **Giacomo Panzera**.  
Contact: giacomo.panzera@psi.ch

## Note

This repository contains the **full modified DNMR source code**.  
It is **not necessary** to download the original DNMR repository separately.

## Added Feature

The new **T2 Fit** tab:

- integrates the selected frequency-domain region;
- plots the integrated signal as a function of echo time;
- fits the decay to extract **T2**.

The fitting model is: S(t) = A * exp(-(t / T2)^r) + c

## Installation

Python packages can sometimes conflict with each other, especially when different projects require different package versions.

For this reason, it is recommended to install **DNMR-T2** inside a dedicated **virtual environment**.  
This is **not mandatory**, but it helps avoid unwanted installation and compatibility errors.

The recommended Python version is **Python 3.12**.  
Higher Python versions may not work correctly with all required dependencies.

Open **PowerShell** and go to the main project folder (cd C:\Users\your_username\path_to\DNMR-T2), i.e. the folder containing: 
```text
pyproject.toml
README.md
src
```
Create and activate a virtual environment: py -3.12 -m venv dnmr-env312
                                           .\dnmr-env312\Scripts\Activate.ps1


When the virtual environment is active, the PowerShell prompt should start with: (dnmr-env312)

Install the required packages and install **DNMR-T2** from this repository:

python -m pip install --upgrade pip setuptools wheel
python -m pip install "numpy==1.26.4"
python -m pip install .
python -m pip install scipy

## pytnt Patch

In some cases, `pytnt` may raise an error related to `numpy.dual`.

If this happens, run the following command once, while the virtual environment is active:

python -c "from pathlib import Path; import sysconfig; p=Path(sysconfig.get_paths()['purelib'])/'pytnt'/'processTNT.py'; s=p.read_text(); s=s.replace('import numpy.dual as npfast', 'import numpy.linalg as npfast'); p.write_text(s); print('Patch pytnt done:', p)"

## Run DNMR-T2

With the virtual environment active, run: python -m DNMR
