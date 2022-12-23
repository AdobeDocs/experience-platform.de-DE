---
description: Erfahren Sie, wie Sie beim Aktivieren von Daten für dateibasierte Ziele Dateiformatierungsoptionen konfigurieren
title: (Beta) Konfigurieren von Dateiformatierungsoptionen für dateibasierte Ziele
exl-id: f59b1952-e317-40ba-81d1-35535e132a72
source-git-commit: a9887535b12b8c4aeb39bb5a6646da88db4f0308
workflow-type: ht
source-wordcount: '565'
ht-degree: 100%

---

# (Beta) Konfigurieren von Dateiformatierungsoptionen für dateibasierte Ziele

>[!IMPORTANT]
>
>Die Funktionalität **[!UICONTROL Dateiformatierungsoptionen]** in Adobe Experience Platform ist derzeit als Beta-Version verfügbar. Dokumentation und Funktionalitäten können sich ändern.
>Wenden Sie sich an den Adobe-Support-Mitarbeiter, um Zugriff auf diese Funktion zu erhalten.
> 
>Die in diesem Dokument beschriebenen Dateiformatierungsoptionen sind derzeit nur für CSV-Dateien verfügbar.

Die Option zur Konfiguration verschiedener Dateiformatierungsoptionen für die exportierten Dateien ist verfügbar, wenn Sie eine [Verbindung](/help/destinations/ui/connect-destination.md) mit einem dateibasierten Ziel herstellen, z. B. [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md#connect), [Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md#connect) oder [SFTP](/help/destinations/catalog/cloud-storage/sftp.md#connect).

Mithilfe der Experience Platform-Benutzeroberfläche können Sie verschiedene Dateiformatierungsoptionen für exportierte Dateien konfigurieren. Sie können verschiedene Eigenschaften der exportierten Dateien an die Anforderungen des Dateiempfangssystems auf Ihrer Seite anpassen, um die aus Experience Platform empfangenen Dateien optimal zu lesen und zu interpretieren.

<!--
* To configure file formatting options for exported files by using the Experience Platform UI, read this document.
* To configure file formatting options for exported files by using the Experience Platform Flow Service API, read [Flow Service API - Destinations](https://developer.adobe.com/experience-platform-apis/references/destinations/).
-->

## Konfiguration der Dateiformatierung {#file-configuration}

>[!IMPORTANT]
>
>Für das Ziel, mit dem Sie eine Verbindung herstellen, stehen möglicherweise nicht alle diese Optionen zur Verfügung. Der Zielentwickler kann bestimmen, welche Dateiformatierungsoptionen am Ziel unterstützt werden sollen. Der Zielentwickler kann bestimmen, welche Optionen beim Herstellen einer Verbindung mit dem Ziel verfügbar sind. Erforderliche Optionen sind in der Experience Platform-Benutzeroberfläche mit einem Sternchen gekennzeichnet.

Um die Dateiformatierungsoptionen anzuzeigen, starten Sie den Workflow [Mit Ziel verbinden](/help/destinations/ui/connect-destination.md) und wählen Sie Segmente als **Dateityp** aus. In diesem Abschnitt werden die Dateiformatierungseinstellungen beschrieben, die für exportierte `CSV`-Dateien verfügbar sind.

![Abbildung mit einigen der verfügbaren Dateiformatierungsoptionen.](/help/destinations/assets/ui/batch-destinations-file-formatting-options/file-formatting-options.png)

### Trennzeichen

Legt für jedes Feld und jeden Wert ein Trennzeichen fest. Beispiel: `,` für kommagetrennte Werte oder `/t` für tabulatorgetrennte Werte.

### Anführungszeichen

Legt ein einzelnes Zeichen fest, das zum Maskieren von angegebenen Werten verwendet wird, wobei das Trennzeichen Teil des Werts sein kann.

### Escape-Zeichen

Legt ein einzelnes Zeichen fest, das zum Maskieren von Anführungszeichen verwendet wird, die innerhalb eines bereits mit Anführungszeichen versehenen Werts liegen.

### Ausgabe leerer Werte

Legt die Zeichenfolgendarstellung eines leeren Werts fest.

### Ausgabe von Nullwerten

Legt die Zeichenfolgendarstellung eines Nullwerts in den exportierten Dateien fest.

Beispielausgabe mit **[!UICONTROL null]** ausgewählt: `male,NULL,TestLastName`
Beispielausgabe mit **&quot;&quot;** ausgewählt: `male,"",TestLastName`
Beispielausgabe mit **[!UICONTROL Leere Zeichenfolge]** ausgewählt: `male,,TestLastName`

### Komprimierungsformat

Legt den Komprimierungs-Codec zum Speichern von Daten in einer Datei fest. Unterstützte Optionen sind GZIP und KEINE.

### Codierung

*Nicht im Screenshot der Benutzeroberfläche dargestellt*. Gibt die Codierung (Zeichensatz) gespeicherter CSV-Dateien an. Die Optionen sind UTF-8 oder UTF-16.

### Escape-Zeichen für Anführungszeichen

*Nicht im Screenshot der Benutzeroberfläche dargestellt*. Eine Markierung, das angibt, ob Werte, die Anführungszeichen enthalten, immer in Anführungszeichen gesetzt werden sollen.

Standardmäßig werden alle Werte mit Escape-Zeichen versehen, die ein Anführungszeichen enthalten.

### Zeilentrennzeichen

*Nicht im Screenshot der Benutzeroberfläche dargestellt*. Definiert das Zeilentrennzeichen, das zum Schreiben verwendet werden soll. Die maximale Länge beträgt 1 Zeichen.

### Vorangestellte Leerzeichen ignorieren

*Nicht im Screenshot der Benutzeroberfläche dargestellt*. Eine Markierung, die angibt, ob vorangestellte Leerzeichen in den zu exportierenden Werten ignoriert werden sollen.

Beispielausgabe mit **[!UICONTROL True]** ausgewählt: `"male","John","TestLastName"`
Beispielausgabe mit **[!UICONTROL False]** ausgewählt: `" male","John","TestLastName"`

### Nachfolgende Leerzeichen ignorieren

Nicht im Screenshot der Benutzeroberfläche dargestellt. Eine Markierung, die angibt, ob nachfolgende Leerzeichen in den zu exportierenden Werten ignoriert werden sollen.

Beispielausgabe mit **[!UICONTROL True]** ausgewählt: `"male","John","TestLastName"`
Beispielausgabe mit **[!UICONTROL False]** ausgewählt: `"male ","John","TestLastName"`

### Nächste Schritte {#next-steps}

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie Dateiexportoptionen für Ihre CSV-Datendateien konfigurieren können, um Dateiinhalte an die Anforderungen Ihres nachgelagerten Dateiempfangssystems anzupassen. Als Nächstes können Sie das [Tutorial zur Aktivierung dateibasierter Ziele](/help/destinations/ui/activate-batch-profile-destinations.md) lesen, um mit dem Export von Dateien in Ihren bevorzugten Cloud-Speicher zu beginnen.
