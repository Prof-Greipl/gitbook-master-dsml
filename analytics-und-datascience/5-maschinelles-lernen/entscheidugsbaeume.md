# Entscheidungsbäume

## Einführende Übung

Wir arbeiten mit dem Titanic-Datensatz nach Feature-Engineering. Unser Modell M berechnet für eine Eingabe die Vorhersage aufgrund eines **Entscheidungsbaums**. Wir verzichten auf eine formale Definition und illustrieren das Vorgehen durch eine Grafik. 

Wir fragen für einen unbekannten Feature-Vektor zu erst nach dem Geschlecht, und dann nach der Klasse. Den Wert im Kreis geben wir als Ergebnis aus.

![Baum 1](../../.gitbook/assets/image%20%2881%29.png)

Natürlich ist dieser Baum nur einer von vielen möglichen Bäumen.

#### Wie bewerten Sie die Werte in den Kreisen in obigem Baum 1? Finden Sie eine bessere Belegung der vier Kreise? 

Lösung:

![Baum 2](../../.gitbook/assets/image%20%28106%29.png)

#### Welche _Accuracy haben_ Baum 1 und Baum 2?

Lösung \(Hinweis: Verwenden Sie obigen Baum mit den Zahlen\): 

Die Accuracy ist von Baum 1 ist:

$$
\frac{77 + 64 +  161 + 72}{891} = 0.419
$$

Die Accuracy ist von Baum 2 ist:

$$
\frac{77 + 391 + 161 + 72}{891} = 0.786
$$

## Vertiefung

### **Motivation**

Nehmen Sie an, dass S die Menge aller Klausurergebnisse ist. $$S_1$$ist die Menge aller bestandenen Klausuren und$$S_0$$  die Menge aller nicht bestandenen Klausuren. Sie wollen unbedingt wissen, ob sie bestanden haben und kennen die Durchfallquote $$p$$ . Bei welchem Wert von p sind sie bereit _für Ihr Ergebnis_ den _höheren Betrag_ an ein fiktives Orakel zu bezahlen?

a\)  $$p $$ gleich 50%

b\)   $$p $$ gleich 5%

### Informationsgehalt

Der Informationsgehalt einer Nachricht, die mit der Wahrscheinlichkeit p auftritt ist

$$
-\log_2(p)
$$

### Entropie

Nehmen Sie an, dass eine Menge S  in Teilmengen $$S_1, S_2,...S_n$$  zerlegt wird. Bezeichnet $$p_i$$  jeweils das Verhältnis der Elemente  von $$S_i$$ im Vergleich zu $$S$$ so bezeichnet

$$
H(S) = -p_1 \log_2(p_1) -p_2 \log_2(p_2) - ... -p_n \log_2(p_n)
$$

die **Entropie von S** und der betrachteten Zerlegung. Der obige Ausdruck ist völlig unabhängig von der Menge S, sondern hängt nur von $$p_1, p_2, ... p_n$$ ab. Wegen $$\sum p_i = 1$$ definiert$$(p_1, p_2, ... p_n)$$ eine \(diskrete\) Verteilungsfunktion.



**Beispiel 2** Für n=2 ist H nur von p abhängig. Hier der Graph für $$(p,1-p)$$ :

![](../../.gitbook/assets/image%20%2890%29.png)

Die Entropie ist ein Maß für die Ungewissheit auf die Frage "Zu welcher Teilmenge gehört ein gegebenes Element aus S?" 

**Numerisches Beispiel \(Titanic\):** Die Menge der 891 Labels enthält 549 mal den Wert 0 \(nicht überlebt\) und 342 man den Wert 1 \(überlebt\). Die Entropie der Menge ist also

$$
- \frac{549}{891} \cdot log_2( \frac{549}{891})  - \frac{342}{891} \cdot log_2( \frac{342}{891}) = 0.961
$$

Wenn Sie also für einen weiteren, uns unbekannten Passagier festlegen sollten, ob er überlebt hat: Wie würden Sie tippen? Und wir zuversichtlich sind Sie, dass sie richtig liegen?



### Entropie einer Partition

Offenbar ist es sinnvoll die Features zu benutzen, um die Qualität der Vorhersage zu verbessern. Nehmen wir an, dass das Feature `Sex` benutzen. Dann zerteilen wir damit den Datensatz in zwei Gruppen, die "Male"-Gruppe und die "Female"-Gruppe.

