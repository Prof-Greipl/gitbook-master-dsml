# Aktivierungsfunktionen

Unser Perzeptron ist für $$\phi(x) = x$$ bisher eine lineares Modell. Lineare Modell haben ihre Grenzen beim Lösen komplexerer Aufgabenstellungen. Wir verwenden daher in der Praxis nicht-lineare, aber immer noch einfache Aktivierungsfunktionen.

## Rectified Linear Unit \(ReLU\)

ReLU modifiziert nur den negative Teil der Identitätsfunktion und setzt den negativen Teil auf Null, daher auch die Bezeichnung "rectifier = Gleichrichter".

$$
\phi(x) = \left\{
\begin{array}{ll}
x &,\text{falls} \geq 0 \\
0 & \, \textrm{sonst} \\
\end{array}
\right.
$$

 Der Graph von ReLU ist recht einfach:

![](../../.gitbook/assets/image%20%28158%29.png)

Die Befehle zum Zeichnen dieses Graphen finden Sie hier. 

Die ReLu Aktivierung erlaubt ein Einstellung eines Neurons so, dass es nur dann eine positive Ausgabe liefert, wenn der Ausgabewert positiv ist. Damit gewinnt der Parameter  $$b$$ eine anschauliche Bedeutung. Das Neuron liefert nur dann ein \(stets positives\) Ergebnis wenn die Gewichtung der Eingabewert größer als $$-b$$ ist.

## Sigmoid

Die Sigmoid-Aktivierung dient dazu, die Ausgaben eines Neurons in das Intervall von 0 bis 1 zu pressen. Die Definition ist etwas komplizierter:

$$
\phi(x) = \frac{1}{1+e^{-x}}
$$

Wie sie leicht sehen, strebt die Sigmoid-Funktion für sehr große Werte von x gegen Eins und für sehr stark negative Werte von x gegen Null. Hier der Funktionsgraph:

![](../../.gitbook/assets/image%20%28159%29.png)

## Netzwerk-Layer \(Input-, Output-Layer\)

Wir wollen nun mehrere Neuronen zu einem Netz verschalten und brauchen dazu eine strukturierte Anordnung der Neuronen. Nachfolgende Grafik zeigt das rechte einfache Konzept eines Layers, in dem wir  drei Neuronen in einer Schicht aufbauen. 

![](../../.gitbook/assets/image%20%28148%29.png)

Wichtig:

1. Man bezeichnet die Ebene der Eingabewerte, also der Features, auch als **Input Layer**
2. Das obige Netz gibt drei Werte aus. Das Layer, das Werte ausgibt, heißt auch **Output-Layer**.



