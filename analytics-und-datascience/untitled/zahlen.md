---
description: Wir starten einfach mit Zahlen.
---

# Datentyp "Zahlen"

## Ganze Zahlen und rationale Zahlen

Zahlen sind recht einfach zu verstehen, wir haben ja oben schon einige Beispiele gesehen. Hier nochmal eine Zusammenfassung wichtiger Beispiele mit rationalen Zahlen: 

```python
a = 2
b = 1/3
c = 1.1
# Funktionen
d = a + b; print(d)
d = a - b; print(d)
d = a * b; print(d)
d = a / b; print(d)
```

## Zufallszahlen

Python kann Zufallszahlen erzeugen. Diese Funktion ist allerdings nicht "eingebaut". Dazu muss mit `import Numpy `ein sogenanntes _Modul _importiert werden.

### Gleichverteilte Zufallszahlen

```python
import numpy as np
# Gleichverteilte Zufallszahl in [0,1]
x = np.random.rand()
print(x)
```

### Normalverteilte Zufallszahl $$μ = 0, \sigma = 1$$ 

Einen Überblick über alle mathematischen Funktionen von NumPy finden sie unter [https://numpy.org/doc/stable/reference/routines.math.html#](https://numpy.org/doc/stable/reference/routines.math.html#)

```python
import numpy as np
x = np.random.normal()
print( x )
```







###



