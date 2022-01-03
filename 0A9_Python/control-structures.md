# Ablauf: if-then-else



## if-then

Die Programmzeile 4 wird nur ausgeführt, wenn die Bedingung erfüllt ist.

```
a = 33
b = 200
if b > a:
  print("b is greater than a")
```



## if-then-else

```
a = 33
b = 20
if b > a:
  print("b is greater than a")
else:
  print("b is equal to or smaller than a")
```



## Übung

Ergänzen sie nachfolgendes Programm so, dass am Ende ausgegeben wird, ob

1. die Zahl x größer also Null ist
2. der String s mit dem Buchstaben "H" beginnt
3. die Zahl x gerade ist

```python
x = 7
s = "HAW Landshut"
# Ergänzung der Programmzeilen zu 1.
# Ergänzung der Programmzeilen zu 2.
# Ergänzung der Programmzeilen zu 3.
```

Ihr Programm soll stets drei Zeilen ausgeben. Die Ausgabe für die obigen Werte von x` `und `s` sollte sein:

![](control-structures.assets/image (195).png)





# Ablauf: loops



## for-loop

```
for x in [1,2,3,4]:
  print(x)

for y in ["Huber", "Maier", "Hans"]:
  print(y)
```



## while-loops

```
a = 10
b = 20
while (a < b):
  print(a)
  a = a+2
print("Ende")
```



# Funktionen



## Definition einer Funktion

```python
def my_function():
  print("Hello from a function")
```



## Aufruf einer Funktion

```
my_function()
```



## Übung

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



## Übung (range)



### range()

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
