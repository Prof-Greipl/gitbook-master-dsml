---
description: >-
  Pandas ist eine Bibliothek um Daten in Excel-ähnlicher Form einfach zu
  analysieren.
---

# Diving into Dataframes

## Diving into Dataframes

Ein Dataframe ist eine Tabellenstruktur von Daten. Bitte beachten Sie zu diesem Abschnitt auch die Videos 11a bis 11f meiner [DSML-Playlist](https://youtube.com/playlist?list=PLfGN40VwjduJPvtP9QUjC0rjM6-ePT9bg)

## Beispiel

```python
import pandas as pd
df = pd.DataFrame({
   "Name": ["Braund, Mr. Owen Harris",
            "Allen, Mr. William Henry",
          "Bonnell, Miss. Elizabeth"],
    "Age": [22, 35, 58],
   "Gender": ["male", "male", "female"]}
  )

# Dataframe ausgeben
print( "\n -------- Data")
print( df )
print( df.shape)

print( "\n -------- Head")
print( df.head(2) )

print( "\n -------- Tail")
print( df.tail(2) )

print( "\n -------- Anzahl der Zeilen")
print( len(df))
```

### Information zum Dataframe

```python
df.info() 
```

![](<../../../.gitbook/assets/image (13).png>)

Der Aufruf `df.colums.values` liefert die Spaltennamen als Array.

```python
print( df.colums.values )
```

### Einfache Statistik

```python
df.describe()
```

![](<../../../.gitbook/assets/image (12).png>)

## Spalten (Series)

Eine Spalte eines Dataframes heist auch _Series._

![](<../../../.gitbook/assets/image (11).png>)

```python
# Eine Spalte aus dem Dataframe herausnehmen
spalte1 = df["Age"]
print( spalte1 )
print( spalte1.dtype )
print( spalte1.shape )
print( type( spalte1 ) )
```

#### Verschiedene Werte in einer Spalte

```python
print( df["Gender"].unique() )
```

#### Anzahl der verschiedenen Werte in einer Spalte

```python
print( df["Gender"].value_counts())
```

#### Operationen auf Spalten (min, max, sum)

```python
print("\n\n Summe/Maximum/Minimum über eine numerische Spalte:")
print( sum(df["Age"]))
print( max(df["Age"]))
print( min(df["Age"]))

print("\n\n Beispiel: Durchschnittsalter:")
avg_age = sum(df["Age"]) / len( df )
print( avg_age )
```



## Teile aus Dataframes auswählen

Wir bearbeiten die gleiche Tabelle, wie oben:

```python
import pandas as pd
df = pd.DataFrame({
   "Name": ["Braund, Mr. Owen Harris",
            "Allen, Mr. William Henry",
          "Bonnell, Miss. Elizabeth"],
    "Age": [22, 35, 58],
   "Gender": ["male", "male", "female"]}
  )
```

### Spalten auswählen

Durch Angabe der Überschriften lassen sich  Dataframes auf ausgewählte Spalten (unten gelb) reduzieren und dadurch verkleinern:

![](<../../../.gitbook/assets/image (14).png>)

```python
df1 = df[["Age","Gender"]]
```

### Zellen lesen und verändern

Sie können eine Zelle über den Zeilen und Spaltenindex ( wie eine Matrix) lesen und ändern.

```python
print( df.iloc[0,0])
df.iloc[0,0] = "Hans, Huber"
df.iloc[0,1] = 40
print( df )
```

Ausgaben:&#x20;

![](<../../../.gitbook/assets/image (20).png>)



### Teile nach Zeilennummern und Spaltennummern auswählen

![](<../../../.gitbook/assets/image (19).png>)

```python
df_1 = df.iloc[1:3, 0]
print( df_1)
```

### Filtern: Kriterien und Treffer

Beim Filtern erzeugen wir eine künstliche Spalte mit "Treffern". Wenn die Tabelle in der jeweiligen Zeile den Werte `False `enthält, kommt sie nicht durch den Filter. &#x20;

```python
```

![](<../../../.gitbook/assets/image (18).png>)

```python
import pandas as pd
df = pd.DataFrame({
   "Name": ["Braund, Mr. Owen Harris",
            "Allen, Mr. William Henry",
          "Bonnell, Miss. Elizabeth"],
    "Age": [22, 35, 58],
   "Gender": ["male", "male", "female"]}
  )

print("\n\n Ausgangsdaten:")
print(df)


# Treffer Vektor
print("\n\n Treffer Vektor für Weiblich:")
treffer_gender = df["Gender"] == "female" 
print( treffer )

df_male = df[ (treffer_gender) ]
print ( df_male )

#Alternativ (und häufig genutzt) kann die 
#Bedigung direkt in die eckige Klammer gesetzt werden
print("\n\n Weiblich:")
df_male = df[ df["Gender"] == "female" ]
print ( df_male )

print("\n\n Älter als 30:")
df_aelter_als_dreissig = df[ df["Age"] > 30 ]
print ( df_aelter_als_dreissig )

print("\n\n Nur Name und Alter, der Personen als 30:")
df_aelter_als_dreissig_1 = df[ df["Age"] > 30 ]
print ( df_aelter_als_dreissig_1[['Name', 'Age'] ] )

print("\n\n Was ist das?")
df_xx = df[ (df["Age"] > 30) |  (df["Gender"] == "female") ]
print ( df_xx )

print("\n\n Und das?")
df_xx = df[ (df["Age"] > 30) &  (df["Gender"] == "female") ]
print ( df_xx )


```

## Sortieren nach einer Spalte

```python
df.sort_values(by="Age", ascending=False)
```

## Gruppieren

Sie kennen "Gruppieren" aus SQL (group by). Hier heißt es nur etwas anders. Sie verstehen die Funktion anhand der Ergebnisse.

```python
print("\n\n Guppierung:")
grouping = df.groupby(['Gender'])

print("\n\n count:")
print (grouping.count())

print("\n\n mean:")
print (grouping.mean())

print("\n\n min:")
print (grouping.min())

print("\n\n max:")
print (grouping.max())

print("\n\n median:")
print (grouping.median())
```

## Dataframes und Numpy-Arrays

#### Spalte aus numpy-Array erzeugen

```python
w = np.array([70.4, 70.5, 70.6])
weight = pd.Series(w, name="Weight")
print( weight);
print( type( weight) )
```

### Numpy-Array aus Dataframe erzeugen

```python
A = df[["Age"]].to_numpy()
print(A)
print(A.shape)
```

### Dataframe aus Numpy-Array erzeugen

```python
A = np.array([[1, 2], [3.1, -4.2]])
df2 = pd.DataFrame(data=A, index=["r1", "r2"], columns=["c1","c2"])
print( df2 )
```

## Dataframes aus Excel-Files erzeugen&#x20;

> Für Titanic lesen Sie bitte die Daten aus der csv-Datei ein!

#### Google-Drive vorbereiten

Folgenden Code brauchen Sie pro Sitzung nur einmal ausführen. Danach können Sie auf ihr Google-Drive zugreifen.

```python
from google.colab import drive
drive.mount('/content/drive')
```

Erzeugen Sie in Google-Drive ein unter `Colab Notebooks `ein  Verzeichnis `data.`

![](<../../../.gitbook/assets/image (15).png>)

Kopieren sie nun die Excel-Dateien auf Moodle in das Verzeichnis `data. `Lesen sie nun die Excel-Datei `titanic_train.xlsx` ein ein Dataframe ein.&#x20;

```python
import pandas as pd
df = pd.read_excel("/content/drive/My Drive/Colab Notebooks/data/titanic_train.xlsx")
```

## Dataframes aus csv-Files erzeugen

```python
from google.colab import drive
import numpy as np
import pandas as pd

drive.mount('/content/drive')
df = pd.read_csv("/content/drive/My Drive/Colab Notebooks/data/titanic_train.csv")
```

