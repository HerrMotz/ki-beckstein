_Grundlagen der KI - Beckstein und Mitschunas_

Suche im Überblick
+ Es geht um heuristische Suchverfahren
+ Warum ist Suche wichtig und welche Bewandnis hat sie für die Erstellung von intelligenten Systemen
+ Lernverfahren funktionieren durch systematisches Probieren

# Grundbegriffe
+ Man hat einen Agenten der in der realen Welt operiert
+ z.B. auf dem Mars und er plant teilautonom.
+ Der Agent hat also ein Repertoire an Handlungen
+ Die Aufgabe ist, eine Folge von Handlungen im Repertoire zu finden, sodass das Ziel erreicht wird

+ In Kalkülen wird das durch Ableitungen gemacht. Der Zustandsraum ist die Welt der Beweise. Die Schritte die getätigt werdne können sind Ableitungsschritte

## Zustandsraum
+ besteht aus der realen Welt

### Modellierung
Es gibt einige Fragen vorab zu klären:

+ Welche Aspekte der Zustandsräume sollen beachtet werden?

+ Wie repräsentiere ich es in einem Rechner?

+ nicht nur die Parameter des Zustandsraums

+ sondern auch die Schritte die möglich sind

+ Wenn geklärt ist wie man es repräsentiert wie kriegt man eine sehr große reale Welt in den Rechner?
	+ Man darf nur so viel wie nötig repräsentieren.

+ Man kennzeichnet potentielle Start- und Zielzustände


+ Wenn diese Modellierung minimal geschieht und nur auf relevanten Bereichen des Zustandsraumes sucht, dann kann diese Suche auch effizient passieren.  

+ Bsp.:
	+ Bei der Modellierung / Suche einer Reise in Erfurt ist der Luftdruck etwa nicht relevant; welche Farbe das Auto hat wahrscheinlich auch nicht.

	+ Navigationsdetails in anderen Städten sind auch nicht relevant für dieses Problem.

  

+ Zustandsräume werden häufig durch Diagramme wie das nachfolgende Beschrieben (siehe Skript Seite 1)

+ In der realen Welt müssen es nicht immer Bäume sein wie hier. Es gibt auch zyklische Bäume (etwa bei Puzzles bei denen man immer wieder die gleichen Schritte durchprobiert)

+ Der Rechner kennt keine realen Details der Repräsentation, weil er sie nicht benötigt. Die Knoten in dem Baum werden (von uns später) mit Details verknüpft.


+ Der Rechner modelliert schrittweise den Baum

	+ er hat durch uns Kenntnis von den relevanten Details

	+ er muss die Bedeutung der Kanten kennen und welche Auswirkung sie auf die Details haben (Kante = Modifikation)

	+ er fügt neue Knoten an die entsprechenden Kanten an (durch systematisches Probieren), sodass irgendwann ein Zielzustand erreicht wird


+ ideal ist, dass er möglich wenig generiert. wenn er den Pfad von $i$ nach $g$ direkt fünde, wäre es perfekt.
+ deswegen ist es so wichtig, dass die Modellierung möglichst minimal ist.

+ Es ist interessant nachzuvollziehen, wie der Baum gewachsen ist
	+ Konvention: was weiter rechts im Baum steht wurde später expandiert
	+ Man kann nicht genau nachvollziehen, welche Kinder zuerst expandiert wurden, wenn das Expansionsverfahren nicht angegeben ist.

**Jetzt: Skript Seite 2**

+ Wichtig ist neben dem Expansionsverfahren auch das Überprüfungsverfahren:
	+ Handelt es sich bei der Beschreibung die durch eine Modifikation erreicht wurde durch einen Zielzustand in der realen Welt?

+ Es muss Kriterien für die Richtung der Expansion geben. Warum (Bezug auf Beispiel von Seite 1) haben wir zuerst auf $c_1$ statt auf $c_2$ expandiert?
	+ Wir wollen nachvollziehen können, warum wir diese Schritte vorgenommen haben.
	+ Wir müssen die Kosten der Aktionen bewerten können. Dies kann durch die Bewertung bzw. Assoziationen der Aktionen in der realen Welt mit konkreten Kosten vornehmen.
	+ Das Ziel des Suchverfahrens ist es, eine möglichst kostengünstige Handlungsfolge zu finden. Dies muss nicht die Erstgefundene sein. 
