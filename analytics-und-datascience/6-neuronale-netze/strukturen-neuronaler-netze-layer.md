# Strukturen Neuronaler Netze \(Layer\)

## Netzwerk-Layer \(Input-, Output-Layer\)

Wir wollen nun mehrere Neuronen zu einem Netz verschalten und brauchen dazu eine strukturierte Anordnung der Neuronen. Nachfolgende Grafik zeigt das rechte einfache Konzept eines Layers, in dem wir  drei Neuronen in einer Schicht aufbauen. 

Wichtig:

![](../../.gitbook/assets/image%20%28151%29.png)

1. Man bezeichnet die Schicht der Eingabewerte, also der Features, auch als **Input Layer**
2. Dier erste Schicht von Neuronen wird als Layer 0 bezeichnet.
3. Jeder Wert aus dem Input-Layer wird mit jedem Werte aus dem Layer 0 verbunden. 
4. Das obige Netz gibt drei Werte aus. Die letzte Schicht, die Werte ausgibt, heißt auch **Output-Layer**.

> Eine Struktur von Neuronen, die einen Feature-Vektor verarbeitet heißt **Neuronales Netz.**

##  Multi Layer Stuktur

Natürlich können wir nun mehrere Schicht \(Layer\) anordnen und miteinander verbinden. Folgende Abbildung zeigt eine derartige Struktur

![](../../.gitbook/assets/image%20%28156%29.png)

Wichtig:

1. Ein Layer, der nicht Output-Layer ist, heißt "**Hidden Layer**".

## Übung 1

Lösen Sie für diese Neuronale Netz nachfolgende Aufgaben:

![](../../.gitbook/assets/image%20%28146%29.png)

a\)  Berechnen Sie den Output des folgenden Netzes für x= \(1,3,5\) und x = \(0,1,0\).

b\) Berechnen Sie das Netz für für x = \(1,3,5\) erneut. Nehmen sie nun aber statt `linear` stets `relu` als Aktivierung an.

## Eigenschaften Neuronaler Netze

### Fully Connected Layer

Ein Layer heißt **Fully Connected Layer** oder auch **Dense Layer,** wenn jedes Neuron in dem Layer mit **allen** Neuronen aus dem vorhergehenden Layer verbunden ist. Der Layer 0 heißt fully connected, wenn jedes Neuron mit jedem Eingabewert verbunden ist. 

> Wir betrachten in diesem Kurs nur Fully Connected Layers

### Feed-Forward Netze

In den Neuronale Netzen, die wir in diesem Kurs betrachten, fließen die Feature-Werte von links nach rechts durch das Netz, werden dabei sukzessive in den Ebenen verarbeitet und führen dann zu einer Ausgabe. Wir sehen insbesondere keine Rücksprünge vor. Derartige Netze heißen **Feed-Forward-Netze**

Nun verstehen wir auch den Befehl zur Konstruktion des Netzes für den Chirps-Case:

```python
%tensorflow_version 2.x
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense, Activation
from tensorflow.keras import optimizers

model = Sequential()
model.add( Dense(1, activation='linear') )
```

Zeile 1 besagt, dass wir ein feed-forward Modell aufbauen und in Zeile 2 wird der erste Layer \(ganz korrekt: Layer 0\) hinzugefügt. Es handelt sich dabei um einen Dense Layer mit  einem Neuron und einer linearen Aktivierung.

## Dense Feed-Forward Netze in Python

Nachfolgender Befehlt konstruiert das Netz aus Übung 1. Beachten Sie dass dabei die Gewicht noch nicht explizit gesetzt werden.

```python
%tensorflow_version 2.x
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense, Activation
from tensorflow.keras import optimizers

model = Sequential()
model.add( Dense(2, activation='linear') )
model.add( Dense(1, activation='linear') )
```



## Dense Layers in Matrix-Schreibweise

In wenn sich in einem Dense Layer z Neuronen befinden, und jedes dieser Neuronen mit m Eingabewerten versorgt wird,  

* z Gewichtsvektoren \(Spaltenvektoren\) jeweils der Dimension m, die wir zu einer Gewichtsmatrix $$W \in \mathbb{R}^{m \times z}$$ 
* z Biaswerte, die wir zu einem Bias-Vektor $$\bold{b} \in \mathbb{R}^z$$ ****zusammenfassen \(Zeilenvektor\)**.** 

Dann lässt sich die Operation eines Layers schreiben als:

$$
\phi(x\cdot W+b)
$$

Achtung: Der Wert in der Klammer ist ein Zeilenvektor!

Nachfolgendes Bild verdeutlicht, was in dem Funktionsargument passiert:

![](../../.gitbook/assets/image%20%28152%29.png)



Dabei ist wieder um $$\phi $$ eine Aktivierungsfunktion, die aber nun auf einen Vektor angewendet wird.  Für die Aktivierungsfunktionen `linear`, `relu`, und `sigmoid` wenden wir diese Funktion einfach auf die einzelnen Einträge an, also  

$$
\phi(\bold{v}) = 
\phi(v_1,v_2, ..,v_n )
=
(\phi(v_1),\phi(v_1), ..,\phi(v_1) )
$$

Hinweis: Das ist formal nicht ganz korrekt, aber wir leisten uns die Unschärfe. Sehen sie das \(formale\) Problem?

### Übung 2

Geben sie für die beiden Layer aus obiger Übung 1  jeweils Gewichtsmatrix und Bias-Vektor an.



