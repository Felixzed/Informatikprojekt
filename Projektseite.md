# Projektseite
[Zurück zur Hauptseite](https://github.com/Felixzed/Informatikprojekt)

Notiz:

Projektseite beschreibt die Funktionsweise des Programms, hier nicht auf den Prozess des programmierens hinweisen, nur funktionsweise erklären.


## Granaten:

Wir beginnen mit on EventHit
Ein hit-event wird generiert, wenn ein Actor einen anderen Actor berührt.

### Apply Radial Damage with Falloff

Dieses hit-event löst einen execution-pin aus, womit wir mit dem verlauf unseres Programmes beginnen können.

![DoRadialDamageImage](.images/UnrealEngineApplyRadialDamageWithFalloff.PNG)

Diese Funktion erlaubt es, in einem Radius um einen Aufschlagspunkt dinge zu "beschädigen"
UnrealEngine kommt mit einem bereits integrierten Schaden-Framwork, also muss ich mich nur sichergehen, dass Gegner auch beschädigt werden können und auch sterben.

Hierbei sind für uns Base Damage, Minimum Damage, Origin, Damage Inner Radius, Damage Outer Radius, Damage Falloff, Damage Causer und Instigated by Controller wichtig.

Base Damage beschreibt hier den Grundschaden den wir Machen wollen in unserem Radius, Minimum Damage den Minimalwert unter den Unser Schaden nicht niedriger fallen kann. Origin ist der Mittelpunkt von dem Radius, Damage Inner Radius beschreibt ab welchem Punkt in einem Radius wir vollen Schaden machen, diesen lasse ich bei "0". Damage Outer Radius beschreibt, ab wann wir den minimalschaden machen. Damage Falloff ist dann noch der Exponent, der zwischen den Werten von Minimum Damage und Base Damage anhand von der Distanz zum Aufschlagspunkt und Outer Radius einen Schadenswert für einen In den Radien stehenden Actor berechnet.

### Add Radial Impulse

AddRadialImpulse ist die Funktion die unserem Granatwerfer erlaubt, dass er bei dem Aufschlagen PhysicsActor wegstoßen kann.

![AddradialImpulseImage](.images/UnrealEngineAddRadialImpulse.PNG)

Die "Radius" und "Strength" pins sind eine Float value und beschreiben jeweils Radius und Stärke des Impulses, außerhalb des Radiuses wirkt der Impuls nicht mehr. "Falloff" beschreibt dann nur noch ob die Funktion die die Impulsstärke berechnet exponentiell oder linear mit der Distanz vom Aufschlagspunkt abällt.
