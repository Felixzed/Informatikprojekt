# Projektseite
[Zurück zur Hauptseite](https://github.com/Felixzed/Informatikprojekt)

Notiz:

Projektseite beschreibt die Funktionsweise des Programms, hier nicht auf den Prozess des programmierens hinweisen, nur funktionsweise erklären.


Granaten:

Wir beginnen mit on EventHit
Ein hit-event wird generiert, wenn ein Actor einen anderen Actor berührt.

Dieses hit-event löst einen execution-pin aus, womit wir mit dem verlauf unseres Programmes beginnen können.

AddRadialImpulse ist die Funktion die unserem Granatwerfer erlaubt, dass er bei dem Aufschlagen PhysicsActor wegstoßen kann.

![AddradialImpulseImage](.images/UnrealEngineAddRadialImpulse.PNG)

Die "Radius" und "Strength" pins sind eine Float value und beschreiben jeweils Radius und Stärke des Impulses, außerhalb des Radiuses wirkt der Impuls nicht mehr. "Falloff" beschreibt dann nur noch, ob die Funktion die die Impulsstärke berechnet exponentiell oder linear mit der Distanz vom Aufschlagspunkt abfallen sollte.
