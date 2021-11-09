# Funktionen mit Arrays

### Beispiel

```python
import numpy as np

x = np.linspace(0,2*np.pi,20);
y = np.sin(x)
print(y)
```

### Visualisierung

```python
import numpy as np
import matplotlib.pyplot as plt

plt.figure()
plt.plot(x, np.sin(x), 'r--')
```

![](<../../.gitbook/assets/image (200).png>)
