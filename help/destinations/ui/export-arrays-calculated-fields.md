---
title: Exportieren von Arrays, Zuordnungen und Objekten aus Real-Time CDP in Cloud-Speicher-Ziele
type: Tutorial
description: Erfahren Sie, wie Sie Arrays, Zuordnungen und Objekte aus Real-Time CDP in Cloud-Speicher-Ziele exportieren.
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: 6122ddc078101c26061e8662de3fcdcb1cb65992
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 7%

---

# Exportieren von Arrays, Zuordnungen und Objekten aus Real-Time CDP in Cloud-Speicher-Ziele {#export-arrays-cloud-storage}

>[!AVAILABILITY]
>
>Die Funktion zum Exportieren von Arrays in Cloud-Speicher-Ziele ist allgemein für die folgenden Ziele verfügbar: [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md), [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md), [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md), [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md), [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md), [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md),

Erfahren Sie, wie Sie Arrays aus Real-Time CDP in [Cloud-Speicherziele](/help/destinations/catalog/cloud-storage/overview.md) exportieren. Lesen Sie dieses Dokument, um den Export-Workflow, die durch diese Funktion aktivierten Anwendungsfälle und die bekannten Einschränkungen zu verstehen.

Auf dieser Seite finden Sie alle Informationen zum Exportieren von Arrays, Karten und anderen Objekttypen aus Experience Platform.

## Grundlinie vorne

Die wichtigsten Informationen zur Funktionalität finden Sie in diesem Abschnitt und weiter unten in den anderen Abschnitten des Dokuments, um detaillierte Informationen zu erhalten.

