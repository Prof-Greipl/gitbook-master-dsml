# Skalare, Vektoren Matrizen mit Numpy

Wir haben in der der Einführung motiviert, dass Vektoren und Matrizen relevant für die Modellierung von Learning Problemen sind. In diesem Abschnitt modellieren wir diese Strukturen mit dem Paket NumPy. Wikipedia bringt es auf den Punkt: "NumPy is a library for the Python programming language, adding support for large, multi-dimensional arrays and matrices, along with a large collection of high-level mathematical functions to operate on these arrays."

Vektoren und Matrizen werden wir als NumPy-Arrays darstellen. Arrays entsprechen Listen, bestehen aber immer nur aus Zahlen!

## NumPy-Vektoren

### Addition und Skalarprodukt

Folgende Befehle erläutern das Thema Vektoren, elementweise Addition, elementweise Multiplikation und Skalarprodukt für Vektoren. Wichtig für die Erzeugung eines Vektors ist Zeile 3.

```python
import numpy as np

y = np.array([5,6,7,8])     # Definiere Vektor y
x = np.array([1,2,3,4])     # Definiere Vektor x
print (f'x    = {x}' )      # Drucke Werte
print (f'y    = {y}' )      # Drucke y


# Addition x+y
y = np.array([5,6,7,8])     # Definiere Vektor y
print (f'x+y  = {x+y}' )    # Drucke x+y

# Skalarprodukt x*y
z = np.dot(x,y)             # Berechne x*y
print (f'x*y  = {z}' )      # Drucke z
```

### Elementweise Operationen

Daneben gibt es noch sinnvolle Befehle, wie die Anwendung einer auf reellen Zahlen operierende Funktion $$f :\mathbb{R} \rightarrow \mathbb{R}$$ auf die einzelnen Elemente eines Vektors (Vertiefung). Nachfolgendes Beispiel zeigt ausgewählte Operationen:

```python
import numpy as np
x = np.array([1,4,9, 0])

print (x+1)
print (x*0.5)
print (np.sqrt(x))
print (np.exp(x))
print (np.sin(x))
```

### Übungen

Berechnen Sie durch Programmbefehle$$v^Tw,$$ $$v+w$$ und $$2 \cdot v$$ für

$$
v = \begin{bmatrix} 1 \\ -3 \\ 2\\ \end{bmatrix} \quad \text{and} \quad w = \begin{bmatrix} 1 \\ 0 \\ 13\\ \end{bmatrix}
$$

