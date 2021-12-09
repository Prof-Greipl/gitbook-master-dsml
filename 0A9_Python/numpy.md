## Zufallszahlen

Python kann Zufallszahlen erzeugen. Diese Funktion ist allerdings nicht "eingebaut". Dazu muss mit `import Numpy `ein sogenanntes _Modul _importiert werden.

### Gleichverteilte Zufallszahlen

```python
import numpy as np
# Gleichverteilte Zufallszahl in [0,1]
x = np.random.rand()
print(x)
```

### Normalverteilte Zufallszahl $$μ = 0, \sigma = 1$$&#x20;

Einen Überblick über alle mathematischen Funktionen von NumPy finden sie unter [https://numpy.org/doc/stable/reference/routines.math.html#](https://numpy.org/doc/stable/reference/routines.math.html#)

```python
import numpy as np
x = np.random.normal()
print( x )
```

---



## 
