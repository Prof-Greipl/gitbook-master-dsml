

# Grundsätzliche Fehlerarten

Bessere Datenqualität wird zu genaueren Ergebnissen führen. 

Mögliche Fehlerquellen: 

- Messtechnisch nicht erfassbare Änderungen des zu messenden Gegenstandes, der Messgeräte, der Umwelt und der Beobachter 

* Ablesefehler
* Tippfehler
* mangelnde Kalibrierung

* falsche Formeln
* falsches Vorzeichen (+ oder -)





# Outliers



[Outliers, Inliers, and Other Surprises that Fly from your Data | Rocket-Powered Data Science (rocketdatascience.org)](http://rocketdatascience.org/?p=473)



# Inliers und Drift

![Original Data, Inliers and Drift (Quelle: Runkler)](1-fehlerarten.assets/image-20211114183020487.png)



# Missing Data or Invalid Data

Hier handelt es sich um fehlende Daten, z.B. leere oder ungültige Zellen in Excel-Files. Was tun?

Möglichkeiten zum Umgang:

- *invalidity list*
- *invalidity value*
- *correction / estimation*; Examples:
  - *mean, median, minimum, maximum*
  - *nearest neighbor*
  - *lineare interpolation*
- *removal of feature vektor*
- *removal of feature*

&#x20;

# Python: Fehler/"Verdächtige"  finden

In diesem und den folgenden Abschnitte arbeiten wir mit folgendem dem Dataframe X. Dieser sollte immer erzeugt sein, sonst funktionieren die weiterten Beispiele nicht.

```
import pandas as pd
import numpy as np

X = pd.DataFrame({
   "jahr": [2010, 2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018, 2019],
    "dax": [6914.19, 5898.35, 7612.39, 9552.16, 9805.55, np.nan, 11481.06, 2917.64, 10558.96, 13249.01] 
   })
```



## Überblick verschaffen  mit Dataframes: `describe` und `info`

Für unsere Feature-Matrix gibt es zwei Python Befehle, die wir zum Start grundsätzlich durchführen:

```
X.describe()
X.info()
```



## Missing Values (`null`-Values, `na`-Values)

Link: https://www.bmc.com/blogs/pandas-nan-missing-data/

Der Aufruf `X.info()` sagt uns, dass nicht zu jeder Spalte alle Daten gefüllt sind.

![Info zu einem Dataframe](1-fehlerarten.assets/image-20211114185903890.png)

Folgender Befehl löscht alle Zeilen mit na-Werten aus dem Dataframe:

```python
XC = X.dropna()
```


