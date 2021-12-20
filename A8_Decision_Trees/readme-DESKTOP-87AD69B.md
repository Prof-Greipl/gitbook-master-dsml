Wir versuchen einen als Modell einen Entscheidungsbaum zu konstruieren, der entlang von Werten eines Feature aufgebaut ist.  Der letzte Knoten jedes Pfades gibt die zugeordnete Klasse an. 

# Aufbau

Nachfolgende Eigenschaften beschreiben einen binären Entscheidungsbaum:

- Ein binärer Entscheidungsbaum besteht aus mindestens einem Knoten (node). Dieser Knoten heißt Wurzel (root [node]()). 
- Jeder Knoten hat entweder zwei Nachfolgeknoten (linker und rechter Nachfolgeknoten) oder keinen Nachfolgeknoten. Außer der Wurzel ist jeder Knoten ein Nachfolgeknoten genau eines anderen Knoten.  
- Ein Knoten ist mit einem Nachfolgeknoten über eine Kante verbunden. Die Tiefe eines Knotens gibt an, wie viele Kanten er von der  Wurzel entfernt ist.
- Ein Pfad ist eine geordnete Liste von Knoten, die durch Kanten verbunden sind 
- Ein Knoten ohne Nachfolgeknoten heißt *Blatt*, andernfalls *innerer Knoten*.
- Jeder innere Knoten enthält genau Bedingung (im ML Kontext:  auf Basis *eines* Feature-Wertes.)
- Jedem Blatt ist genau eine Klasse (label) zugeordnet.
- Die Baumhöhe (engl. *tree depth*) ist die maximal auftretende Tiefe eines Knotens. 



 

# Prediction

Ein Entscheidungsbaum erlaubt auf folgende Weise eine *Prediction* für einen Feature-Vektor:

- Die Wurzel erthält den Feature-Vektor als Eingabe.  

- Der Feature-Vektor fließt definiert gemäß dem Ergebnis der Abfrage im jeweiligen Knoten (wahr: linker Knoten, falsch: rechter Knoten)  einen Pfad bis zu einem Blatt.
- Die diesem Blatt zugeordnete Klasse (label) ist die *Prediction* für den Feature-Vektor. 





# Beispiel 

Zur Vereinfachung wählen wir im folgenen Beispiel nur *versicolor*- und *viriginica*-Datensätze aus, arbeiten also mit zwei Klassen und 100 Datensätzen. Einen möglichen Entscheidungsbaum zeigt nachfolgendes Bild. Die Abbildung ist bereits mit Werten angereichert, die wir erst im nächsten Abschnitt brauchen.

![image-20211203200915482](readme.assets/image-20211203200915482.png)



Sie können die Zahlen aus obigem Entscheidungsbaum mit Excel nachvollziehen oder - schneller - mit folgenden kleinen Programmen berechnen.



# Qualität eines Baumes (Accuracy)

Um die Qualität eines konkreten Baumes zu bewerten lassen wir alle vorliegenden Feature-Vektoren durch den Baum fließen und berechnen die somit die Genauigkeit des obigen Baumes. Offensichtlich werden im linken Blatt 16 Datensätze, im rechte Blatt 50 Datensätze richtig klassifiziert. Das macht eine Genauigkeit von 66%.

## Python (Iris mit zwei Arten)

Wir wählten zuerst nur die beiden Klassen Versicolor und Viriginca aus. Die letzte Zeile des folgenden Programms ist entscheidend. Der Rest unterscheidet sich nicht vom bereits bekannten Ladevorgang.

```python
import pandas as pd
from sklearn import datasets

iris = datasets.load_iris()
iris_df = pd.DataFrame(iris.data)
iris_df['class']=iris.target_names[iris.target ]
iris_df.columns=['sepal_len', 'sepal_wid', 'petal_len', 'petal_wid', 'class']
iris_df = iris_df[50:]
```

Mit folgenden Programmzeilen lassen sich die Zahlen schnell berechnen:

