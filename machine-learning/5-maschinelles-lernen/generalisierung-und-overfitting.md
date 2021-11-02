# Generalisierung und Overfitting

**Generalisierung **beschreibt,  wie ein Modell auf Daten aus der "gleichen" Datenquelle funktioniert, die nicht Teil des Trainings waren. (_never  before seen data_**, **nbs-data). Aus diesem Grund trennen wir unseren Datenbestand in Trainings- und Testdaten auf.

Der Begriff der Generalisierung hängt eng mit dem Begriff des **Overfitting **zusammen: Ein Modell passt sich so gut an die Trainingsdaten an, dass es auf nbs-Daten schlecht funktioniert. Wie sprechen auch von **maschinellem Auswendiglernen.**

Bei nachfolgendem Regressions-Beispiel sind die x-Koordinaten der Punkte die Features und die y-Koordinaten die Labels. Während die blaue Kurve alle Punkte exakt trifft, ist die schwarze Gerade die bessere Lösung für das Problem. Die Gefahr des Overfittings besteht immer dann, wenn das Modell so komplex wird, dass es zwar alle labels sehr gut vorhersagt, aber die Struktur der Daten (im Bild die der offensichtlich lineare Zusammenhang) dabei verloren geht.

![Quelle: Wikipedia](<../../.gitbook/assets/image (120).png>)

****
