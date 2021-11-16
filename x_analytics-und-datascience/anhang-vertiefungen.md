---
description: >-
  Vertiefungen sind nicht prüfungsrelevant, sofern dies nicht ausdrücklich
  gekennzeichnet ist. Sie sind aber möglicherweise hilfreich für das Verstehen
  des Stoffes.
---

# Anhang: Vertiefungen

## Numerische Daten mit Numpy

### Elementweise Anwendung einer Funktion auf eine Matrix

Für ein Matrix $$\bold{A} \in\mathbb{R}^{n\times m }$$ lässt sich aus einer Funktion $$\tilde{f} :\mathbb{R} \rightarrow \mathbb{R}$$ eine Funktion $$f :\mathbb{R^n} \rightarrow \mathbb{R}^n$$ , definieren mittels:

$$
f(\bold{x}) =\begin{bmatrix}
\tilde{f}(x_1) \\
 \tilde{f}(x_2) \\ 
\vdots \\
\tilde{f}(x_n)
\end{bmatrix}  \quad \text{wobei}  \quad
\bold{x} = 
\begin{bmatrix}
\bold{x_1} \\
\bold{x_1} \\
\vdots \\
\bold{x_{n}}
\end{bmatrix}
$$

Sie sehen übrigens an diesem Beispiel, dass die Regel "_Vektor = Spaltenvektor_" hier etwas Platz braucht. In der kürzeren aber etwas schwerer zu lesenden Version könnte man schreiben:

$$
f(\bold{x})^T = 
\begin{bmatrix}
\tilde{f}(x_1), \tilde{f}(x_2), ..., \tilde{f}(x_n) 
\end{bmatrix}
$$

Dann stehen nämlich auf beiden Seiten der Gleichung Zeilenvektoren.

### Zerlegung eines Farbbildes in Farbkanäle

```python
import numpy as np
import matplotlib.pyplot as plt

url = 'http://www.dietergreipl.de/wp-content/uploads/2019/10/owl-50267_1920.png'
eule = plt.imread( url )

plt.figure()
plt.imshow( eule[:,:,0], cmap=plt.cm.get_cmap('Reds'), vmin=0, vmax=1)

plt.figure()
plt.imshow( eule[:,:,1], cmap=plt.cm.get_cmap('Greens'), vmin=0, vmax=1)

plt.figure()
plt.imshow( eule[:,:,2], cmap=plt.cm.get_cmap('Blues'), vmin=0, vmax=1)
```

### Histogramm über einen Farbkanal

```python
import numpy as np
import matplotlib.pyplot as plt

url = 'http://www.dietergreipl.de/wp-content/uploads/2019/10/owl-50267_1920.png'
eule = plt.imread( url )

plt.figure()
eule_rot = eule[:,:,0].flatten()
plt.hist( eule_rot, bins=200, range=(0,1))
```

## Analytische Berechnung des Optimums 

### Herleitung

Für die MSE-Verlustfunktion

$$
L(w,b)  = \sum_{i=0}^{n-1} (x_iw +b -y _i)^2
$$

ist 

$$
\begin{align}
\frac{\partial L}{\partial w} 
&= 2\sum_{i=0}^{n-1} (x_iw +b -y _i)  x_i  \\
&= 2\sum_{i=0}^{n-1} (x_i^2 w +x_ib -x_iy _i)  \\
&= 2w\sum_{i=0}^{n-1} x_i^2 +2b \sum_{i=0}^{n-1} x_i  - 2\sum_{i=0}^{n-1}x_iy_i 
\end{align}
$$

und

$$
\begin{align}
\frac{\partial L}{\partial b} 
&= 2\sum_{i=0}^{n-1} (x_i w +b - y_i)   \\
&= 2 w \sum_{i=0}^{n-1} (x_i) + 2nb - 2 \sum_{i=0}^{n-1}y_i 
\end{align}
$$

Setzt man $$\frac{\partial L}{\partial w} =0$$ , $$\frac{\partial L}{\partial b} =0$$ , so erhält man zwei lineare Gleichungen, die es erlauben den optimalen Wert $$w^*$$ und $$b^*$$ zu berechnen.

### Beispiel

Betrachten wir die Werte im Dataframe 

![](../.gitbook/assets/image%20%28157%29.png)

so ergibt sich \(gerundet, mit Hilfe von Excel und nach Division durch den Faktor von $$w^*$$\):

$$
\begin{align}
0 &= w^* + 0,0285503776017683 \cdot b^* - 0,444114938294345 \\
0 &= w^* + 0,0354838709677419 \cdot b^* -0,479032258064516 
\end{align}
$$

und damit

$$
\begin{align}
 w^* &= 0,300334218870512 \\
b^* &= 5,03603565001285 
\end{align}
$$

Schließlich ergibt sich mit dem entsprechenden Modell als minimaler Loss der Wert 

$$
8,57336688506454
$$

Vergleichen Sie die Werte mit dem Ergebnis unseres neuronalen Netzes!

## Zeichnen der Aktivierungsfunktion

Wenn sie andere Aktivierungsfunktionen zeichnen wollen, ersetzen sie einfach in Zeile 13 'relu' durch 'sigmoid'

```python
%tensorflow_version 2.x
import numpy as np
import matplotlib.pyplot as plt

from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense,Activation

kernel = np.array([ [1] ] )
bias = np.array( [0]); 
weights = [kernel, bias]

model = Sequential([
  Dense(1, input_dim = 1, activation='relu')         
])
model.layers[0].set_weights(weights)

X = np.linspace(-1,1,2000)
y = model.predict(X)

# Visualisierung 
plt.figure()
plt.figure( figsize=(10,10))
plt.axis([-1, 1, -0.25, 1])
plt.axes().set_aspect(1)
plt.grid()
plt.plot(X, y, label="linear")
plt.show()
```



