# 3 Numerische Daten

In diesem Kapitel geht es im Kern um Zahlen, Vektoren und Matrizen. All das ist ihnen bekannt, aber weshalb spielt es für maschinelles Lernen - und da wollen wir hin - eine wichtige Rolle.

## Modellierung des Lernproblems

### Problembeschreibung

Nehmen Sie an wir haben Daten zu _vielen gleichartigen  Beobachtungen_, Messungen oder Auswertungen. Dies könnten sein:

1. Zählung, wie häufig Grillen innerhalb von 25 Sekunden zirpen, einschließlich der aktuellen Außentemperatur.
2. Aufzeichnungen von Hubraum, Anzahl der Zylinder, Gewicht und Baujahr eines Autos, einschließlich des jeweiligen Benzinverbrauchs
3. Webshop-Auswertungen zu Wochentag, Artikeln, Browser, Region, Preis einschließlich der Anzahl der Verkäufe. 
4. Messungen zum Zustand einer Maschine \(Lautstärke, Vibration, Energieverbrauch\) einschließlich der Aussage ob in den nächsten 10 Tagen nach der Messung ein Ausfall der Maschine erfolgte.

Die spannende Frage ist nun, ob sich aus diesen _vielen gleichartigen  Beobachtungen_ eine einzelne Beobachtung vorhersagen lässt, also

1. Lässt sich aus der Anzahl des Zirpens von Grillen innerhalb von 25 Sekunden die Außentemperatur vorhersagen?
2. Lässt sich aus dem {Hubraum, Anzahl der Zylinder, Gewicht, Baujahr} der Benzinverbrauch vorhersagen?
3. Lässt sich aus {Wochentag, Artikel, Browser, Region, Preis} auf die Anzahl der Verkäufe schließen?
4. Lässt sich aus dem Tripel {Lautstärke, Vibration, Energieverbrauch} vorhersagen, ob die Maschine innerhalb der nächsten 10 Tage ausfällt?



Die Beantwortung der genannten Fragen hat offensichtlich einen gewissen Wert. 

### Modellierung

Unser Ansatz ist nun, dass wir das Problem mathematisch modellieren:  Finde eine Funktion $$P$$ , mit

$$
P (l,v,e) \in [0,1]
$$

wobei $$l$$ für die gemessene Lautstärke, $$v$$  für das numerische Ergebnis der Vibrationsmessung und schließlich $$e$$  für den gemessenen Energieverbrauch steht. Das Ergebnis  beschreibt dann die Wahrscheinlichkeit für den Ausfall der Maschine innerhalb der nächsten 10 Tage. Eine exemplarische Beobachtung wäre also ein Vektor der Form

$$
(60, 40, 1750, 0)
$$

der besagt, dass die Maschine bei einer Lautstärkenmessung von 27, einem Vibrationswert von 40 und einer Energieaufnahme von 1750 nicht ausgefallen ist. \(Letzteres ergibt sich aus dem letzten Wert 0. Wäre die Maschine ausgefallen so stünde dort eine 1\).

Aus dieser Überlegung leitet sich folgendes ab: 

* Eine einzelne Beobachtung oder Messung ist also ein Vektor \(Zeilenvektor\). Wir strukturieren den Zeilenvektor so, dass die letzte Spalte der Wert ist, den wir vorhersagen wollen.
* Eine Menge von Beobachtung ist eine Matrix.

Wenn wir mehrere Beobachtungen haben, also z.B: 

$$
(60,40,1750,0) \\ (80,32,1950,1) \\ (23, 17,1720,0) \\ ...
$$

Dann definieren wir eine Matrix und eine Vektor

$$
X    =   \begin{bmatrix}
           60,40,1750\\
           80,32,1950 \\
23,17,1720 \\
           \vdots \\
           
         \end{bmatrix} \in \mathbb{R}^{N \times 3} \quad \text{und} \quad
y    =   \begin{bmatrix}
          0\\
           1 \\
0 \\
           \vdots \\
           
         \end{bmatrix}
\in \mathbb{R}^{N}
$$

Wobei  $$N \in  \mathbb{N}$$ die Anzahl der Messungen oder Beobachtungen ist. Unter diesen Annahmen suchen wir nun eine Funktion  P mit 

$$
P(X) = y
$$

Würden wir eine derartige Funktion finden, so könnten wir hoffen, dass wir aus der Beobachtung von Laustärke, Vibration und Energieaufnahme durch Auswertung mittels P eine Aussage über die Ausfallwahrscheinlichkeit innerhalb der nächsten 10 Tage machen können.

Aus diesem Beispiel sollte klar werden, weshalb wir  uns in diesem Abschnitt mit Vektoren und Matrizen beschäftigen.



  

 









