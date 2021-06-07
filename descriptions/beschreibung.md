Entwicklung eines Frameworks für Anwenderstudien im Bereich Explainable Artificial Intelligence (XAI)
=====================================================================================================

Motivation
----------

Explainable Artifical Intelligence (XAI) bezeichnet automatisierte Methoden, die Anwendern die Funktionsweise eines trainierten Machine Learning (ML) Modells erklären sollen.
Die generierten Erklärungen sollen Anwendern von ML Modellen dabei helfen, die Modelle auf bestimmte Eigenschaften zu prüfen, die nicht formal verifizierbar sind.
Darunter fallen beispielsweise die "Sicherheit" oder "Fairness" eines ML Modells im Kontext seiner Anwendung.
Man bezeichnet die Fähigkeit von Anwendern, solche Anforderungen an ML Modelle zu prüfen, oft als "Verständnis" der ML Modelle durch die Anwender.

Der Erfolg von XAI Methoden bemisst sich an ihrem Beitrag zu diesem Verständnis.
Zur Evaluation von XAI sind also Anwenderstudien nötig, die dieses Verständnis mit und ohne Unterstüzung von XAI vergleichen.
Solche Studien sind bisher rar.


Ziel
----

Ziel des Projekts ist die Entwicklung einer Software, mit der man aussagekräftige Anwenderexperimente mit verschiedenen XAI Methoden durchführen kann.
Die Software implementiert keine ML Modelle und XAI Methoden selbst, sondern bindet diese über existierenden Code ein.
Die Software bietet eine Benutzeroberfläche zur Durchführung verschiedener Experimente.
Wichtig sind dabei u.a. die Verwaltung von Studienteilnehmern, die Persistierung von Messdaten in einer Datenbank und die Umsetzung verschiedener Visualisierungen.

Ein Anwenderexperiment kann z.B. wie folgt ablaufen:
Alle Anwender bekommen Bilder gezeigt, zusammen mit einer Klassifikation in die Klassen "drinnen" und "draußen" durch ein neuronales Netz.
Die Hälfte der Anwender erhält zudem von einer XAI Methode "Erklärungen" zu den Klassifikationen.
Die Erklärungen sind eine Hervorhebung derjenigen Pixel auf den Bildern, die im neuronalen Netz einen besonders großen "Einfluss" auf die Klassifikation hatten.
Danach erhalten alle Teilnehmer textuelle Beschreibungen weiterer Bilder, z.B. "Ein Bild das 3 Personen, 1 Tisch und 1 Kuchen zeigt".
Die Teilnehmer sollen nun vorhersagen, wie das Netz diese Bilder klassifiziert.
Die Vorhersagen der Teilnehmer werden gespeichert und das Experiment ist beendet.
Man kann nun z.B. untersuchen, ob die Teilnehmer, die Erklärungen erhalten haben, bessere Vorhersagen gemacht haben.


Nebenbedingungen
----------------

Die Software soll als Webanwendung mit einer Client-Server-Architektur implementiert werden.
Das Backend soll in Python implementiert werden, da die meisten XAI Methoden eine Python API nutzen.
Die Client-Seite kann z.B. in Javascript implementiert werden, oder in Type-Script oder Python.

Die Software muss nicht in ein Bestandssystem integriert werden. Das ermöglicht eine flexible Planung.
Beim Design sind Sie gehalten, sehr auf Trennung einzelner Komponenten und Erweiterbarkeit zu achten, da die Software weiter entwickelt und verwendet werden soll.

Die Software soll im Forschungsbetrieb eingesetzt werden.
Die Teilnehmer des Projekts sollten also damit einverstanden sein, dem KIT ein Recht auf die Nutzung der Software und auf die Weiterentwicklung des Quellcodes einzuräumen.


Dieses Projekt eignet sich für Studierende mit einem Interesse an:
-------------------------------------------------------------------

  * Data Science/Maschinellem Lernen und XAI,

  * Datenbankentwurf und -anbindung,

  * Webentwicklung, und

  * Datenvisualisierungen.


