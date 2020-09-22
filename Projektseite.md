# Projektseite
[Zurück zur Hauptseite](https://github.com/Felixzed/Informatikprojekt)

Notiz:

Projektseite beschreibt die Funktionsweise des Programms, hier nicht auf den Prozess des programmierens hinweisen, nur funktionsweise erklären.

## Glossar:

Actor: Jede Form von Objekt das ein Teil des Spielgeschehens ist. (Z.b. Spielercharakter, Wand, Kiste, Sound-Emitter, Schalter)


## Granaten:

Generiert wird dieser Actor von dem Spielercharakter, er schießt das Objekt in die Richtung, in die die Kamera zeigt.

Wir beginnen mit on EventHit
Ein hit-event wird generiert, wenn ein Actor einen anderen Actor berührt.
Dieses hit-event löst einen execution-pin aus, womit wir mit dem verlauf unseres Programmes beginnen können.

### Apply Radial Damage with Falloff

![DoRadialDamageImage](.images/UnrealEngineApplyRadialDamageWithFalloff.PNG)

Diese Funktion erlaubt es, in einem Radius um einen Aufschlagspunkt dinge zu "beschädigen"
UnrealEngine kommt mit einem bereits integrierten Schaden-Framwork, also muss nur definiert werden, dass Gegner auch beschädigt werden können und auch sterben.

Hierbei sind für uns Base Damage, Minimum Damage, Origin, Damage Inner Radius, Damage Outer Radius, Damage Falloff, Damage Causer und Instigated by Controller wichtig.

Base Damage beschreibt hier den Grundschaden den wir Machen wollen in unserem Radius, Minimum Damage den Minimalwert unter den Unser Schaden nicht niedriger fallen kann. Origin ist der Mittelpunkt von dem Radius, Damage Inner Radius beschreibt ab welchem Punkt in einem Radius wir vollen Schaden machen, diesen lasse ich bei "0". Damage Outer Radius beschreibt, ab wann wir den minimalschaden machen. Damage Falloff ist dann noch die Methode, die zwischen den Werten von Minimum Damage und Base Damage anhand von der Distanz zum Aufschlagspunkt und Outer Radius einen Schadenswert für einen Actor berechnet.

### Add Radial Impulse

AddRadialImpulse ist die Funktion, die unserem Granatwerfer erlaubt nach dem Aufschlagen PhysicsActor wegzustoßen.

![AddradialImpulseImage](.images/UnrealEngineAddRadialImpulse.PNG)

"Target" Beschreibt, welches Objekt den Impuls erfahren soll.
"Origin" ist der Punkt, von dem der Radius ausgeht.
Die "Radius" und "Strength" pins sind eine Float value und beschreiben jeweils die Größe des Radius und Stärke des Impulses, außerhalb des Radiuses wirkt der Impuls nicht mehr. "Falloff" beschreibt dann ob die Funktion die die abfallende Impulsstärke berechnet exponentiell oder linear mit der Distanz vom Aufschlagspunkt abfällt. Und "Vel Change" diktiert ob der Impuls die Masse des weggestoßenen Objektes ignorieren sollte.

Ein visuelles Beispiel:

![AddradialImpulseExplanationImage](.images/AddRadialImpulseExplanation.png)

Wir nehmen "Radius" und "Strength" als eine Konstante. Wir haben keine Absicht, die Schadenswerte in irgendeiner Art zu ändern.
