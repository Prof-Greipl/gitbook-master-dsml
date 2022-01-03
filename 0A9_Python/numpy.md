# Wofür brauchen wir Numpy?

Numpy ist eine Sammlung von Funktionen für effiziente Erzeugung, Berechnung und Bearbeitung von Zahlenstrukturen, zum Beispiel Vektoren oder Matrizen. &#x20;Wir werden Numpy-Arrays nutzen, um die Datensätze für maschinelles Lernen zu bearbeiten.

###### Links für diesen Abschnitt

| Link                                                                                                                                     | Beschreibung                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| [https://www.w3schools.com/python/numpy/default.asp](https://www.w3schools.com/python/numpy/default.asp)                                 | Eine umfangreiche, langsame Einführung. Wir brauchen davon aber nur, was in in diesem Script behandelt wird.  |
| [https://www.w3schools.com/python/numpy/numpy\_creating\_arrays.asp](https://www.w3schools.com/python/numpy/numpy\_creating\_arrays.asp) | arange                                                                                                        |
|                                                                                                                                          |                                                                                                               |

**Wichtig:** Beginnen Sie jeden Programmblock, in dem sie numpy-Funktionen brauchen, mit der Zeile

`import numpy as np`



# Einfache Funktionen

```python
import numpy as np

# Sinus
x = np.sin(0)
print( x )

# Quadrieren
x = np.square(3)
print( x )

# PI
x = np.pi
print( x )

# Eulersche Zahl
x = np.e
print( x )

# Gleichverteilt in [0,1[ 
x = np.random.random()
print(x)

# Erwartungswert 0, Standardabweichung 1
x = np.random.normal(0,1)
print(x)
```



# Vektoren 

Da Feature-Vektoren für uns eine wichtige Rolle spielen, gehen wir näher auf Vektoren in Numpy ein. 



## Erzeugung  "per Hand"

Folgende Befehle erläutern das Thema Vektoren, elementweise Addition, elementweise Multiplikation und Skalarprodukt für Vektoren. Wichtig für die Erzeugung eines Vektors ist Zeile 3.

```python
import numpy as np

y = np.array([5,6,7,8])     # Definiere Vektor y
x = np.array([1,2,3,4])     # Definiere Vektor x
print (f'x    = {x}' )      # Drucke Werte
print (f'y    = {y}' )      # Drucke y
```



## `np.ones() und np.zeros()`

`np.ones(n)` erzeugt einen Vektor der Dimension n, der nur aus Einsen besteht. Analog funktioniert `np.zeros`

```python
v = np.ones(10)
w = np.zeros(10)
```



## `np.arange`()

Mit `np.arange` erzeugen wir automatisch Strukturen, die wir häufiger brauchen. Beschäftigen Sie sich mit den Ausgaben und experimentieren sie etwas, dann wird die jeweilige Funktion recht schnell klar.

```python
import numpy as np

x = np.arange(1,2,0.1)
print( x )
print( x[2] )
print( len(x) )
print ( type(x) )
```



##  `np.linspace`()

```python
import numpy as np

x = np.linspace(0,2*np.pi,20);
print(x)
print( len(x))
```



## Elementweise Operationen

 Nachfolgendes Beispiel zeigt ausgewählte Operationen. Beachten Sie, dass sie die letzten 4Operationen so im Mathe-Unterricht nicht gelernt haben. Sie sind jedoch recht hilfreich!

```python
import numpy as np
x = np.array([1, 4, 9, 0])
y = np.array([1, 0, 1, 0])

print(x*0.5)
print(x+y)
print (x.dot(y))

print (x+1)
print(x*y)
print (np.sqrt(x))
print (np.sin(x))
```



### Übung

Berechnen Sie durch Programmbefehle $$v^Tw,$$ $$v+w$$ und $$2 \cdot v$$ für

$$
v = \begin{bmatrix} 1 \\ -3 \\ 2\\ \end{bmatrix} \quad \text{and} \quad w = \begin{bmatrix} 1 \\ 0 \\ 13\\ \end{bmatrix}
$$







## Zufallszahlen

Link: [https://www.w3schools.com/python/numpy/numpy\_random.asp](https://www.w3schools.com/python/numpy/numpy\_random.asp)

```python
import numpy as np

# Gleichverteilt in [0,1[, 10 Werte
ua = np.random.random(10)
print(ua)

# Erwartungswert 0, Standardabweichung 1, 10 Werte
na = np.random.normal(0,1,10)
print(na)
```





# Matrix

Sie erinnern sich an die Feature-Matrix? Also, los gehts..



## Auffrischung

Gegeben sind die nachfolgenden Vektoren und Matrizen:

$$
A = \begin{bmatrix} 2 & -1 \\ 4 & 0 \\ 9 & 3 \end{bmatrix} \quad\quad\quad C = \begin{bmatrix} 1 & 0 \\ 4 & -1 \end{bmatrix} \quad\quad\quad v = \begin{bmatrix} 1 \\ 4 \\ \end{bmatrix} \quad\quad\quad w = \begin{bmatrix} -1 \\ 3 \\ \end{bmatrix}
$$

Berechnen Sie auf Papier:

* $$A \cdot v$$
* $$A \cdot C$$
* $$wv^t$$



## Matrix als Numpy-Array

Matrizen werden in Numpy als eine Ansammlung von Zeilenvektoren aufgebaut!

```python
import numpy as np

A = np.array([[1,2],[3,4], [5,6], [7,8]])
print( A )
print( A[0,0] )
print( A[0,1] )
```

Obiges Programm ergibt die nachfolgende Ausgabe. Die Indizierung der Element funktioniert erwartungsgemäß, allerdings wird mit der Zählung bei Null begonnen!

![](<numpy.assets/image5.png>)



## Shape (Dimension)

Eine Matrix hat eine Anzahl von Zeilen und Spalten, die wir üblicherweise mit n und m bezeichnet haben. Folgender Befehl liefert die Anzahl der Zeilen und Spalten einer Matrix:

```python
import numpy as np

A = np.array([[1,2],[3,4], [5,6], [7,8]])
print( A.shape )  # Ausgabe: (4,2)
```

Die Ausgabe (4,2) besagt, dass die Matrix vier Zeilen und zwei Spalten besitzt.



## Addition und Multiplikation mit einem Skalar

```python
import numpy as np

A = np.array([[1,2],[3,4], [5,6], [7,8]])
B = np.array([[10,20],[30,40], [50,60], [70,80]])
s = 2;
print (2*A)     # Mulitplikation mit einem Skalar
print (A+B)
```



## Matrixmultiplikation

Die Matrixmultiplikation erfolgt ebenfalls über den Befehl `np.dot` Immer auf die passenden shapes achten!

Beispiel
$$
A = \begin{bmatrix} 1 & 2 \\ 3 & 4 \\ 5 & 6 \end{bmatrix} \quad\quad\quad
B = \begin{bmatrix} 1 & 0 \\ 0 & 2 \end{bmatrix}  \quad\quad\quad
A \cdot B = \begin{bmatrix} 1 & 4 \\ 3 & 8 \\ 5 & 12 \end{bmatrix} \quad\quad\quad
$$
Mit Numpy: `np.dot()`

```python
import numpy as np

A = np.array([[1,2],[3,4], [5,6], [7,8]])
B = np.array([[1,0],[0,2]])
AB = np.dot(A, B) 
print( AB )
```

Ausgabe:

![image-20211211102921206](numpy.assets/image-20211211102921206.png)

## Übung

Lassen sie die Rechnungen in "Auffrischung" in Numpy durchführen.



## Vertiefend



### Zeilenvektoren und Spaltenvektoren

Eigentlich sollten wir unterscheiden zwischen

- Vektor der Dimension $$n$$
- $$1 \times n$$ Matrix ("Zeilenvektor")
- $$n \times 1$$ Matrix ("Spaltenvektor")

In Numpy geht das auch, wie folgende Code zeigt. Wie üblich werden aber Vektoren in das entsprechende Format gebracht. (Stören sie sich bitte nicht an runden und eckigen Klammern - sie haben keine Bedeutung.)
$$
v = \begin{bmatrix} 2 \\ 2 \\ 3 \end{bmatrix} \quad\quad\quad 
vz = (-1, 2, 3)
$$

```python
import numpy as np

v  = np.array([1,2,3])          # Vektor
vz = np.array([[1,2,3]])        # 1 x 3 Matrix
vs = np.array([[1], [2], [3]])  # 3 x 1 Matrix

print(f'v  : {v}')
print(f'vz : {vs}')
print(f'vs : {vz}')

print(f'Shape v  :{v.shape}')
print(f'Shape vz :{vz.shape}')
print(f'Shape vs :{vs.shape}')
```

Wir sollten also stets überlegen, mit welchem shape wir operieren.



### Transponierung

```python
import numpy as np

A = np.array([[1,2],[3,4], [5,6], [7,8]])
AT = np.transpose(A)
print(AT)
```



## Lösung

Lösung zu "Auffrischung"

```python
import numpy as np

A = np.array([[2,-1],[4,0],[9,3]])
C = np.array([[1,0],[4,-1]])
v = np.array([1,4])
w = np.array([-1,3])

res = np.dot(A,v)
print(f'\n Av =\n  {res}, \n Shape = {res.shape}')

res = np.dot(A,C)
print(f'\n A x C = \n {res}, \n Shape = {res.shape}')

res = np.dot(v, w)
print(f'\n <w,v> = \n {res}, \n Shape = {res.shape}')
```

