# Feature-Matrix und Label-Vektor



> Wir wiederholen und präzisieren in diesem Abschnitt auch die Begriffe _Feature _und _Label_.&#x20;

## Feature

Ein Feature ist eine Eingabe für unsere Problemstellung. Aus einem oder mehreren Werten für Features wollen wir eine Vorhersage treffen. Bei Titanic sind _Pclass, Sex, Age, _etc. Features. _Survived _ist kein Feature, da wir diesen Wert vorhersagen wollen. Die Anzahl der Features einer Problemstellung nennen notieren wir mit dem Buchstaben $$m$$.

## Eingabe (Feature Vektor)

Eine Eingabe oder auch Feature-Vektor besteht aus einem konkreten Wert für jedes Feature. Diese Werte notiert man in der Regel als Vektor $$x  \in \mathbb{R}^{m}$$ . (Streng genommen müssten wir $$x^T$$ schreiben, da es sich um einen Zeilenvektor handelt. Wir machen das aber nur, wenn es für das Verständnis relevant ist.) Ein Feature-Vektor ist stets (tatsächlich oder möglicherweise) durch _Feature Engineering _aus  einer Beobachtung hervorgegangen. In nachfolgender Abbildung ist ein Feature-Vektor gelb markiert.

$$
x = (1,1,3,1,0,8,1)
$$

## Label

Ein Label ist ein Wert aus einer Ergebnismenge $$Y$$ . Bei Titanic ist diese Ergebnismenge $$\{0,1\}$$, interpretiert als _nicht überlegt_ und _überlebt_. Wir notieren den Label  (möglichst) mit dem Buchstaben $$y$$.&#x20;

## Labelled Example

Ein _labelled example _besteht aus einem _Feature Vektor _ $$x$$ und  einem zugehörigen _Label _$$y$$.&#x20;

![](<../../.gitbook/assets/image (91).png>)

## Beispiel (Titanic)

In nachfolgendem Bild entspricht die farbig hinterlegte Zeile einem _labelled Example_. Die Eingabe ist gelb hinterlegt und der Label ist rot hinterlegt. Lassen Sie sich nicht durch die Reihenfolge der Spalte stören.

![](<../../.gitbook/assets/image (77).png>)

Formal notiert:

$$
x = (1,1,3,1,0,8,1) \quad y = 1
$$



## Datensatz, Feature-Matrix und Label-Vektor

Ein Datensatz ist eine Menge von $$n$$ labelled Examples $$(\bold{x_i}, y_i)$$ mit $$\bold{x_i} \in  \mathbb{R}^m$$ und $$y_i \in Y$$.  Betrachtet man die Eingaben als Zeilenvektoren und schichtet sie aufeinander, so erhält man ein Feature-Matrix über den reellen Zahlen, die wir mit $$\bold{X}$$  bezeichnen. Wenn wir nun die Labels analog zu den Eingaben aufschichten, so erhalten wir einen Label-Vektor  $$\bold{y}$$. Es ist dann:

$$
\bold{X}= 
\begin{bmatrix}
x_0  \\
x_1  \\
\vdots  \\

x_{n-1}
\end{bmatrix}
\in \mathbb{R}^{n \times m}
\quad\text{      und      } \quad
\bold{y}= 
\begin{bmatrix}
y_0  \\
y_1  \\
\vdots  \\
y_{n-1}
\end{bmatrix}

\in\mathbb{R}^{n}
$$

Für Titanic ist also nach dem Schritt Feature Engineering:  $$n = 891$$ und $$m =$$ 7. Die Zeilen einer Feature Matrix repräsentieren jeweils eine Eingabe. In der nachfolgenden Abbildung ist die Feature Matrix für Titanic mit schwarzen Klammern markiert und der Label-Vektor$$\bold{y}$$in roten Klammern.

&#x20;

![](<../../.gitbook/assets/image (78).png>)

