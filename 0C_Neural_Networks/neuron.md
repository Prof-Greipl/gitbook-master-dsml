

# Neuron (Perceptron)

Ein Neuron (auch Perzeptron genannt) ist der Grundbaustein neuronaler Netzwerke. Ein Neuron hat folgende Grundeigenschaften

* die Eingabe eines Neurons ist ein Vektor $$x \in \mathbb{R}^m$$ .
* die Ausgabe eines Neurons ist eine reelle Zahl und wird auch **Activation **genannt.

Ein Neuron entspricht damit einer Funktion, die von $$\mathbb{R}^m$$ nach $$\mathbb{R}$$ abbildet.

 

![](<./assets/image (132).png>)





# Gewichtsvektor und Bias

Wir geben nun dieser Funktion einen Struktur. Sie wird wie folgt funktionieren:

![](<./assets/image (123).png>)

In Vektorschreibweise berechnet ein Neuron also

$$
\phi( \bold{x} \cdot \bold{w} + b), \quad\text{mit} \quad w \in \mathbb{R}^m, b \in \mathbb{R}
$$

Wir werden für $$\phi$$ meist recht einfache Funktionen werden, z.B. wie in obiger Folie erläutert  $$\phi(x) = x$$. Die Vektor  $$w$$ heißt **Gewichtsvektor **(_weight vector_ oder kurz _weight)_, die Zahl $$b$$ heißt **Bias. **Häufig wird der Bias ebenfalls als weight betrachtet. Dann sprechen wir _nur_ von Weights. Wir wollen das aber in diesem Modul vermeiden, wenn es geht.

> **Ein Neuron ist also von m+1 Werten (Parametern) abhängig, mit denen man das Verhalten des Neurons einstellen kann.**

![](<./assets/image (130).png>)



# Beispiel

Nachfolgendes Beispiel erläutert die Rechnung eines Neurons per Hand:

![](<./assets/image (135).png>)





# Übung

Berechnen Sie die Ausgabe des folgenden Neurons:

![](<./assets/image (131).png>)



# Neuron mit Python

Nach folgende Zeilen vollziehen die Rechnung on obiger Folie nach.

```python
import numpy as np
# x is a row vector with shape (1,3)
x = np.array([3,2,-0.5])
print( x.shape)

# w is a col vector with shape (3,1)
w = np.array([-4,1,2])
print( w.shape)

# Bias or Interception
b=4
output = np.dot(x,w) + b 

print( output )
print( output.shape)
```



# Neuron mit Python und Keras

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



