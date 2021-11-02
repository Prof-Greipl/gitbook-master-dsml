# Überblick verschaffen

## Zeilenüberlick

Zu Beginn untersuchen wir einige Zeilen und verschaffen uns einen Überblick über die Daten.

```python
print( len(df))     # Gibt die Anzahl der Zeilen aus
df.head(5)          # Zeigt die ersten 5 Datensätze
```

![](<../../../.gitbook/assets/image (24).png>)

#### Hinweis

Der print-Befehl für einen Dataframe gibt maximal 10 Zeilen eines Dataframes aus. Der folgende Befehl erzwingt, dass alle Zeilen ausgegeben werden.  Verwenden Sie das für die Untersuchung der Spalte `Age`.

```
pd.set_option('display.max_rows', None)
```

## Spaltenüberblick

Natürlich haben wir uns beim Untersuchen der Zeilen schon mit den Spalten beschäftigt. Nun Untersuchen wir für jede Spalte den Datentyp und die Anzahl der verfügbaren Werte.

```
df.info()
```

Sie sehen die folgende Ausgabe:

![](<../../../.gitbook/assets/image (31).png>)

Wir erkennen aus obiger Ausgabe folgende Informationen für Titanic:

* Der Datensatz enthält 891 Zeilen und 12 Spalten
* 7 der 11 Spalten enthalten Zahlen als Werte
* Nicht für jede Spalte sind alle 891 Zeilen gefüllt. Die Spalte `Age `enthält zum Beispiel nur 714 Werte.

Wie ordnen allen Spalten Datentypen zu. In unserem Fall sind dies 

* ganze Zahlen (`int64`)
* reelle Zahlen (`float64`)
* Zeichenketten (`object`)

Weitere Datentypen sind zum Beispiel logische Werte oder Datum/Uhrzeit.

Hinweis: Folgender Befehl liefert die Spalten als Array (Zeile 1) und den Namen der ersten Spalte `PassengerId` (Zeile 2)

```
print( df.columns.values )
print( df.columns.values[0] )
```

![](<../../../.gitbook/assets/image (33).png>)

## Verschiedene Werte pro Spalte? 

### `df.value_counts() `verwenden

Nachfolgender Befehl speichert Anzahl der verschiedenen Werte für die Spalte `Sex` aus:

```
s_age_count = df["Age"].value_counts()
print( s_age_count )     
```

Ergebnis: Wir sehen, dass 30 Personen im Alter von 24 Jahren im Datensatz sind. Die Tabelle ist absteigend nach Häufigkeit sortiert.

![](<../../../.gitbook/assets/image (62).png>)

Wenn Sie nach der ersten Spalte, dem Index sortieren wollen, dann ersetzen sie Zeile 1 oben durch 

```
s_age_count = df["Age"].value_counts().sort_index()
```

Ergebnis:  Es sind 7 Kinder mit einem Jahr  im Datensatz

![](<../../../.gitbook/assets/image (45).png>)

## Fehlende Werte?

Der Aufruf `df.info()` (siehe oben) sagt uns, dass nicht zu jeder Spalte alle Daten gefüllt sind. Die Spalte `Age` enthält z.B. nur für 714 Passagiere Werte.  Diese sogenannten _missing values _können zu einem Problem werden.

##
