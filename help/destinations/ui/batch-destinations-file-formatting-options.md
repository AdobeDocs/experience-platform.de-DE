---
description: Erfahren Sie, wie Sie beim Aktivieren von Daten für dateibasierte Ziele Dateiformatierungsoptionen konfigurieren
title: (Beta) Dateiformatierungsoptionen für dateibasierte Ziele konfigurieren
source-git-commit: 23a7a1997e05d2bde26de5b73a23ea051bf2b3bb
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 20%

---

# (Beta) Dateiformatierungsoptionen für dateibasierte Ziele konfigurieren

>[!IMPORTANT]
>
>Die **[!UICONTROL Dateiformatierungsoptionen]** -Funktion in Adobe Experience Platform ist derzeit als Beta-Version verfügbar. Dokumentation und Funktionalität können sich ändern.
>Wenden Sie sich an Ihre Adobe-Support-Mitarbeitenden, um Zugriff auf diese Funktion zu erhalten.
> 
>Die in diesem Dokument beschriebenen Dateiformatierungsoptionen sind derzeit nur für CSV-Dateien verfügbar.

Die Option zur Konfiguration verschiedener Dateiformatierungsoptionen für die exportierten Dateien ist verfügbar, wenn Sie [connect](/help/destinations/ui/connect-destination.md) in ein dateibasiertes Ziel, z. B. [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md#connect), [Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md#connect)oder [SFTP](/help/destinations/catalog/cloud-storage/sftp.md#connect).

Mithilfe der Experience Platform-Benutzeroberfläche können Sie verschiedene Dateiformatierungsoptionen für exportierte Dateien konfigurieren. Sie können verschiedene Eigenschaften der exportierten Dateien an die Anforderungen des Dateiempfangssystems auf Ihrer Seite anpassen, um die aus Experience Platform empfangenen Dateien optimal zu lesen und zu interpretieren.

<!--
* To configure file formatting options for exported files by using the Experience Platform UI, read this document.
* To configure file formatting options for exported files by using the Experience Platform Flow Service API, read [Flow Service API - Destinations](https://developer.adobe.com/experience-platform-apis/references/destinations/).
-->

## Dateiformatierung {#file-configuration}

>[!IMPORTANT]
>
>Für das Ziel, mit dem Sie eine Verbindung herstellen, stehen möglicherweise nicht alle diese Optionen zur Verfügung. Es ist Sache des Ziel-Entwicklers, zu bestimmen, welche Dateiformatierungsoptionen am Ziel unterstützt werden sollen. Der Ziel-Entwickler kann bestimmen, welche Optionen beim Herstellen einer Verbindung zum Ziel verfügbar sind. Die erforderlichen Optionen sind in der Experience Platform-Benutzeroberfläche mit einem Sternchen gekennzeichnet.

Um die Dateiformatierungsoptionen anzuzeigen, starten Sie die [Verbindung zum Ziel herstellen](/help/destinations/ui/connect-destination.md) Workflow und Auswahl von Segmenten als **Dateityp**. In diesem Abschnitt werden die für den exportierten `CSV` Dateien.

![Bild mit einigen der verfügbaren Dateiformatierungsoptionen.](/help/destinations/assets/ui/batch-destinations-file-formatting-options/file-formatting-options.png)

### Trennzeichen

Legt für jedes Feld und jeden Wert ein Trennzeichen fest. Beispiel: `,` für kommagetrennte Werte oder `/t` für tabulatorgetrennte Werte.

### Anführungszeichen

Legt ein einzelnes Zeichen fest, das zum Maskieren von angegebenen Werten verwendet wird, wobei das Trennzeichen Teil des Werts sein kann.

### Escape-Zeichen

Legt ein einzelnes Zeichen fest, das zum Maskieren von Anführungszeichen verwendet wird, die innerhalb eines bereits mit Anführungszeichen versehenen Werts liegen.

### Ausgabe leerer Werte

Legt die Zeichenfolgendarstellung eines leeren Werts fest.

### Nullwertausgabe

Legt die Zeichenfolgendarstellung eines Nullwerts in den exportierten Dateien fest.

Beispielausgabe mit **[!UICONTROL null]** selected: `male,NULL,TestLastName`
Beispielausgabe mit **&quot;&quot;** selected: `male,"",TestLastName`
Beispielausgabe mit **[!UICONTROL Leere Zeichenfolge]** selected: `male,,TestLastName`

### Komprimierungsformat

Legt fest, welcher Komprimierungscodec beim Speichern von Daten in einer Datei verwendet werden soll. Unterstützt werden GZIP und KEINE.

### Codierung

*Nicht im UI-Screenshot angezeigt*. Gibt die Kodierung (Zeichensatz) gespeicherter CSV-Dateien an. Die Optionen sind UTF-8 oder UTF-16.

### Char to Escape Anführungszeichen

*Nicht im UI-Screenshot angezeigt*. Eine Markierung, die angibt, ob Werte, die Anführungszeichen enthalten, immer in Anführungszeichen gesetzt werden sollen.

Standardmäßig werden alle Werte mit Escape-Zeichen versehen, die ein Anführungszeichen enthalten.

### Zeilenabstand

*Nicht im UI-Screenshot angezeigt*. Definiert das Zeilentrennzeichen, das zum Schreiben verwendet werden soll. Die maximale Länge beträgt 1 Zeichen.

### Leere Leerzeichen ignorieren

*Nicht im UI-Screenshot angezeigt*. Eine Markierung, die angibt, ob vorangestellte Leerzeichen aus den zu exportierenden Werten übersprungen werden sollen.

Beispielausgabe mit **[!UICONTROL True]** selected: `"male","John","TestLastName"`
Beispielausgabe mit **[!UICONTROL False]** selected: `" male","John","TestLastName"`

### Leerzeichen am Ende ignorieren

Nicht im Screenshot der Benutzeroberfläche angezeigt. Eine Markierung, die angibt, ob nachfolgende Leerzeichen aus den zu exportierenden Werten übersprungen werden sollen.

Beispielausgabe mit **[!UICONTROL True]** selected: `"male","John","TestLastName"`
Beispielausgabe mit **[!UICONTROL False]** selected: `"male ","John","TestLastName"`

### Nächste Schritte {#next-steps}

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie Dateiexportoptionen für Ihre CSV-Datendateien konfigurieren können, um den Dateiinhalt an die Anforderungen Ihres nachgelagerten Dateiempfangssystems anzupassen. Als Nächstes können Sie die [Tutorial zur Aktivierung dateibasierter Ziele](/help/destinations/ui/activate-batch-profile-destinations.md) , um mit dem Export von Dateien an Ihren bevorzugten Cloud-Speicher zu beginnen.
