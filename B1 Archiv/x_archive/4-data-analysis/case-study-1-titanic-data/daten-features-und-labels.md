# Daten, Features und Labels

## Features und Labels

Für dieses Modul gehen wir stets von folgender Ausgangsposition aus:

1. Unsere Daten liegen in Tabellenform vor.
2. Eine Spalte ist entweder ein _**feature **_oder ein _**label **_- niemals beides.
3. Labels sind Spalten, deren Werte wir gerne korrekt vorhersagen würden, sofern wir die Werte in den feature-Spalte kennen.
4. Eine Zeile der Tabelle nennen wir Datensatz.&#x20;

In unserem Datensatz ist die Spalte survived die einzige label-Spalte (oder nur _label_). Die anderen Spalte sind feature-Spalten ( oder nur _features_).

## Welche Arten von Daten liegen vor?

### Metrische Daten (quantitative Daten)

Metrische Daten sind Zahlen, die Rangunterschiede beschreiben und messen. Mit metrischen Daten lässt sich sinnvoll rechnen. Ihre Differenz lässt sich interpretieren, die Sortierung metrischer Daten ist sinnvoll. Metrische Daten können  **kontinuierlich **sein, d.h. sie können jeden Wert eines Intervalls annehmen. **Diskrete **Daten nehmen nur Werte aus einer meist kleinen Menge natürlicher Zahlen an).

| Diskrete Daten                            | Kontinuierliche Daten          |
| ----------------------------------------- | ------------------------------ |
| Augenzahl beim Würfeln, Anzahl der Kinder | Körpergröße, Temperatur, Preis |

### Kategorische Daten (nicht-metrische, qualitative Daten)

Bei **nominalskalierten Daten** handelt es sich um Daten, die in keinerlei natürliche Reihenfolge gebracht werden können – beispielsweise um das Geschlecht, die Haarfarbe oder die Telefonnummer. Feststellbar ist hier lediglich, ob zwei Datensätze im Hinblick auf ein nominalskaliertes Merkmal die gleichen Werte aufweisen – d.h. ob etwa beide befragten Personen blond sind oder ob sie über unterschiedliche Haarfarben verfügen.&#x20;

_"Im Gegensatz zu nominalskalierten Daten können **ordinalskalierte Daten** zwar in eine natürliche Reihenfolge gebracht werden – da allerdings die Abstände zwischen den einzelnen Werten nicht quantifizierbar sind, kann mit ihnen nicht “normal gerechnet” werden, obwohl es sich auf den ersten Blick um “normale Zahlen” handelt. Das klassische Beispiel hierfür sind Schulnoten. Schulnoten weisen sowohl eine natürliche Reihenfolge (eine 1 ist besser als eine 2, eine 2 ist besser als eine 3 usw.) als auch unterschiedliche Abstände zwischen den einzelnen Werten auf (der Notenbereich der 1 umfasst den Bereich von 92% bis 100% der maximal erreichbaren Punkte, der Notenbereich der 5 dagegen den Bereich von 0% bis 49%). Aus diesem Grund sind Rechenoperationen wie etwa das Addieren oder das Subtrahieren von Noten nicht sinnvoll: Zwei “2er” ergeben keinen “4er” – und wenn man von einem “4er” einen “1er” abzieht, erhält man auch keinen “3er”. Wenn man aber Schulnoten nicht addieren (oder dividieren) kann, folgt daraus auch, dass man beispielsweise kein arithmetisches Mittel aus ihnen bilden darf – auch wenn das leider an sehr vielen Schulen konsequent falsch praktiziert wird (und damit Generationen von Schülerinnen und Schülern für die Statistik verdorben werden)."  _([Quelle](https://wissenschafts-thurm.de/grundlagen-der-statistik-wie-unterscheidet-man-zwischen-nominal-ordinal-und-kardinalskala/) für diesen Abschnitt; mit eigener Korrektur)

### Gemischte Daten (alphanumerische Daten)

Manche Daten bestehen aus einer Mischung aus numerischen und Buchstaben, sogenannten alphanumerischen Daten. Manchmal lassen sich diese Daten sinnvoll aufteilen in einen numerischen und einen kategorischen Teil.&#x20;

### Titanic: Datentypen

| Feature/Label | Datenart   |
| ------------- | ---------- |
| PassengerId   | Nominal    |
| Survived      | Nominal    |
| Pclass        | Ordinal    |
| Name          | Nominal    |
| Cabin         | Nominal    |
| Age           | Continuous |
| SibSp         | Discrete   |
| Parch         | Discrete   |
| Ticket        | Nominal    |
| Fare          | Continuous |
| Cabin         | Nominal    |
| Embarked      | Nominal    |

Grafisch

![](<../../../.gitbook/assets/image (61).png>)
