---
description: Überblick über die Begriffe
---

# Variablen

Variablen sind Platzhalter für Werte, wir sprechen vom _Wert einer Variable_.  Im nachfolgendem Beispiel wird der Variable mit dem Namen `x`in Zeile 1 der Wert 1 zugewiesen. Variablen haben immer einen Namen. Einen Wert erhalten sie erst  durch eine sog. Zuweisung (wie in Zeile 1). In Zeile 2 drucken wir den Wert aus. Führen Sie also folgende Phython-Befehle aus:

```python
x = 1
print(x)
```

> Die erstmalige Zuweisung eines Wertes an eine Variable heißt Initialisierung.

### "Eingebaute" Datentypen

Sie können sich sicher vorstellen, was folgendes Programm ausgibt.

```python
s = "HAW-Landshut"
# Mit Gartenzaun wird eine Kommentarzeile markiert.
print(s)
```

Der Wert der Variable s ist nun keine Zahl, wie oben, sondern ein Text, im Fachjargon ein _String_. Wir kennen also nun die Datentypen _Zahl _und _Zeichenkette_.  Dies sind in Python "fest eingebaute" Datentypen, die wir ohne weiteres verwenden können.

### Vorgriff: Operationen

Unter einer Operationen versteht man die Erzeugung eines neuen Wertes aus anderen Werten. Sie kennen natürlich die Operationen der Addition, Subtraktion, Division oder Multiplikation von numerischen Werten. das funktioniert in Python wie in Excel. Führen sie folgenden Befehle aus und versuchen Sie die Ergebnisse zu verstehen:

```python
a = 1
b = 2
c = a + b; print(c)
c = a - b; print(c)
c = a * b; print(c)
c = a / b; print(c)
```

 Etwas schwieriger wird es schon bei Wertes des Datentyps String. Folgendes Programm liefert einen Fehler. Warum wohl?

```python
s1 = "HAW"
s2 = "Landshut"
print(s1-s2)
```

Zusammengefasst: Operationen hängen auch von den Werten ab, die sie verarbeiten. Wir schauen uns deshalb im nächsten Abschnitt Datentypen zusammen mit den wichtigsten Operationen an.

###





