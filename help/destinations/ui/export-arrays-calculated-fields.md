---
title: (Beta) Verwenden von berechneten Feldern, um Arrays in flache Schemadateien zu exportieren
type: Tutorial
description: Erfahren Sie, wie Sie berechnete Felder verwenden können, um Arrays in flachen Schemadateien aus Real-Time CDP in Cloud-Speicher-Ziele zu exportieren.
badge: Beta
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: 787aaef26fab5ca3acff8303f928efa299cafa93
workflow-type: tm+mt
source-wordcount: '1477'
ht-degree: 5%

---

# (Beta) Verwenden von berechneten Feldern, um Arrays in flache Schemadateien zu exportieren {#use-calculated-fields-to-export-arrays-in-flat-schema-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="(Beta) Unterstützung von Export-Arrays"
>abstract="Verwenden Sie das Steuerelement **Berechnetes Feld hinzufügen**, um einfache Arrays aus Ganzzahlen, Zeichenfolgen oder booleschen Werten von Experience Platform in Ihr gewünschtes Cloud-Speicherziel zu exportieren. Es gelten einige Einschränkungen. In der Dokumentation finden Sie ausführliche Beispiele und unterstützte Funktionen."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html?lang=de#examples" text="Beispiele"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html?lang=de#known-limitations" text="Bekannte Einschränkungen"

>[!AVAILABILITY]
>
>* Die Funktion zum Exportieren von Arrays über berechnete Felder befindet sich derzeit in Beta. Dokumentation und Funktionalitäten können sich ändern.

Erfahren Sie, wie Sie Arrays über berechnete Felder aus Real-Time CDP in flachen Schemadateien in [Cloud-Speicher-Ziele](/help/destinations/catalog/cloud-storage/overview.md) exportieren. Lesen Sie dieses Dokument, um die durch diese Funktion aktivierten Anwendungsfälle zu verstehen.

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

