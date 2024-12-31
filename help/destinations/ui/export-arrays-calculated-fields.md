---
title: Verwenden von berechneten Feldern zum Exportieren von Arrays als Zeichenfolgen
type: Tutorial
description: Erfahren Sie, wie Sie berechnete Felder verwenden, um Arrays von Real-Time CDP als Zeichenfolgen in Cloud-Speicher-Ziele zu exportieren.
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: 9b64e39d25ad94aa834c8e207396b37c2a121243
workflow-type: tm+mt
source-wordcount: '1556'
ht-degree: 7%

---

# Verwenden von berechneten Feldern zum Exportieren von Arrays als Zeichenfolgen{#use-calculated-fields-to-export-arrays-as-strings}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="Unterstützung von Export-Arrays"
>abstract="<p>Verwenden Sie das Steuerelement **Berechnetes Feld hinzufügen**, um einfache Arrays aus Ganzzahlen, Zeichenfolgen, Objektwerten oder booleschen Werten von Experience Platform in Ihr gewünschtes Cloud-Speicherziel zu exportieren. </p><p> Arrays müssen mithilfe der Funktion `array_to_string` als Zeichenfolgen exportiert werden. In der Dokumentation finden Sie ausführliche Beispiele und unterstützte Funktionen.</p>"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html?lang=de#examples" text="Beispiele"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html?lang=de#known-limitations" text="Bekannte Einschränkungen"

>[!AVAILABILITY]
>
>Die Funktion zum Exportieren von Arrays über berechnete Felder ist im Allgemeinen verfügbar.

Erfahren Sie, wie Sie Arrays über berechnete Felder aus Real-Time CDP in [Cloud-Speicherziele](/help/destinations/catalog/cloud-storage/overview.md) als Zeichenfolgen exportieren. Lesen Sie dieses Dokument, um die Anwendungsfälle zu verstehen, die durch diese Funktion aktiviert werden.

Hier erhalten Sie ausführliche Informationen über berechnete Felder - was diese sind und warum sie wichtig sind. Lesen Sie die unten verlinkten Seiten, um eine Einführung in berechnete Felder in die Datenvorbereitung und weitere Informationen zu allen verfügbaren Funktionen zu erhalten:

* [Handbuch zur Benutzeroberfläche und Übersicht](/help/data-prep/ui/mapping.md#calculated-fields)
* [Funktionen zur Datenvorbereitung](/help/data-prep/functions.md)

<!--

>[!IMPORTANT]
>
>Not all functions listed above are supported *when exporting fields to cloud storage destinations* using the calculated fields functionality. See the [supported functions section](#supported-functions) further below for more information.

-->

## Arrays und andere Objekttypen in Platform {#arrays-strings-other-objects}

Beim Experience Platform können Sie [XDM-Schemata](/help/xdm/home.md) verwenden, um verschiedene Feldtypen zu verwalten. Bevor die Unterstützung für Array-Exporte hinzugefügt wurde, konnten Sie einfache Schlüssel-Wert-Paarfelder wie Zeichenfolgen aus Experience Platform in Ihre gewünschten Ziele exportieren. Ein Beispiel für ein solches Feld, das zuvor für den Export unterstützt wurde, ist `personalEmail.address`:`johndoe@acme.org`.

Andere Feldtypen in Experience Platform umfassen Array-Felder. Lesen Sie mehr über [Verwalten von Array-Feldern in der Experience Platform-Benutzeroberfläche](/help/xdm/ui/fields/array.md). Zusätzlich zu den zuvor unterstützten Feldtypen können Sie jetzt Array-Objekte wie das folgende Beispiel exportieren, die mithilfe der `array_to_string`-Funktion zu einer Zeichenfolge verkettet werden.

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

## Bekannte Einschränkungen {#known-limitations}

Beachten Sie die folgenden bekannten Einschränkungen, die derzeit für diese Funktion gelten:

* Der Export in JSON- oder Parquet *Dateien mit hierarchischen* wird derzeit nicht unterstützt. Sie können Arrays in CSV-, JSON- und Parquet *Dateien (nur als Zeichenfolgen) exportieren* indem Sie die Funktion `array_to_string` verwenden.

## Voraussetzungen {#prerequisites}

[Verbinden](/help/destinations/ui/connect-destination.md) mit dem gewünschten Cloud-Speicher-Ziel, schreiten Sie durch die [Aktivierungsschritte für Cloud-Speicher-Ziele](/help/destinations/ui/activate-batch-profile-destinations.md) und gelangen Sie zum Schritt [Zuordnung](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).

## Exportieren berechneter Felder {#how-to-export-calculated-fields}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_control"
>title="Aktivieren des hierarchischen Ausgabeschemas"
>abstract="Aktivieren Sie diese Option, wenn Sie hierarchische Strukturen wie Arrays exportieren möchten."

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_calculated_field_disabled"
>title="„Berechnete Felder hinzufügen“ ist deaktiviert"
>abstract="Dieses Steuerelement ist deaktiviert, da Sie beim Herstellen einer Verbindung zum Ziel ausgewählt haben, flache Strukturen zu exportieren."

Wählen Sie im Zuordnungsschritt des Aktivierungs-Workflows für Cloud-Speicher-Ziele **[!UICONTROL Berechnetes Feld hinzufügen]** aus.

![Berechnetes Feld hinzufügen, das im Zuordnungsschritt des Batch-Aktivierungs-Workflows hervorgehoben ist.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

Dadurch wird ein modales Fenster geöffnet, in dem Sie Funktionen und Felder auswählen können, um Attribute aus dem Experience Platform zu exportieren.

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

## Beispiele für unterstützte Funktionen zum Exportieren von Arrays {#supported-functions}

Alle dokumentierten [Datenvorbereitungsfunktionen](/help/data-prep/functions.md) werden beim Aktivieren von Daten für dateibasierte Ziele unterstützt.

Die folgenden Funktionen, die speziell für die Handhabung von Arrays gelten, werden zusammen mit Beispielen dokumentiert.

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

## Beispiele für Funktionen zum Exportieren von Arrays {#examples}

In den folgenden Abschnitten finden Sie Beispiele und weitere Informationen zu einigen der oben aufgeführten Funktionen. Die übrigen aufgelisteten Funktionen finden Sie in der [Dokumentation zu allgemeinen Funktionen im Abschnitt Datenvorbereitung](/help/data-prep/functions.md).

### `array_to_string` Funktion zum Exportieren von Arrays {#array-to-string-function-export-arrays}

Verwenden Sie die Funktion `array_to_string` , um die Elemente eines Arrays mithilfe eines gewünschten Trennzeichens wie `_` oder `|` zu einer Zeichenfolge zu verketten.

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

### `filterArray` Funktion zum Exportieren gefilterter Arrays

Verwenden Sie die Funktion `filterArray` zum Filtern der Elemente eines exportierten Arrays. Sie können diese Funktion mit der weiter oben beschriebenen `array_to_string` kombinieren.

Wenn Sie mit dem `organizations` Array-Objekt von oben fortfahren, können Sie eine Funktion wie `array_to_string('_', filterArray(organizations, org -> org.founded > 2021))` schreiben, wodurch die Organisationen mit einem Wert für `founded` im Jahr 2021 oder neuer zurückgegeben werden.

![Beispiel für die filterArray-Funktion.](/help/destinations/assets/ui/export-arrays-calculated-fields/filter-array-function.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus: Beachten Sie, wie die beiden Elemente des Arrays, die das Kriterium erfüllen, mithilfe des `_`-Zeichens zu einer einzigen Zeichenfolge verkettet werden.

```
John,Doe,johndoe@acme.org, "{'id':123,'orgName':'Acme Inc','founded':1990,'latestInteraction':1708041600000}_{'id':789,'orgName':'Energy Corp','founded':2021,'latestInteraction':1725753600000}"
```

### `transformArray` Funktion zum Exportieren transformierter Arrays

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

### `flattenArray` Funktion zum Exportieren von reduzierten Arrays

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

<!--

### Hashing functions {#hashing-functions}

In addition to the functions specific for exporting arrays or elements from an array, you can use hashing functions to hash attributes in the exported files. For example, if you have any personally identifiable information in attributes, you can hash those fields when exporting them. 

You can hash string values directly, for example `md5(personalEmail.address)`. If desired, you can also hash individual elements of array fields, assuming elements in the array are strings, like this: `md5(purchaseTime[0])`

The supported hashing functions are:

|Function | Sample expression |
|---------|----------|
| `sha1` | `sha1(organizations[0])` |
| `sha256` | `sha256(organizations[0])` |
| `sha512` | `sha512(organizations[0])` |
| `hash` | `hash("crc32", organizations[0], "UTF-8")` |
| `md5` |  `md5(organizations[0], "UTF-8")` |
| `crc32` | `crc32(organizations[0])` |

{style="table-layout:auto"}

-->