Die Entropie des "Male"-Gruppe ist:

$$
- \frac{468}{577} \cdot log_2( \frac{468}{577})  - \frac{109}{577} \cdot log_2( \frac{109}{577}) = 0.699
$$

Die Entropie des "Female"-Gruppe ist:

$$
- \frac{81}{314} \cdot log_2( \frac{81}{314})  - \frac{233}{314} \cdot log_2( \frac{233}{314}) = 0.824
$$

Der _erwartete_ Entropie **\(Entropie der Partition\)** ist damit

$$
\frac{577}{891} \cdot 0.699  \quad + \quad \frac{314}{891} \cdot 0.824 =   0.743
$$

 Die Einführung der Abfrage nach dem Geschlecht hat also die Entropie von 0.96 auf einen 0.743 reduziert.

### Übung

Berechnen Sie analog zu obigem Abschnitt die _erwartete Entropie_ für

a\) Pclass

b\) Age

c\) Embarked

d\) Fare

## Aufteilung in Training-Set und Test-Set

Wir teilen unseren Datensatz in einen Trainings-Teil und einen Test-Teil auf.

![](../../.gitbook/assets/image%20%28107%29.png)

| Menge | Beschreibung |
| :--- | :--- |
| X\_train | Dataframe mit Feature-Vektoren der Trainings-Set |
| y\_train | Dataframe mit Label-Vektor des Trainings-Sets |
| X\_test | Dataframe mit Feature-Vektoren der Test-Sets |
| y\_test | Dataframe mit Label-Vektor des Trainings-Sets |
| TRAIN\_SPLIT | Anzahl der Examples im Training-Set, der Rest geht zum Test-Set |

## Decison-Tree mit Titanic

### Aufteilung in Training- und Test-Set

Wir nutzen hier noch keine Validierung. Die Variable TRAIN\_SPLIT enthält die Anzahl der Examples aus dem Training-Set.

```python
from matplotlib import pyplot as plt
from sklearn import datasets
from sklearn.tree import DecisionTreeClassifier 
from sklearn import tree

TRAIN_SPLIT = 891
X_train = df[0:TRAIN_SPLIT]
y_train = X_train['Survived']
X_train = X_train.drop(['Survived'], axis=1)
print( X_train.head())

print(f'\nShape of Training-Data : {X_train.shape}')

X_test = df[TRAIN_SPLIT:]
y_test = X_test['Survived']
X_test = X_test.drop(['Survived'], axis=1)

print(f'Shape of Test-Data : {X_test.shape}')

# Reduce columns of Training/Test Data if needed
#cols = ['Sex', 'Pclass']
cols = X_train.columns
X_train = X_train[ cols ]
X_test = X_test[ cols ]
```

Modifizieren Sie Zeilen 21 und 22, wenn Sie nicht alle Features für den Lernprozess einsetzen wollen. 

![](../../.gitbook/assets/image%20%28122%29.png)

### Entscheidungsbaum erzeugen

```python
clf = DecisionTreeClassifier(random_state=1234, criterion = 'entropy', max_depth=200)
model = clf.fit(X_train, y_train)
print("Accuracy-Training", clf.score(X_train, y_train))
```

![](../../.gitbook/assets/image%20%28109%29.png)

### Prediction

Wir wollen nun einen einzelnen Datensatz vorhersagen und mit den Trainingsdaten vergleichen:

```python
print("#    Tra      Pre  Fehler")
for i in range(0,10):
  y_pred = model.predict( X_train.iloc[i:i+1])[0]  
  print(f'{i}    {y_train[i]}      {y_pred}')
```

Erläuterung:

* Zeile 3 Mit `X_train.iloc[i:i+1]` wählen wir die i-te Zeile in der Feature-Matrix `X_train` aus.

Wenn Sie noch die fehlerhaften Klassifizierungen markieren wollen:

```python
c=0;
print("#    Tra      Pre  Fehler")
for i in range(0,10):
  y_pred = model.predict( X_train.iloc[i:i+1])[0]  
  
  error = "<- Fehler"
  if y_pred == y_train[i]:
    c = c+1
    error = " "

  print(f'{i}    {y_train[i]}      {y_pred}  {error}')
  
print("Insgesamt korrekt : ",c)
```

