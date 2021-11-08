# C3.1 Fehlerarten

## Grundsätzliche Fehlerarten

### Stochastische Fehler

Quellen: Messtechnisch nicht erfassbare Änderungen der Maßkörper, der Messgeräte, des Messgegenstandes, der Umwelt und der Beobachter hervorgerufen:

* Ablesefehler
* Tippfehler
* mangelnde Kalibrierung

(Auch numerische Berechnungen, z.B. mit einem Computer, sind in der Regel nicht beliebig genau, sondern fehlerhaft.)

Quelle: [AT-6.pdf (tu-dresden.de)](https://tu-dresden.de/bu/umwelt/hydro/iak/ressourcen/dateien/systemanalyse/studium/folder-2009-01-29-lehre/folder-2009-04-03-at/AT-6.pdf?lang=de)

Modellierung durch _additive noise_.

### Systematische Fehler

Systematische Fehler: werden hauptsächlich durch Unvollkommenheiten der Maßverkörperung der Messgeräte, der Messverfahren und des Messgegenstandes sowie von messtechnisch erfassbaren Einflüssen der Umwelt und persönlichen Einflüssen der Beobachter hervorgerufen. Sie haben

* falsche Formeln,
* falsches bestimmtes Vorzeichen (+ oder -)
* unter gleichen Bedingungen den gleichen Betrag, d.h. sie können durch Wiederholung der Messung nicht festgestellt werden, sondern nur durch ein anderes (genaueres) Messgerät oder Messverfahren

Quelle: [AT-6.pdf (tu-dresden.de)](https://tu-dresden.de/bu/umwelt/hydro/iak/ressourcen/dateien/systemanalyse/studium/folder-2009-01-29-lehre/folder-2009-04-03-at/AT-6.pdf?lang=de)

## Beispiel

### Inliers und Drift

Beispiele:

![](<../../.gitbook/assets/image (11).png>)

### Outliers

![](<../../.gitbook/assets/image (21).png>)

Vertiefung:

[Outliers, Inliers, and Other Surprises that Fly from your Data | Rocket-Powered Data Science (rocketdatascience.org)](http://rocketdatascience.org/?p=473)

### Missing Data

Hier handelt es sich um fehlenden Daten. Was tun?&#x20;

## Python: Fehler finden

### Überblick verschaffen

#### describe und info

Für unsere Feature-Matrix gibt es zwei Python Befehle, die wir zum Start grundsätzlich durchführen:

```
X.describe()
X.info()
```

#### Histogramme

```
import matplotlib.pyplot as plt
import seaborn as sns

X = pd.DataFrame({
   "jahr": [2010, 2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018, 2019],
    "dax": [6914.19, 5898.35, 7612.39, 9552.16, 9805.55, np.nan, 11481.06, 2917.64, 10558.96, 13249.01] 
   }
  )

sns.set()
sns.histplot( X, 
             x ="dax", 
             binwidth=2000,
             kde = False)
plt.show()
```

&#x20;

### Missing Values (`null`-Values)

Der Aufruf `df.info()` sagt uns, dass nicht zu jeder Spalte alle Daten gefüllt sind.&#x20;

### Outliers

Wir verwenden zunächst Boxplots ([https://seaborn.pydata.org/generated/seaborn.boxplot.html](https://seaborn.pydata.org/generated/seaborn.boxplot.html))&#x20;

```
import seaborn as sns
sns.boxplot(x = X["dax"])
X.describe()
```

### Übung 1

Die Definition von Quartilen ist nicht eindeutig. Finden Sie anhand des folgenden Dataframes (und leichten Modifikationen) heraus, wie Seaborn die Quartile berechnet.

```
T = pd.DataFrame({
   "data": [1,2,3,4,5,6,7,8,9,10,11]
   }
  )
sns.boxplot(x = T["data"])
T.describe()
```

### Übung 2

Folgendes Beispiel zeigt, dass bei mehrfach auftretenden Werten Vorsicht geboten ist.

```
import seaborn as sns
T = pd.DataFrame({
   "data": [1, 1, 1, 5, 5, 5, 5, 5, 5, 5]
   }
  )
sns.boxplot(x = T["data"])
T.describe()
```