```python
filter_crit = (iris_df["petal_len"] <= 4)
filter_ver  = (iris_df["class"] == "versicolor")
filter_vir  = (iris_df["class"] == "virginica")

print( "Total      : ", iris_df[ filter_crit]["class"].count() )
print( "Versicolor : ", iris_df[ filter_crit & filter_ver]["class"].count() )
print( "Virginica  : ", iris_df[ filter_crit & filter_vir]["class"].count() )
```





# Modellfamilie und Optimaler Baum

In diesem Abschnitt geht es um die Frage, wie wir den besten Baum finden. Dazu definieren wir zunächst unsere **Modellfamilie**: wir betrachten alle binären Entscheidungsbäume der Höhe 1 (Später werden wir die Höhe noch ändern!)

Für einen gegebenen Baum werden wir jedem Datensätze eine Klasse zuordnen. Für $$k$$ Klassen entstehen also entsprechen viele Mengen. Formal sprechen wir von einer Zerlegung des Datensatzes. 





## Optimaler Baum nach Training

Wir berechnen der optimalen Baum der Höhe 1 mittels Python.

![Iris mit 2 Klassen: Optimaler Baum der Höhe 1](readme.assets/image-20211129092942002.png)

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



## Übung

1. Berechnen sie die Werte in den Knoten mit dem Phython-Programm aus dem vorhergehenden Abschnitt.
2. Welche *Accuracy* hat dieser Baum?
3. Wie viele verschiedene Bäume der Höhe eins gibt es?



 

# Lernverfahren

In diesem Abschnitt werfen wir einen Blick auf das Lernverfahren. Zur Vereinfachung konzentrieren wir uns auf Bäume der Höhe 1. Dazu suchen wir **ein Feature**, das einen möglichst guten Split (auch Zerlegung genannt) der Datensätze erlaubt.



# GINI-Impurity

# Qualität eines Knotens 

Jeder Knoten eines Entscheidungsbaums bestimmt eine Zerlegung seiner Datensätze gemäß den zugeordneten Klassen. Wir wollen, dass in dieser Zerlegung eine Menge (Klasse) möglichst dominierend ist.  

## Zerlegung

Für eine endliche Menge $$S$$  heißen die Teilmengen $$S_1, S_2,...S_k$$  Zerlegung, wenn jedes Element aus $$S$$ in genau einer der Teilmengen enthalten ist.

Wie man an obigem Beispiel sieht, lässt sich jedem Knoten eine Zerlegung derjenigen Datensätze zuordnen, die den Baum in der Trainingsphase durchfließen. In einem Blatt wünschen wir uns, dass eine der Teilmengen, möglichst viele Elemente enthält. Im besten Fall sind $$k-1$$ Mengen leer!



## Beispiel 

Sie sehen oben zwei mögliche Entscheidungsbäume für Iris mit unterschiedlicher Accuracy. Offensichtlich hängt die Accuracy von der Entscheidung am Wurzelknoten ab. Diese Entscheidung erzeugt zwei Teilmengen  mit 54 Elementen im linken Knoten und 46 Elemente im rechten Knoten. 



## Gini-Impurity einer binären Zerlegung

Nehmen Sie an, dass eine Menge S  in Teilmengen $$S_1, S_2,...S_k$$  zerlegt wird (und damit den Elementen einer Teilmengen jeweils ein Label zugeordnet ist.) Mit  $$p_i$$  bezeichnen wir jeweils das Verhältnis der Elemente  von $$S_i$$ im Vergleich zu $$S$$. Wegen $$\sum p_i = 1$$ definiert $$P = (p_1, p_2, ... p_n)$$ eine (diskrete) Verteilungsfunktion. 

Wir wählen nun aus Menge $$S$$  zufällig  Elemente aus Für jedes gewählte Element raten wir, zu welcher Teilmenge es gehört. Beim Raten halten wir die obige Verteilungsfunktion ein. Wie hoch ist die Wahrscheinlichkeit - die wir im folgenden GINI nennen - , dass wir falsch raten?

