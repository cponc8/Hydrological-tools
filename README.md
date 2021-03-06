# CemaNeige

## Overview
Python object to run the CemaNeige snow accounting routine (Valéry et al 2014, see reference).

First run of the model will take longer as time is needed for compilation.

## Prerequisites
* Python3 software

* Python3 packages: pandas, numpy, csv and numba 

## Content
* **CemaNeige.py**: Python object to run the CemaNeige snow accounting routine.

* **MyCatchment_CemaNeigeInfo.csv**: datafile containing CemaNeige parameters for an imaginary catchment. QNBV: average annual snow accumulation [mm], AltiBand: quantiles of elevation [m], Z50: median altitude [m].

* **MyCatchment_data.csv**: Synthetic time series of Dates (Date), total precipitation (p, [mm]) and air temperature (tair, [°C])

## Reference
Valéry A., Andréassian, V. and Perrin, C.: "As simple as possible but not simpler": What is useful in a temperature-based snow-accounting routine? Part 2 - Sensitivity analysis of the Cemaneige snow accounting routine on 380 catchments, Journal of Hydrology, 517, 1176-1187, doi={10.1016/j.jhydrol.2014.04.058}, 2014.

## Working exemple
```python

# Load objects
import pandas as pd
import CemaNeige

# Declarations
CtchName = 'myCatchment'
datafile = '%s_data.csv' % (CtchName)

# Load data
data = pd.read_csv(datafile,sep=',',header='infer')
data['Date'] = pd.to_datetime(data['Date'],format='%Y-%m-%d %H:%M:%S')
Date = data['Date']
inSnow = np.array( (data['p'], data['tair']) )

# Run CemaNeige
SnowM = CemaNeige(CtchName)
melt = SnowM.RunModel(inSnow,Date)        
                
```
