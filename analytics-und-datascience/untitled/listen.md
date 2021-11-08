---
description: 'Listen: Einer der wichtigsten Datentypen. Listen werden häufig Arrays genannt.'
---

# Datentyp "Arrays" (Listen)

## Grundlegendes

Listen sind eine geordnete Ansammlung von Elementen. Elemente können dabei z.B. Zahlen oder Zeichenketten sein und doppelt in der Liste auftauchen. Listen sind änderbar. Mit Listen erhalten wir erstmals eine Struktur von Werten oder anderen Elementen.

```
int_list = [1, 2 , 3]
print( int_list )
```

## Einfache Operationen auf Listen

Wir brauchen für Listen folgende einfachen Operationen.

```python
int_list = [10, 20, 30]

# Länge der Liste
i = len( int_list )
print(i)

# Zugriff auf das n-te Element mit eckigen Klammern
el = int_list[0]
print( el )

#auch
n = 2
el = int_list[n]
print( el )


#Änderung eines Listen eintrags
int_list[1] = -1
print( int_list )


```

> Achtung: Die Nummerierung von Listen beginnt immer bei Null

### Übung 1

Erläutern Sie die folgenden Befehle und die Ausgabe:

```python
int_list = [10, 20, 30]
n=-1
print( int_list[n] )
```

## Slicing&#x20;

Häufig müssen wir Listen zerlegen oder auf Listenteile zugreifen.

```python
x = [0,1,2,3,4,5,6,7,8,9]

# Teilliste
one_to_four = x[1:5]
print( one_to_four )

#...vom Listenstart weg
first_three = x[:3]
print( first_three )

# ... bis zum Listenenden
last_four = x[-4:]
print( last_four )

with_out_first_and_last = x[1:-1]
print( with_out_first_and_last  )
```

### Übung 2

Strings verhalten sich teils wie Listen. Versuchen sie Slicing-Funktionen von Listen auf Strings anzuwenden.

## Verlängern und Anhängen

Sie können Listen um Elemente verlängern oder an Listen weitere Listen anhängen:

```python
x = [0,1,2,3,4,5,6,7,8,9]

# Anhängen einer Liste an x; x wird dadruch verändert
x.extend( [10,11])
print (x)

y = x +  ['A', 'B', 'C']
print(y) 
print(x) # x bleibt unverändert
```

&#x20;

