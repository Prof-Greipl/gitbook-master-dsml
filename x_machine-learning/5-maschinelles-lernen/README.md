# 6 Maschinelles Lernen

## Problemstellung

Wir wollen für ein Ereignis oder ein Objekt eine Eigenschaft oder ein Ergebnis bestimmen. Das Ereignis (oder Objekt) beschreiben wir durch Feature-Vektoren, das Ergebnis nennen wir Label. Bei Titanic ist das Objekt ein Passagier, beschrieben durch einen Feature-Vektor bestehend aus  Werten für die Features _Pclass, Sex, Age, SibSp, Parch, Fare _und _Embarked_). Der Label ist 0 (für _nicht überlebt_)  und 1 (für _überlebt_)

Um die Problemstellung zu lösen, verwenden wir einen Lernalgorithmus, die aus (meist vielen) exemplarischen Feature-Vektoren und Labels ein Programm zur Problemlösung erstellt. Das konkrete Programm zur Problemlösung erzeugt also ein Lernalgorithmus, nicht ein Programmierer.  (Gleichwohl stellt ein Mensch immer noch wesentliche Weichen für dieses Verfahren). Wir sagen, dass der Computer aus den gegebenen Daten _lernt_, ein Programm zur Problemlösung zu erstellen. Deshalb nennt man diesen Ansatz auch allgemein **Maschinelles Lernen.** 

## Hinweis

Im nachfolgenden Text werden mehrmals Beispiele auf der Basis des Titanic-Datensatzes gegeben. Diese Beispiel beziehen sich auf den Datensatz nach Feature-Engineering, wie in obigem Abschnitt entwickelt. Ihr Datensatz hat also nun folgende Beschreibung:

![](<../../.gitbook/assets/image (104).png>)

##

