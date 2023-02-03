_Grundlagen der KI - Beckstein und Mitschunas_

Suche im Überblick
+ Es geht um heuristische Suchverfahren
+ Warum ist Suche wichtig und welche Bewandnis hat sie für die Erstellung von intelligenten Systemen?
+ Lernverfahren funktionieren durch systematisches Probieren

# Grundbegriffe
+ Man hat einen Agenten der in der realen Welt operiert
+ Die Aufgabe der Suche ist, eine Folge von Handlungen im Repertoire zu finden, sodass ein vorgegebenes Ziel erreicht wird

+ _Beispiel:_
	+ Eine Sonde ist auf dem Mars und soll autonom (wenigstens teilautonom) Leben auf dem Mars finden
	+ Diese Sonde bzw. Agent hat ein Repertoire an Handlungen. Die Aufgabe der Suche ist es nun zu bestimmen wie die Sonde vorgeht um Leben auf dem Mars zu finden.
	
_Beispiel 2:_ In Kalkülen wird das durch Ableitungen gemacht. Der Zustandsraum ist die Welt der Beweise. Die Schritte die getätigt werden können sind Ableitungsschritte.

## Zustandsraum
+ Ist eine Abbildung der realen Welt in eine Systembeschreibung. Man modelliert also die reale Welt nach bestimmten Eigenschaften.

### Modellierung
Es gibt einige Fragen vorab zu klären:

+ Welche Aspekte der Zustandsräume sollen beachtet werden?

+ Wie repräsentiere ich einen Zustandsraum in einem Rechner? (nicht nur die Parameter des Zustandsraums sondern auch die Schritte die möglich sind)

+ Wenn geklärt ist wie man ihn repräsentiert; wie kriegt man eine sehr große reale Welt in den Rechner? → Man darf nur so viel wie unbedingt nötig repräsentieren.

+ Man kennzeichnet potentielle Start- und Zielzustände

+ Wenn diese Modellierung minimal geschieht und nur auf relevanten Bereichen des Zustandsraumes sucht, dann kann die Suche auch effizient passieren.  

+ _Bsp.:_
	+ Bei der Modellierung / Suche einer Reise in Erfurt ist der Luftdruck etwa nicht relevant; welche Farbe das Auto hat wahrscheinlich auch nicht.
	+ Navigationsdetails in anderen Städten (wie Rom oder Teheran) sind auch nicht relevant für dieses Problem.

  
+ Zustandsräume werden häufig durch Diagramme wie das nachfolgende Beschrieben (siehe Skript Seite 1)

+ In der realen Welt müssen es nicht immer Bäume sein. Es gibt auch zyklische Graphen die durch Suchen entstehen (etwa bei Puzzles wenn man wild herumprobiert. Man kehrt möglicherweise zum Ausgangspunkt zurück.)

+ Der Rechner kennt keine realen Details der Repräsentation, weil er sie nicht benötigt. Die Knoten in dem Baum werden (von uns später) mit Details verknüpft.

+ Der Rechner erstellt schrittweise den Baum durch ein Suchverfahren

	+ er hat durch uns Kenntnis von den relevanten Details (wurden im Zustandsraum modelliert)

	+ er muss die Bedeutung der Kanten kennen und welche Auswirkung sie auf die Details haben (Knoten = Beschreibung bzw. Zustand, Kante = Modifikation der Beschreibung)

	+ er fügt neue Knoten an die entsprechenden Kanten an (durch systematisches Probieren, auch **Expansion** genannt), sodass irgendwann ein Zielzustand erreicht wird


+ Ideal wäre es, wenn er den Baum möglichst wenig expandiert. Wenn er den Pfad von $i$ nach $g$ direkt fünde, wäre es perfekt.
+ Deswegen ist es so wichtig, dass die Modellierung möglichst minimal ist. Der Baum wäre sonst aufgrund dessen schon unhandlich groß.

+ Es ist interessant nachzuvollziehen, wie der Baum gewachsen ist.
	+ **Konvention:** was weiter rechts im Baum steht wurde später expandiert
	+ Auch sollte man das Expansionsverfahren angeben. Man kann sonst nicht genau nachvollziehen, welche Knoten zuerst expandiert wurden. Zum Beispiel werden bei Breitensuche zuerst die Geschwister, bei Tiefensuche zuerst die Kinder expandiert (mehr dazu später).

**Skript Seite 2**

+ Wichtig ist neben dem Expansionsverfahren ist auch das **Überprüfungsverfahren:**
	+ Handelt es sich bei der Beschreibung die durch eine Modifikation erreicht wurde nun um einen Zielzustand in der realen Welt?

+ Das Ziel des Suchverfahrens ist es, eine möglichst kostengünstige Handlungsfolge zu finden. Dies muss nicht die Erstgefundene sein. 
	+ Es muss Kriterien für die Richtung der Expansion geben. Warum (Bezug auf Beispiel von Seite 1) haben wir zuerst auf $c_1$ statt auf $c_2$ expandiert?
	+ Wir wollen nachvollziehen können, warum wir diese Schritte vorgenommen haben.
	+ Wir müssen den Aufwand der Aktionen bewerten können. Dies kann man durch die Bewertung der Aktionen in der realen Welt mit konkreten Kosten im Graphen vornehmen.
+ Beispiel:
	+ Radfahren und Autofahren kann günstiger oder teurer sein. Auf die Zeit betrachtet ist Autofahren günstiger. Wenn man die Umwelt in Betracht zieht ist Radfahren besser.

Das heißt:
_Wie können wir steuern, dass möglichst früh gefundene Lösungen auch optimal sind?_

Es ist nämlich leider sehr teuer (oder gar unmöglich) _alle_ Lösungen zu finden bzw. einen Graphen vollständig zu expandieren.

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

_Beispiel Schach:_
+ Die Kanten / Modifikationen sind die Züge
+ Die Beschreibungen (bzw. die Knoten oder Zustände) sind die Positionen der Figuren auf dem Schachbrett
+ Die Heuristik ist dann die Auwahl eines möglichst guten nächsten Zuges, sodass ein Zielzustand möglichst schnell erreicht wird bzw. möglichst wenig Expansionsschritte notwendig sind. 