Anhand des Zirpens von Grillen kann man mehr oder weniger verlässlich die Lufttemperatur berechnen. Die Körperfunktionen von Grillen verändert sich wie bei anderen Insekten auch durch veränderte Lufttemperatur.  Wie alle Insekten sind Grillen kaltblütig und nehmen die sie umgebende Temperatur an. Je wärmer, desto häufigeres Zirpen, denn: Ist es wärmer, laufen die Körperfunktionen – wie auch Bewegungen – schneller ab, die Grillen sind aktiver. \[…] Da Grillen also bei erhöhter Temperatur häufiger Zirpen, kann man aus der Häufigkeit des Zirpens die Lufttemperatur ableiten. Die Formel dafür ist sehr simpel. Um die Temperatur in Grad Celsius zu errechnen, zählt man das Zirpen einer einzelnen Grille in einem Intervall von 25 Sekunden. ([Quelle](https://www.heute.at/s/so-verraten-ihnen-grillen-die-aktuelle-temperatur-54218483))

# Dataset

Nehmen wir an, dass folgende kleine Menge von labelled examples vorliegt: 

![](<readme.assets/image (136).png>)

Natürlich wollen wir nun - wie üblich - aus dem feature den label vorhersagen. Offensichtlich handelt es sich um ein Regressionsproblem. Nachfolgendes Bild visualisiert die Daten:

![image-20211205172941481](readme.assets/image-20211205172941481.png)

# Phython

```python
from matplotlib import pyplot as plt
import seaborn as sns


import pandas as pd
import numpy as np

chirps = pd.DataFrame({
    "Count": [31,16,29,43,27,19,47,9,45,5,39],
    "Temp": [9.4,10.5,17.1,24.3,14.6,9.9,16.9,6.4,17.7,7.5,14.2]    
})


fig,ax = plt.subplots(figsize=(9, 9))
ax.set_aspect('equal')
ax.set_title("Chirps-Data") 
ax.set_xlabel("Count")
ax.set_ylabel("Temperature")

ax.set_xlim(0, 50)
ax.set_ylim(0, 35)

sns.set()
sns.scatterplot(data = chirps, x = "Count", y="Temp", label="Temp")
```



# Modellfamilie

Unsere Modellfamilie sind die linearen Funktionen  $$M_{w,b} : \mathbb{R} \rightarrow   \mathbb{R}$$, definiert durch

$$
M_{w,b}(x) = x \cdot w +b
$$

Wir suchen also $$w$$ und $$b$$  in $$\mathbb{R}$$, so dass unser dadurch definiertes Modell unseren Datensatz möglichst gut vorhersagt. Offenbar ist M für fest gewähltes w und b eine lineare Funktion, die wir gut visualisieren können.



## Übung

1. Tragen sie die Funktion (Gerade) $$M_{2,5}$$ in das Koordinatensystem in diesem [Link](https://hawlandshutde-my.sharepoint.com/:p:/g/personal/dgreipl_az_haw-landshut_de/EVP2qxD2yfhFspTxcEiDBA8BSx3up_SbE0lADod7WLM9EQ?e=e5h7mw) in **die erste Folie** ein. 
2. Tragen sie die aus Ihrer Sicht beste Gerade für obigen Datensatz in das Koordinatensystem in diesem [Link](https://hawlandshutde-my.sharepoint.com/:p:/g/personal/dgreipl_az_haw-landshut_de/EVP2qxD2yfhFspTxcEiDBA8BSx3up_SbE0lADod7WLM9EQ?e=e5h7mw) **in die zweite Folie** ein. Nennen sie eine Abschätzung für Gewicht $$w$$ und Bias $$b$$  dieser Gerade.



# Fehlerfunktion (Loss)

Um die Qualität eines gewählten Modells zu verwenden verwenden wir den schon bekannten  MSE:

$$
\text{MSE}(w,b) = \frac{1}{n}\sum_{i=0}^{n-1} (M_{w,b}(x_i) -y_i) ^2
$$

für alle $$n$$ labelled examples$$(x_i,y_i)$$ aus dem Dataset. Durch Einsetzen der Definition von $$M$$ ergibt sich nun:

$$
\begin{align*}
\text{MSE}(w,b)
    &= \frac{1}{n}\sum_{i=0}^{n-1} ( x_i\cdot w + b - y_i ) ^2
\end{align*}
$$



# Visualisierung der Fehlerfunktion

Der MSE ist eine reelle Zahl, die von w und b abhängt.  Wir können daher den MSE-Graph als Fläche über der Weight-Bias Eben plotten. Der Pfeil zeigt auf den Wert von $$w$$ und $$b$$, an dem wir das Minimum der Fehlerfunktion erwarten.

![image (138) (1)](readme.assets/image (138) (1).png)

Am tiefsten Punkt der Fläche haben wir das beste Modell gefunden. Der kleine Punkt in der Grafik markiert in etwa diesen Punkt. Aber wir kommen wir dorthin?



# Gradientenabstieg (_gradient descent_)

Wir haben eben gesehen, dass die Fehlerfunktion MSE nur von w und b abhängt. Das Minimum von Funktionen lässt sich unter bestimmten Umständen, so wie in diesem Beispiel,  durch die erste Ableitung berechnen. In der Praxis gelingt das aber nur selten. Erfolgversprechender ist das sukzessive Absteigen  auf der Fläche. Da unserer Fehlerfunktion differenzierbar ist, ist der negative Gradient die beste Abstiegsrichtung. In folgender Abbildung ist zur Verdeutlichung ein willkürlicher "Abstiegspfad" eingezeichnet:

![](<readme.assets/image (125).png>)

  



Das Abstiegsverfahren lässt sich etwas besser anhand eines Grafen einer Loss-Funktion $$L: \mathbb{R} \rightarrow \mathbb{R}$$ veranschaulichen. Wir nehmen dabei an, dass wir den Loss (=MSE) nur entlang der w-Achse minimieren wollen, also  angenommen, dass der Loss  nur von $$w$$ abhängt.





## Skizzierung des Abstiegsverfahrens

Ist L differenzierbar und  $$L´(w_0) < 0$$ für einen zufällig gewählten Startwert $$w_0$$ , so gilt wegen
$$
L^´(w_0) = \lim_{h \rightarrow 0} \frac{L(w_0+h) - L(w_0)}{h}  <0
$$

für hinreichend kleines $$h_0 > 0$$:

$$
\frac{L(w_0+h_0) - L(w_0)}{h_0}  <0
$$

und damit

$$
L(w_0+h_0) < L(w_0)
$$

Nun setzt man $$w_1 = w_0 + h_0$$ und fährt weiter fort. 



# Optimales Modell mit Python

Wir können die optimalen Paramater einfach berechnen lassen. Das Ergebnis ist: 

![image-20211205175741435](readme.assets/image-20211205175741435.png)

Übrigens lässt sich das auch analytisch berechnen. Sie können das hier nachlesen.



## Python

Wir erzeugen zunächst die recht einfache Feature Matrix $$X \in \mathbb{R}^{11 \times 1}$$ und den Label-Vektor $$y\in \mathbb{R}^{11}$$ 

```
from sklearn.linear_model import LinearRegression

X = chirps["Count"].to_numpy().reshape(11,-1)
y = chirps["Temp"].to_numpy().reshape(11,-1)
print(y)

reg = LinearRegression().fit(X, y)
print("weight vector   w = : ", reg.coef_ )
print("intercept value b = : ", reg.intercept_)

y_pred = reg.predict(X)
print("              MSE = : ", ((y-y_pred)*(y-y_pred)).sum()/11 )
```



# Visualisierung des optimalen Modells



Folgende Abbildung zeigt das optimale Modell:

![image-20211205180928324](readme.assets/image-20211205180928324.png)

## Python

```python
from matplotlib import pyplot as plt
import seaborn as sns
import pandas as pd
import numpy as np

chirps = pd.DataFrame({
    "Count": [31,16,29,43,27,19,47,9,45,5,39],
    "Temp": [9.4,10.5,17.1,24.3,14.6,9.9,16.9,6.4,17.7,7.5,14.2]    
})

X = chirps["Count"].to_numpy().reshape(11,-1)
y = chirps["Temp"].to_numpy().reshape(11,-1)
print(y)

reg = LinearRegression().fit(X, y)
w = reg.coef_[0][0] 
b = reg.intercept_[0]

x_values = np.array([0, 50])
y_values = np.array([b, 50*w + b])

fig,ax = plt.subplots(figsize=(9, 9))
ax.set_aspect('equal')
ax.set_title("Chirps-Data") 
ax.set_xlabel("Count")
ax.set_ylabel("Temperature")

ax.set_xlim(0, 50)
ax.set_ylim(0, 35)

sns.set()
sns.scatterplot(data = chirps, x = "Count", y="Temp", label="Temp")
sns.lineplot(x=x_values,y=y_values, color="red", label="best line xw+b")
```



# Vertiefung : Analytische Berechnung des Optimums&#x20;



Wir berechnen (Kandidaten für das Optimum der MSE-Verlustfunktion analytisch:

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



Für unsere Werte ergibt sich (gerundet, mit Hilfe von Excel und nach Division durch den Faktor von $$w^*$$):
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

Vergleichen Sie die Werte mit dem Ergebnis oben!
