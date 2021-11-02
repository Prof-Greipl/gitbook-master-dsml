---
description: Dieses Kapitel enthält Lösungen zu ausgewählten Aufgaben.
---

# Lösungen zu Übungen

## Lösungen zu _Numerische Daten mit Numpy_

### Übung zu Vektoren

```python
import numpy as np

v = np.array([1,-3,2])     # Definiere Vektor v
w = np.array([1,0,13])     # Definiere Vektor w
print(f'Skalarprodukt "x*y": {np.dot(v,w)}')
print(f'Summe v+w:           {v+w}')
print(f'Produkt 2*v:         {v+w}')
```

### Übung zu Matrix

Inhalte: Matrix, Matrixprodukt in Numpy

```python
import numpy as np
A = np.array([[2,-1],[4,0],[9,3]])
C = np.array([[1,0],[4,-1]])
v = np.array([1,4])
w = np.array([-1,3])

res = np.dot(A,v)
print(f'\n Av =\n  {res}, \n Shape = {res.shape}')

res = np.dot(A,C)
print(f'\n AC = \n  {res}, \n Shape = {res.shape}')

VT = np.array([[1,4]])
W = np.array([[1],[4]])

res = np.dot(W, VT)
print(f'\n W VT = \n {res}, \n Shape = {res.shape}')

```

### Liste von Zufallszahlen als Funktion

```python
def liste_rand(n):
  liste = []
  for i in range(n):
     liste.extend( [ np.random.rand()] )
  return liste

```

### Scatterplot von Paaren aus Zufallszahlen

```python
import numpy as np
from matplotlib import pyplot as plt

n=5000
x = np.random.rand(n)
y = np.random.rand(n)
plt.scatter( x,y)
plt.axis("equal")
plt.show()
```

### Funktionen: np.zeros(), np.amax(), np.amin()

```python
import numpy as np

# np.zeros funktioniert analog zu np.ones()
A = np.zeros((4,10))
print(A)
print(A.shape)

# np.amax() und np.amin() bestimmen den maximalen und mininalen
# Wert einer Numpy-Arrays

print(np.amax(A)) # sollte offensichtlich Null ein...
print(np.amin(A)) # ebenfalls

B = np.random.rand(100,100)
print(np.amax(B)) # sollte nahe bei 1 sein ...
print(np.amin(B)) # sollte nahe bei 0 sein ...
```

## Lösungen zu Titanic

### Übung zu Überlebensraten

```python
# Anzahl der Überlebenden
#print( df.groupby(["Survived"]).count()  )

# einfacher
total_survivors = len( df[ df["Survived"] == 1] )
print(f"Anzahl der Überlebenden ........................ : { total_survivors }")

# Males
total_male = len( df[ df["Sex"] == "male"] )
print(f"Anzahl männlich Passagiere ..................... : { total_male }")

total_male_survivors = len( df[  ( df["Sex"] == "male" ) & ( df["Survived"] == 1 ) ])
print(f"Anzahl überlebender männlich Passagiere ........ : { total_male_survivors }")

# Females
total_female = len( df[ df["Sex"] == "female"] )
print(f"Anzahl weiblicher Passagiere ................... : { total_female }")

total_female_survivors = len( df[  ( df["Sex"] == "female" ) & ( df["Survived"] == 1 ) ])
print(f"Anzahl überlebender männlich Passagiere ........ : { total_female_survivors }")

print(f"Überlebensquote männlicher Passagiere .......... : { total_male_survivors/ total_male}")
print(f"Überlebensquote weiblicher Passagiere .......... : { total_female_survivors/ total_female}")
print(f"Überlebensquote gesamt ......................... : { total_survivors / (total_female + total_male) }")
```

### Übung: Cleaning der`Age`-Spalte

```python
df_age_clean = df[ df["Age"] <= 80]
df_age.describe()
```

Ergebnis:

![](<../.gitbook/assets/image (25).png>)
