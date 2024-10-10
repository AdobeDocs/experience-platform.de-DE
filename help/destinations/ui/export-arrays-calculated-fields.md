---
title: Berechnete Felder zum Exportieren von Arrays als Zeichenfolgen verwenden
type: Tutorial
description: Erfahren Sie, wie Sie berechnete Felder verwenden können, um Arrays aus Real-Time CDP als Zeichenfolgen in Cloud-Speicher-Ziele zu exportieren.
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: 6fec0432f71e58d0e17ac75121fb1028644016e1
workflow-type: tm+mt
source-wordcount: '1513'
ht-degree: 0%

---

# Berechnete Felder zum Exportieren von Arrays als Zeichenfolgen verwenden{#use-calculated-fields-to-export-arrays-as-strings}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="Export-Arrays unterstützen"
>abstract="<p>Verwenden Sie das Steuerelement **Berechnetes Feld hinzufügen** , um Arrays von int-, string-, boolean- und object-Werten von Experience Platform an Ihr gewünschtes Cloud-Speicher-Ziel zu exportieren.</p><p> Arrays müssen mithilfe der Funktion `array_to_string` als Zeichenfolgen exportiert werden. In der Dokumentation finden Sie ausführliche Beispiele und unterstützte Funktionen.</p>"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html?lang=de#examples" text="Beispiele"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html?lang=de#known-limitations" text="Bekannte Einschränkungen"

>[!AVAILABILITY]
>
>* Die Funktion zum Exportieren von Arrays über berechnete Felder ist allgemein verfügbar.

Erfahren Sie, wie Sie Arrays über berechnete Felder aus Real-Time CDP als Zeichenfolgen in [Cloud-Speicher-Ziele](/help/destinations/catalog/cloud-storage/overview.md) exportieren. Lesen Sie dieses Dokument, um die durch diese Funktion aktivierten Anwendungsfälle zu verstehen.

Erhalten Sie umfassende Informationen zu berechneten Feldern - was diese sind und warum sie wichtig sind. Auf den unten verlinkten Seiten erhalten Sie eine Einführung in berechnete Felder in der Datenvorbereitung sowie weitere Informationen zu allen verfügbaren Funktionen:

* [Benutzerhandbuch und Übersicht](/help/data-prep/ui/mapping.md#calculated-fields)
* [Funktionen zur Datenvorbereitung](/help/data-prep/functions.md)

<!--

>[!IMPORTANT]
>
>Not all functions listed above are supported *when exporting fields to cloud storage destinations* using the calculated fields functionality. See the [supported functions section](#supported-functions) further below for more information.

-->

## Arrays und andere Objekttypen in Platform {#arrays-strings-other-objects}

Unter Experience Platform können Sie [XDM-Schemas](/help/xdm/home.md) verwenden, um verschiedene Feldtypen zu verwalten. Zuvor war es Ihnen möglich, einfache Schlüssel-Wert-Paar-Felder wie Zeichenfolgen aus dem Experience Platform in Ihre gewünschten Ziele zu exportieren. Ein Beispiel für ein solches Feld, das zuvor für den Export unterstützt wurde, ist `personalEmail.address`:`johndoe@acme.org`.

Andere Feldtypen im Experience Platform umfassen Array-Felder. Erfahren Sie mehr über [Verwalten von Array-Feldern in der Experience Platform-Benutzeroberfläche](/help/xdm/ui/fields/array.md). Zusätzlich zu den zuvor unterstützten Feldtypen können Sie jetzt Array-Objekte wie das folgende Beispiel exportieren, die mithilfe der Funktion `array_to_string` in eine Zeichenfolge verkettet werden.

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

Weitere Informationen dazu, wie Sie mit verschiedenen Funktionen auf Elemente von Arrays zugreifen, Arrays umwandeln und filtern, Array-Elemente in eine Zeichenfolge einbinden und vieles mehr, finden Sie unter [umfassende Beispiele](#examples) .

## Bekannte Einschränkungen {#known-limitations}

Beachten Sie die folgenden bekannten Einschränkungen, die derzeit für diese Funktion gelten:

* Der Export in JSON- oder Parquet-Dateien *mit hierarchischen Schemas* wird derzeit nicht unterstützt. Mithilfe der Funktion `array_to_string` können Sie Arrays in CSV-, JSON- und Parquet-Dateien *nur als Zeichenfolgen exportieren*.

## Voraussetzungen {#prerequisites}

[ Verbinden Sie](/help/destinations/ui/connect-destination.md) mit einem gewünschten Cloud-Speicher-Ziel, gehen Sie durch die [Aktivierungsschritte für Cloud-Speicher-Ziele](/help/destinations/ui/activate-batch-profile-destinations.md) und gehen Sie zum Schritt [Zuordnung](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) .

## Berechnete Felder exportieren {#how-to-export-calculated-fields}

Wählen Sie im Zuordnungsschritt des Aktivierungs-Workflows für Cloud-Speicher-Ziele **[!UICONTROL Berechnetes Feld hinzufügen]** aus.

![Fügen Sie ein berechnetes Feld hinzu, das im Zuordnungsschritt des Batch-Aktivierungsarbeitsablaufs hervorgehoben ist.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

Dadurch wird ein modales Fenster geöffnet, in dem Sie Funktionen und Felder auswählen können, um Attribute aus der Experience Platform zu exportieren.

![Modales Fenster der Funktion des berechneten Felds, für das noch keine Funktion ausgewählt wurde.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

Verwenden Sie beispielsweise die Funktion `array_to_string` im Feld `organizations` , wie unten dargestellt, um das Organisations-Array als Zeichenfolge in eine CSV-Datei zu exportieren. Weitere Informationen dazu und weitere Beispiele finden Sie weiter unten unter ](#array-to-string-function-export-arrays).[

![Modales Fenster der Funktion des berechneten Felds mit ausgewählter Funktion &quot;Array-zu-String&quot;.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

Wählen Sie **[!UICONTROL Speichern]** aus, um das berechnete Feld beizubehalten und zum Zuordnungsschritt zurückzukehren.

![Modales Fenster der Funktionalität des berechneten Felds, wobei die Funktion &quot;Array-zu-String&quot;ausgewählt und das Steuerelement &quot;Speichern&quot;hervorgehoben ist.](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

Füllen Sie im Zuordnungsschritt des Workflows das Feld **[!UICONTROL Ziel]** mit dem Wert der Spaltenüberschrift aus, die Sie für dieses Feld in den exportierten Dateien verwenden möchten.

![Zuordnungsschritt mit hervorgehobenem Zielfeld.](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![Zielfeld auswählen 2](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

Wenn Sie bereit sind, wählen Sie **[!UICONTROL Weiter]** aus, um mit dem nächsten Schritt des Aktivierungs-Workflows fortzufahren.

![Zuordnungsschritt mit markiertem Zielfeld und ausgefülltem Zielwert.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## Beispielunterstützte Funktionen zum Exportieren von Arrays {#supported-functions}

Bei der Aktivierung von Daten für dateibasierte Ziele werden alle dokumentierten [Datenvorbereitungsfunktionen](/help/data-prep/functions.md) unterstützt.

Die folgenden Funktionen, die speziell für die Verarbeitung von Arrays-Exporten gelten, werden zusammen mit Beispielen dokumentiert.

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

In den folgenden Abschnitten finden Sie Beispiele und weitere Informationen zu einigen der oben aufgeführten Funktionen. Die übrigen aufgelisteten Funktionen finden Sie in der Dokumentation zu den allgemeinen Funktionen im Abschnitt &quot;Datenvorbereitung&quot;](/help/data-prep/functions.md).[

### `array_to_string` -Funktion zum Exportieren von Arrays {#array-to-string-function-export-arrays}

Verwenden Sie die Funktion `array_to_string` , um die Elemente eines Arrays mithilfe eines gewünschten Trennzeichens wie `_` oder `|` in eine Zeichenfolge zu verketten.

Sie können beispielsweise die folgenden XDM-Felder wie im Screenshot der Zuordnung gezeigt mit einer `array_to_string('_',organizations)` -Syntax kombinieren:

* `organizations` Array
* `person.name.firstName` Zeichenfolge
* `person.name.lastName` Zeichenfolge
* `personalEmail.address` Zeichenfolge

![Zuordnungsbeispiel, einschließlich der Funktion array_to_string .](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-array-to-string-function.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus. Beachten Sie, wie die Elemente des Arrays mithilfe des Zeichens `_` in eine einzelne Zeichenfolge verkettet werden.

```
First_Name,Last_Name,Personal_Email,Organization
John,Doe,johndoe@acme.org, "{'id':123,'orgName':'Acme Inc','founded':1990,'latestInteraction':1708041600000}_{'id':456,'orgName':'Superstar Inc','founded':2004,'latestInteraction':1692921600000}_{'id':789,'orgName':'Energy Corp','founded':2021,'latestInteraction':1725753600000}"
```

### `flattenArray` -Funktion zum Exportieren von reduzierten Arrays

Verwenden Sie die Funktion `flattenArray` , um ein exportiertes mehrdimensionales Array zu reduzieren. Sie können diese Funktion mit der oben beschriebenen Funktion `array_to_string` kombinieren.

Wenn Sie mit dem Array-Objekt `organizations` von oben fortfahren, können Sie eine Funktion wie `array_to_string('_', flattenArray(organizations))` schreiben. Beachten Sie, dass die Funktion `array_to_string` das Eingabe-Array standardmäßig in eine Zeichenfolge reduziert.

Die resultierende Ausgabe entspricht der oben beschriebenen `array_to_string` -Funktion.


### `filterArray` -Funktion zum Exportieren gefilterter Arrays

Verwenden Sie die Funktion `filterArray` , um die Elemente eines exportierten Arrays zu filtern. Sie können diese Funktion mit der oben beschriebenen Funktion `array_to_string` kombinieren.

Wenn Sie mit dem Array-Objekt `organizations` von oben fortfahren, können Sie eine Funktion wie `array_to_string('_', filterArray(organizations, org -> org.founded > 2021))` schreiben und die Organisationen mit einem Wert für `founded` im Jahr 2021 oder höher zurückgeben.

![Beispiel der Funktion &quot;filterArray&quot;.](/help/destinations/assets/ui/export-arrays-calculated-fields/filter-array-function.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus. Beachten Sie, wie die beiden Elemente des Arrays, die die Bedingung erfüllen, mithilfe des Zeichens `_` in einer einzelnen Zeichenfolge verkettet werden.

```
John,Doe,johndoe@acme.org, "{'id':123,'orgName':'Acme Inc','founded':1990,'latestInteraction':1708041600000}_{'id':789,'orgName':'Energy Corp','founded':2021,'latestInteraction':1725753600000}"
```

### `transformArray` -Funktion zum Exportieren transformierter Arrays

Verwenden Sie die Funktion `transformArray` , um die Elemente eines exportierten Arrays zu transformieren. Sie können diese Funktion mit der oben beschriebenen Funktion `array_to_string` kombinieren.

Wenn Sie mit dem Array-Objekt `organizations` von oben fortfahren, können Sie eine Funktion wie `array_to_string('_', transformArray(organizations, org -> ucase(org.orgName)))` schreiben und die Namen der Organisationen zurückgeben, die in Großbuchstaben konvertiert wurden.

![Beispiel der transformArray-Funktion.](/help/destinations/assets/ui/export-arrays-calculated-fields/transform-array-function.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus. Beachten Sie, wie die drei Elemente des Arrays transformiert und mit dem Zeichen `_` in eine einzelne Zeichenfolge verkettet werden.

```
John,Doe,johndoe@acme.org,ACME INC_SUPERSTAR INC_ENERGY CORP
```

### `iif` -Funktion zum Exportieren von Arrays {#iif-function-export-arrays}

Verwenden Sie die Funktion `iif` , um Elemente eines Arrays unter bestimmten Bedingungen zu exportieren. Wenn Sie beispielsweise mit dem Array-Objekt `organizations` von oben fortfahren, können Sie eine einfache bedingte Funktion wie `iif(organizations[0].equals("Marketing"), "isMarketing", "isNotMarketing")` schreiben.

![Zuordnungsbeispiel, einschließlich der if-Funktion.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-iif-function.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus. In diesem Fall ist das erste Element des Arrays Marketing, sodass die Person Mitglied der Marketing-Abteilung ist.

```
`First_Name,Last_Name, Personal_Email, Is_Member_Of_Marketing_Dept
John,Doe, johndoe@acme.org, "isMarketing"
```

### `add_to_array` -Funktion zum Exportieren von Arrays {#add-to-array-function-export-arrays}

Verwenden Sie die Funktion `add_to_array` , um einem exportierten Array Elemente hinzuzufügen. Sie können diese Funktion mit der oben beschriebenen Funktion `array_to_string` kombinieren.

Wenn Sie mit dem Array-Objekt `organizations` von oben fortfahren, können Sie eine Funktion wie `source: array_to_string('_', add_to_array(organizations,"2023"))` schreiben und die Organisationen zurückgeben, zu denen eine Person im Jahr 2023 gehört.

![Zuordnungsbeispiel, einschließlich der Funktion add_to_array.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-add-to-array-function.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus. Beachten Sie, wie die drei Elemente des Arrays mithilfe des Zeichens `_` in eine einzelne Zeichenfolge verkettet werden und 2023 ebenfalls am Ende der Zeichenfolge angehängt wird.

```
`First_Name,Last_Name,Personal_Email,Organization_Member_2023
John,Doe, johndoe@acme.org,"Marketing_Sales_Finance_2023"
```

### `coalesce` -Funktion zum Exportieren von Arrays {#coalesce-function-export-arrays}

Verwenden Sie die Funktion `coalesce` , um auf das erste Element, das nicht null ist, eines Arrays zuzugreifen und es in eine Zeichenfolge zu exportieren.

Sie können beispielsweise die folgenden XDM-Felder wie im Screenshot der Zuordnung gezeigt kombinieren, indem Sie eine `coalesce(subscriptions.hasPromotion)` -Syntax verwenden, um den ersten `true` von `false` -Wert im Array zurückzugeben:

* `"subscriptions.hasPromotion": [null, true, null, false, true]` Array
* `person.name.firstName` Zeichenfolge
* `person.name.lastName` Zeichenfolge
* `personalEmail.address` Zeichenfolge

![Zuordnungsbeispiel, einschließlich der Koalesce-Funktion.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-coalesce-function.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus. Beachten Sie, wie der erste Wert, der nicht null ist, im Array in die Datei exportiert wird.`true`

```
First_Name,Last_Name,hasPromotion
John,Doe,true
```

### `size_of` -Funktion zum Exportieren von Arrays {#sizeof-function-export-arrays}

Verwenden Sie die Funktion `size_of` , um anzugeben, wie viele Elemente in einem Array vorhanden sind. Wenn Sie beispielsweise über ein Array-Objekt `purchaseTime` mit mehreren Zeitstempeln verfügen, können Sie mit der Funktion `size_of` angeben, wie viele separate Käufe von einer Person getätigt wurden.

Sie können beispielsweise die folgenden XDM-Felder wie im Screenshot der Zuordnung gezeigt kombinieren.

* `"purchaseTime": ["1538097126","1569633126,"1601255526","1632791526","1664327526"]` Array, das fünf separate Kaufzeiten durch den Kunden angibt
* `personalEmail.address` Zeichenfolge

![Zuordnungsbeispiel, einschließlich der size_of-Funktion.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-size-of-function.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus. Beachten Sie, wie die zweite Spalte die Anzahl der Elemente im Array anzeigt, die der Anzahl der separaten Käufe des Kunden entsprechen.

```
`Personal_Email,Times_Purchased
johndoe@acme.org,"5"
```

### Indexbasierter Array-Zugriff {#index-based-array-access}

Sie können auf einen Index eines Arrays zugreifen, um ein einzelnes Element aus dem Array zu exportieren. Beispiel: Wenn Sie wie im obigen Beispiel für die Funktion `size_of` nur beim ersten Kauf eines bestimmten Produkts auf ein bestimmtes Produkt zugreifen und es exportieren möchten, können Sie mit `purchaseTime[0]` das erste Element des Zeitstempels exportieren, mit `purchaseTime[1]` das zweite Element des Zeitstempels exportieren, mit `purchaseTime[2]` das dritte Element des Zeitstempels exportieren usw.

![Zuordnungsbeispiel, das zeigt, wie auf ein Element eines Arrays zugegriffen werden kann.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-index.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus und exportiert den Kunden zum ersten Mal, wenn er einen Kauf tätigt:

```
`Personal_Email,First_Purchase
johndoe@acme.org,"1538097126"
```

### Funktionen `first` und `last` zum Exportieren von Arrays {#first-and-last-functions-export-arrays}

Verwenden Sie die Funktionen `first` und `last` , um das erste oder letzte Element in ein Array zu exportieren. Wenn Sie beispielsweise mit dem Array-Objekt `purchaseTime` mit mehreren Zeitstempeln aus den vorherigen Beispielen fortfahren, können Sie diese verwenden, um Funktionen zum Exportieren der ersten oder letzten von einer Person getätigten Kaufzeit zu verwenden.

![Zuordnungsbeispiel, einschließlich der ersten und letzten Funktionen.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-first-last-functions.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus und exportiert das erste und letzte Mal, dass der Kunde einen Kauf tätigt:

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