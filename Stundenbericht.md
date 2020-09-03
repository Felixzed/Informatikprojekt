# Stundenbericht Informatikprojekt

[Zurück zur Hauptseite](https://github.com/Felixzed/Informatikprojekt)

### Notiz:
Stundenlog sollte beschreiben, was man in einer Stunde (Oder auch Schulstunde) Arbeit am Projekt erreicht hast.

## Erste Stunde: 45 min.
Einführung in Organisatorisches, keine Arbeit am Projekt.

## Zweite Stunde: 45 min.
Arbeit an dem Projekt-Github, Arbeit an Projektwichtigen Dateien wie z.B. Stundenbericht und Readme

## Heimarbeit: 2 Stunden
Projekt erstellt.
Features: First-Person Character der Schießen, Springen und sich bewegen kann.
Brainstorming an dem Minimal Viable Product (MVP)

Erstellung Trello: https://trello.com/b/FDvxKhjR/informatikprojekt-2020

## Dritte stunde: 45 min.
Weitere Arbeit an der GitHub repository.

Erstellung Design Doc: https://docs.google.com/document/d/1RfED8MwGAkDmg-AF9oWtLQ55LMtbvNNZ1ETjN1LYYiw/edit

## Vierte Stunde: 45 min. 
Arbeit an potentieller Angehensweise für Munition, Schussfunktion und Explosionsmechaniken.

## Fünfte Stunde: 45 min.
Nachforschen von Blueprint-Programmierung, Arbeit an Organisationsprogrammen.

## Sechste Stunde: 45 min.
Weiteres Forschen an Blueprint.

## Heimarbeit: 3 Stunden
Neu: Granatwerfer Schussfunktionalität - Waffe Schießt explodierende Projektile, die andere PhysicsActors vom Aufschlagpunkt wegstößt.
Neu: Test-Map
Neu: Ragdoll-Charactere, die korrekt von Impulsen weggestoßen werden.

Besondere Schwierigkeiten:


![AddradialImpulseImage](.images/UnrealEngineAddRadialImpulse.PNG)

Add Radial Impulse war hier schwieriger zu verstehen, da ich in einem Radius PhysicsEnabled Actor von dem "Origin" (Sprich; dem Aufschlagspunkt) ausgehend wegstoßen wollte, die "Target" Node hier Definiert nicht allerdings wie vorher angenommen die 3D-Form die der Radius annimmt (z.B. Würfel, Sphere) sondern eher beschreibt es **welches** Objekt von dem Origin ausgehend in einem Radius weggestoßen werden soll. Nun musste ich einen Weg herausfinden, jedes Objekt das potentiell Weggestoßen werden konnte in diesem einen "Target" Pin anzugeben.

Gelöst habe ich dies mit einem "For" loop:

![ForLoopImage](.images/UnrealEngineForLoop.PNG)

Der ForLoop war hier perfekt, ich habe einfach jedem Objekt das Physik simuliert einen Tag gegeben, der sich "PhysicsEnabled" nennt, nun erstellen wir eine "GetActorsWithTag" node, und lassen den ausgegebenen Array in den ForLoop laufen, welcher nun für jeden Eintrag in dem Array einmal "Loop Body" ausführt, und "Completed" ausgibt, sobald alle Elemente in dem Array verarbeitet sind.

Das ganze sieht dann so aus:

*Hier noch bild hinzufügen*
