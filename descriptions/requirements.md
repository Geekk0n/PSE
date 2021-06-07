Kriterien für das Framework für Teilnehmerstudien im Bereich XAI
==============================================================

Muss-Kriterien
--------------

### Konfiguration von Studien und Experimenten

Mit dem Framework können Forscher *Studien* konfigurieren, die aus mehreren *Experimenten* bestehen.
Experimente setzen sich zusammen aus einem *Briefing*, einem *Treatment* und einem *Measurement*, siehe unten.
Die von Forschern konfigurierten Studien werden vom Framework in einer relationalen Datenbank verwaltet.


### Verwaltung von Studienteilnehmern

Das Framework bietet ein Webformular an, über das sich Studienteilnehmer registrieren können.
Forscher können zudem manuell Teilnehmer hinzufügen oder löschen.


### Automatisierte Durchführung konfigurierter Studien

Konfigurierte Studien können vom Framework automatisiert durchgeführt werden.
Registrierte Teilnehmer werden zufällig einem Experiment der Studie zugeordnet.
Zudem werden sie innerhalb des Experiments zufällig entweder der *Kontrollgruppe* oder der *Testgruppe* zugeordnet.
Die folgende Auflistung beschreibt den allgemeinen Ablauf eines Experiments, anhand dreier Phasen *Briefing*, *Treatment* und *Measurement*.
Der Ablauf für die Kontrollgruppe unterscheidet sich teilweise von dem für die Testgruppe.

  1. Briefing:
    
      - Kontroll und Test: Zeigt eine Beschreibung eines ML Modells.
      - Test: Zeigt eine Beschreibung und ein Beispiel der im Treatment verwendeten XAI Methode.

 2. Treatment:
   
     - Test: Instanziiert eine XAI Methode für das ML Modell.
       Fordert die Teilnehmer auf, mit der XAI Methode zu interagieren, um ein Verständnis des ML Modells zu entwickeln.
     - Kontroll: Zeigt Teilnehmern alle Informationen über das ML Modell an, die für die Interaktion mit der XAI Methode notwendig wären.
       Lässt Teilnehmer jedoch nicht mit der XAI Methode interagieren.
     - Beispiel: *Feature Attribution (FA)* bezeichnet XAI Methoden, die zu einem gegebenen Input-Output-Paar eines ML Modells eine Gewichtung der Input-Attribute liefern.
       Die Gewichtung soll den Einfluss der verschiedenen Input-Attribute auf den Output des Modells wiedergeben.
       Bei FA Methoden sieht die Testgruppe das Input-Output-Paar und die Gewichtung der Input-Attribute, die Kontrollgruppe sieht jedoch nur das Input-Output-Paar.

  3. Measurement:
     
     Kontroll und Test: Misst das "Verständnis" der Teilnehmer über das ML Modell. 
     Siehe Punkt *Measurements* für die zu implementierenden Maße.
     Speichert die Messergebnisse für die Kontroll- und Testgruppe getrennt in der Datenbank.

Das Framework definiert abstrakte Codeschnittstellen für Briefings, Treatments und Measurements, die Forscher implementieren können.
Zudem enthält das Framework bereits einige nutzbare Implementierungen, die wir im Folgenden beschreiben.


### Treatments

Das Framework enthält bereits folgende Implementierungen von Treatments:

  * Feature Attributions:
    
    Teilnehmer sehen eine Visualisierung von Feature Attributions (FAs).
    D.h., sie bekommen ein Input-Output-Paar eines ML Modells angezeigt, zusammen mit der Information, welche Teile des Inputs für den Output aus Sicht des ML Modells besonders "relevant" sind.
    Abhängig vom Typ der Inputs des ML Modells können Forscher zwischen verschiedenen Visualisierungen von FAs wählen:

      - bei Bildern: FAs eingeblendet als Maske. Verschiedene Optionen: multiplikativ, als Farbe, ...
      - bei niedrigdimensionalen, tabellarischen Daten: FAs als Balkendiagramm über die verschiedenen Features.


### Measurements

Das Framework enthält bereits folgende Implementierungen von Measurements:

  1. *Vorhersagen:* Zeigt Teilnehmern ausgewählte Beschreibungen von Eingaben des ML Modells.
     Lässt dann die Teilnehmer, für jede der Eingaben, die zugehörige Ausgabe des ML Modells vorhersagen.

  2. *Fehlervorhersagen:* Zeigt Teilnehmern ausgewählte Beschreibungen von Eingaben des ML Modells.
     Lässt dann die Teilnehmer, für jede der Eingaben, den Fehler des ML Modells vorhersagen.
     Beispiel: Das ML Modell ist ein binärer Classifier.
     Dann sagt der Teilnehmer vorher, ob das ML Modell ein True Positive, False Positive, True Negative oder False Negative liefert.

  3. *Subjektives Verständnis:* Fragt Teilnehmer, wie gut sie, nach ihrer eigenen Einschätzung, das ML Modell verstehen.

