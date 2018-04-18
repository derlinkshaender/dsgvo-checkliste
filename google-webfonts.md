Google WebFonts

## Wo ist das Problem?

Viele Websites nutzen aus dem Internet eingebettete Schriftarten, sei es Google Webfonts, die Icon-Schriftart FontAwesome oder Adobe Typekit und andere.
Damit lassen sich ansprechende Seiten erstellen, das Laden der Schriftart-Dateien von einer externen Quelle übermittelt
aber personenbezogene Daten an den Anbieter der Schriftarten (z.B. Google), ohne das hierzu vorher die Einwilligung des Nutzers erteilt wurde. Damit lassen sich Profiling betreiben bzw. werden Daten übetragen, die laut DSGVO als personenbezogene Daten gelten.

## Wie finde ich heraus, ob ich betroffen bin?

Zur Überprüfung, ob auf der eigenen Homepage Schriften aus externen Quellen eingebunden sind, eignet sich der Dienst "Webbkoll" (https://webbkoll.dataskydd.net/en/). Dort trägt man die URL seiner Seite ein und klickt auch "Check". Auf der Ergebnisseite tauchen Anfragen zur entfernten Schriftarten-Dateien im Bereich "Third-Party-Requests" auf. Bei Google Fonts wird zum Beispiel Kontakt zum Server "fonts.gstatic.com" aufgenommen. Findet sich also ein derartiger Eintrag bei den Ergebnissen, sollten Sie einen der unten genannten Schritte unternehmen.

## Wie lässt sich das Problem lösen?


## Auf eingebundene Schriftarten verzichten

### Wie erfahren/technikaffin muss ich dafür sein?

Gar nicht.

Die einfachste Lösung, aber auch die typographisch langweiligste. Sie benutzen einfach nur Standard-Schriftarten, die der Browser der Besucher unterstützt. Falls Sie gerade mit einem Webauftritt beginnen, ist das eine einfache Lösung, die Sie später jederzeit ausbauen können durch die Schritte weiter unten.

Wenn Sie für Ihre Homepage ein Content-Management-System nutzen (CMS), wie zum Beispiel Wordpress, Joomla oder Drupal, dann sollten Sie sich für ein Design/Theme entscheiden, welches auf die Einbindung von Google Fonts verzichtet. Für Wordpress wäre ein entsprechendes Theme z.B. Hueman (https://wordpress.org/themes/hueman/).

Teilweise werden aber externe Schriften auch durch Erweiterungen (Plugins) aufgerufen, die im CMS installiert sind. Sollte also der Aufruf externer Schriften nicht durch den Wechsel des Themes unterbunden werden können, sollte man prüfen, ob die Deaktivierung einzelner Plugins zur Lösung beitragen kann.

## Die benötigten Schriftarten lokal auf dem eigenen Webauftritt ablegen

### Wie erfahren/technikaffin muss ich dafür sein?

Mittel.

Sie benötigen folgende Kenntnisse:

* die [CSS-Dateien](https://de.wikipedia.org/wiki/Cascading_Style_Sheets) Ihres Webauftritts anpassen
* wissen, welche Schriftarten (in welchen Schriftschnitten) Sie aktuell beziehen
* die heruntergeladenen Schriftartdateien entpacken und auf Ihren Webserver transpotieren


### Vorgehen

Ein Hilfsmittel ist der [Google Webfont Helper](https://google-webfonts-helper.herokuapp.com/fonts), mit sich die benötigten Schriftarten als Archiv herunterladen lassen. Diese werden dann einfach in ein Verzeichnis auf Ihrem Webspace entpackt. Nun muss nur noch der Verweis in allen Stylesheets (den .css Dateien) auf die lokale Kopie anstelle der externen URL geändert werden.

In Ihren Stylesheets sieht die EInbindung einer Schrift (hier am Beispiel von _OpenSans_ von Google Webfonts) in etwa so aus:

    @font-face {
      font-family: 'Open Sans';
      font-style: normal;
      font-weight: 400;
      src: local('Open Sans Regular'), 
           local('OpenSans-Regular'), 
           url(https://fonts.gstatic.com/s/opensans/v15/mem8YaGs126MiZpBA-UFVZ0bf8pkAg.woff2) format('woff2'),
           url(https://fonts.gstatic.com/s/opensans/v15/mem8YaGs126MiZpBA-UFVZ0bf8pkAg.woff) format('woff');
    }

Diese externe URL, die auf die Google Font-Server zeigt, ersetzen Sie nun durch den lokalen Pfad auf Ihrem Webserver, an dem die heruntergeladenen Schriftarten liegen. Beispiel (hier liegen die Schriftarten im gleiche Ordner wie die css-Dateien):


    @font-face {
      font-family: 'Open Sans';
      font-style: normal;
      font-weight: 400;
      src: url('open-sans-v15-latin-regular.eot'); /* IE9 Compat Modes */
      src: local('Open Sans Regular'), 
           local('OpenSans-Regular'),
           url('open-sans-v15-latin-regular.woff2') format('woff2'), /* Super Modern Browsers */
           url('open-sans-v15-latin-regular.woff') format('woff'), /* Modern Browsers */
           url('open-sans-v15-latin-regular.ttf') format('truetype'), /* Safari, Android, iOS */
           url('open-sans-v15-latin-regular.svg#OpenSans') format('svg'); /* Legacy iOS */


Durchsuchen Sie alle nun alle CSS-Dateien nach entsprechenden Einträgen und tauschen Sie die Angabe der Schriftart aus.

Bei einigen Wordpress-Themes erfolgt der Aufruf der externen Schriften durch einen Eintrag in einer PHP-Datei. Diese muss dann noch zusätzlich angepasst werden. Das Vorgehen wird in diesem Video erklärt: https://t.co/dBmENnG4GZ