Andere Feldtypen im Experience Platform umfassen Array-Felder. Erfahren Sie mehr über [Verwalten von Array-Feldern in der Experience Platform-Benutzeroberfläche](/help/xdm/ui/fields/array.md). Zusätzlich zu den zuvor unterstützten Feldtypen können Sie nun Array-Objekte wie `organizations:[marketing, sales, engineering]` exportieren. Weitere Informationen dazu, wie Sie mit verschiedenen Funktionen auf Elemente von Arrays zugreifen, Array-Elemente in eine Zeichenfolge einbinden und vieles mehr können Sie unter [extensiven Beispielen](#examples) finden.

## Bekannte Einschränkungen {#known-limitations}

Beachten Sie die folgenden bekannten Einschränkungen für die Beta-Version dieser Funktion:

* Der Export in JSON- oder Parquet-Dateien mit hierarchischen Schemata wird derzeit nicht unterstützt. Sie können Arrays nur in CSV-, JSON- und Parquet-Dateien mit flachen Schemas exportieren.
* Derzeit können Sie mit *nur einfache Arrays (oder Arrays mit primitiven Werten) nach Cloud-Speicher-Zielen exportieren*. Dies bedeutet, dass Sie Array-Objekte exportieren können, die string-, int- oder boolesche Werte enthalten. Sie können keine Maps oder Arrays von Maps oder Objekten exportieren. Das modale Fenster der berechneten Felder zeigt nur die Arrays an, die Sie exportieren können.

## Voraussetzungen {#prerequisites}

[ Verbinden Sie](/help/destinations/ui/connect-destination.md) mit einem gewünschten Cloud-Speicher-Ziel, gehen Sie durch die [Aktivierungsschritte für Cloud-Speicher-Ziele](/help/destinations/ui/activate-batch-profile-destinations.md) und gehen Sie zum Schritt [Zuordnung](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) .

## Berechnete Felder exportieren {#how-to-export-calculated-fields}

Wählen Sie im Zuordnungsschritt des Aktivierungs-Workflows für Cloud-Speicher-Ziele **[!UICONTROL (Beta) Berechnetes Feld hinzufügen]** aus.

![Fügen Sie ein berechnetes Feld hinzu, das im Zuordnungsschritt des Batch-Aktivierungsarbeitsablaufs hervorgehoben ist.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

Dadurch wird ein modales Fenster geöffnet, in dem Sie Attribute auswählen können, die Sie zum Exportieren von Attributen aus Experience Platform verwenden können.

>[!IMPORTANT]
>
>In der Ansicht **[!UICONTROL Feld]** sind nur einige Felder aus Ihrem XDM-Schema verfügbar. Zeichenfolgenwerte und Arrays von String-, int- und booleschen Werten werden angezeigt. Beispielsweise wird das Array `segmentMembership` nicht angezeigt, da es andere Array-Werte enthält.

![Modales Fenster der Funktion des berechneten Felds, für das noch keine Funktion ausgewählt wurde.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

Verwenden Sie beispielsweise die Funktion `join` im Feld `loyaltyID` , wie unten dargestellt, um ein Array von Treueprogramm-IDs als Zeichenfolge zu exportieren, die mit einem Unterstrich in einer CSV-Datei verkettet ist. Weitere Informationen dazu und weitere Beispiele finden Sie weiter unten unter ](#join-function-export-arrays).[

![Modales Fenster der berechneten Feldfunktionalität mit ausgewählter Join-Funktion.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

Wählen Sie **[!UICONTROL Speichern]** aus, um das berechnete Feld beizubehalten und zum Zuordnungsschritt zurückzukehren.

![Modales Fenster der berechneten Feldfunktionalität mit ausgewählter Join-Funktion und hervorgehobenem Speichersteuerelement.](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

Füllen Sie im Zuordnungsschritt des Workflows das Feld **[!UICONTROL Ziel]** mit dem Wert der Spaltenüberschrift aus, die Sie für dieses Feld in den exportierten Dateien verwenden möchten.

![Zuordnungsschritt mit hervorgehobenem Zielfeld.](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![Zielfeld auswählen 2](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

Wenn Sie bereit sind, wählen Sie **[!UICONTROL Weiter]** aus, um mit dem nächsten Schritt des Aktivierungs-Workflows fortzufahren.

![Zuordnungsschritt mit markiertem Zielfeld und ausgefülltem Zielwert.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## Unterstützte Funktionen {#supported-functions}

Bei der Aktivierung von Daten für dateibasierte Ziele werden alle dokumentierten [Datenvorbereitungsfunktionen](/help/data-prep/functions.md) unterstützt.

Beachten Sie jedoch, dass umfassende Anwendungsfallbeschreibungen und Beispielausgabeinformationen derzeit nur in der Beta-Version der berechneten Felder und Array-Unterstützung für Ziele für die folgenden Funktionen bereitgestellt werden:

* `join`
* `coalesce`
* `size_of`
* `iif`
* `index-based array access`
* `add_to_array`
* `to_array`
* `first`
* `last`
* `sha256`
* `md5`

## Beispiele für Funktionen zum Exportieren von Arrays {#examples}

In den folgenden Abschnitten finden Sie Beispiele und weitere Informationen zu einigen der oben aufgeführten Funktionen. Die übrigen aufgelisteten Funktionen finden Sie in der Dokumentation zu den allgemeinen Funktionen im Abschnitt &quot;Datenvorbereitung&quot;](/help/data-prep/functions.md).[

### `join` -Funktion zum Exportieren von Arrays {#join-function-export-arrays}

Verwenden Sie die Funktion `join` , um die Elemente eines Arrays mithilfe eines gewünschten Trennzeichens wie `_` oder `|` in eine Zeichenfolge zu verketten.

Sie können beispielsweise die folgenden XDM-Felder wie im Screenshot der Zuordnung gezeigt mit einer `join('_',loyalty.loyaltyID)` -Syntax kombinieren:

* `"organizations": ["Marketing","Sales,"Finance"]` Array
* `person.name.firstName` Zeichenfolge
* `person.name.lastName` Zeichenfolge
* `personalEmail.address` Zeichenfolge

![Zuordnungsbeispiel, einschließlich der Join-Funktion.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-join-function.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus. Beachten Sie, wie die drei Elemente des Arrays mithilfe des Zeichens `_` in einer einzelnen Zeichenfolge verkettet werden.

```
`First_Name,Last_Name,Personal_Email,Organization
John,Doe,johndoe@acme.org, "Marketing_Sales_Finance"
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

Verwenden Sie die Funktion `add_to_array` , um einem exportierten Array Elemente hinzuzufügen. Sie können diese Funktion mit der oben beschriebenen Funktion `join` kombinieren.

Wenn Sie mit dem Array-Objekt `organizations` von oben fortfahren, können Sie eine Funktion wie `source: join('_', add_to_array(organizations,"2023"))` schreiben und die Organisationen zurückgeben, zu denen eine Person im Jahr 2023 gehört.

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

### Hashfunktionen {#hashing-functions}

Zusätzlich zu den spezifischen Funktionen für den Export von Arrays oder Elementen aus einem Array können Sie Hash-Funktionen für Hash-Attribute in den exportierten Dateien verwenden. Wenn Sie beispielsweise persönlich identifizierbare Informationen in Attributen haben, können Sie diese Felder beim Exportieren hash.

Sie können Zeichenfolgenwerte direkt hashen, z. B. `md5(personalEmail.address)`. Falls gewünscht, können Sie auch einzelne Elemente von Array-Feldern hashen, vorausgesetzt die Elemente im Array sind Zeichenfolgen wie folgt: `md5(purchaseTime[0])`

Folgende Hashing-Funktionen werden unterstützt:

| Funktion | Beispielausdruck |
|---------|----------|
| `sha1` | `sha1(organizations[0])` |
| `sha256` | `sha256(organizations[0])` |
| `sha512` | `sha512(organizations[0])` |
| `hash` | `hash("crc32", organizations[0], "UTF-8")` |
| `md5` | `md5(organizations[0], "UTF-8")` |
| `crc32` | `crc32(organizations[0])` |

{style="table-layout:auto"}