Wenn Forscher sowohl die Measurements 1. und 2. erheben wollen, soll das gleichzeitig möglich sein, d.h., die Teilnehmer geben zwei Vorhersagen pro gezeigter Eingabebeschreibung ab.

Für den Fall, dass die Eingaben des ML Modells Bilder sind, bietet das Framework bereits Code, um folgende Beschreibungen von Bildern entgegenzunehmen und anzuzeigen:

  * Typ und Anzahl verschiedener Objekte auf den Bildern.
  * Name und Flächenanteil verschiedener Farben auf den Bildern.


Kann-Kriterien, nach Absprache
------------------------------

### Visualisierungen der Studienergebnisse

Nach Abschluss einer Studie wollen Forscher die Ergebnisse analysieren.
Dafür sind Visualisierungen notwendig.
Das Framework könnte bereits Code enthalten, um Visualisierungen aus den Ergebnissen zu erzeugen.


### Weitere Treatments oder Measurements

Das Framework könnte weitere Treatments oder Measurements bereits vorprogrammiert enthalten.


Abgrenzung
----------

Die Anwendung muss keine ML Modelle oder XAI Methoden selbst implementieren.
Stattdessen soll die Anwendung alle Daten, die sie über ML Modelle oder XAI Methoden benötigt, über abstrakte Codeschnittstellen abfragen.
Forscher können die Schnittstellen für beliebige ML Modelle oder XAI Methoden implementieren.



Nicht-funktionale Anforderungen
-------------------------------

  * Zwischen Frontend und Backend wird strikt getrennt.
    Backend: Läuft auf Server, steuert die gesamte Studie, hält Datenbankverbindungen.
    Frontend: Läuft im Browser, interagiert mit einem Teilnehmer, informiert Backend, wird evtl. von Backend aktualisiert.

  * Das Backend ist in Python implementiert.

  * Code-Qualität:
    Der Quellcode ist Englisch.
    Sprechende Variablennamen.
    Geringes Coupling, hohe Kohäsion.
    MVC & andere Patterns.

  * Erweiterbarkeit:
    Das Hinzufügen weiterer Treatments und Measurements ist ohne Änderungen im Bestandscode möglich.

  * Die Datenbank soll ein normalisiertes Schema haben und mit sinnvollen Integritätsbedingungen versehen werden,
    insbesondere mit Primary Keys, Foreign Keys und Uniqueness Constraints.


User Story 1
============

Phase 1: Zuordnung zum Experiment
---------------------------------

Tom registriert sich über das Webformular für eine Studie.
Die Studie untersucht den Beitrag von Feature Attribution (FA) Techniken zum Teilnehmerverständnis eines bestimmten Image Classifiers.
Tom ruft die Studie auf.
Unsichtbar für Tom ordnet ihm die Studie ein Experiment zu.
Das Experiment ist gekennzeichnet durch

  * eine FA Technik,
  * einen Typ von FA Visualisierungen,
  * eine menschenverständliche, abstrakte Terminologie zur Beschreibung von Bildern.

Ebenfalls unsichtbar wird Tom der Testgruppe innerhalb des Experiments zugeordnet.


Phase 2: Briefing des Teilnehmers
-------------------------------

Nun erhält Tom eine kurze Beschreibung der Aufgabe, für die der Image Classifier trainiert wurde.
Da Tom in der Testgruppe ist, erhält er zudem eine kurze Erklärung über FAs.
Die Erklärung beinhaltet ein Beispielbild, mit der Klasse des Bildes und der auf dem Bild eingeblendeten FA, entsprechend Tom's zugeordneter FA Technik und Visualisierung.


Phase 3: Treatment
------------------

Als Treatment sieht Tom nun eine Folge von Bildern und zugehörigen Klassifikationen, sowie auf den Bildern visualisierte FAs.
Die verwendete FA Technik und die Art der Visualisierung bleibt für alle Bilder konstant, die Tom sieht.


Phase 4: Measurement
--------------------

Nach dem Treatment beginnt für Tom der Measurement-Teil der Studie.
Tom bekommt zunächst eine kurze Beschreibung der Aufgabe angezeigt, die er während des Measurements lösen soll.
Die Aufgabe ist, für gegebene Beschreibungen von Bildern, die Ausgabe des Klassifikators vorherzusagen.
Tom versucht die Aufgabe zu lösen.
Die Vorhersagen von Tom werden in der Datenbank des Experiments gespeichert.
Die Studie teilt Tom mit, dass sein Experiment beendet ist.


User Story 2
============

Ina nimmt an derselben Studie Teil wie Tom oben.
Sie wird wie Tom einem Experiment zugeordnet.

Allerdings wird sie der Kontrollgruppe innerhalb des Experiments zugeordnet.
Dadurch ändert sich folgendes:

  * Briefing: Ina erhält während des Briefings keine Erklärung über FA Methoden.
  * Treatment: Als Treatment sieht Ina eine Folge von Bildern und zugehörigen Klassifikationen, jedoch keine FAs.

Die Measurement-Phase verläuft wie bei Tom.



