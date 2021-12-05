# Feature Engineering

Für die meisten Machine Learning Modelle werden wir Feature-Daten löschen, neu erzeugen,  oder modifizieren.

Zur Vorbereitung lesen sie die Originaldate in den Dataframe mit dem `df_original `ein. Verwenden sie die csv-Datei t_itanic\_train.csv_ auf Moodle.

```
from google.colab import drive
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

drive.mount('/content/drive')
df_original = pd.read_csv("/content/drive/My Drive/Colab Notebooks/data/titanic_train.csv")
```

## Löschen

In der Analyse kann sich ergeben, dass bestimmte Daten in keiner Weise den Label beeinflussen (was immer damit gemeint ist..). Diese Spalten lassen wir weg, um den Datensatz klein zu halten.

Für Titanic löschen wir die Spalten `Name, PassengerId, Ticket und Cabin. `

```
df = df_original
df = df.drop(['Name','PassengerId','Ticket','Cabin'], axis=1)
```

## Nominale Kategoriewerte  in Zahlen umwandeln

Wenn wir mit Daten rechnen wollen, müssen wir Strings vermeiden. Dies betrifft die  features `Sex` und Embarked. Wir  ersetzen für `Sex` den Wert `male `durch 0 und den Wert `female `durch 1&#x20;

```
df['Sex'] = df["Sex"].map( {'male': 0, 'female': 1} ).astype(int)
```

## Missing-Values ergänzen

Missing Values sind hinderlich, da sie mathematische Operationen unmöglich machen. Wir haben missing values in den Spalten `Age `und `Embarked`

### `Feature Embarked`

