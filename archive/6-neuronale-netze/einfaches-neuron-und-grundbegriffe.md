# Einfaches Neuron und Grundbegriffe

&#x20;Künstliche neuronale Netze haben, ebenso wie künstliche Neuronen, ein biologisches Vorbild. Man stellt sie natürlichen [neuronalen Netzen](https://de.wikipedia.org/wiki/Neuronales\_Netz) gegenüber, die eine Vernetzung von [Neuronen](https://de.wikipedia.org/wiki/Nervenzelle) im [Nervensystem](https://de.wikipedia.org/wiki/Nervensystem) eines Lebewesens darstellen.&#x20;

![Biologische und Künstliche Neuronen (Quelle: https://www.datacamp.com/)](<../../.gitbook/assets/image (144).png>)

Bei KNNs geht es allerdings mehr um eine Abstraktion ([Modellbildung](https://de.wikipedia.org/wiki/Modell)) von Informationsverarbeitung, weniger um das Nachbilden biologischer neuronaler Netze und Neuronen, was eher Gegenstand der [Computational Neuroscience](https://de.wikipedia.org/wiki/Computational\_Neuroscience) ist. (Quelle: Wikipedia)

## Ein Neuron

Ein Neuron ist der Grundbaustein neuronaler Netzwerke. Ein Neuron hat folgende Grundeigenschaften

* die Eingabe eines Neurons ist ein Vektor $$x \in \mathbb{R}^m$$ .
* die Ausgabe eines Neurons ist eine reelle Zahl und wird auch **Activation **genannt.

Ein Neuron entspricht damit einer Funktion von, die von $$\mathbb{R}^m$$ nach $$\mathbb{R}$$ abbildet.

&#x20;

![](<../../.gitbook/assets/image (111).png>)

### Gewichtsvektor und Bias

Wir geben nun dieser Funktion einen Struktur. Sie wird wie folgt funktionieren:

![](<../../.gitbook/assets/image (112).png>)

In Vektorschreibweise berechnet ein Neuron also

$$
\phi( \bold{x} \cdot \bold{w} + b), \quad\text{mit} \quad w \in \mathbb{R}^m, b \in \mathbb{R}
$$

Wir werden für $$\phi$$ meist recht einfache Funktionen werden, z.B. wie in obiger Folie erläutert  $$\phi(x) = x$$. Die Vektor  $$w$$ heißt **Gewichtsvektor **(_weight vector_ oder kurz _weight)_, die Zahl $$b$$ heißt **Bias. **Häufig wird der Bias ebenfalls als weight betrachtet. Dann sprechen wir _nur_ von Weights. Wir wollen das aber in diesem Modul vermeiden, wenn es geht.

> **Ein Neuron ist also von m+1 Werten (Parametern) abhängig, mit denen man das Verhalten des Neurons einstellen kann.**

![](<../../.gitbook/assets/image (114).png>)

### Beispiel

Nachfolgendes Beispiel erläutert die Rechnung eines Neurons per Hand:

![](<../../.gitbook/assets/image (113).png>)

### Übung

Berechnen Sie die Ausgabe des folgenden Neurons:

![](<../../.gitbook/assets/image (115).png>)

### Neuron mit Python

Nach folgende Zeilen vollziehen die Rechnung on obiger Folie nach.

```python
import numpy as np
# x is a row vector with shape (1,3)
x = np.array([[3,2,-0.5]])
print( x.shape)

# w is a col vector with shape (3,1)
w = np.array([[-4],[1],[2]])
print( w.shape)

# b is a vector with shape (1,)
b = np.array([4])
print( b.shape )

output = np.dot(x,w) + b 

print( output )
print( output.shape)
```

### Neuron mit Python und Keras

Nachfolgendes Programmstück definiert ein Neuronales Netz, bereits als Model. Wir trainieren das Modell noch nicht, sondern setzten die Gewichte manuell. Der Trainingsprozess würde die Gewichte so setzten, dass die _Activations _für jeden Input möglichst nahe an den Labels wären.

```python
%tensorflow_version 2.x
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense, Activation
import numpy as np;

# Activations: linear, relu, sigmoid, tanh, 
# Baue neuronales Netz mit
#  - einem Neuron
#  - drei Eingängen
#  - einer linearen Activation-Function phi
layer_0 = Dense(1, input_dim=3, activation='linear')
model = Sequential() # klären wir später
model.add( layer_0 ) # klären wir später

# Setze Gewichte und Bias des einen Neurons
my_kernel = np.array([ [-4], [1], [2] ] )
my_bias = np.array( [4] ); 
model.layers[0].set_weights( [ my_kernel, my_bias ] )

# now feed two feature vectors into the model
X = np.array([
              [3,2,-0.5],
              [30,20,-0.5]
              ])

# Calculate the activation of the neuron
y = model.predict( X );
print( y );
```

## Case Study: Chirps (Grillen)

Anhand des Zirpens von Grillen kann man mehr oder weniger verlässlich die Lufttemperatur berechnen. Die Körperfunktionen von Grillen verändern sich wie bei anderen Insekten auch durch veränderte Lufttemperatur. Denn wie alle Insekten sind Grillen kaltblütig und nehmen die sie umgebende Temperatur an. Je wärmer, desto häufigeres Zirpen. Ist es wärmer, laufen die Körperfunktionen – wie auch Bewegungen – schneller ab, die Grillen sind aktiver. \[…] Da Grillen also bei erhöhter Temperatur häufiger Zirpen, kann man aus der Häufigkeit des Zirpens die Lufttemperatur ableiten. Die Formel dafür ist sehr simpel. Um die Temperatur in Grad Celsius zu errechnen, zählt man das Zirpen einer einzelnen Grille in einem Intervall von 25 Sekunden.

### Dataset

Nehmen wir an, dass folgende kleine Menge von labelled examples vorliegt:&#x20;

![](<../../.gitbook/assets/image (117).png>)

Natürlich wollen wir nun - wie üblich - aus dem feature den label vorhersagen. Offensichtlich handelt es sich um ein Regressionsproblem.&#x20;

Mit folgendem Code definieren wir unseren Dataset:

```python
df = pd.DataFrame({
    "Count": [31,16,29,43,27,19,47,9,45,5,39],
    "Temp": [9.4,10.5,17.1,24.3,14.6,9.9,16.9,6.4,17.7,7.5,14.2]
    
})
```

### Das "Grillen-Neuron"

Wenn wir ein Neuron mit _einem _Eingabewert und _linearer Activation_ bauen, so ist die Ausgabe des Neurons

$$
y = M(x) = x \cdot w +b
$$

Wir suchen also $$w$$ und $$b$$  in $$\mathbb{R}$$, so dass unser dadurch definiertes Modell unseren Datensatz möglichst gut vorhersagt. Offenbar ist M für fest gewähltes w und b eine lineare Funktion, die wir gut visualisieren können.

### Übung

1. Visualisieren Sie den Dataset mit einem Scatter-Plot.
2. Skizzieren sie das "Grillen-Neuron" analog zur Abbildung im Abschnitt "Beispiel"
3. Geben sie eine visuelle Abschätzung für Gewicht und Bias
4. Erläutern Sie anhand dieses Beispiels der Begriff einer _Modellfamilie_.

Lösung zu 2:

![](<../../.gitbook/assets/image (131).png>)

### Loss

Um die Qualität eines gewählten Modells zu verwenden verwenden wir den schon bekannten  MSE:

$$
MSE = \frac{1}{n}\sum_{i=0}^{n-1} (M(x_i) -y_i) ^2
$$

für alle $$n$$ labelled examples$$(x_i,y_i)$$ aus dem Dataset. ** **Durch Einsetzen der Definition von $$M$$ ergibt sich nun:

$$
\begin{align*}
MSE 
    &= \frac{1}{n}\sum_{i=0}^{n-1} ( x_i\cdot w + b - y_i ) ^2
\end{align*}
$$

### Neuronales Netz und Learning

Folgender Code erzeugt die Modellfamilie und berechnet dann das optimale Modell:

```python
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense, Activation
from tensorflow.keras import optimizers

#Create Neural Netwotk
model = Sequential()
model.add( Dense(1, activation='linear') )
model.compile(loss='mean_squared_error', optimizer='adam')


# Run the training
history = model.fit(X,y, verbose=0, epochs=20000)

print("Result")
[weight, bias] = model.layers[0].get_weights();
print(f'Weight:{weight}')
print(f'Bias:{bias}')
```

(Mögliche) Ausgabe:&#x20;

![](<../../.gitbook/assets/image (129).png>)

### &#x20;Visualisierung des gelernten Modells

Folgende Grafik visualisiert das Geschehen bisher:

* Die roten Punkte zeigen die _labelled examples_
* Die blauen Punkte zeigen die _predictions _für die features
* Die blaue Linie visualisiert das Modell&#x20;

![](<../../.gitbook/assets/image (132).png>)

### Visualisierung der Fehlerfunktion

Der MSE ist eine reelle Zahl, die von w und b abhängt.  Wir können daher den MSE-Graph als Fläche über der Weight-Bias Eben plotten.&#x20;

![](<../../.gitbook/assets/image (124).png>)

Am tiefsten Punkt der Fläche haben wir das beste Modell gefunden. Der kleine Punkt in der Grafik markiert in etwa diesen Punkt.

### Gradientenabstieg (_gradient descent_)

Wir haben eben gesehen, dass die Fehlerfunktion MSE nur von w und b abhängt. Das Minimum von Funktionen lässt sich unter bestimmten Umständen durch die erste Ableitung berechnen. In der Praxis gelingt das aber nur selten. Erfolgversprechender ist das sukzessive Absteigen  auf der Fläche. Da unserer Fehlerfunktion differenzierbar ist, ist der negative Gradient die beste Abstiegsrichtung.

In folgender Abbildung ist ein willkürlicher "Abstiegspfad" eingezeichnet:

&#x20;&#x20;

![](<../../.gitbook/assets/image (125).png>)

Der Abstiegsverfahren lässt sich etwas besser anhand eines Grafen einer Loss-Funktion $$L: \mathbb{R} \rightarrow \mathbb{R}$$ veranschaulichen. Es wir dabei angenommen, dass der Loss (auch "Cost") nur von $$w$$ abhängt. &#x20;

![](<../../.gitbook/assets/image (150).png>)

Ist L differenzierbar und  $$L´(x_0) < 0$$ für einen zufällig gewählten Startwert $$x_0$$ , so gilt wegen

$$
L´(x_0) = \lim_{h \rightarrow 0} \frac{f(x_0+h) - f(x_0)}{h}  <0
$$

für hinreichend kleines $$h_0 > 0$$:

$$
\frac{f(x_0+h_0) - f(x_0)}{h_0}  <0
$$

und damit

$$
f(x_0+h_0) < f(x_0)
$$

Nun setzt man $$x_1 = x_0 + h_0$$ und fährt weiter fort.&#x20;

### Trainingsschritt und Epochen

Ein **Trainingsschritt **(learning-step) ist eine neue Festlegung der Parameter eines Modells, so dass der Loss kleiner wird. Diese neue Festlegung funktioniert auf der Basis des Gradienten der Loss-Funktion. In obigem Beispiel wäre der Trainingsschritt $$h_0.$$ Eine **Epoche **ist ein Trainingsschritt auf der Grundlage aller Trainingsdaten. Wir identifizieren für den Moment eine Epoche mit einem Abstiegsschritt.

### Visualisierung des Lernfortschritts

![](<../../.gitbook/assets/image (130).png>)