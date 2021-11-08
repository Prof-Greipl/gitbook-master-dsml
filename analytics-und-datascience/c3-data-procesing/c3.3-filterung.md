# C3.3 Filterung

Filterung modifiziert Werte aus unserem Datensatz. Wir betrachten untern den zahlreichen Filteransätzen lediglich die Glättung von Werte durch Moving Average Techniken.

## Moving Average

### Python: Beispiel

```
import pandas as pd
import numpy as np

N = 400
y = x*x + 0.2 * e
fig = plt.figure(figsize=(8,8))
plt.plot( x, x*x, color="black", linestyle='-')
plt.plot( x, y, color="red", linestyle='-')
```

![Noisy Data](<../../.gitbook/assets/image (1).png>)

Wir glätten nun die Daten mit einem Moving Average Verfahren.

```
y_filtered = pd.Series(y).rolling(window=50, center=True).mean()
plt.plot( x, y_filtered, color="green", linestyle='-')
```

Ergebnis:

![Filterung mit Movin Average der Fenstergröße 50.](<../../.gitbook/assets/image (6).png>)