Ausgabe: 

![](../../.gitbook/assets/image%20%28111%29.png)

### Manuelle Berechnung der Accuracy

```python
y_pred = model.predict( X_train )
check_vector = y_pred==y_train
c = check_vector.sum()
print(check_vector[0:10])
print("Accuracy (manuell) ..: ", c/N)
```

Ausgabe: 

![](../../.gitbook/assets/image%20%28112%29.png)

Erläuterung:

* Zeile 3 summiert die Werte im Vektor \(True entspricht einer 1\)
* Zeile 4 gibt zum Test den Vergleichsvektor aus.

### Feature-Reduktion

Wir verwenden nun, wie in der Einführenden Übung nur die Features `Sex` und `Pclass`:

```python
cols = ['Sex', 'Pclass']
X_train = X_train[ cols ]
clf = DecisionTreeClassifier(random_state=1234, criterion = 'entropy', max_depth=2)
model = clf.fit(X_train, y_train)
print("Accuracy-Training ....: ", model.score(X_train, y_train))
```

Ausgabe:

![](../../.gitbook/assets/image%20%28110%29.png)

Hinweis:

* Wir haben die maximale Tiefe des Baumes auf 2 beschränkt `(max_depth)`.

### Visualisierung des Baums

```python
print("Creating Tree ... ")
fig = plt.figure(figsize=(25,20))
p = tree.plot_tree(clf, 
                   feature_names=X_train.columns,  
                   class_names=['0', '1'],
                   filled=True)
```

Ausgabe:

![](../../.gitbook/assets/image%20%28113%29.png)

Vergleichen Sie diesen Baum mit dem Baum in der [einführenden Übung](entscheidugsbaeume.md#wie-bewerten-sie-die-werte-in-den-kreisen-in-obigem-baum-finden-sie-eine-bessere-belegung-der-vier-kreise).

### Übung: Alternatives Paar von Features

Wählen Sie sich ein alternatives Paar von Features. Dann:

1. Stellen Sie _einen möglichen_ Entscheidungsbaum per Hand auf
2. Berechnen Sie den _besten_ Entscheidungsbaum mit sklearn und vergleichen Sie ihr Ergebnis.

### Übung: Bestes Feature Paar?

Welches ist das beste Feature-Paar \(bei einer Baumtiefe von 2\)?

### Training-Sets und Test-Sets

Wir verändern nun das Szenario so, dass wir nicht alle Examples zum Trainieren verwenden, sondern ein paar zum Test übrig lassen:

```python
TRAIN_SPLIT = 700
X_train = df[0:TRAIN_SPLIT]
y_train = X_train['Survived']
X_train = X_train.drop(['Survived'], axis=1)


X_test = df[TRAIN_SPLIT:]
y_test = X_test['Survived']
X_test = X_test.drop(['Survived'], axis=1)

print(f'\nShape of Training-Data : {X_train.shape}')
print(f'\nShape of Test-Data : {X_test.shape}')

cols = X_train.columns
X_train = X_train[ cols ]
X_test = X_test[ cols ]


clf = DecisionTreeClassifier(random_state=1234, criterion = 'entropy', max_depth=200)
model = clf.fit(X_train, y_train)
print("Accuracy-Training ....: ", model.score(X_train, y_train))
print("Accuracy-Test ........: ",  model.score(X_test, y_test))
```

 

![](../../.gitbook/assets/image%20%28115%29.png)

Folgendes Diagramm zeigt die die beiden Accuracies in Abhängigkeit von TRAIN\_SPLIT 

![](../../.gitbook/assets/image%20%28118%29.png)

Wie interpretieren Sie die beiden Kurven?

## Random-Forrest mit Titanic

![](../../.gitbook/assets/image%20%28119%29.png)

```python
random_forest = RandomForestClassifier(
    n_estimators=50, # Number of differnet trees tried
    max_depth=200)
model = random_forest.fit(X_train, y_train)

train_score = round(model.score(X_train, y_train) * 100, 2)
test_score = round(model.score(X_test, y_test) * 100, 2)
```

## Abschlussübung

Ihre Abschlussübung finden Sie unter Advertising-Übung am Ende dieses GitBooks.

