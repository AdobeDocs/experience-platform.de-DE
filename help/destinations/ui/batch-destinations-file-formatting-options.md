---
description: Erfahren Sie, wie Sie beim Aktivieren von Daten für dateibasierte Ziele Dateiformatierungsoptionen konfigurieren
title: Konfigurieren von Dateiformatierungsoptionen für dateibasierte Ziele
exl-id: f59b1952-e317-40ba-81d1-35535e132a72
source-git-commit: 4dd6e8685ff5cc61342b20e971216416918b95da
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 48%

---

# Konfigurieren von Dateiformatierungsoptionen für dateibasierte Ziele

>[!IMPORTANT]
> 
>Die in diesem Dokument beschriebenen Dateiformatierungsoptionen sind derzeit nur für CSV-Dateien verfügbar.

Die Option zur Konfiguration verschiedener Dateiformatierungsoptionen für die exportierten Dateien ist verfügbar, wenn Sie eine [Verbindung](/help/destinations/ui/connect-destination.md) mit einem dateibasierten Ziel herstellen, z. B. [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md#connect), [Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md#connect) oder [SFTP](/help/destinations/catalog/cloud-storage/sftp.md#connect).

Mithilfe der Experience Platform-Benutzeroberfläche können Sie verschiedene Dateiformatierungsoptionen für exportierte Dateien konfigurieren. Sie können verschiedene Eigenschaften der exportierten Dateien an die Anforderungen des Dateiempfangssystems auf Ihrer Seite anpassen, um die aus Experience Platform empfangenen Dateien optimal zu lesen und zu interpretieren.

<!--
* To configure file formatting options for exported files by using the Experience Platform UI, read this document.
* To configure file formatting options for exported files by using the Experience Platform Flow Service API, read [Flow Service API - Destinations](https://developer.adobe.com/experience-platform-apis/references/destinations/).
-->

## Dateiformatierungskonfiguration für CSV-Dateien {#file-configuration}

Um die Dateiformatierungsoptionen anzuzeigen, starten Sie den Workflow [Mit Ziel verbinden](/help/destinations/ui/connect-destination.md). Wählen Sie **Datentyp: Segmente** und **Dateityp: CSV** aus, um die Dateiformatierungseinstellungen anzuzeigen, die für die exportierten `CSV`-Dateien verfügbar sind.

>[!IMPORTANT]
>
>Für das Ziel, mit dem Sie eine Verbindung herstellen, stehen möglicherweise nicht alle diese Optionen zur Verfügung. Der Zielentwickler kann bestimmen, welche Dateiformatierungsoptionen am Ziel unterstützt werden sollen. Der Zielentwickler kann bestimmen, welche Optionen beim Herstellen einer Verbindung mit dem Ziel verfügbar sind. Erforderliche Optionen sind in der Experience Platform-Benutzeroberfläche mit einem Sternchen gekennzeichnet.
> 
>Die von Adobe erstellten Cloud-Speicher-Ziele - [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [Data Landing Zone](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [Google Cloud Storage](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [SFTP](/help/destinations/catalog/cloud-storage/sftp.md) - unterstützen derzeit nur die sechs unten hervorgehobenen CSV-Optionen.

![Abbildung mit einigen der verfügbaren Dateiformatierungsoptionen.](../assets/ui/batch-destinations-file-formatting-options/file-formatting-options.png)

### Trennzeichen {#delimiter}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_delimiter"
>title="Trennzeichen"
>abstract="Verwenden Sie dieses Steuerelement, um ein Trennzeichen für jedes Feld und jeden Wert festzulegen. In der Dokumentation finden Sie Beispiele für jede Auswahl."

Verwenden Sie dieses Steuerelement, um ein Trennzeichen für jedes Feld und jeden Wert in den exportierten CSV-Dateien festzulegen. Verfügbare Optionen sind:

* `(:)`
* `(,)`
* `(|)`
* `(;)`
* `(\t)`

#### Beispiele

Sehen Sie sich die folgenden Beispiele für den Inhalt in den exportierten CSV-Dateien mit jeder Auswahl in der Benutzeroberfläche an.

* Beispielausgabe mit **[!UICONTROL Doppelpunkt`(:)`]** ausgewählt: `male:John:Doe`
* Beispielausgabe mit **[!UICONTROL Komma`(,)`]** ausgewählt: `male,John,Doe`
* Beispielausgabe mit **[!UICONTROL Pipe`(|)`]** ausgewählt: `male|John|Doe`
* Beispielausgabe mit **[!UICONTROL Semikolon`(;)`]** ausgewählt: `male;John;Doe`
* Beispielausgabe mit **[!UICONTROL Registerkarte`(\t)`]** ausgewählt: `male \t John \t Doe`

### Anführungszeichen {#quote-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_quoteCharacter"
>title="Anführungszeichen"
>abstract="Verwenden Sie diese Option, wenn Sie doppelte Anführungszeichen aus exportierten Zeichenfolgen entfernen möchten. In der Dokumentation finden Sie Beispiele für jede Auswahl."

Verwenden Sie diese Option, um zu steuern, ob doppelte Anführungszeichen entfernt oder in exportierten Zeichenfolgen beibehalten werden sollen.

Folgende Optionen sind verfügbar:

* **[!UICONTROL NULL (\0000)]**. Verwenden Sie diese Option, um doppelte Anführungszeichen aus exportierten CSV-Dateien zu entfernen.
* **[!UICONTROL Anführungszeichen („)]**. Verwenden Sie diese Option, wenn die Zeichenfolgenwerte ein Trennzeichen oder doppelte Anführungszeichen enthalten. Mit dieser Option können Sie die Trennzeichen oder doppelten Anführungszeichen in Ihren exportierten CSV-Dateien beibehalten, sodass Sie korrekt identifizieren können, welcher Wert welchem Feld entspricht.

#### Beispiele

Betrachten Sie den Eingabewert `Anna,"Doe,John"`.

Sehen Sie sich die folgenden Beispiele für den Inhalt aus exportierten CSV-Dateien mit jeder Auswahl in der Benutzeroberfläche an.

* Beispielausgabe mit **[!UICONTROL Null-Zeichen (\0000)]** ausgewählt: `Anna,Doe,John`
* Beispielausgabe mit **[!UICONTROL doppelten Anführungszeichen („)]** ausgewählt: `Anna,"Doe,John"`

### Escape-Zeichen {#escape-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_escapeCharacter"
>title="Escape-Zeichen"
>abstract="Legt ein einzelnes Zeichen fest, das zum Maskieren von Anführungszeichen verwendet wird, die innerhalb eines bereits mit Anführungszeichen versehenen Werts liegen. In der Dokumentation finden Sie Beispiele für jede Auswahl."

Verwenden Sie diese Option, um ein einzelnes Zeichen zum Maskieren von Anführungszeichen in einem bereits angegebenen Wert festzulegen. Diese Option ist beispielsweise nützlich, wenn eine Zeichenfolge in doppelte Anführungszeichen gesetzt wird, wobei ein Teil der Zeichenfolge bereits in doppelte Anführungszeichen gesetzt wird. Diese Option bestimmt, welches Zeichen die inneren doppelten Anführungszeichen ersetzen soll. Verfügbare Optionen sind:

* Schrägstrich `(\)`
* Einfaches Anführungszeichen `(')`

#### Beispiele

Sehen Sie sich die folgenden Beispiele für den Inhalt aus exportierten CSV-Dateien mit jeder Auswahl in der Benutzeroberfläche an.

* Beispielausgabe mit **[!UICONTROL Zurück-Schrägstrich`(\)`]**: `"Test,\"John\",LastName"`
* Beispielausgabe mit &quot;**[!UICONTROL Anführungszeichen`(')`]** ausgewählt: `"Test,'"John'",LastName"`

### Ausgabe leerer Werte {#empty-value-output}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_emptyValueOutput"
>title="Ausgabe leerer Werte"
>abstract="Verwenden Sie diese Option, um festzulegen, wie leere Werte in den exportierten CSV-Dateien dargestellt werden sollen. In der Dokumentation finden Sie Beispiele für jede Auswahl."

Verwenden Sie dieses Steuerelement, um die Zeichenfolgendarstellung eines leeren Werts festzulegen. Diese Option bestimmt, wie leere Werte in Ihren exportierten CSV-Dateien dargestellt werden. Verfügbare Optionen sind:

* **[!UICONTROL Null (null)]**
* **Leere Zeichenfolge in doppelten Anführungszeichen (“„)**
* **[!UICONTROL Leere Zeichenfolge]**

#### Beispiele

Sehen Sie sich die folgenden Beispiele für den Inhalt aus exportierten CSV-Dateien mit jeder Auswahl in der Benutzeroberfläche an.

* Beispielausgabe mit **[!UICONTROL null]** ausgewählt: `male,NULL,TestLastName`. In diesem Fall wandelt Experience Platform den leeren Wert in einen Nullwert um.
* Beispielausgabe mit **&quot;&quot;** ausgewählt: `male,"",TestLastName`. In diesem Fall wandelt Experience Platform den leeren Wert in ein Paar doppelter Anführungszeichen um.
* Beispielausgabe mit **[!UICONTROL Leere]**: `male,,TestLastName`. In diesem Fall behält die Experience Platform den leeren Wert bei und exportiert ihn unverändert (ohne doppelte Anführungszeichen).

>[!TIP]
>
>Der Unterschied zwischen der Ausgabe eines leeren Werts und der Ausgabe eines Nullwerts im folgenden Abschnitt besteht darin, dass ein leerer Wert einen tatsächlichen Wert hat, der leer ist. Der NULL-Wert hat überhaupt keinen Wert. Stellen Sie sich vor, dass der leere Wert ein leeres Glas auf der Tabelle und der Null-Wert überhaupt kein Glas auf der Tabelle hat.

### Ausgabe von Nullwerten {#null-value-output}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_nullValueOutput"
>title="Ausgabe von Nullwerten"
>abstract="Verwenden Sie dieses Steuerelement, um die Zeichenfolgendarstellung eines Nullwerts in den exportierten Dateien festzulegen. In der Dokumentation finden Sie Beispiele für jede Auswahl."

Verwenden Sie dieses Steuerelement, um die Zeichenfolgendarstellung eines Nullwerts in den exportierten Dateien festzulegen. Diese Option bestimmt, wie Nullwerte in Ihren exportierten CSV-Dateien dargestellt werden. Verfügbare Optionen sind:

* **[!UICONTROL Null (null)]**
* **Leere Zeichenfolge in doppelten Anführungszeichen (“„)**
* **[!UICONTROL Leere Zeichenfolge]**

#### Beispiele

Sehen Sie sich die folgenden Beispiele für den Inhalt aus exportierten CSV-Dateien mit jeder Auswahl in der Benutzeroberfläche an.

* Beispielausgabe mit **[!UICONTROL null]** ausgewählt: `male,NULL,TestLastName`. In diesem Fall findet keine Umwandlung statt und die CSV-Datei enthält den Nullwert.
* Beispielausgabe mit **&quot;&quot;** ausgewählt: `male,"",TestLastName`. In diesem Fall ersetzt Experience Platform den Nullwert durch doppelte Anführungszeichen um eine leere Zeichenfolge.
* Beispielausgabe mit **[!UICONTROL Leere]**: `male,,TestLastName`. In diesem Fall ersetzt Experience Platform den Nullwert durch eine leere Zeichenfolge (ohne doppelte Anführungszeichen).

### Komprimierungsformat {#compression-format}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_compressionFormat"
>title="Komprimierungsformat"
>abstract="Legt den Komprimierungstyp zum Speichern von Daten in einer Datei fest. Unterstützte Optionen sind GZIP und KEINE. In der Dokumentation finden Sie Beispiele für jede Auswahl."

Legt den Komprimierungstyp zum Speichern von Daten in einer Datei fest. Unterstützte Optionen sind GZIP und KEINE. Diese Option bestimmt, ob komprimierte Dateien exportiert werden.

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
