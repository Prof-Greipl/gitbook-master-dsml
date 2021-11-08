# Vertiefungen zu Machine Learning

## Thema: Analytische Berechnung des Optimums&#x20;

### Herleitung

Für die MSE-Verlustfunktion

$$
L(w,b)  = \sum_{i=0}^{n-1} (x_iw +b -y _i)^2
$$

ist&#x20;

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

Betrachten wir die Werte im Dataframe&#x20;

![](<../../.gitbook/assets/image (136).png>)

so ergibt sich (gerundet, mit Hilfe von Excel und nach Division durch den Faktor von $$w^*$$):

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

Schließlich ergibt sich mit dem entsprechenden Modell als minimaler Loss der Wert&#x20;

$$
8,57336688506454
$$

Vergleichen Sie die Werte mit dem Ergebnis unseres neuronalen Netzes!

## Thema: Zeichnen von Aktivierungsfunktionen

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

