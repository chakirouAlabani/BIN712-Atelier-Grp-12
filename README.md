## Data cleaning

- import
- identify categorical data
    - convert categorical to int

`Class`
```python
  {'Class 1' : 1, 'Class 2':2, 'Class 0':0, 'Class -1':-1, 'Class -2':-2}

- identify missing data
    - analyse and replace
      
 *Data with missing values*
- vsurf_V (18 values)
- vsurf_S (13 values)
- vsurf_R (7 values)
- ASA+  (2 values)
- a_heavy (1 value)
- ASA- (1 value)
- a_IC (1 value)

*Before replacing missing data, it was decided to identify and replace/remove outliers

- identify outliers 
    - analyse and replace/remove

*Using error bar of mean for each feature, the following features were identified as having outliers :*
**Features with smaller error margins were not considered outliers**
- CASA- (10 values out of bounds)
- DCASA (10 values out of bounds)
- pmi (14 values out of bounds)
- pmi2 (11 values out of bounds)
- pmi3 (10 values out of bounds)
- vsurf_R (*1 value below lower_boundary*)

*A histogramme of the Data distribution of each feature was done and one feature stood out as having the outlier be removed*
- vsurf_R

*The remaining Features were managed using the upper boundary as replacement value for all outliers outside this boundary*

`For each feature:`
```python
  Q1 = data1['pmi'].quantile(0.25)
  Q3 = data1['pmi'].quantile(0.75)
  IQR = Q3 - Q1
  upper_boundery = Q3 + 1.5*IQR
  
  condition = data1['pmi']>upper_boundery
  condition.sum() # 14 values are outside the upper_boundary
  data1['pmi'][data1['pmi']>Q3] = upper_boundery

