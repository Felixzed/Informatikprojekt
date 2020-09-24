# Projektseite
[Zurück zur Hauptseite](https://github.com/Felixzed/Informatikprojekt)

Notiz:

Projektseite beschreibt die Funktionsweise des Programms, hier nicht auf den Prozess des programmierens hinweisen, nur funktionsweise erklären.

## Glossar:

Actor: Jede Form von Objekt das ein Teil des Spielgeschehens ist. (Z.b. Spielercharakter, Wand, Kiste, Sound-Emitter, Schalter)

Execution-Pin: Visuelle Darstellung vom Scriptverlauf, jede Funktion wie z.B. "Launch Character" in Unreal Engine hat einen Execution-Pin Ein- und Ausgang. Blueprint-Scripte starten immer mit einem festen Start-Block der verschiedene Events im Spielverlauf darstellt, diese Start-Blöcke haben nur einen Execution-Output, womit ein Script anfängt.
## Granaten:

Generiert wird dieser Actor von dem Spielercharakter, er schießt das Objekt in die Richtung, in die die Kamera zeigt.

Wir beginnen mit on EventHit
Ein hit-event wird generiert, wenn ein Actor einen anderen Actor berührt.
Dieses hit-event löst einen execution-pin aus, womit wir mit dem verlauf unseres Programmes beginnen können.

### Apply Radial Damage with Falloff

![DoRadialDamageImage](.images/UnrealEngineApplyRadialDamageWithFalloff.PNG)

Diese Funktion erlaubt es, in einem Radius um einen Aufschlagspunkt dinge zu "beschädigen"
UnrealEngine kommt mit einem bereits integrierten Schaden-Framework, also muss nur definiert werden, dass Gegner auch beschädigt werden können und auch sterben.

Hierbei sind für uns Base Damage, Minimum Damage, Origin, Damage Inner Radius, Damage Outer Radius, Damage Falloff, Damage Causer und Instigated by Controller wichtig.

Base Damage beschreibt hier den Grundschaden den wir Machen wollen in unserem Radius, Minimum Damage den Minimalwert unter den Unser Schaden nicht niedriger fallen kann. Origin ist der Mittelpunkt von dem Radius und Damage Inner Radius beschreibt ab welchem Punkt in einem Radius wir vollen Schaden machen, diesen lasse ich bei "0". Damage Outer Radius beschreibt, ab wann wir den minimalschaden machen. Damage Falloff ist dann noch die Methode, die zwischen den Werten von Minimum Damage und Base Damage anhand von der Distanz zum Aufschlagspunkt und Outer Radius einen Schadenswert für einen Actor berechnet.

### Add Radial Impulse

AddRadialImpulse ist die Funktion, die unserem Granatwerfer erlaubt nach dem Aufschlagen PhysicsActor wegzustoßen.

![AddradialImpulseImage](.images/UnrealEngineAddRadialImpulse.PNG)

"Target" Beschreibt, welches Objekt den Impuls erfahren soll.
"Origin" ist der Punkt, von dem der Radius ausgeht.
Die "Radius" und "Strength" pins sind eine Float value und beschreiben jeweils die Größe des Radius und Stärke des Impulses. Außerhalb des Radius wirkt der Impuls nicht mehr. "Falloff" beschreibt dann ob die Funktion, die die abfallende Impulsstärke berechnet, exponentiell oder linear mit der Distanz vom Aufschlagspunkt abfällt. Und "Vel Change" diktiert, ob der Impuls die Masse des weggestoßenen Objektes ignorieren sollte.

Ein (Toll gezeichnetes) visuelles Beispiel:

![AddradialImpulseExplanationImage](.images/AddRadialImpulseExplanation.png)

Alle Actors, die von den Physikaktionen der Granaten betroffen werden sollen, sind mit dem "PhysicsEnabled"-Tag gekennzeichnet. 

Zuerst wird der AddRadialImpulse zwecks ForLoop ein Array von allen Actors auf der Map die den Tag "PhysicsEnabled" besitzen gegeben.
ForLoop gibt von einem Array für jeden Eintrag einmal die präzisen Daten aus. Hiermit definieren wir im Grunde dass mehr als ein Actor von AddRadialImpulse betroffen sein soll, da AddRadialImpulse eine sogenannte "Primitive Object Reference" braucht, sprich die einfach Identifikationsdaten von einem Objekt auf einer Karte.

![ForLoopImage](.images/UnrealEngineForLoop.PNG)

AddRadialImpulse folgt bei dem ForLoop allerdings dem ablauf von "Loop Body", der für jeden eintrag in einem Array abgefeuert wird. Der weite Scriptverlauf folgt "Completed", was ein signal schickt, sobald alle Einträge in dem Array verarbeitet wurden. 

"Radius" und "Strength" ist definiert als eine Konstante. Es besteht keine Absicht, die Schadenswerte in irgendeiner Art während des Spielverlaufes zu ändern.

