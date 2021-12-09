# Ablauf: Funktionen

### Definition einer Funktion

```python
def my_function():
  print("Hello from a function")
```

### Aufruf einer Funktion

```
my_function()
```

### Übung (Funktion)

Was gibt folgendes Programm aus?

```python
def name( vorname, nachname):
  e = vorname + ", " + nachname
  return e

def verdoppeln(x):
  return 2*x

z = verdoppeln(4)
print(z)
print ( type(z) )
print( name("Hans", "Huber"))
```

### Übung: Eingebaute Funktionen

#### range()

```
z = range(10)
print( z )
print( type(z) )
for i in z:
  print(i)
```

**Die Funktion range kann mehr als einen Parameter aufnehmen (maximal 3). Erklären Sie die Ausgabe folgender Programme**

```python
print("Range mit zwei Parametern:");
my_range = range(10,20)
for i in my_range:
  print(i)

print("Range mit drei Parametern:"):
my_range = range(10,30,3)
for i in my_range:
  print(i)
```
