---
description: Für diesen Abschnitt untersuchen wir Spalten mit qualitativen Werten. .
---

# Analyse qualitativer Spalten

Qualitative Daten erläutern ein feature eines Datensatzes durch Zuordnung einer Kategorie näher. Beispiel sind `male `oder `female. `Teils werden für qualitative Daten auch Zahlen verwendet, zum Beispiel `1` für Survived und `0` für den unglücklicheren Ausgang.&#x20;

Für qualitätive features interessieren uns

* die Anzahl der möglichen Werte
* den Wert, der am häufigsten auftritt
* die Anzahl, wie oft der häufigste Wert auftritt
* eine Liste der Werte mit der Anzahl des Auftretens.

Wir beantworten diese Fragen zuerst und tauchen dann tiefer.

## Überblick

Eine leichte Abänderung des describe-Befehls gibt uns Information zu Spalten, die nicht durchgängig Zahlen enthalten.

```
df.describe(include=['O'])
```

![](<../../../.gitbook/assets/image (24).png>)

Interpretation:

* Name: Namen  sind eindeutig für jeden Datensatz
* Sex: Von den 891 Passagieren sind 577 männlich.
* Ticket: Für die 891 Passagiere gibt es 681 Tickets.
* Cabin: Kabinen tauchen mehrfach auf. Passagiere haben sich möglicherweise Kabinen geteilt.
* Embarked: Es treten drei mögliche Werte auf. Die meisten Passagiere (644) haben der Wert `S `(Southampton)
* Missing Values in der Spalte `Cabin`

Die Anzahl der Einträge mit dem jeweiligen Auftreten erhalten Sie durch `df.value_counts()`, genau wie für quantitative Daten.

Beispiel:

```
s_embarked_count = df["Embarked"].value_counts().sort_index()
print( s_embarked_count )  
```

![](<../../../.gitbook/assets/image (54).png>)

## Countplots

Countplots stellen grafisch dar, wie häufig Werte auftreten.

```
import seaborn as sns
sns.countplot( data=df, x="Embarked")
```

Ergebnis:\


![](<../../../.gitbook/assets/image (55).png>)