Offensichtlich ist für $$k=2$$ und $$P = (p_1,p_2)$$:
$$
\begin{align}
\text{GINI}(p_1, p_2) \quad 
& = \quad p_1 \cdot (1-p_1) + p_2 \cdot (1-p_2) \\
& = \quad 2 p_1 p_2\\
& = \quad 1 - p_1^2 - p_2^2
\end{align}
$$
wegen $$1 = (p_1 + p_2)^2 = p_1^2 + 2p_1p_2 + p_2^2$$.



 

### Beispiel ($$k=2$$)

![Zerlegung von 10 Zahlen in blaue und rote Werte](readme.assets/image-20211130172946647.png)



Obige Menge von 10 Zahlen lässt sich ein Teilmenge $$S_1$$ der blauen Werte und eine weitere Teilmenge $$S_2$$ der roten Werte aufteilen. Damit ergibt sich $$p_1 = 0.6$$ und $$p_2 = 0.4$$, also
$$
GINI(P) = 1 - 0.36 - 0.16 = 0.48
$$

> 



### Übung

Berechnen Sie für die Zerlegungen der Knoten in nachfolgendem Entscheidungsbaum die GINI-Werte:

![image-20211202184650173](readme.assets/image-20211202184650173.png)



###  Wie groß kann GINI für $$k=2$$ werden?

Für $$k=2$$ und $$P = (p_1,p_2)$$ ist wegen $$p_2 = 1-p_1$$  
$$
GINI(p_1, p_2) = 2p_1 \cdot (1-p_1)
$$
Offensichtlich gilt
$$
GINI(0,1) = GINI(1,0) = 0 \quad \text{und} \quad GINI(\frac{1}{2}, \frac{1}{2}) = \frac{1}{2}
$$
Folgende Abbildung zeigt den Plot von $$p \rightarrow 2p(1-p)$$:

![GINI in Abhängigkeit von p](readme.assets/image-20211202184126689.png

![image-20211202184254174](readme.assets/image-20211202184254174.png)

> Je größer der GINI Wert ist, desto diffuser ist die Menge



## GINI-Impurity für einer allgemeinen Zerlegung

Nehmen wir nun an, dass eine endliche Menge S  in $$k$$ Teilmengen $$S_1, S_2,...S_k$$  zerlegt wird. Mit  $$p_i$$  bezeichnen wir weiterhin das Verhältnis der Anzahl der Elemente  von $$S_i$$ im Vergleich zu $$S$$. Wegen $$\sum p_i = 1$$ definiert $$(p_1, p_2, ... p_n)$$ eine (diskrete) Verteilungsfunktion. Definieren wir die Impurity von $$S$$ wie oben, als die Wahrscheinlichkeit der Fehlklassifikation eines beliebigen Elementes von $$S$$, so gilt


$$
\begin{align}\text{GINI}(p_1, \dots, p_k) \quad & = \quad \sum_{i=1}^k p_i \cdot \sum_{j \neq i} p_j \\
& = \quad \sum_{i=1}^k (p_i \cdot  (1-p_i)) \\
& = \quad \sum_{i=1}^k (p_i -  p_i^2 ) \\
& = \quad 1 - \sum_{i=1}^k p_i^2
\end{align}
$$


# Qualität eines Splits

In einem Baum führt ein Knoten, der kein Blatt ist, zu einer Aufteilung der Samples dieses Knoten in zwei Teilmengen, die linke Menge $$S_L$$ und die rechte Menge $$S_R$$.

![image-20211202185542367](readme.assets/image-20211202185542367.png)

 

Für beide Mengen lässt sich der GINI-Wert ausrechnen:
$$
GINI(S_L) = 0  \quad \text{und} \quad GINI(S_R) = \frac{8}{25} =  0.32
$$
Der **erwartete** GINI-Wert des Split ist damit:
$$
GINI = \frac{1}{2} \cdot GINI(S_L) + \frac{1}{2} \cdot GINI(S_R) = \frac{4}{25} = 0.16
$$
Der Split reduziert also den GINI-Wert von $$0.5$$ auf $$0.16$$. 

## Übung

Berechnen sie die Qualität der folgenden Splits.

**Split 1:**

![image-20211202191203861](readme.assets/image-20211202191203861.png)

**Split 2:**

![image-20211202191346064](readme.assets/image-20211202191346064.png)

