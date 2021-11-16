# Skalare, Vektoren und Matrizen

In diesem Abschnitt wiederholen wir ein paar Begriffe aus der Linearen Algebra, die bekannt sein sollten. Die Notationen wählen wir so, dass sie zur [Anwendung in NumPy ](numpy.md)passen.

## Skalar

Die meisten Objekte der Linearen Algebra sind Strukturen von Zahlen, zum Beispiel Vektoren oder Matrizen. Skalare dagegen sind ganz einfach nur Zahlen, in unserem Fall reelle Zahlen. Wir bezeichnen Skalare mit kleinen kursiven Buchstaben. Wir schreiben zum Beispiel $$s \in \mathbb{R}.$$

## Vektor

Ein Vektor ist ein Tupel reeller Zahlen, die in einer bestimmten Weise angeordnet sind. Jede Zahlen aus dem Tupel ist über einen Index genau bestimmt. Wir notieren einen Vektor mit einem kleinen und fett gedruckten Buchstaben, also z.B. $$\bold{x}$$ . Die einzelnen Zahlen des Vektors werden kursiv gedruckt und mit ihrem Index notiert, also die erste Zahl mit $$x_1$$, die zweite Zahl mit $$x_2$$ und so weiter. Enthält der Vektor n reelle Zahlen so ist der Vektor ein Element des n-fachen kartesischen Produktes der reellen Zahlen $$\mathbb{R}$$, kurz $$\mathbb{R}^{n}$$. Um die Elemente eines Vektors explizit anzugeben, notieren wir sie als **Spalte**

$$
\bold{x} = \begin{bmatrix}
x_1 \\
x_2 \\
\vdots \\
x_n \\
\end{bmatrix}
\in \mathbb{R}^n
$$

Die Zahl n heißt **Dimension des Vektors.**

## Matrix

Eine \(reell-wertige\) Matrix ist eine zweidimensionale, in Zeilen und Spalten angeordnete Struktur von reellen Zahlen. Jedes Element einer Matrix $$\bold{A}$$ wird über zwei Indizes bestimmt. Wir notieren eine Matrix mit einem fett gedruckten Großbuchstaben und die Elemente der Matrix mit dem Buchstaben der Matrix, aber nun nicht-fett und kursiv gedruckt und mit zwei Indizes versehen. Besteht eine Matrix aus n Zeilen und m Spalten, so notieren wir das durch $$\bold{A}\in\mathbb{R}^{n\times m }$$ und nennen$$\bold{A}$$eine Matrix mit der "_Dimension n kreuz m_"

$$
\bold{A}= 
\begin{bmatrix}
A_{1,1} & A_{1,2} & \cdots & A_{1,m}  \\
A_{2,1} & A_{2,2} & \cdots & A_{2,m}  \\
\vdots & \vdots & \ddots & \vdots \\
A_{n,1} & A_{n,2} & \cdots & A_{n,m}  \\
\end{bmatrix}
$$

### Elementweise Addition

Ist $$\bold{B} \in\mathbb{R}^{n\times m }$$, also eine Matrix der gleichen Dimension, wie $$\bold{A}$$, so lässt sich die Summe $$\bold{A+B}$$ bilden durch:

$$
(A+B)_{i,j} = A_{i,j} + B_{i,j}
$$

wir addieren also einfach die Elemente auf jeweiligen Positionen.

### Multiplikation mit Skalar

Die Matrix $$\bold{A}$$ lässt sich mit einer reellen Zahl $$s$$ \(also einem _Skalar_\) multiplizieren und die entstehende Matrix $$\bold{sA}$$ ist wie erwartet definiert durch

$$
(sA)_{i,j} = s \cdot A_{i,j}
$$

wir multiplizieren also jedes Element der Matrix mit dem Skalar $$s$$.

### Transponieren

Durch **Transponieren** wird aus einer Matrix $$\bold{A}\in\mathbb{R}^{n\times m }$$ eine neue Matrix $$\bold{A^T} \in\mathbb{R}^{m\times n }$$ erzeugt. Dabei gilt

$$
(A^T)_{j,i} = A_{i,j}  \quad \text{für } \quad i \in {1,...,n}  
\quad \text{und} \quad 
j \in {1,...,m}
$$

Transponieren lässt sich durch eine Art _spiegeln von_ $$\bold{A}$$ an deren Hauptdiagonale verstehen. Die Hauptdiagonale ist die gedachte Linie, die vom Element $$A_{0,0}$$ im Winkel von 45 Grad nach rechts unten verläuft. Zum Beispiel:

$$
\bold{A} = \begin{bmatrix}
1 & 2  \\
3 & 4  \\
5 & 6  \\
\end{bmatrix}  \in \mathbb{R}^{3\times 2 }
\quad\Rightarrow\quad
\bold{A^T} = \begin{bmatrix} 
1 & 3 & 5  \\
2 & 4  & 6 \\
\end{bmatrix}
\in \mathbb{R}^{2\times 3 }
$$

### Matrixprodukt

Wir können zwei Matrizen $$\bold{A}$$ und $$\bold{B}$$ multiplizieren, wenn die Anzahl der Zeilen in B der Anzahl der Spaten in A entspricht. Für $$\bold A \in\mathbb{R}^{n\times m }$$ und $$\bold B \in\mathbb{R}^{m\times p }$$ gilt für das Produkt $$\bold{C}= \bold{ A} \bold B \in\mathbb{R}^{n\times p }$$