Für zwei Datensätze fehlt Werte für das Feature`  Embarked.  `Wir setzen deren Wert auf den Wert, der in der Spalte am häufigsten vorkommt.  Wir haben oben schon gesehen, dass dies der Wert "S" ist, rechnen diesen Wert aber mittles `mode() `nochmals aus. (Lesen sie [hier ](https://en.wikipedia.org/wiki/Mode\_\(statistics\))mehr zum Modus einer Spalte.)&#x20;

```
freq_port = df["Embarked"].mode()[0]  # returns the values, that appears most often
df["Embarked"] = df["Embarked"].fillna(freq_port)

print("Most frequently appearing port : ", freq_port)
print( df["Embarked"].describe() )
```

Ergebnis (nun gibt es keine NAs mehr):

![](<../../.gitbook/assets/image (62).png>)

Nun mappen wir, wie oben für `Sex`, das Feature `Embarked `auf numerische Werte:

```
df['Embarked'] = df['Embarked'].map( {'S': 0, 'C': 1, 'Q': 2} ).astype(int)
```

Nun ist `Embarked `eine numerische Spalte.&#x20;

```
df["Embarked"].describe()
```

Ergebnis:

![](<../../.gitbook/assets/image (64).png>)

### Feature Age

Wir könnten beim Alter grundsätzlich vorgehen wie oben. Hier lohnt sich aber eine Berücksichtigung des  Zusammenhangs zwischen den Features `Alter `und `Pclass`.

Aus der Auswertung der Alterswerte in Abhängigkeit von der Klasse ergibt sich ein klarer Zusammenhang.&#x20;

![](<../../.gitbook/assets/image (63).png>)

Deshalb setzen wir missing values für das Alter auf den Median der Alterswerte in der jeweiligen Klasse. Unrealistisch hohe Alterswerte behandeln wir analog. Das Programm ist etwas komplizierter, und  wir gehen nicht auf jede einzelne Zeile ein:

```
def complete_age():
  guess_ages = np.zeros((2,3))
  total = 0
  for i in range(0, 2):
        for j in range(0, 3):
            guess_df = df[ (df['Sex'] == i) & (df['Pclass'] == j+1) ]['Age'].dropna() 
            age_guess = guess_df.median()

            # Convert random age float to nearest .5 age
            guess_ages[i,j] = int( age_guess/0.5 + 0.5 ) * 0.5

  # do the replacement for null values and unrealistic high values
  for i in range(0, 2):
       for j in range(0, 3):
        df.loc[ (df.Age.isnull()) & (df.Sex == i) & (df.Pclass == j+1),'Age'] = guess_ages[i,j]
        df.loc[ (df.Age > 93) & (df.Sex == i) & (df.Pclass == j+1),'Age'] = guess_ages[i,j]
        print(f"i,j = ({i},{j})   # = {guess_ages[i,j] }")                
```

Ergebnis:

![](<../../.gitbook/assets/image (79).png>)

Die gelb markierte Zeile sagt aus dass nicht vorhandene Alterswerte für männliche Passagiere in der Klasse 2 auf 30 Jahre gesetzt wurden.

## Quantitative Features kategorisieren

Häufig sind wir nicht an den konkreten Werten quantitativer features interessiert, sondern teilen sie lieber in Gruppen ein.&#x20;

### Age (lineare Einteilung)

Wir wollen das Alter durch eine Altersgruppe ersetzen.&#x20;

```
age_labels= range(0,8)
df['AgeBand'] = pd.cut(df['Age'], len( age_labels ))
print( df[['Age','AgeBand']].groupby(['AgeBand']).count() )
print( df[[ "AgeBand"]].describe() )
```

Ergebnis:

![](<../../.gitbook/assets/image (68).png>)

Die graue Linie trennt die beiden Ausgaben. Beachten Sie den Zusammenhang der gelben Bereiche.

Da wir die AgeBands lieber mit den Zahlen 0 bis 7 nummerieren, verändern wir den Befehl nochmals in:

```
df = df_original
age_labels= range(0,8)
df['Age'] = pd.cut(df['Age'], len( age_labels ), labels=age_labels).astype(int)
print( df[[ "Age"]].describe() )
```

Ergebnis:

![](<../../.gitbook/assets/image (69).png>)

Beachten Sie, dass wir nun die Werte in Spalte Age durch Angabe des Altersbereichs ersetz haben. Unser Datensatz  sieht nun in den ersten fünf nun wie folgt aus:

![](<../../.gitbook/assets/image (70).png>)

Wir sehen nun 7 numerische features und einen Label.

### Fare (percentile Einteilung)

Wir bringen die Fares noch in eine kategorisierte Darstellung aber nun über eine percentile Einteilung.

```
fare_labels= range(0,10)
df['FareBand'] = pd.qcut(df['Fare'], len( fare_labels)) 
print( df[['Age','FareBand']].groupby(['FareBand']).count() )
```

Ergebnis:

![](<../../.gitbook/assets/image (71).png>)

Schließlich ändern wir den Befehl in ober Zeile 2 ob, so dass wir die Werte in Spalte Fare direkt durch Gruppen ersetzen.

```
df['Fare'] = pd.qcut(df['Fare'], len( fare_labels), labels=fare_labels).astype(int)
df = df.drop(['FareBand'], axis=1)
df.head()
```

Ergebnis:

![](<../../.gitbook/assets/image (72).png>)

## Abschluss

Wir haben nun einen Dataframe, der nur aus numerischen Spalten besteht (_category _zählt dazu) und keine Nullwerte mehr aufweist.

![](<../../.gitbook/assets/image (73).png>)



## Code Summary

Hier finden sie den gesamten Code als einen Text. Im Zweifel fahren Sie mit diesem Code fort, um die Daten für das nächsten Abschnitt zu erhalten.

```python
from google.colab import drive
import pandas as pd
import numpy as np

drive.mount('/content/drive')
df_original = pd.read_csv("/content/drive/My Drive/Colab Notebooks/data/titanic_train.csv")


def complete_age():
  guess_ages = np.zeros((2,3))
  total = 0
  for i in range(0, 2):
        for j in range(0, 3):
            guess_df = df[ (df['Sex'] == i) & (df['Pclass'] == j+1) ]['Age'].dropna()
            age_guess = guess_df.median()
            guess_ages[i,j] = int( age_guess/0.5 + 0.5 ) * 0.5

  # do the replacement for null values and unrealistic high values
  for i in range(0, 2):
       for j in range(0, 3):
        df.loc[ (df.Age.isnull()) & (df.Sex == i) & (df.Pclass == j+1),'Age'] = guess_ages[i,j]
        print(f"i,j = ({i},{j})   # = {guess_ages[i,j] }")

df = df_original;

# Löschen von Features #####################################
df = df.drop(['Name', 'PassengerId', 'Ticket', 'Cabin'], axis=1 )
#df.head()

# Mapping #################################################
# Sex---
df['Sex'] = df['Sex'].map( {'female':1, 'male':0   } ).astype( int )
#df.head()

# Missing Values ###########################################
# Embarked--
freq_port = df['Embarked'].mode()[0]
df['Embarked'] = df['Embarked'].fillna( freq_port )
df['Embarked'] = df['Embarked'].map( {'S':0, 'C':1, 'Q':2 } ).astype( int )
#df.info()

# Age -----
complete_age()


# Quantitative Features kategorisieren ####################
# Age --
age_labels = range(0,8)
df['Age'] = pd.cut( df['Age'], len( age_labels ), labels=age_labels ).astype( int )
df.head()

# Fare ---
fare_labels= range(0,10)
df['Fare'] = pd.qcut(df['Fare'], len( fare_labels), labels=fare_labels ).astype( int )

df.info()
```

## Übung

### Wie viele weibliche Reisenden buchten jeweils welche Klasse? Wie hoch ist jeweils deren Überlebensrate?

Lösung (Es sind alternative Lösungen möglich.):

```python
df_h = df[ df['Sex'] == 1]
df_h[ ['Survived', 'Pclass'] ].groupby('Pclass').count()
df_h[ ['Survived', 'Pclass'] ].groupby('Pclass').mean()

```



### Wie hoch ist die Überlebensrate in den jeweiligen Altersgruppe

```python
df [ ['Survived', 'Age'] ].groupby('Age').mean()
```



