# Numpy-Arrays

## Arrays-"Handgemacht"

```python
import numpy as np

x = np.array([1,2,3,4])
print(x)
```

## `arange `und `linspace`

```python
import numpy as np

x = np.arange(1,2,0.1)
print( x )
print( x[2] )
print( len(x) )
print ( type(x) )
```

## `Arrays mit Zufallszahlen`

Link: [https://www.w3schools.com/python/numpy/numpy_random.asp](https://www.w3schools.com/python/numpy/numpy_random.asp)

###

```python
import numpy as np

# Zufallszahl - gleichverteilt zzischen 0 und 1
u = np.random.rand()
print(u)
# Zufallszahl - standard-normalverteilt: E = 0; sigma = 1
n = np.random.normal()
print(n)
```

```python
import numpy as np

ua = np.random.rand(10)
print(ua)
na = np.random.normal(size=10)
print(na)
```

## Visualisierungsübung



1. Sie können mit numpy  eine Liste mit 50 gleichverteilen Zufallszahlen erstellen. Erzeugen Sie zwei dieser Listen (x und y) und zeigen sie die Paare (x\[i], y\[i]) in einem Scatterplot an. ([Lösung](../../vertiefungen/loesungen-und-vertiefungen.md#scatterplot-von-paaren-aus-zufallszahlen))
2. Welches Ausgabe erwarten Sie, wenn Sie jeweils 2000 Zahlen erzeugen?
3. Wiederholen sie Aufgabe 1 mit der Normalverteilung statt der Gleichverteilung. Überlegen sie  bitte vorher: welche grafischen Ausgabe erwarten sie?
