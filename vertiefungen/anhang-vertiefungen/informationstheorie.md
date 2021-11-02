---
description: >-
  Für das Design von Entscheidungsbäumen oder die Definition von Loss-Funktionen
  für multi-kategorische Probleme sind Grundkenntnisse in Informationstheorie
  hilfreich.
---

# Informationstheorie (in Bearbeitung)

## Diskrete Zufallsvariablen und Wahrscheinlichkeitsfunktionen

Eine **Zufallsvariable **$$X$$** heißt diskret**,  wenn sie (abhängig vom Zufall) einen Wert aus einer  endlichen  Menge möglicher Werte annimmt. Diese Menge heißt **Ereignismenge.  **Besteht die Ereignismenge aus Zahlen, so heißt die Zufallsvariable auch **Zufallsgröße**. Dies  muss aber nicht unbedingt der Fall sein.  Zum Beispiel ist auch $$\{"\text{Kopf}", "\text{Zahl}"\}$$eine mögliche Ereignismenge für ein Zufallsvariable. Wenn wir keine andere Definition treffen, notieren wir die Ereignismenge in der Form $$\{x_1, ... , x_n\}$$.  (Die Menge kann auch abzählbar unendlich viele Elemente enthalten- aber das interessiert uns hier nicht.) Die **Wahrscheinlichkeit**, mit der X den Wert $$x_i$$ annimmt, notieren wir mit $$P(X = x_i)$$ , oder kurz $$p_i$$.

## Information

Wir wollen den Informationsgehalt von Nachrichten messen, die wir von einem Sender empfangen. Hierzu nehmen wir an, dass die Nachrichtenquelle einer diskreten Zufallsvariable entspricht und die möglichen Nachrichten die Ereignismenge bilden. Den Informationsgehalt einer konkreten Nachricht  $$x_i$$ notieren wir mit $$I(p_i)$$. Zur Vereinfachung der Notation  definieren wir also den Informationsgehalt abhängig von der jeweiligen Wahrscheinlichkeit der Nachricht, und nicht von der Nachricht selbst. Sofern der konkrete Index  Nachricht ohne Bedeutung ist, lassen wir ihn auch weg und schreiben nur$$I(p)$$.

Wir wollen Informationsgehalt $$I(p)$$ einer  aus endlich vielen Möglichkeiten und mit der Wahrscheinlichkeit $$p$$ auftretenden Nachricht messen. Wir fordern zuerst, dass der Informationsgehalt einer derartigen Nachricht  stets eine nicht negative Zahl ist, also

$$
I(p) \geq 0
$$

Weiterhin soll eine Information über ein _seltenes _Ereignis soll einen höheren Informationswert haben, als eine Information über ein _häufiger auftretendes_ Ereignis, also

$$
p \leq q \quad\Rightarrow\quad I(p) \geq I(q)
$$

Schließlich soll gelten, dass der Informationsgehalt für zwei _unabhängige _Nachrichten mit Auftretenswahrscheinlichkeiten  $$p >0$$ und $$q > 0$$ die Summe der jeweiligen einzelnen Informationsgehalte ist, also

$$
I(p\cdot q)=  I(p) + I(q)
$$

Zur Illustration der beiden letzten Aussagen nehmen sie an, dass jemand würfelt und eine Münze wirft. Die Wahrscheinlichkeit $$p$$ für den Ausgang des Münzwurfs ist $$1/2$$ und die Wahrscheinlichkeit $$q$$ für ein konkretes Würfelergebnis ist $$1/6$$. Der Informationsgehalt über den Ausgang des Würfelergebnisses soll also  höher sein, als der Informationsgehalt über den Ausgang des Münzwurfes.

Der Informationsgehalt lässt sich auch als ein Maß für die _Reduktion unserer Unsicherheit_ über den Ausgang eines Ereignisses beschreiben. Die Nachricht über den Ausgang des Münzwurfs hat unsere Unsicherheit von 2 Möglichkeiten auf _eine _Möglichkeit reduziert. Die Information über den Ausgang des Würfelns aber hat unsere Unsicherheit von 6 Möglichkeiten auf _eine_ Möglichkeit reduziert!

Um obige Eigenschaften zu erfüllen, definieren wir den **Informationsgehalt** einer Nachricht mit Wahrscheinlichkeit $$p$$ mit:

$$
I(p) = \log_b(\frac{1}{p}) = - \log_b(p)
$$

für ein beliebige Basis  $$b > 0$$.  Sie können selbst leicht nachprüfen, dass die Forderungen eingehalten sind.

#### Welche Basis? (b=2)

Wenn wir fordern, dass eine Information, die unsere Unsicherheit über die Ausprägung eines Ereignisses halbiert, den Informationswert 1 haben soll, so erreichen wir dies mit $$b=2$$ da $$1 = -\log_2(1/2)$$. Mit dieser Wahl ist die Einheit des Informationsgehalts **bit**.

Unsere Wahl hat einige Eigenschaften, die wir auch explizit hätten  fordern  können, zum Beispiel: Eine Nachricht mit der Wahrscheinlichkeit 1, z.B. "Der Münzwurf ergab Kopf oder Zahl", hat Informationswert 0. (Dies gilt sogar unabhängig von der Basis)

## Entropie

Der Informationsgehalt bezieht sich nur auf eine _einzelne _Nachricht. Wir betrachten nun eine endliche Menge X von Nachrichten, wobei jede Nachricht $$x_i$$ mit der Wahrscheinlichkeit $$p_i$$ auftritt. Dann können wir den mittleren (erwarteten)  Informationsgehalt einer Nachricht aus der Menge X berechnen mit

$$
H(X) = -  \sum_{x\in X} P(x)  \cdot \log_2( P(x))
$$

Weil $$H$$ nur von den  Verteilung $$P$$abhängt, schreiben wir auch $$H(P)$$ statt $$H(X).$$ Damit kommen wir zur Definition der **Entropie **$$H(P)$$**einer endlichen Verteilung **$$P = \{p_1,..p_n\}$$****

$$
H(P) = -  \sum_{i = 1}^n  p_i  \cdot \log_2( p_i)
$$

