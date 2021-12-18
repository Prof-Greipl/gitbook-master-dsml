Anhand des Zirpens von Grillen kann man mehr oder weniger verlässlich die Lufttemperatur berechnen. Die Körperfunktionen von Grillen verändern sich wie bei anderen Insekten auch durch veränderte Lufttemperatur. Denn wie alle Insekten sind Grillen kaltblütig und nehmen die sie umgebende Temperatur an. Je wärmer, desto häufigeres Zirpen. Ist es wärmer, laufen die Körperfunktionen – wie auch Bewegungen – schneller ab, die Grillen sind aktiver. \[…] Da Grillen also bei erhöhter Temperatur häufiger Zirpen, kann man aus der Häufigkeit des Zirpens die Lufttemperatur ableiten. Die Formel dafür ist sehr simpel. Um die Temperatur in Grad Celsius zu errechnen, zählt man das Zirpen einer einzelnen Grille in einem Intervall von 25 Sekunden.



# Dataset

Nehmen wir an, dass folgende kleine Menge von labelled examples vorliegt: 

![](<../.gitbook/assets/image (117).png>)

Natürlich wollen wir nun - wie üblich - aus dem feature den label vorhersagen. Offensichtlich handelt es sich um ein Regressionsproblem. 

Mit folgendem Code definieren wir unseren Dataset:

```python
df = pd.DataFrame({
    "Count": [31,16,29,43,27,19,47,9,45,5,39],
    "Temp": [9.4,10.5,17.1,24.3,14.6,9.9,16.9,6.4,17.7,7.5,14.2]   
})
```



Visualisuerung

![image-20211213120259149](grillen.assets/image-20211213120259149.png)



Phyton

```python
%tensorflow_version 2.x
import numpy as np
import pandas as pd

import matplotlib.pyplot as plt
import seaborn as sns

df = pd.DataFrame({
    "Count": [31,16,29,43,27,19,47,9,45,5,39],
    "Temp": [9.4,10.5,17.1,24.3,14.6,9.9,16.9,6.4,17.7,7.5,14.2]
    
})

X = df["Count"]
y = df["Temp"]

print( X.shape )
print( y.shape )

sns.set()
fig,ax = plt.subplots(figsize=(6, 6))
ax.set_aspect("equal")
ax.set_xlim(0, 50)
ax.set_ylim(0, 30)

ax.set_title("Data")
ax.set_xlabel("Count")
ax.set_ylabel("Temperature")
sns.scatterplot(x = X, y = y)
```



# Das "Grillen-Neuron"

Wenn wir ein Neuron mit *einem* Eingabewert $$(m=1)$$ und *linearer Activation* bauen, so ist die Ausgabe des Neurons

$$
y = M_{w,b}(x) = x \cdot w +b
$$

Dies entspricht aber exakt unserem Modell im Fall der Regression!





# Neuronales Netz und Learning

Folgender Code erzeugt die Modellfamilie und berechnet dann das optimale Modell:

```python
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense, Activation
from tensorflow.keras import optimizers
from keras.utils.vis_utils import plot_model
import pandas as pd

# Acvtivations: linear, relu, sigmoid, tanh, 
model = Sequential()
model.add( Dense(1, activation='linear') )
model.compile(loss='mean_squared_error', optimizer='adam')

# Run the training
history = model.fit(X,y, verbose=0, epochs= 20000)

# We display the weighst and biases
print(f'Loss   : {history.history["loss"][-1]}')

print("Neuron :")
[weight, bias] = model.layers[0].get_weights();
print(f'Weight : {weight}')
print(f'Bias   : {bias}')
```

(Mögliche) Ausgabe: 

![image-20211213120941774](grillen.assets/image-20211213120941774.png)



##  Visualisierung des gelernten Modells

Folgende Grafik visualisiert das Geschehen bisher:

* Die blauen Punkte zeigen die _labelled examples_
* Die orangen Punkte zeigen die _predictions _für die features
* Die rote Linie visualisiert das Modell, als Ergebnis des Trainings 

![image-20211213121545814](grillen.assets/image-20211213121545814.png)











## Trainingsschritt und Epochen

Ein **Trainingsschritt **(learning-step) ist eine neue Festlegung der Parameter eines Modells, so dass der Loss kleiner wird. Diese neue Festlegung funktioniert auf der Basis des Gradienten der Loss-Funktion. In obigem Beispiel wäre der Trainingsschritt $$h_0.$$ Eine **Epoche **ist ein Trainingsschritt auf der Grundlage aller Trainingsdaten. Wir identifizieren für den Moment eine Epoche mit einem Abstiegsschritt.





## Visualisierung des Lernfortschritts

![image-20211213122600715](grillen.assets/image-20211213122600715.png)





## Python: Anzeige der Lernkurve

```python
import seaborn as sns

# Lernfortverhalten visualisieren
fig,ax = plt.subplots( figsize=(8,4) )
ax.set_title("Lernverlauf (MSE)")
ax.set_xlabel("Epochen")
ax.set_ylabel("MSE (Loss)")
ax.set_ylim(0,40)
sns.lineplot( x = history.epoch, y = history.history["loss"], label = "Train. Loss")
```



## Lösungen im Vergleich

![Lösung nach 10.000 Epochen vs. optimale Lösung](grillen.assets/image-20211218113536441.png)



## Python: Anzeige der Lösungen

```python
from matplotlib import pyplot as plt
import seaborn as sns
import pandas as pd
import numpy as np

chirps = pd.DataFrame({
    "Count": [31,16,29,43,27,19,47,9,45,5,39],
    "Temp": [9.4,10.5,17.1,24.3,14.6,9.9,16.9,6.4,17.7,7.5,14.2]    
})

X = chirps["Count"].to_numpy().reshape(11,-1)
y = chirps["Temp"].to_numpy().reshape(11,-1)
print(y)

x_values = np.array([0, 50])
print(bias.shape)
print(weight.shape)

y_netz = np.array([bias, 50*weight[0] + bias]).flatten()
y_best = np.array([5.036035, 50*0.3003342 + 5.036035])

fig,ax = plt.subplots(figsize=(9, 9))
ax.set_aspect('equal')
ax.set_title("Chirps-Data") 
ax.set_xlabel("Count")
ax.set_ylabel("Temperature")

ax.set_xlim(0, 50)
ax.set_ylim(0, 35)

sns.set()
sns.scatterplot(data = chirps, x = "Count", y="Temp", label="Temp")

sns.lineplot(x=x_values,y= y_best, color="red", label="best line xw+b")
sns.lineplot(x=x_values,y= y_netz, color="blue", label="Neuron line")

```

