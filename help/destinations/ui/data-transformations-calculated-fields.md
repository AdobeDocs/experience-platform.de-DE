---
title: Durchführen von Umwandlungen an Daten, die mithilfe berechneter Felder in Cloud-Speicher-Ziele exportiert wurden
type: Tutorial
description: Erfahren Sie, wie Sie mit der Funktion „Berechnete Felder“ Umwandlungen an Daten durchführen können, die an Cloud-Speicherziele exportiert wurden
exl-id: 1e14f964-4c03-4d0c-be8d-c3dcb48a335a
source-git-commit: 14c672ef57e0b0247020075552c782ed18db8484
workflow-type: tm+mt
source-wordcount: '1595'
ht-degree: 3%

---

# Durchführen von Umwandlungen an Daten, die mithilfe berechneter Felder in Cloud-Speicher-Ziele exportiert wurden {#data-transformation-calculated-fields}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="Hinzufügen von berechneten Feldern"
>abstract="<p>Verwenden Sie das Steuerelement **Berechnetes Feld hinzufügen**, um verschiedene Datenumwandlungen von Daten durchzuführen, die an Cloud-Speicherziele exportiert wurden. Sie können beispielsweise Hashing auf Daten anwenden, Arrays zu Zeichenfolgen verketten und vieles mehr."

<!--

disable additional URLs for a while

>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-maps-objects.html#examples" text="Examples"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-maps-objects.html#known-limitations" text="Known limitations"

-->

>[!AVAILABILITY]
>
>Die Funktion zum Ausführen von Umwandlungen an Daten, die in Cloud-Speicher-Ziele exportiert wurden, ist allgemein für die folgenden Ziele verfügbar: [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md), [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md), [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md), [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md), [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md), [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md) sowie für alle benutzerdefinierten von Partnern erstellten Cloud-Speicher-Ziele, die über [Destination SDK](/help/destinations/destination-sdk/overview.md) erstellt wurden.

Um verschiedene Umwandlungen an Daten durchzuführen, die in Cloud-Speicher-Ziele exportiert wurden, müssen Sie die Funktion „Berechnete Felder“ im Zuordnungsschritt des Export-Workflows verwenden. Ausführliche Informationen zu berechneten Feldern finden Sie auf den unten verlinkten Seiten. Diese Seiten enthalten eine Einführung in berechnete Felder in die Datenvorbereitung und weitere Informationen zu allen verfügbaren Funktionen:

* [Handbuch zur Benutzeroberfläche und Übersicht](/help/data-prep/ui/mapping.md#calculated-fields)
* [Funktionen zur Datenvorbereitung](/help/data-prep/functions.md)

## Voraussetzungen {#prerequisites}

So verwenden Sie berechnete Felder für Datenumwandlungen:

1. [Verbinden](/help/destinations/ui/connect-destination.md) mit einem gewünschten Cloud-Speicher-Ziel. Wenn Sie eine Verbindung zum gewünschten Cloud-Ziel herstellen, schalten Sie die Option **[!UICONTROL Arrays, Karten, Objekte exportieren]** [aus](/help/destinations/ui/export-arrays-maps-objects.md##export-arrays-maps-objects-toggle).
2. Führen Sie die [Aktivierungsschritte für Cloud-Speicher](/help/destinations/ui/activate-batch-profile-destinations.md)Ziele aus und gelangen Sie zum Schritt [Zuordnung](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).

## Arbeiten mit berechneten Feldern {#how-to-export-calculated-fields}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_control"
>title="Aktivieren des hierarchischen Ausgabeschemas"
>abstract="Schalten Sie diese Einstellung ein, um den Export von Arrays, Zuordnungen und Objekten in JSON- oder Parquet-Dateien zu aktivieren."

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_calculated_field_disabled"
>title="„Berechnete Felder hinzufügen“ ist deaktiviert"
>abstract="Dieses Steuerelement ist deaktiviert, weil Sie beim Einrichten dieser Zielverbindung den Umschalter zum **Exportieren von Arrays, Zuordnungen und Objekten** auf *ein* geschaltet haben. Um berechnete Felder und die darin verfügbaren Funktionen zu verwenden, richten Sie eine neue Zielverbindung ein, bei der der Umschalter zum **Exportieren von Arrays, Zuordnungen und Objekten** auf *aus* geschaltet ist."

Wählen Sie im Zuordnungsschritt des Aktivierungs-Workflows für Cloud-Speicher-Ziele **[!UICONTROL Berechnetes Feld hinzufügen]** aus.

>[!TIP]
>
>Das **[!UICONTROL Berechnetes Feld hinzufügen]**-Steuerelement ist für Zielverbindungen deaktiviert, bei denen das **[!UICONTROL Exportieren von Arrays, Zuordnungen und]**&quot; deaktiviert wurde. [Weitere Informationen](/help/destinations/ui/export-arrays-maps-objects.md#export-arrays-maps-objects-toggle).

![Berechnetes Feld hinzufügen, das im Zuordnungsschritt des Batch-Aktivierungs-Workflows hervorgehoben ist.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

Dadurch wird ein modales Fenster geöffnet, in dem Sie Funktionen und Felder auswählen können, um Attribute aus Experience Platform zu exportieren.

![Modales Fenster der berechneten Feldfunktionalität, bei dem noch keine Funktion ausgewählt ist.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

Verwenden Sie beispielsweise die Funktion `array_to_string` im Feld `organizations` wie unten gezeigt, um das Organisations-Array als Zeichenfolge in eine CSV-Datei zu exportieren. Sehen Sie [weitere Informationen hierzu und weitere Beispiele weiter unten](#array-to-string-function-export-arrays).

![Modales Fenster der berechneten Feldfunktionalität mit ausgewählter Array-zu-String-Funktion.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

Wählen Sie **[!UICONTROL Speichern]** aus, um das berechnete Feld beizubehalten und zum Zuordnungsschritt zurückzukehren.

![Modales Fenster der berechneten Feldfunktion mit ausgewählter Array-zu-String-Funktion und hervorgehobenem Steuerelement „Speichern“.](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

Füllen Sie im Zuordnungsschritt des Workflows das Feld **[!UICONTROL Zielfeld]** mit dem Wert der Spaltenüberschrift aus, die Sie für dieses Feld in den exportierten Dateien anzeigen möchten.

![Zuordnungsschritt mit hervorgehobenem Zielfeld.](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![Zielfeld 2 auswählen](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

Wenn Sie bereit sind **[!UICONTROL wählen Sie]** Weiter) aus, um mit dem nächsten Schritt des Aktivierungs-Workflows fortzufahren.

![Zuordnungsschritt mit hervorgehobenem Zielfeld und ausgefülltem Zielwert.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## Beispiele für unterstützte Funktionen zum Ausführen von Datenumwandlungen {#supported-functions}

Alle dokumentierten [Datenvorbereitungsfunktionen](/help/data-prep/functions.md) werden beim Aktivieren von Daten für dateibasierte Ziele unterstützt.

Die folgenden Funktionen, die speziell für die Handhabung von Arrays oder das Anwenden von Hashing auf Felder gelten, werden zusammen mit Beispielen dokumentiert.

* `array_to_string`
* `flattenArray`
* `filterArray`
* `transformArray`
* `coalesce`
* `size_of`
* `iif`
* `index-based array access`
* `add_to_array`
* `to_array`
* `first`
* `last`

## Beispiele für Funktionen zur Durchführung von Datenumwandlungen {#examples}

In den folgenden Abschnitten finden Sie Beispiele und weitere Informationen zu einigen der oben aufgeführten Funktionen. Die übrigen aufgelisteten Funktionen finden Sie in der [Dokumentation zu allgemeinen Funktionen im Abschnitt Datenvorbereitung](/help/data-prep/functions.md).

### `array_to_string` Funktion zum Exportieren von Arrays {#array-to-string-function-export-arrays}

Verwenden Sie die Funktion `array_to_string` , um die Elemente eines Arrays mithilfe eines gewünschten Trennzeichens wie `_` oder `|` zu einer Zeichenfolge zu verketten. Diese Funktion ist nützlich, wenn Sie die Elemente eines Arrays aus Experience Platform in eine CSV-Datei exportieren möchten.

Sie können beispielsweise die folgenden XDM-Felder wie im Screenshot zur Zuordnung gezeigt unter Verwendung einer `array_to_string('_',organizations)` Syntax kombinieren:

* `organizations`
* `person.name.firstName`
* `person.name.lastName`
* `personalEmail.address`

![Zuordnungsbeispiel mit der Funktion array_to_string.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-array-to-string-function.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus: Beachten Sie, wie die Elemente des Arrays mithilfe des `_`-Zeichens zu einer einzigen Zeichenfolge verkettet werden.

```
First_Name,Last_Name,Personal_Email,Organization
John,Doe,johndoe@acme.org, "{'id':123,'orgName':'Acme Inc','founded':1990,'latestInteraction':1708041600000}_{'id':456,'orgName':'Superstar Inc','founded':2004,'latestInteraction':1692921600000}_{'id':789,'orgName':'Energy Corp','founded':2021,'latestInteraction':1725753600000}"
```

### `filterArray` Funktion zum Exportieren gefilterter Arrays {#filter-array}

Verwenden Sie die Funktion `filterArray` zum Filtern der Elemente eines exportierten Arrays. Sie können diese Funktion mit der weiter oben beschriebenen `array_to_string` kombinieren.

Wenn Sie mit dem `organizations` Array-Objekt von oben fortfahren, können Sie eine Funktion wie `array_to_string('_', filterArray(organizations, org -> org.founded > 2021))` schreiben, die die Organisationen mit einem Wert für `founded` im Jahr 2021 oder neuer zurückgibt.

![Beispiel für die filterArray-Funktion.](/help/destinations/assets/ui/export-arrays-calculated-fields/filter-array-function.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus: Beachten Sie, wie die beiden Elemente des Arrays, die das Kriterium erfüllen, mithilfe des `_`-Zeichens zu einer einzigen Zeichenfolge verkettet werden.

```
John,Doe,johndoe@acme.org, "{'id':123,'orgName':'Acme Inc','founded':1990,'latestInteraction':1708041600000}_{'id':789,'orgName':'Energy Corp','founded':2021,'latestInteraction':1725753600000}"
```

### `transformArray` Funktion zum Exportieren transformierter Arrays {#transform-array}

Verwenden Sie die Funktion `transformArray` , um die Elemente eines exportierten Arrays zu transformieren. Sie können diese Funktion mit der weiter oben beschriebenen `array_to_string` kombinieren.

Wenn Sie mit dem `organizations` Array-Objekt von oben fortfahren, können Sie eine Funktion wie `array_to_string('_', transformArray(organizations, org -> ucase(org.orgName)))` schreiben und die Namen der in Großbuchstaben konvertierten Organisationen zurückgeben.

![Beispiel für die Funktion „transformArray“](/help/destinations/assets/ui/export-arrays-calculated-fields/transform-array-function.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus: Beachten Sie, wie die drei Elemente des Arrays mithilfe des `_`-Zeichens transformiert und in eine einzelne Zeichenfolge verkettet werden.

```
John,Doe,johndoe@acme.org,ACME INC_SUPERSTAR INC_ENERGY CORP
```

### `iif` Funktion zum Exportieren von Arrays {#iif-function-export-arrays}

Verwenden Sie die Funktion `iif` , um Elemente eines Arrays unter bestimmten Bedingungen zu exportieren. Wenn Sie beispielsweise von oben mit dem `organizations` Array-Objekt fortfahren, können Sie eine einfache bedingte Funktion wie `iif(organizations[0].equals("Marketing"), "isMarketing", "isNotMarketing")` schreiben.

![Zuordnungsbeispiel mit der iif-Funktion.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-iif-function.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus: In diesem Fall ist das erste Element des Arrays Marketing , sodass die Person Mitglied der Marketing-Abteilung ist.

```
`First_Name,Last_Name, Personal_Email, Is_Member_Of_Marketing_Dept
John,Doe, johndoe@acme.org, "isMarketing"
```

### `add_to_array` Funktion zum Exportieren von Arrays {#add-to-array-function-export-arrays}

Verwenden Sie die Funktion `add_to_array` , um einem exportierten Array Elemente hinzuzufügen. Sie können diese Funktion mit der weiter oben beschriebenen `array_to_string` kombinieren.

Wenn Sie mit dem `organizations` Array-Objekt von oben fortfahren, können Sie eine Funktion wie `source: array_to_string('_', add_to_array(organizations,"2023"))` schreiben und die Organisationen zurückgeben, denen eine Person im Jahr 2023 angehört.

![Zuordnungsbeispiel einschließlich der Funktion „add_to_array“.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-add-to-array-function.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus: Beachten Sie, wie die drei Elemente des Arrays mithilfe des `_`-Zeichens zu einer einzigen Zeichenfolge verkettet werden und 2023 ebenfalls am Ende der Zeichenfolge angehängt wird.

```
`First_Name,Last_Name,Personal_Email,Organization_Member_2023
John,Doe, johndoe@acme.org,"Marketing_Sales_Finance_2023"
```

### `flattenArray` Funktion zum Exportieren von reduzierten Arrays {#flatten-array}

Verwenden Sie die Funktion `flattenArray` , um ein exportiertes multidimensionales Array zu reduzieren. Sie können diese Funktion mit der weiter oben beschriebenen `array_to_string` kombinieren.

Wenn Sie mit dem `organizations` Array-Objekt von oben fortfahren, können Sie eine Funktion wie `array_to_string('_', flattenArray(organizations))` schreiben. Beachten Sie, dass die Funktion `array_to_string` das Eingabe-Array standardmäßig in eine Zeichenfolge reduziert.

Die resultierende Ausgabe ist die gleiche wie für die weiter oben beschriebene `array_to_string`.

### `coalesce` Funktion zum Exportieren von Arrays {#coalesce-function-export-arrays}

Verwenden Sie die Funktion `coalesce` , um auf das erste Element eines Arrays, das nicht null ist, zuzugreifen und es in eine Zeichenfolge zu exportieren.

Sie können beispielsweise die folgenden XDM-Felder kombinieren, wie im Screenshot der Zuordnung gezeigt, indem Sie eine `coalesce(subscriptions.hasPromotion)` Syntax verwenden, um die erste `true` `false` Werts im Array zurückzugeben:

* `"subscriptions.hasPromotion": [null, true, null, false, true]`
* `person.name.firstName`
* `person.name.lastName`
* `personalEmail.address`

![Zuordnungsbeispiel mit der Zusammenführungsfunktion.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-coalesce-function.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus: Beachten Sie, wie der erste `true` ungleich null im -Array in die Datei exportiert wird.

```
First_Name,Last_Name,hasPromotion
John,Doe,true
```

### `size_of` Funktion zum Exportieren von Arrays {#sizeof-function-export-arrays}

Verwenden Sie die Funktion `size_of` , um anzugeben, wie viele Elemente in einem Array vorhanden sind. Wenn Sie beispielsweise über ein `purchaseTime` Array-Objekt mit mehreren Zeitstempeln verfügen, können Sie die `size_of`-Funktion verwenden, um anzugeben, wie viele separate Käufe von einer Person getätigt wurden.

Sie können beispielsweise die folgenden XDM-Felder unten kombinieren, wie im Screenshot zur Zuordnung dargestellt.

* `"purchaseTime": ["1538097126","1569633126,"1601255526","1632791526","1664327526"]` Array, das fünf separate Kaufzeiten des Kunden angibt
* `personalEmail.address`

![Zuordnungsbeispiel mit der Funktion size_of.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-size-of-function.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus: Beachten Sie, dass in der zweiten Spalte die Anzahl der Elemente im Array angegeben ist, die der Anzahl der separaten Käufe entspricht, die vom Kunden getätigt wurden.

```
`Personal_Email,Times_Purchased
johndoe@acme.org,"5"
```

### Indexbasierter Array-Zugriff {#index-based-array-access}

>[!IMPORTANT]
>
>Im Gegensatz zu den anderen auf dieser Seite beschriebenen Funktionen *Sie zum Exportieren einzelner Elemente eines Arrays* das Steuerelement **[!UICONTROL Berechnete Felder]** in der Benutzeroberfläche verwenden.

Sie können auf einen Index eines Arrays zugreifen, um ein einzelnes Element aus dem Array zu exportieren. Beispiel: Wenn Sie ähnlich wie im obigen Beispiel für die Funktion `size_of` nur beim ersten Kauf eines bestimmten Produkts auf zugreifen und es exportieren möchten, können Sie `purchaseTime[0]` verwenden, um das erste Element des Zeitstempels zu exportieren, `purchaseTime[1]` das zweite Element des Zeitstempels zu exportieren, `purchaseTime[2]` das dritte Element des Zeitstempels zu exportieren usw.

![Zuordnungsbeispiel, das zeigt, wie der Zugriff auf ein Element eines Arrays möglich ist.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-index.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus und exportiert das erste Mal, dass der Kunde einen Kauf getätigt hat:

```
`Personal_Email,First_Purchase
johndoe@acme.org,"1538097126"
```

### `first` und `last` Funktionen zum Exportieren von Arrays {#first-and-last-functions-export-arrays}

Verwenden Sie die Funktionen `first` und `last` zum Exportieren des ersten oder letzten Elements in einem Array. Wenn Sie beispielsweise mit dem `purchaseTime` Array-Objekt mit mehreren Zeitstempeln aus den vorherigen Beispielen fortfahren, können Sie diese Funktionen verwenden, um die erste oder letzte von einer Person getätigte Kaufzeit zu exportieren.

![Zuordnungsbeispiel mit den ersten und letzten Funktionen.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-first-last-functions.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus und exportiert das erste und letzte Mal, dass der Kunde einen Kauf getätigt hat:

```
`Personal_Email,First_Purchase, Last_Purchase
johndoe@acme.org,"1538097126","1664327526"
```

### Hash-Funktionen {#hashing-functions}

Andere verfügbare Funktionen sind spezifisch für den Export von Arrays oder Elementen aus einem Array. Sie können Hash-Funktionen verwenden, um Attribute in den exportierten Dateien zu hashen. Wenn beispielsweise in Attributen personenbezogene Daten vorhanden sind, können Sie diese Felder beim Exportieren hashen.

Sie können Zeichenfolgenwerte direkt hashen, z. B. `md5(personalEmail.address)`. Falls gewünscht, können Sie auch einzelne Elemente von Array-Feldern hashen, unter der Annahme, dass Elemente im Array Zeichenfolgen sind, wie in diesem Beispiel: `md5(purchaseTime[0])`

Folgende Hash-Funktionen werden unterstützt:

| Funktion | Beispielausdruck |
|---------|----------|
| `sha1` | `sha1(organizations[0])` |
| `sha256` | `sha256(organizations[0])` |
| `sha512` | `sha512(organizations[0])` |
| `hash` | `hash("crc32", organizations[0], "UTF-8")` |
| `md5` | `md5(organizations[0], "UTF-8")` |
| `crc32` | `crc32(organizations[0])` |

{style="table-layout:auto"}
