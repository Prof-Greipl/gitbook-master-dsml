---
description: >-
  Für diesen Abschnitt untersuchen wir Spalten mit quantitativen Werten. Die
  Werte sind in der Regel über einen größeren Bereich verstreut und erlauben
  sinnvolle Rechenoperationen.
---

# Analyse quantitativer Spalten

## Maximum, Minimum, Durchschnitt, Quantile

Hier geht es um die Frage, wie sich die Werte in den einzelnen Spalten verteilen. Wir wissen zum Beispiel schon, dass die Spalte `Age`87 verschiedene Werte enthält. Wir wollen untersuchen, wie sich die 87 Werte auf die 819 Datensätze verteilen. Halt, aus der `missing values` Untersuchung wissen wir schon, dass es nur 714 Datensätze mit einem gültigen Eintrag gibt.&#x20;

Wir starten immer mir dem Aufruf  `describe()  `Er gibt uns für jede numerische Spalte einen Informationen zu

* Anzahl der verfügbaren  Werte (wussten wir schon)
* minimalen, maximalen und durchschnittlichen Wert
* Standardabweichung
* Quantile (lesen Sie mehr dazu [hier](https://de.wikipedia.org/wiki/Empirisches\_Quantil#Spezielle\_Quantile))

Bitte machen sie sich klar, dass nicht alle Werte einen Sinn haben. Wie wollen wir die durchschnittliche Passagiernummer interpretieren.  Mehr zur describe()-Funktion finden Sie [hier](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.describe.html).

```
df.describe()
```

![](<../../../.gitbook/assets/image (98) (1).png>)

## Werte mit Histogrammen visualisieren

Für Spalten mit Zahlen können wir uns durch Histogramme einen Überblick über die Verteilung der Werte verschaffen.  Nachfolgende Befehl gibt eine Darstellung der Verteilung der Werte in der Spalte `Age `mit 40 bins.

```python
# Example 1
import seaborn as sns
import matplotlib.pyplot as plt
sns.histplot(data=df[ df["Age"] < 81], x="Age", bins=40, stat="count")
```

Ergebnis:

![](<../../../.gitbook/assets/image (85).png>)

## Boxplots

Folgende Grafik illustriert das Konzept eines Boxplots

![](<../../../.gitbook/assets/image (50).png>)

Wir erzeugen einen Boxplot anhand einer exemplarischen Spalte mit den Zahlen von 1 bis 100.

```python
df_test = pd.DataFrame( data= np.arange(1,101), columns = ["Werte"])
sns.boxplot(x = df_test["Werte"])
```

Ergebnis:

![](<../../../.gitbook/assets/image (49).png>)

Hängen wir nun die Zahl 160 als weiteren Wert an, so erhalten wir einen _Outlier_. Der Boxplot wie folgt aus:

```python
v = np.append( np.arange(1,101),  [160])
df_test = pd.DataFrame( data= v, columns = ["Werte"])
sns.boxplot(x = df_test["Werte"])
```

![](<../../../.gitbook/assets/image (51).png>)

Boxplots geben uns also Auskunft über die Streuweite von Werten, also darüber, ob es Ausreißer gibt, und wie eng die Werte sich um den Median gruppieren.

## Übungen&#x20;

### Übung Histogramme (zum Befehlsblock _Example 1_)

1. Weshalb  ist es sinnvoll, den Dataframe in Zeile 3  zu verändern?
2. Experimentieren Sie mit den dem Wert für `bins`. Ist 40 ein guter Wert?
3. Visualisieren Sie auch die anderen numerischen Spalten.

### Übung Boxplots

Erzeugen Sie  Boxplots für die quantitativen Spalten der Titanic -Daten und interpretieren sie die Ergebnisse.