$$
C_{i,j} = \sum_{l=1}^m  A_{i,l} B_{l,j}
$$

## Zurück zu Vektoren: Spalten- und Zeilenvektoren

Da wir Vektoren grafisch in einer Spalte notiert haben, nennen wir sie auch _Spaltenvektoren_. Ein Vektor lässt sich offensichtlich als eine Matrix interpretieren, die nur aus einer Spalte besteht. Wenn wir diese Matrix, wie oben dargestellt, transponieren, entsteht eine Matrix entspricht, die nur aus einer Zeile besteht. Diese Matrix bezeichnen wir als Zeilenvektor. Diese Analogie führt uns zum Konzept eines transponierten Vektors:

$$
\bold{x} = 
\begin{bmatrix}
x_1 \\
x_2 \\
\vdots \\
x_n \\
\end{bmatrix}
\in \mathbb{R}^{n \times 1}
\quad\Rightarrow\quad
\bold{x^T} =  
\begin{bmatrix}
x_1,  x_2 , \dots, x_n \\
\end{bmatrix}
\in\mathbb{R}^{1 \times n}
$$

In der Regel identifizieren wir $$\mathbb{R}^{n \times 1}$$ und $$\mathbb{R}^{1 \times n}$$, aber grundsätzlich besteht doch ein Unterschied.

Zusammenfassend:

* Vektoren sind für uns _immer_ Spaltenvektoren \(deshalb können wir den Begriff _Spaltenvektor_ in der Regel weglassen\)
* Zeilenvektoren sind für uns stets transponierte Spaltenvektoren. 

Die die Notation eines Vektors als Spalte immer etwas Platz benötigt, notiert man z.B. nur $$\bold{x^T} = \begin{bmatrix} 1, 2 ,3 \\ \end{bmatrix}$$. Zeilenvektoren lassen sich ja in einer Zeile schön notieren. Damit ist aber zwingend klar, dass

$$
\bold{x} = 
\begin{bmatrix}
1 \\
2 \\
3
\end{bmatrix}
$$

Die Unterscheidung von Zeilenvektoren und Spaltenvektoren mag zunächst etwas künstlich erscheinen, sie wird aber später die Arbeit mit unseren Software-Tools deutlich erleichtern.

### Multiplikation mit Skalar und elementweise Addition

Betrachtet man einen Vektor als $$x, y \in \mathbb{R}^{n}$$ jeweils als Matrix, so ergeben folgende Definitionen sofort Sinn:

$$
s \cdot\bold{ x} = 
\begin{bmatrix}
s\cdot x_1 \\
s\cdot x_2 \\
\vdots \\
s\cdot x_n \\
\end{bmatrix}
\quad \text{und}\quad
\bold{x} + \bold{y}= 
\begin{bmatrix}
x_1 + y_1 \\
x_2 + y_2 \\
\vdots \\
x_n + y_n \\
\end{bmatrix}
$$

Sie sind im Grunde lediglich Konsequenzen aus der Identifikation von Spaltenvektoren und Matrizen. Gleiches gilt für die Gleichungen $$s \cdot\bold{ x^T} = (s \cdot\bold{ x^T})$$ und $$\bold{ x^T} + \bold{ y^T} = (\bold{ x} + \bold{ y})^T$$

### Skalarprodukt

Man kann aus zwei Vektoren $$x, y \in \mathbb{R}^{n}$$ gleicher Dimension ein spezielles _Produkt_ bilden, das wir mit $$\bold{x}^T\bold{y}$$ notieren.\(Zur Unterscheidung haben wir oben die Bezeichnung _Multiplikation mit einem Skalar_ gewählt\). Es ist definiert als das Produkt aus den jeweils zugeordneten Matrizen und es folgt:

$$
\bold{x}^T\bold{y} =  \sum_{i=0}^{n} x_i \cdot y_i
$$

Bitte überlegen Sie kurz, dass obige Gleichheit keine Definition ist, sondern aus der Definition des [Matrixproduktes ](skalare-vektoren-und-matrizen.md#matrixprodukt-und-skalarprodukt)folgt!

## Übungen

### Skalarprodukt

Berechnen Sie $$v^T w$$, $$ v+w$$ und $$2 \cdot v$$ für

$$
v    =   \begin{bmatrix}
1 \\
-3 \\
2\\
\end{bmatrix}
\quad \text{and} \quad 
w    =   \begin{bmatrix}
1 \\
0 \\
13\\
\end{bmatrix}
$$

### Matrixprodukt 1

Berechnen sie $$A \cdot v$$ für

$$
A = \begin{bmatrix} 
1 & 2 & 3 \\ 
7 & -1 & 2 \\ 
0 & 4 & -1
\end{bmatrix} 
\quad \text{and} \quad 
v = \begin{bmatrix}
 1 \\-3 \\ 2 
\end{bmatrix}
$$



### Matrixprodukt 2 

Berechnen Sie $$ vw^T$$ für die beiden oben angegebenen Vektoren \(Vorsicht!\).

### Matrixprodukt 3

Berechnen sie $$A  \times C$$ für 

$$
A = \begin{bmatrix} 
2 & -1 \\ 
4 & 0 \\ 
9 & 3
\end{bmatrix}
\quad\text{und} \quad
C = \begin{bmatrix} 
1 & 0 \\ 
4 & -1 
\end{bmatrix}
$$

