---
jupyter:
  jupytext:
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.14.4
  kernelspec:
    display_name: Python 3 (ipykernel)
    language: python
    name: python3
---

# Final Project: Extreme Events
## ATSC 448
## Miles Epstein

Our goal is to investigate how climate change can cause extreme events--both by shifting mean climate values and by changing flow patterns and thus natural variability. To do this, we will find the frequency of extreme event in the past climate, determine trends in mean climate values over the course of LENS1 simulations, and calculate the expected frequency of those extreme events if the only change to the climate was that change in mean. Then, we will compare these frequencies to the frequencies in the modelled future climate.


First, we will access the necessary data from LENS1

```python
import intake
import xarray as xr

import intake_esm

# CESM LENS1 URL:
url ="https://raw.githubusercontent.com/NCAR/cesm-lens-aws/main/intake-catalogs/aws-cesm1-le.json"

```

```python
test
```
