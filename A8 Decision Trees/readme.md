# Grundidee

Wir versuchen einen Entscheidungsbaum zu konstruieren, der als Eingabe einen Feature-Vektor nimmt und als Ausgabe die zugeordnete Klasse. 

Zur Vereinfachung wählen wir im nächsten Beispiel nur *versicolor*- und *viriginica*-Datensätze aus, arbeiten also mit zwei Klassen und 100 Datensätzen.

Ein möglicher Entscheidungsbaum sieht dann so aus:

![Einfacher (und schlechter) Entscheidungsbaum](readme.assets/image-20211129091334434.png)

Jeder Knoten beschreibt (in Klammern die Werte für den obersten Knoten, auch Wurzel/Root genannt):

- die Anzahl der Datensätze, die in den Knoten fließen (#100)
- die Anzahl der Datensätzen mit den einzelnen Klassen (#50 / #50)
- die Qualität des Knotens (dazu später mehr)
- die Prediction, die für Datensätze dieses Block getroffen wird (hier *versicolor* - warum??). 
- das Kriterium für die weitere Aufspaltung.

Sie können die Zahlen mit Excel nachvollziehen oder - schneller - mit folgenden kleinen Programmen berechnen.

Bitte beachten:

- In einem Knoten darf nur *ein* *Feature* mit einer Vergleichsoperation abgefragt werden
- Die Baumhöhe ist definiert durch: Anzahl der Knotenebenen unter dem Wurzelknoten (in obigem Baum 1).
- Die Modellfamilie ist die Menge aller Bäume einer bestimmten Höhe.

## Python

### Auswahl von versicolor und virginica

Die letzte Zeile ist entscheidend. Der Rest unterscheidet sich nicht vom bereits bekannten Ladevorgang.

```python
import pandas as pd
from sklearn import datasets

iris = datasets.load_iris()
iris_df = pd.DataFrame(iris.data)
iris_df['class']=iris.target_names[iris.target ]
iris_df.columns=['sepal_len', 'sepal_wid', 'petal_len', 'petal_wid', 'class']
iris_df = iris_df[50:]
```

### "Manuelle Abfrage" von Werten

```python
filter_crit = (iris_df["petal_len"] <= 4)
filter_ver  = (iris_df["class"] == "versicolor")
filter_vir  = (iris_df["class"] == "virginica")


print( "Total      : ", iris_df[ filter_crit]["class"].count() )
print( "Versicolor : ", iris_df[ filter_crit & filter_ver]["class"].count() )
print( "Virginica  : ", iris_df[ filter_crit & filter_vir]["class"].count() )
```



# Berechnung des optimalen Baums 

Unsere Modellfamilie ist nun die Menge aller Bäume der Höhe zwei und wir versuchen den besten Baum im Sinne der *Accuracy* zu finden. Dazu hilft uns Python:

![Optimaler Baum der Höhe 1](readme.assets/image-20211129092942002.png)

## Übung

1. Berechnen sie die Werte in den Knoten mit dem Phython-Programm aus dem vorhergehenden Abschnitt.
2. Welche Accuracy hat dieser Baum?



## Python

```python

X = iris_df.sample(frac=1).reset_index(drop=True)
y = X['class']
X = X.drop(['class'], axis=1)

print(f'\nShape of Feature Matrix : {X.shape}')
print(f'\nShape of Labels : {X.shape}')

clf = DecisionTreeClassifier(random_state=1234, criterion = 'gini', max_depth=1)
model = clf.fit(X, y)

fig = plt.figure(figsize=(8,8))
p = tree.plot_tree(clf
                   , feature_names=X.columns
                   , class_names=['versicolor', 'virginica']
                   , filled=True
                   )
```