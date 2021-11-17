---
description: to be done
---

# Datentransformation

## Standardisierung (Min-Max-Scaling)

Ziel: Vermeiden extrem unterschiedlicher Wertebereiche verschiedener Features.

Beispiel: Nehmen wir an, dass in einem Datensatz mit zwei Features 

- das erste Feature $$x$$ einer Normalverteilung von mit $$\mu=5000,\sigma=2000$$ entspricht
- das zweite Feature  $$y$$ einer Normalverteilung von mit $$\mu=100,\sigma=20$$ entspricht

Dies kann für numerische Verfahren erhebliche Probeme bereiten. In vielen Fällen macht es Sinn metrische Features wie folgt in den Bereich von [0,1] zu skalieren:
$$
x_k = \frac{x_k - x_{min}}{x_{max} - x_{min}}
$$
Verfährt man für das zweite Feature y analog, so sieht Plot für skalierte und und unskalierte Daten wie folgt aus:

![Features nach Skalierung](4-datentransformation.assets/image-20211116190745543.png)

### Python-Code

```python
import numpy as np
import matplotlib.pyplot as plt

N = 100
x = np.random.normal(5000, 2000, N)
y = np.random.normal(100, 20, N)

fig, ax = plt.subplots(1,2, figsize=(15,7))
ax[0].set_xlim(0,10000)
ax[0].set_ylim(0,10000)
ax[0].set_aspect('equal')
ax[0].set_xlabel('x')
ax[0].set_ylabel('y')
ax[0].set_title('Features (unskaliert)')
ax[0].scatter(x, y, marker='+', color='black')
ax[1].set_xlim(0,1)
ax[1].set_ylim(0,1)
ax[1].set_aspect('equal')
ax[1].set_xlabel('x')
ax[1].set_ylabel('y')
ax[1].set_title('Features (skaliert)')
ax[1].scatter((x - x.min())/(x.max()-x.min()), (y - y.min())/(y.max()-y.min()), marker='+', color='black')

plt.show()
print(f"x-min/mean/x_max = {x.min()} / {x.mean()}/ {x.max()}")
print(f"y-min/mean/y_max = {y.min()} / {y.mean()} / {y.max()}")
```



## Label-Transformation

![image-20211117175431514](4-datentransformation.assets/image-20211117175431514.png)

### Python-Code

```python
import numpy as np
from sklearn.preprocessing import LabelEncoder

le = LabelEncoder()
le.fit( ["Virginica", "Setosa", "Versicolor", "Virginica"] )
print( "Classes : ")
print( le.classes_)

le.transform(["Virginica", "Virginica", "Setosa", "Versicolor", "Versicolor"])
print( "\nEncoding : ")
print( le.transform(["Virginica", "Setosa", "Setosa"]) )

print( "\nInverse Encoding : ")
print( le.inverse_transform([2,0,0]))
```

Output:

![image-20211117175518233](4-datentransformation.assets/image-20211117175518233.png)

## One-Hot Encoding

One-Hot-Encoding ist eine Methode, um kategorische Daten als binäre Vektoren darzustellen. Folgende Grafik verdeutlicht die Methode und illustriert den Namen. 

One-Hot-Encoding funktioniert in folgenden beiden Schritten:

1. Extrahiere aus einem Feature/Label die auftretenden Kategorie-Werte
2. Transformiere den/die Kategorie-Wert/e in einen Vektor.

![image-20211117181805616](4-datentransformation.assets/image-20211117181805616.png)

### Python-Code

Glücklicherweise gibt es einen Funktion in `sklearn`, die das für uns erledigt. Folgender Code sollte einfach zu verstehen sein.

```python
from sklearn.preprocessing import OneHotEncoder

enc = OneHotEncoder(sparse=False)
enc.fit( [['A','B'], ['B','A'], ['A','Z'], ['X','Z'], ['A','Z']] )
print("\nKategorien: \n", enc.categories_)

# Transformieren eines Wertes
print("\nOne-Hot-Encoding von [A,Z] : \n", enc.transform( [['A','A']] ) )
```

Ausgabe:

![image-20211117181828638](4-datentransformation.assets/image-20211117181828638.png)



