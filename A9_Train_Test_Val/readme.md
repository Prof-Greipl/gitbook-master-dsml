## Aufteilung in Training-Set und Test-Set

Wir teilen unseren Datensatz in einen Trainings-Teil und einen Test-Teil auf.

![](<../../.gitbook/assets/image (107).png>)

| Menge       | Beschreibung                                                 |
| ----------- | ------------------------------------------------------------ |
| X_train     | Dataframe mit Feature-Vektoren der Trainings-Set             |
| y_train     | Dataframe mit Label-Vektor des Trainings-Sets                |
| X_test      | Dataframe mit Feature-Vektoren der Test-Sets                 |
| y_test      | Dataframe mit Label-Vektor des Trainings-Sets                |
| TRAIN_SPLIT | Anzahl der Examples im Training-Set, der Rest geht zum Test-Set |



## Decison-Tree mit Iris

### Aufteilung in Training- und Test-Set

Wir nutzen hier noch keine Validierung. Die Variable TRAIN_SPLIT enthält die Anzahl der Examples aus dem Training-Set.

```python
from matplotlib import pyplot as plt
from sklearn import datasets
import seaborn as sns
import pandas as pd
from sklearn import tree

iris = datasets.load_iris()
iris_df = pd.DataFrame(iris.data)
iris_df['class']=iris.target
iris_df.columns=['sepal_len', 'sepal_wid', 'petal_len', 'petal_wid', 'class']

X = iris_df.sample(frac=1).reset_index(drop=True)
print( X.head(5) )

TRAIN_SPLIT = 100
X_train = X[0:TRAIN_SPLIT]
y_train = X_train['class']
X_train = X_train.drop(['class'], axis=1)
print( X_train.head())

X_test = X[TRAIN_SPLIT:]
y_test = X_test['class']
X_test = X_test.drop(['class'], axis=1)

print(f'\nShape of Training-Data : {X_train.shape}')
print(f'\nShape of Test-Data     : {X_test.shape}')
```

Modifizieren Sie Zeilen 21 und 22, wenn Sie nicht alle Features für den Lernprozess einsetzen wollen. 

![](<../../.gitbook/assets/image (122) (1).png>)

### Entscheidungsbaum erzeugen

```python
clf = DecisionTreeClassifier(random_state=1234, criterion = 'gini', max_depth=1)
model = clf.fit(X_train, y_train)
print("Accuracy-Training : ", clf.score(X_train, y_train))

if len(X_test) > 0:
  print("Accuracy-Testing: ", clf.score(X_test, y_test))


print("Creating Tree ... ")
fig = plt.figure(figsize=(8,8))
sns.set_style('dark')
#plt.style.use('whitegrid')
p = tree.plot_tree(clf
                   , feature_names=X.columns
                   , class_names=['setosa', 'versicolor', 'virginica']
                   , filled=True
                   )

```



### Einzelne Prediction

Wir wollen nun einen einzelnen Datensatz vorhersagen und mit den Trainingsdaten vergleichen:

```python
y_pred = model.predict( X_train.iloc[i:i+1])[0]    
```

Erläuterung: Mit` X_train.iloc[i:i+1]` wählen wir die i-te Zeile in der Feature-Matrix `X_train` aus.



### Manuelle Berechnung der Accuracy

```python
N = X_train.shape[0]
y_pred = model.predict( X_train )
check_vector = y_pred==y_train
c = check_vector.sum()
print(check_vector[0:10])
print("Accuracy (manuell) ..: ", c/N)
```



Erläuterung:

* Zeile 3 summiert die Werte im Vektor (True entspricht einer 1)
* Zeile 4 gibt zum Test den Vergleichsvektor aus.

