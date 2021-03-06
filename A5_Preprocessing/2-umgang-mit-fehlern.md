# C3.2 Umgang mit Fehlern

## Grundsätzliche Möglichkeiten

* Removal of feature vector
* Removal of features
* Special handling: Invalidity lists
* Correction / estimation: replacement by
  * mean, median, minimum, maximum
  * nearest neighbor
  * linear interpolation

## Beispiel DAX

### Ersetzen eines nan durch mean, median, minimum, maximum (`fillna()`)

```python
import pandas as pd;
import numpy as np;
X = pd.DataFrame({
   "jahr": [2010, 2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018, 2019],
    "dax": [6914.19, 5898.35, 7612.39, 9552.16, 9805.55, np.nan, 11481.06, 2917.64, 10558.96, 13249.01] 
   })

ersatzwert = X["dax"].mean() 
X["dax"].fillna(ersatzwert, inplace = True)
X
```

### Übung

Versuchen sie ein Ersetzen mit dem Minimum, Maximum oder Median. Zeichen Sie ein Histogramm nach Ersetzung.

### Removal of Feature-Vector (`dropna()`)

```
X = pd.DataFrame({
   "jahr": [2010, 2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018, 2019],
    "dax": [6914.19, 5898.35, 7612.39, 9552.16, 9805.55, np.nan, 11481.06, 2917.64, 10558.96, 13249.01] 
   }
  )
XC = X.dropna()
XC
```

