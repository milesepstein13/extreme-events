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

TODO: Beef this up with writing from proposal and sources, etc. If this is an ok format for the final report (to ask)


First, we will access the necessary data from LENS1

```python
import intake
import xarray as xr

import intake_esm

# CESM LENS1 URL:
url ="https://raw.githubusercontent.com/NCAR/cesm-lens-aws/main/intake-catalogs/aws-cesm1-le.json"
cat = intake.open_esm_datastore(url)
cat_subset = cat.search(
    experiment=["CTRL","20C","HIST", "RCP85"],
    #TODO: Add other variables here
    long_name=['total (convective and large-scale) precipitation rate (liq + ice)'], 
)
dset_dict = cat_subset.to_dataset_dict(zarr_kwargs={"consolidated": True}, storage_options={"anon": True})
```

```python
[key for key in dset_dict.keys()][:10]
cat_subset.df.tail()
```

```python
unique = cat.unique()
unique
unique['long_name']
unique['units']
cat
```

```python
ds_RCP = dset_dict["atm.RCP85.daily"]
ds_CTRL = dset_dict["atm.20C.daily"]


# Select Just at Vancouver's coordinates

# just NE of Vancouver (to ensure we're over land)
van_lon = 236.9
van_lat = 49.3
ds_RCP = ds_RCP.sel(lat = van_lat, lon = van_lon, method='nearest')
ds_RCP
ds_CTRL = ds_CTRL.sel(lat = van_lat, lon = van_lon, method='nearest')
ds_CTRL


```

First, we will look at the distribution max temps in the past climate TODO: Define past climate. Control? Current

```python
# is the ctrl usable for this? ask. 
# save datasets to be usable
import matplotlib.pyplot as plt
#control = ds_CTRL.TREFHTMX[0, :].to_numpy()
ds_CTRL.PRECT.to_dataframe().to_csv('data/20c_precip.csv')
ds_RCP.PRECT.to_dataframe().to_csv('data/rcp_precip.csv')
```

Based on that, we need to define what we mean by an "extreme event"

```python
plt.hist(control, 100)
```

Therefore, in the past the frequency of extreme events was:

```python
# will want to include error bars if possible. Ask rachel about this in class
```

Now, we can look at the distribution of max temps in the future. We can determine the mean trend in max temperatures over the time period

```python
import numpy as np
import pandas as pd
np.savetxt('data/maxtemps_ctrl.csv', control)
```

If the only temperature changes were according to this trend (no change in the distribution), we can find the predicted distribution of max temperatures

```python
test = pd.read_csv('data/maxtemps_ctrl_test.csv')
test
```

And count the frequency of extreme events:

```python

```

Now, we can see how this compares to the frequency of extreme events directly modelled:

```python

```

So, we can discuss....