+ Beispiel:
	+ Radfahren und Autofahren kann günstiger oder teurer sein. Auf die Zeit betrachtet ist Autofahren günstiger.

Das heißt:
_Wie können wir steuern, dass möglichst früh gefundene Lösungen auch optimal sind?_

Es ist nämlich leider sehr teuer (oder oft unmöglich) _alle_ Lösungen bzw. einen Graphen mit allen Lösungen zu finden.

#### Definition
Jede Aktion hat positive Kosten. Die Kosten sind immer größer als 0, seien sie noch so klein. Dies ist wichtig, damit man heuristisch suchen kann. Sonst kann man sehr lange Aktionsfolgen finden, die in Summe keine Kosten besitzen.

**Seite 3**

Die Modifikation ist hier das Eintragen eines Wortes. In den Donut kann man insgesamt 5 Wörter eintragen. 
+ Die Aktion besteht darin immer ganze Wörter einzufügen; _nicht aber_ einzelne Buchstaben einzufügen. Dies ist eine bewusste Entscheidung der Modellierung.
+ Ein Rechner wird hier in einem Wörterbuch nach passenden Wörtern suchen und sie einsetzen.
+ Dieses Problem kann problemlos algorithmisch dargstellt werden.

**Seite 4**

Die Modifikation ist jetzt Eintragen eines einzelnen Buchstaben. Verzweigungsgrad kann maixmal 26 betragen und ist damit kleiner als zuvor. Es gibt erstmal mehr dreistellige Wörter als Buchstaben, das nimmt natürlich mit jeder Modifikation ab.

Frage: was hat dieses Aufstellen eines Graphen mit Intelligenz zu tun?
Antwort: Nichts. Wurde auch nicht behauptet. Die Modifikation ist momentan erstmal das anspruchsvolle.

**Seite 5**

$L$ im Skript wird von Beckstein "Openlist" (noch nicht abgearbeitete Knoten) genannt. Die "Closedlist" wären dann bereits abgearbeitete Knoten.

**Seite 6**

+ Die Beschriftung der Knoten ist die Reihenfolge in der sie expandiert wurden.

+ Man spricht bei den jetzt vorgestellten Expansionsverfahren von blinden Verfahren, weil sie nicht intelligent sind, sondern rein durch algorithmisches Absuchen lösen.  
+ Tiefenexpansion bzw. Tiefensuche expandiert zuerst die Kinder, dann die Geschwister

**Seite 7**

+ Tiefenexpansion kann zum Verhungern von Knoten führen. Weil man immer erst die Kinder expandieren muss, könnte ein Knoten in d=1 (in der Grafik Beschriftet mit 2), der eine Lösung ist, niemals zur Expansion kommen, wenn man den linken Teilgraphen beliebig expandieren könnte

+ Bei Breitensuche ist fair, weil der Expansionsgrad in jeder Stufe endlich ist. So kommt jeder Knoten garantiert mit der Expansion dran.

+ Breitensuche ist allerdings mit viel Speicheraufwand verbunden. Man muss erst eine gesamte Ebene expandieren (und sie auch abspeichern) bevor man weitergeht.

## Begriff der Heuristik
+ Eine Funktion mit dem wir unnötige Expansion verhindern können. 
+ Wir bestimmen also einen möglichst guten Knoten den wir als nächstes expandieren.
+ Interessant ist gar nicht ein absoluter numerischer Wert für die beste nächste Expansion, sondern eine ungefähre Schätzung welche der verfügbaren Optionen besser ist als eine andere.

### Beispiel
+ Schach:
	+ Die Kanten / Modifikationen sind die Züge
	+ Die Beschreibungen (bzw. die Knoten oder Zustände) sind die Positionen der Figuren auf dem Schachbrett
	+ Die Heuristik ist dann die Auwahl eines möglichst guten nächsten Zuges, sodass ein Zielzustand möglichst schnell erreicht wird bzw. möglichst wenig Expansionsschritte notwendig sind. 