([Lösung](https://the-technology-lab.gitbook.io/bw-610-dsml/analytics-und-datascience/loesungen-und-vertiefungen#uebung-zu-vektoren))

## Numpy-Matrix

### Basics

Matrizen werden in Numpy als eine Ansammlung von Zeilenvektoren aufgebaut!

```python
A = np.array([[1,2],[3,4], [5,6], [7,8]])
print( A )
print( A[0,0] )
print( A[0,1] )
```

Obiges Programm ergibt die nachfolgende Ausgabe. Die Indizierung der Element funktioniert erwartungsgemäß, allerdings wird mit der Zählung bei Null begonnen!

![](<2_skalare-vektoren-matrizen-mit-numpy.assets/image (5) (1) (1) (1).png>)

### Shape (Dimension)

Eine Matrix hat eine Anzahl von Zeilen und Spalten, die wir üblicherweise mit n und m bezeichnet haben. Folgende Befehl liefert die Anzahl der Zeilen und Spalten einer Matrix

```python
import numpy as np
A = np.array([[1,2],[3,4], [5,6], [7,8]])
print( A.shape )  # Ausgabe: (4,2)
```

Die Ausgabe (4,2) besagt, dass die Matrix vier Zeilen und zwei Spalten besitzt.

### Zeilenvektoren und Spaltenvektoren

> In NumPy gibt es keine Identifikation von Vektoren mit Spaltenvektoren!

Folgendes Beispiel zeigt, dass Phython Vektoren nicht mit Spaltenvektoren oder gar Zeilenvektoren identifiziert.

```python
import numpy as np
x_vektor        = np.array([1,2,3])   
x_zeilenvektor  = np.array([[1,2,3]]) 
x_spaltenvektor = np.array([[1], [2], [3]])

print(f'x_vektor        :{x_vektor}')
print(f'x_zeilenvektor  :{x_zeilenvektor}')
print(f'x_spaltenvektor :{x_spaltenvektor}')

print(f'Shape x_vektor        :{x_vektor.shape}')
print(f'Shape x_zeilenvektor  :{x_zeilenvektor.shape}')
print(f'Shape x_spaltenvektor :{x_spaltenvektor.shape}')
```

Wir müssen uns also stets überlegen, ob wir mit einer Matrix oder einem Vektor operieren wollen.

### Addition und Multiplikation mit einem Skalar

```python
A = np.array([[1,2],[3,4], [5,6], [7,8]])
B = np.array([[10,20],[30,40], [50,60], [70,80]])
s = 2;
print (2*A)     # Mulitplikation mit einem Skalar
print (A+B)
```

### Transponierung

```python
A = np.array([[1,2],[3,4], [5,6], [7,8]])
AT = np.transpose(A)
print(AT)
```

### Matrixmultiplikation

Die Matrixmultiplikation erfolgt ebenfalls über den Befehl `np.dot`

```python
A = np.array([[1,2],[3,4], [5,6], [7,8]])
B = np.array([[10,20],[30,40], [50,60], [70,80]])

C = np.dot(A, np.transpose(B))   # Addition
```

### Übung

**Gegeben sind die nachfolgenden Vektoren und Matrizen:**

$$
A = \begin{bmatrix} 2 & -1 \\ 4 & 0 \\ 9 & 3 \end{bmatrix} \quad\quad\quad C = \begin{bmatrix} 1 & 0 \\ 4 & -1 \end{bmatrix} \quad\quad\quad v = \begin{bmatrix} 1 \\ 4 \\ \end{bmatrix} \quad\quad\quad w = \begin{bmatrix} -1 \\ 3 \\ \end{bmatrix}
$$

Berechnen Sie **durch Programmbefehle**:

* $$Av$$
* $$AC$$
* $$wv^t$$

([Lösung](https://the-technology-lab.gitbook.io/bw-610-dsml/analytics-und-datascience/loesungen-und-vertiefungen#uebung-zu-matrix))

## Erzeugung von Numpy-Matrizen und Numpy-Vektoren

### np.ones( .. )

`np.ones(n)` erzeugt einen Vektor der Dimension n, der nur aus Einsen besteht.

```python
v = np.ones(1000)
print (v.shape)
```

`np.ones( (n,m))` erzeugt eine nxm Matrix, die nur Einsen aus Einträge hat

```python
import numpy as np
A = np.ones((4,10))
print(A)
print(A.shape)
```

### np.random.rand(n,m)

erzeugt eine nxm Matrix mit gleichverteilten Zufallszahlen

```python
import numpy as np
R = np.random.rand(5,3)
print (R)
print (R.shape)
```

Wenn Sie `randn `statt rand schreiben, erhalte Sie eine Normalverteilung

### Reshape und Flatten

```python
import numpy as np

# Reshaping
v = np.array([1,2,3,4,5,6,7,8,9,10,11,12])
A = v.reshape((3,4) )
print( A )
print( A.shape)

# Flattening
w = A.flatten()
print(w)
print(w.shape)
```

### Übung

Informieren Sie sich über die Befehle `np.zeros()`, `np.amax()` und `np.amin() `Testen Sie ihr Verständnis anhand einiger Befehle!

([Lösung](https://the-technology-lab.gitbook.io/bw-610-dsml/analytics-und-datascience/loesungen-und-vertiefungen#funktionen-np-zeros-np-amax-np-amin))
