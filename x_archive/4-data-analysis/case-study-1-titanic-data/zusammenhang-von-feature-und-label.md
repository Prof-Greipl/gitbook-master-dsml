---
description: >-
  In diesem Abschnitt geht es darum, ob wir aus feature-Werten auf den
  label-Werte schließen können. wir nähern uns damit unserem eigentlichen Ziel.
---

# Zusammenhang von feature und label

Bevor wir uns die Auswertungen eintauchen: Die Überlebensrate im Datensatz ist 39,2 Prozent.&#x20;

## Zusammenhang qualitativer features und label

### Numerische Auswertungen

```
df[ ["Pclass","Survived"]].groupby("Pclass").mean().sort_values(by='Survived', ascending=False)
```

![](<../../../.gitbook/assets/image (38).png>)

Wenn wir die Überlebensabhängigkeit von Geschlecht, Hafen, Geschwistern/Lebenspartnern analysieren, ergibt sich folgendes Bild:

![](<../../../.gitbook/assets/image (26).png>)

![](<../../../.gitbook/assets/image (27).png>)

![](<../../../.gitbook/assets/image (28).png>)

![](<../../../.gitbook/assets/image (29).png>)

### Pointplots

Achtung: Die y-Spalte bei Point-Plot muss numerisch sein, da pro x-Wert der Durchschnittswert gebildet wird. Sie sehen, dass es sehr hilfreich ist, dass die Tatsache des Überlebens mit der Zahl `1` kodiert ist, und nicht etwa mit `yes` oder `no`.

```
import matplotlib.pyplot as plt
sns.pointplot( data = df, x = "Sex", y="Survived" )
```

![](<../../../.gitbook/assets/image (43).png>)

Und an einem anderen Beispiel:

![](<../../../.gitbook/assets/image (45).png>)

### Multiple Pointplots

Multiple Pointplots erlauben uns, den Einfluss auf die Werte eines weiteren qualitativen features zu erweitern:

```
grid = sns.FacetGrid(df, row='Embarked', size=3, aspect=1.5)
grid.map(sns.pointplot, 'Pclass', 'Survived', 'Sex', palette='deep')
grid.add_legend()
```

![](<../../../.gitbook/assets/image (46).png>)

### Grid-Plots

In diesem Beispiel erzeugen wir eine Matrix von Plots und erhalten damit Informationen über eine weitere Dimension (hier: Fare).

```
grid = sns.FacetGrid(df, row='Embarked', col='Survived', size=2.2, aspect=1.6)
grid.map(sns.barplot, 'Sex', 'Fare', alpha=.5, ci=None)
grid.add_legend()
```

![](<../../../.gitbook/assets/image (47).png>)

## Zusammenhang quantitativer features mit label

Es macht recht wenig Sinn mit der Spalte Age gleiches wie oben zu versuchen, wie folgender Versuch zeigt:

```
import matplotlib.pyplot as plt
sns.pointplot( data = df, x = "Age", y="Survived" )
```

![](<../../../.gitbook/assets/image (56).png>)

Es liegen einfach zu viele Werte auf der x-Achse, oder umgekehrt gesagt: zu jedem x-Wert gibt es nur eine erratisch geringe Zahl von y-Werten, die dann zum Ergebnis führen.&#x20;

### Kategorisierung

Eine sehr häufig angewendete Lösung dieses Problems, ist die Transformation eines quantitative features in ein ordinales feature. Dies kann recht einfach gemacht werden: Statt das korrekte Alter zu verwenden,  ordnen wir das Alter in Altersgruppen ein. Wie wählen Altersgruppen on \[1,..6) , \[6,..10), usw. Wenn wir die Altersangaben bis 85 Jahre auswerten entstehen 16 Gruppen zu je 5 Jahren, also

| Alter     | AgeGroup |
| --------- | -------- |
| 0,1,2,3,4 | 0        |
| 5,6,7,8,9 | 1        |
| 10,...14  | 2        |

Folgende Zeilen erweitern unseren Datensatz um eine neue Spalte `AgeGroup.`

```
df_age_clean = df[ df["Age"] < 81 ]
s_age_group =  df_age_clean["Age"]/5 
df['Age_Group'] = s_age_group.astype('int64')
```

Ergebnis: Wir sehen Age\_Group als neue Spalte, die von Age abgeleitet ist:

![](<../../../.gitbook/assets/image (57).png>)

Nun  haben wir ein neues qualitatives Feature, von dem wir uns die Counts anzeigen lassen (Befehl als Übung!):

![](<../../../.gitbook/assets/image (86).png>)

Schließlich erzeugen wir den Pointplot:

![](<../../../.gitbook/assets/image (87).png>)
