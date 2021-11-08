---
description: >-
  In dieser Case Study wenden wir unsere Kenntnisse aus dem letzten Abschnitt
  auf die bekannten Titanic-Dataset an. Sie finden die Datei auf Moodle.
---

# Exploratory Data Analysis mit Titanic

## Der Titanic-Datensatz

![](<../../../.gitbook/assets/image (17).png>)

![](<../../../.gitbook/assets/image (16).png>)

> HINWEIS: Die Übungsaufgabe finden Sie [hier](../titanic-uebung.md).

## Links

{% embed url="https://www.encyclopedia-titanica.org/titanic-passenger-list/" %}

## Laden der Daten

Wir laden den Datensatz in ein Dataframe. Dieses dient als Grundlage für die weiteren Arbeiten.

```
import pandas as pd
df = pd.read_excel("/content/drive/My Drive/Colab Notebooks/data/titanic_train.xlsx")
```

## Analyse-Fragestellung: Welches Problem wollen wir lösen?

> Wir wissen aus dem Datensatz, welche Passagiere das Unglück überlebten. Können wir ein Modell erzeugen, das aus den Daten  - ohne die Information über das Überleben - vorhersagen kann, ob ein Passagier überlebt?

## Visualisierung mit `Seaborn`

In diesem Abschnitt nutzen wir das Paket `Seaborn `zur Visualisierung von Daten mit statistischem Fokus. Lesen sie dazu [diesen Artikel ](https://seaborn.pydata.org/introduction.html)durch.

Wir importieren das Paket stets mit der Zeile:

```python
import seaborn as sns
```

