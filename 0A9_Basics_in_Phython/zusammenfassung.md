---
description: Schon ne ganze Menge gelernt...
---

# Datentypen in der Übersicht

Nachfolgendes Programmstück beschreibt exemplarisch die nun bekannten Datentypen. Mit `type()` kann man sich den Datentyp einer Variable ausgeben lassen (oft hilfreich!)

```python
x = 1; 
print( f"1 : {type(x)}")

x = 1.1; 
print( f"1.1 : {type(x)}")

x = 4/2; 
print( f"4/2 : {type(x)}")

x = 'String'; 
print( f"'String' : {type(x)}")

x = [1,2,4]; 
print( f"[1,2,3] : {type(x)}")

x = (1,2);
print( f"(1,2) : {type(x)}")

x = 1 < -3
print( f"False : {type(x)}")
```

### Zusammenfassung der Datentypen



| Eingebauter Datentyp | Kürzel     | Beispiele              |
| -------------------- | ---------- | ---------------------- |
| Text (Strings)       | str        | `x = "Haw-Landshut"`   |
| Zahlen (Numerisch)   | int, float | `x = 1` oder `x = 1.1` |
| Listen               | list       | `x = [1,2,3]`          |
| Tupel                | tuple      | `x = (1,2)`            |
| Wahrheitswerte       | bool       | `x = (1 < 3)`          |



