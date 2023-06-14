# MVVM Grundlagen

Ziel dieser Aufgabe ist es, Erfahrung mit grundlegenden Konzepten des Architektur-Patterns MVVM zu sammeln und dies praktisch anhand dens Frameworks [Knockout.js](https://knockoutjs.com/) anzuwenden.

## Aufgabenstellung 

Sie überarbeiten auf Basis von HTML, CSS und JavaScript mit Hilfe des JavaScript Frameworks Knockout.js[^1] die Start- bzw. Übersichtsseite für Ihre Team-Mitglieder. 

Bei der Gestaltung und dem Design der Seite sind Sie weitestgehend frei. Folgende Anforderungen müssen jedoch zwingend erfüllt sein: 

- Ihre Seite enthält die Liste mit Ihren Team-Mitgliedern (Vorname, Name, Bild).
- Die Daten in der Liste werden aus den in der vorherigen Aufgabe erstellebn JSON-Dateien geladen.
- Im Gegensatz zur vorherigen Aufgabe werden die Daten jedoch über Knockout bzw. das MVVM-Pattern in die Seite geladen.
- Bei der Auswahl eines Team-Mitglied kommt man auf die Detailansicht Ihrer jeweiligen Visitenkarte. 
- Auch hier werden  die Daten via Knockout und dem MVVM-Pattern geladen.  
* Es besteht die Möglichkeit von der Detailseite zurück zur Hauptseite zu gelangen. 
* Alle Informationen werden via MVVM geladen 
* Beschreiben Sie in einer README.txt Datei kurz, wie ein neuer Datensatz hinzugefügt werden kann. 

## Hinweise 

* In dieser Aufgabe werden die Daten statisch geladen, Sie können die Daten/Angaben, URLs für Bilder direkt den JS-Dateien hinterlegen
* Für die Bewertung wird in der Liste ein zusätzlicher Eintrag angelegt und getestet. 
* Für die Bewertung wird ein zufällig ausgewählter Browser (Google Chrome, Microsoft Edge oder Safari) genutzt. 

* Ihr CSS darf *keine* Fehler und Warnings gemäß CSS Level 3 + SVG enthalten. Die Validierung findet mittels des W3C-Validators https://jigsaw.w3.org/css-validator/ statt[^3].

* Warnings (z.B. durch *Webkit-Properties`[^2]im Validator) werden als Fehler gewertet und führen zu Punktabzug.
  > *Note:* Avoid using on websites. These properties will only work in WebKit applications.

Quelle: https://developer.mozilla.org/en-US/docs/Web/CSS/WebKit_Extensions

## Bewertung 

* Für jede Abweichung von den Anforderungen werden Punkte abgezogen. 
* Dateien die falsch oder nicht fristgemäß abgegeben wurden, werden **nicht** bewertet. 

## Referenzen

[^1]: [Knockout JS](https://knockoutjs.com/)  
[^2]: [Web Kit Extension](https://developer.mozilla.org/en-US/docs/Web/CSS/WebKit_Extensions)  
[^3]: [W3C Validator](https://jigsaw.w3.org/css-validator)