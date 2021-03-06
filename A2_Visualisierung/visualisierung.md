---
description: >-
  In diesem Abschnitt beschäftigen wir uns mit der Visualisierung von Daten mit
  der Bibliothek matplotlib.
---

# A.2 Visualisierung mit matplotlib

## Matplotlib

Mathplotlib ([https://matplotlib.org/](https://matplotlib.org)) ist eine Sammlung von Funktionen (Bibliothek)zum Visualisieren von Daten. Es gibt hierzu mächtigere Bibliotheken, aber für den Start ist das ok. Dokumentation und ergänzende Inhalte finden sie auf [https://matplotlib.org/tutorials/introductory/pyplot.html#sphx](https://matplotlib.org/tutorials/introductory/pyplot.html#sphx)&#x20;

## Liniendiagramme

Hier ein erstes Beispiel:

```python
from matplotlib import pyplot as plt

years = [1950, 1960, 1970, 1980, 1990, 2000, 2010]
gdp = [33.2, 543.3, 1075.9, 2862.5, 5979.6, 10289.7, 14958.3]

# Erstelle Liniendiagramm 
plt.plot( years, gdp, color="green", marker='o', linestyle='-')

# Füge Titel hinzu
plt.title('Nominal GDP')

# Beschrifte y-Achse
plt.ylabel('Billons of USD')

# ... und zeige die Grafik an.
plt.show()
```

Sie sollten folgende Ausgabe sehen:

![](<../.gitbook/assets/image (1).png>)

Können Sie die x-Achse noch mit "Years" beschriften?

### Übung

1. Können Sie die x-Achse in obiger Kurve noch mit "Years" beschriften?
2. Versuchen obige Kurve mit anderer Farbe, Linienart und Punktmarkierungen zu zeichnen! (Hinweis: [https://matplotlib.org/gallery/lines\_bars\_and\_markers/line\_styles\_reference.html](https://matplotlib.org/gallery/lines\_bars\_and\_markers/line\_styles\_reference.html), [https://matplotlib.org/3.1.0/gallery/color/named\_colors.html](https://matplotlib.org/3.1.0/gallery/color/named\_colors.html), [https://matplotlib.org/api/markers\_api.html](https://matplotlib.org/api/markers\_api.html)) &#x20;

### Achsen

Mit dem nachfolgendem Befehl legen Sie durch die ersten Einträge der Liste den Bereich der x-Achse und mit den nachfolgenden Zahlen der Bereich der y-Achse fest.  Fügen Sie den Befehl vor `plt.show()` ein!

```python
plt.axis([1900, 2020, 0, 20000])
```

Obige Ausgabe zeigt, dass die Achsen nicht gleich skaliert sind. Sie erreichen dies mit dem Befehl. Beachten Sie, dass der Skalierungsbefehl immer _vor _der Definition der Achsen kommen muss.

```python
plt.axis('scaled')
```



## Balkendiagramme

Balkendiagramme werden wir immer wieder benötigen. Betrachten Sie folgendes Beispiel (aus :

```python
movies = ['Annie Hall', 'Ben-Hur', 'Casablanca', 'Gandhi', 'West Side Story']
num_oscars = [5,11,3,8,10]
plt.bar( [0,1,2,3,4], num_oscars )

plt.title('My favourite Movies')
plt.ylabel('# of Academy Awards')
plt.xticks([0,1,2,3,4], movies)
plt.show()
```

Sie sollten folgendes Ergebnis sehen:

![](<../.gitbook/assets/image (2).png>)

Können Sie in Zeilen 3 und  7 die Listen durch einen range ersetzen?&#x20;

## Scatterplots

Paarweise Daten (Punktwolken) lassen sich durch Scatterplots darstellen.&#x20;

```python
test1_punkte = [99, 90, 85, 97, 80]
test2_punkte = [100,85, 60, 90, 70]
plt.scatter( test1_punkte, test2_punkte)
plt.show()
```

Obiges Programm sollte ergeben:

![](<../.gitbook/assets/image (3).png>)

Was stört sie an der Ausgabe?



### Übung

In der Übung zu ranges haben sie eine Liste mit 50 gleichverteilen Zufallszahlen erstellt.&#x20;

1. Erzeugen Sie zwei dieser Listen und zeigen sie das Ergebnis in einem Scatterplot an. ([Lösung](../vertiefungen/loesungen-und-vertiefungen.md#scatterplot-von-paaren-aus-zufallszahlen))
2. Welches Ausgabe erwarten Sie, wenn Sie jeweils 2000 Zahlen erzeugen

## Histogramm

```python
// Some code
import matplotlib.pyplot as plt
x = [1,2,2,3,3,3,4,4,5]
(n, bins, patches) = plt.hist(x, bins="auto")
print(f"n   = {n}")
print(f"bin = {bins}")
print(f"patches = {patches}")
```

## Funktionsgrafen plotten

Häufig wollen wir den Grafen einer Funktion f: R->R plotten. In diesem Fall geben die Paare für eine Auswahl von x aus dem Definitionsbereich die Paare (x,f(x)) eine Menge von Punkten, die wir durch eine Linie verbinden. Wir nehmen als Beispiel die Funktion

$$
f(x) = x^3 - 2x -1
$$

auf dem Intervall \[min,max]. Wir wollen an `n` verschiedenen x-Werten plotten.

### Einzelschritte

Wir  erzeugen zuerst die Menge eine Liste mit x-Werten mit der Funktion `x_werte`

```python
def x_werte (min, max, n):
  liste = []
  for i in range(n):
     liste.extend( [min + i*(max-min)/n] )
  return liste

print (x_werte(-1,1,11))
```

Versuchen sie diese Funktion zu verstehen!

Nun brauchen wir die Funktionswerte. Wieder programmieren wir selbst eine Funktion:

```python
def f( liste ):
  n = len(liste)
  y = []
  for i in range(n):
    x = liste[i]
    y.extend( [ x*x*x + 2*x - 1 ] )
  return y
```

Schließlich zeigen wir die Funktion an. Insgesamt ergibt das folgendes Programm:

### Gesamtes Programm

```python
from matplotlib import pyplot as plt

def x_werte (min, max, n):
  liste = []
  for i in range(n):
     liste.extend( [min + i*(max-min)/n] )
  return liste

def f( liste ):
  n = len(liste)
  y = []
  for i in range(n):
    x = liste[i]
    y.extend( [ x*x*x - 2*x - 1 ] )
  return y

min = -2
max = 2
N = 1000

x_values = x_werte(min,max,N)
y_values = f(x_values)
plt.plot( x_values, y_values, color='blue', linestyle='solid')
plt.axis('scaled')                 # Achsen gleich skalieren
#plt.gca().set_aspect('equal', adjustable='box')
plt.axis([-2,2,-3,3])
plt.grid(True)
plt.show()
```

Ausgabe:

![](<../.gitbook/assets/image (4).png>)







