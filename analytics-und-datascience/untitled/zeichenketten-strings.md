---
description: 'Auch recht simple: Strings'
---

# Datentyp "Strings"

Zeichenketten sind ebenfalls recht einfach zu verstehen. Führen Sie folgendes Beispiel aus:

```python
vorname = "Hans"
nachname = 'Huber'
name = vorname + ", " + nachname
print(name)
```

### f-Strings

Statt eine zusammengesetzte Zeichenkette mit dem "+" - Operator auf zubauen, kann ein sogenannter f-String verwendet werden \(siehe Zeile 3\). f-Strings bringen für uns keine neue Funktion, machen aber die Verknüpfung von Strings einfacher.

```python
vorname = "Hans"
nachname = 'Huber'
name = f"{vorname}, {nachname}"
print(name)
```



