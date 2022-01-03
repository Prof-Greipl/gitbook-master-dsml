# Vertiefungen zu Python and Data Analysis

## Thema: Numerische Daten mit Numpy

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