* Die Fähigkeit zum Exportieren von Arrays, Zuordnungen und Objekten hängt von Ihrer Auswahl des Umschalters **Exportieren von Arrays, Zuordnungen,**) ab. Lesen Sie mehr darüber [weiter unten auf der Seite](#export-arrays-maps-objects-toggle).
* Sie können Arrays, Zuordnungen und Objekte nur in `JSON`- und `Parquet`-Dateien in Cloud-Speicher-Ziele exportieren. Personen und Zielgruppen potenzieller Kunden werden unterstützt, Konto-Zielgruppen jedoch nicht.
* Sie *können* Arrays, Zuordnungen und Objekte in CSV-Dateien exportieren, jedoch nur mithilfe der Funktion „Berechnete Felder“ und indem Sie sie mithilfe der Funktion &quot;`array_to_string`&quot; zu einer Zeichenfolge verketten.

## Arrays und andere Objekttypen in Platform {#arrays-strings-other-objects}

In Experience Platform können Sie [XDM-Schemata](/help/xdm/home.md) verwenden, um verschiedene Feldtypen zu verwalten. Bevor die Unterstützung für Array-Exporte hinzugefügt wurde, konnten Sie einfache Schlüssel-Wert-Paarfelder wie Zeichenfolgen aus Experience Platform an Ihre gewünschten Ziele exportieren. Ein Beispiel für ein solches Feld, das zuvor für den Export unterstützt wurde, ist `personalEmail.address`:`johndoe@acme.org`.

Andere Feldtypen in Experience Platform umfassen Array-Felder. Lesen Sie mehr über [Verwalten von Array-Feldern in der Experience Platform-Benutzeroberfläche](/help/xdm/ui/fields/array.md). Sie können jetzt Array-Objekte wie im folgenden Beispiel exportieren.

```
organizations = [{
  id: 123,
  orgName: "Acme Inc",
  founded: 1990,
  latestInteraction: "2024-02-16"
}, {
  id: 456,
  orgName: "Superstar Inc",
  founded: 2004,
  latestInteraction: "2023-08-25"
}, {
  id: 789,
  orgName: 'Energy Corp',
  founded: 2021,
  latestInteraction: "2024-09-08"
}]
```

Siehe weiter unten [ausführliche Beispiele](#examples) wie Sie verschiedene Funktionen verwenden können, um auf Elemente von Arrays zuzugreifen, Arrays umzuwandeln und zu filtern, Array-Elemente in eine Zeichenfolge zu verknüpfen und vieles mehr.

Zusätzlich zu Arrays können Sie auch Zuordnungen und Objekte aus Experience Platform in Ihr gewünschtes Cloud-Speicher-Ziel exportieren. Lesen Sie mehr über [Karten](/help/xdm/ui/fields/map.md) und [Objekte](/help/xdm/ui/fields/object.md) in Experience Platform.

## Voraussetzungen {#prerequisites}

[Verbinden](/help/destinations/ui/connect-destination.md) mit dem gewünschten Cloud-Speicher-Ziel, schreiten Sie durch die [Aktivierungsschritte für Cloud-Speicher-Ziele](/help/destinations/ui/activate-batch-profile-destinations.md) und gelangen Sie zum Schritt [Zuordnung](/help/destinations/ui/activate-batch-profile-destinations.md#mapping). Beim Herstellen einer Verbindung zum gewünschten Cloud-Ziel müssen Sie den Umschalter **[!UICONTROL Arrays exportieren, Karten, Objekte]**. Weitere Informationen finden Sie im folgenden Abschnitt.

## Exportieren von Arrays, Karten, Objekten umschalten {#export-arrays-maps-objects-toggle}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_maps_objects"
>title="Exportieren von Arrays, Zuordnungen und Objekten"
>abstract="<p> Schalten Sie diese Einstellung auf <b>ein</b>, um den Export von Arrays, Zuordnungen und Objekten in JSON- oder Parquet-Dateien zu aktivieren. Sie können diese Objekttypen in der Ansicht Quellfeld des Zuordnungsschritts auswählen. Wenn der Umschalter aktiviert ist, können Sie die Option Berechnete Felder im Zuordnungsschritt nicht verwenden.</p><p>Mit diesem Umschalter <b>Aus</b> können Sie die Option Berechnete Felder verwenden und beim Aktivieren von Zielgruppen verschiedene Datenumwandlungsfunktionen anwenden. Allerdings können Sie Arrays, Zuordnungen und Objekte <i>nicht</i> in JSON- oder Parquet-Dateien exportieren, sondern müssen dafür ein separates Ziel konfigurieren.</p>"

Beim Herstellen einer Verbindung zu einem Cloud-Speicher-Ziel können Sie die **[!UICONTROL Exportieren von Arrays, Karten, Objekten]** ein- oder ausschalten.

![Exportieren Sie Arrays, Karten, Objekte ein- oder ausschalten und markieren Sie das Pop-up.](/help/destinations/assets/ui/export-arrays-calculated-fields/export-objects-toggle.gif)

Schalten Sie diese Einstellung auf **ein**, um den Export von Arrays, Zuordnungen und Objekten in JSON- oder Parquet-Dateien zu aktivieren. Sie können diese Objekttypen in der Ansicht der Quellfelder des [Zuordnungsschritts“ auswählen, ](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) Sie Zielgruppen für Cloud-Speicher-Ziele aktivieren. Wenn diese Einstellung jedoch aktiviert ist, können Sie die Option „Berechnete Felder“ nicht verwenden, um Daten bei Aktivierung umzuwandeln.

Mit diesem Umschalter **Aus** können Sie die Option Berechnete Felder verwenden und beim Aktivieren von Zielgruppen verschiedene Datenumwandlungsfunktionen anwenden. Sie können jedoch keine Arrays, Zuordnungen und Objekte in JSON- oder Parquet-Dateien exportieren und müssen dafür ein separates Ziel konfigurieren.

## Arrays, Karten, Objekte exportieren *ein* {#export-arrays-maps-objects-toggle-on}

Wenn diese Einstellung aktiviert ist, können Sie ganze Objekte (z. B. `person.name`) und Arrays exportieren, indem Sie sie im Zuordnungsschritt des Aktivierungs-Workflows über die Quellfeldauswahl auswählen.

![Wählen Sie Objekte über die Quellfeldauswahl im Zuordnungsschritt des Aktivierungs-Workflows aus.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-object.gif)

Wenn diese Option aktiviert ist, verhindert die Benutzeroberfläche, dass Benutzer berechnete Felder verwenden, und das Steuerelement **[!UICONTROL Berechnete Felder hinzufügen]** ist deaktiviert, wie unten dargestellt. Um berechnete Felder für Datenumwandlungen zu verwenden, richten Sie eine Zielverbindung ein, während Sie den Umschalter deaktivieren.

![Steuerung der berechneten Felder deaktiviert.](/help/destinations/assets/ui/export-arrays-calculated-fields/calculated-fields-disabled.png)

## Arrays, Karten, Objekte exportieren *aus* {#export-arrays-maps-objects-toggle-off}

Wenn diese Option auf *Aus* gesetzt ist, können Sie die Option Berechnete Felder verwenden und beim Aktivieren von Zielgruppen verschiedene Datenumwandlungsfunktionen anwenden. Sie können jedoch keine Arrays, Zuordnungen und Objekte in JSON- oder Parquet-Dateien exportieren und müssen dafür ein separates Ziel konfigurieren.

Sie *können* Arrays, Zuordnungen und Objekte mithilfe der Funktion „Berechnete Felder“ in CSV-Dateien exportieren und mithilfe der Funktion &quot;`array_to_string`&quot; zu einer Zeichenfolge verketten. [Weitere Informationen ](#array-to-string-function-export-arrays) Verwendung dieser Funktion.

Erfahren Sie mehr über die Arbeit mit berechneten Feldern, um [Umwandlungen an Daten durchzuführen, die an Cloud-Speicherziele exportiert wurden](/help/destinations/ui/data-transformations-calculated-fields.md).

## Beispiele für exportierte Dateien {#sample-exported-files}

Mithilfe dieser Funktion können Sie Parquet- und JSON-Dateien exportieren, wobei die Daten die Struktur aus Experience Platform beibehalten. Nachfolgend finden Sie ein Beispiel für eine exportierte JSON-Datei.

+++ Wählen Sie aus, um die exportierte JSON-Datei anzuzeigen.

```json
{
  "person_name_firstName": "John",
  "person_name_lastName": "Smith",
  "_acmeinc_customer_hs_main_address_scalar": "Oak Avenue No 12",
  "_acmeinc_customer_hs_locations_array": [
    "home address 12",
    "office address 12"
  ],
  "_acmeinc_customer_hs_date_array": [
    "2024-11-14",
    "2024-11-15"
  ],
  "_acmeinc_customer_hs_customer_obj_emails_array0": "john.smith@example.com",
  "_acmeinc_customer_hs_customer_obj": {
    "emails_array": [
      "john.smith@example.com",
      "j.smith@example.com"
    ],
    "name_scalar": "John Smith"
  },
  "_acmeinc_customer_hs_addresses_array_obj": [
    {
      "is_primary": true,
      "streetName_scalar": "Maple Street",
      "streetNo_int": 12
    },
    {
      "is_primary": false,
      "streetName_scalar": "Pine Road",
      "streetNo_int": 45
    }
  ],
  "_acmeinc_customer_hs_addresses_array_obj0": {
    "is_primary": true,
    "streetName_scalar": "Maple Street",
    "streetNo_int": 12
  }
}
```

+++