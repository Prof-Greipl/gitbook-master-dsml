# Modellfamilie und Loss

## Modell (Model) und Prediction

Ein **Modell **_M_ ist eine Repräsentation des Programms, das einem Feature-Vektor x einen Label y zuordnet, also

$$
M: \mathbb{R}^m \rightarrow Y \\ M(x) = y
$$

Jedes Modell ist grundsätzlich eine Lösung der Aufgabenstellung (wobei es gute und schlechte Lösungen gibt..). Bei Titanic wäre der Ansatz, jeder Eingabe $$x$$ den Label  0 zuzuordnen, ein Modell - wenn auch kein besonders gutes...

Der Wert $$M(x)$$ heißt auch **Vorhersage **oder **Prediction** des Modells für den Feature-Vektor $$x$$. Ein Modell ist also dann "gut", wenn die Vorhersage  $$M(x)$$ möglichst oft dem erwarteten Ergebnis entspricht oder nahe daran liegt.&#x20;

### Klassifikation

Besteht die Ergebnismenge Y aus $$k$$ Elementen , also  $$Y = \{0, \dots,k-1\}$$, ( $$k \geq 2)$$ . So spricht man von **Klassifikation**. Dabei ist  $$k$$  meist im maximal zweistelligen Bereich. Für den Spezialfall $$k=2$$ sprechen wir von **binärer Klassifikation**. Die zugehörige Problemstellung heißt Klassifikationsproblem.

### Regression

Wählen wir$$Y = \mathbb{R}$$, weil die Labels quantitative Daten sind, so spricht man von **Regression**.&#x20;

![](<../../.gitbook/assets/image (92).png>)

## Loss&#x20;

Um zu bewerten, wie gut (oder schlecht) ein Modell ist, messen wir für einen Datensatz $$(X,y)$$, wie weit die Vorhersagen von den Labels abweichen. Man verwendet zum Beispiel für Regressionsprobleme in der Regel den sogenannten _mean squared error _(MSE):

$$
\text{MSE}(M,X,y) = \frac{1}{n}\sum_{i=0}^{n-1} (M(x_i) - y_i)^2
$$

Wir behandeln den Loss für Klassifizierung eventuell später noch.&#x20;

## Accuracy

Für **Klassifikation **definieren wir die Qualität des Verfahrens durch den Anteil der korrekt klassifizierten Eingaben, also

$$
A(M, X,y) = \frac{\text{Anzahl der korrekten Vorhersagen}}{\text{Anzahl der Examples}}=\frac{| \{ x_i, \text {mit }M(x_i) = y_i\}|}{n}
$$



## Modellfamilie

Man kann sich leicht überlegen, dass es sehr, sehr viele Modelle zu einem Datensatz gibt. Um mit dieser Vielfalt umzugehen, betrachtet man eine _Modellfamilie_, also eine konkrete Menge von passender Modellen, die von Parametern definiert wird. Das zu einem Parameter $$p$$ gehörige Modell nennen wir $$M_p$$ . Hört sich recht schwierig an, daher ein Titanic-Beispiel, bei dem  $$p$$ eine positive reelle Zahl ist.

$$
M_p(x) = \left\{
\begin{array}{ll}
0 & \text{falls } x_{Age} \geq p \\
1 & \, \textrm{sonst} \\
\end{array}
\right.
$$

Dabei bezeichnet $$x_{Age}$$ den Wert für das Alter aus der Eingabe $$x$$. Wir machen also die Vorhersage von einem Altersgruppe $$p$$ abhängig.

Wir picken zwei Modelle aus der Modellfamilie heraus: Das Modell $$M_{100}$$ sagt jedem Passagier das Überleben voraus und ist damit für unseren Datensatz zu 38,4 Prozent korrekt. Das Modell $$M_{0}$$  sagt für jeden Passagier _nicht überleben_ vorher ist zu 61,6 Prozent korrekt. (Warum?)  Irgendwie scheint $$M_{100}$$ besser zu funktionieren als $$M_{0}$$ . Wir definieren "besser funktionieren" später, aber nun ist die Frage: Gibt es ein $$p \in [0,100]$$, so dass $$M_p$$ besser als $$M_{100}$$ ist? (Hinweis: Versuchen sie mal $$p = 0.5$$ )

## Definition Machine-Learning

Gegeben sein ein  Datensatz, also eine Feature-Matrix $$X$$ und einen Label-Vektor  $$y$$ . Unter Maschine Learning man einen Algorithmus, der aus einer Modellfamilie ein konkretes Modell mit möglichst geringen Loss (oder hoher Accuracy) auswählt.

&#x20;

