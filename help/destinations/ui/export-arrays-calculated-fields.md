---
title: (Beta) Verwenden Sie berechnete Felder, um Arrays in flachen Schemadateien zu exportieren
type: Tutorial
description: Erfahren Sie, wie Sie berechnete Felder verwenden können, um Arrays in flachen Schemadateien aus Real-Time CDP in Cloud-Speicher-Ziele zu exportieren.
badge: „Beta“
source-git-commit: 77fd0ace252bae66478f73a1dc4b7d4a3ccb867d
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 2%

---


# (Beta) Verwenden Sie berechnete Felder, um Arrays in flachen Schemadateien zu exportieren {#use-calculated-fields-to-export-arrays-in-flat-schema-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="(Beta) Unterstützung von Export-Arrays"
>abstract="Exportieren Sie einfache Arrays von int-, string- oder booleschen Werten von Experience Platform in Ihr gewünschtes Cloud-Speicher-Ziel. Es gelten einige Einschränkungen. In der Dokumentation finden Sie ausführliche Beispiele und unterstützte Funktionen."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#examples" text="Beispiele"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#known-limitations" text="Bekannte Einschränkungen"

>[!AVAILABILITY]
>
>* Die Funktion zum Exportieren von Arrays über berechnete Felder ist derzeit als Beta-Version verfügbar. Dokumentation und Funktionalitäten können sich ändern.

Erfahren Sie, wie Sie Arrays über berechnete Felder aus Real-Time CDP in flachen Schemadateien in Cloud-Speicher-Ziele exportieren. Lesen Sie dieses Dokument, um die durch diese Funktion aktivierten Anwendungsfälle zu verstehen.

Erhalten Sie umfassende Informationen zu berechneten Feldern - was diese sind und warum sie wichtig sind. Auf den unten verlinkten Seiten erhalten Sie eine Einführung in berechnete Felder in der Datenvorbereitung sowie weitere Informationen zu allen verfügbaren Funktionen:

* [Benutzerhandbuch und Übersicht](/help/data-prep/ui/mapping.md#calculated-fields)
* [Funktionen zur Datenvorbereitung](/help/data-prep/functions.md)

>[!IMPORTANT]
>
>Nicht alle oben aufgeführten Funktionen werden unterstützt *beim Exportieren von Feldern in Cloud-Speicher-Ziele* unter Verwendung der Funktion für berechnete Felder. Siehe [Abschnitt zu unterstützten Funktionen](#supported-functions) Weitere Informationen finden Sie weiter unten.

## Arrays und andere Objekttypen in Platform {#arrays-strings-other-objects}

Unter Experience Platform können Sie [XDM-Schemata](/help/xdm/home.md) zur Verwaltung verschiedener Feldtypen. Zuvor war es Ihnen möglich, einfache Schlüssel-Wert-Paar-Felder wie Zeichenfolgen aus dem Experience Platform in Ihre gewünschten Ziele zu exportieren. Ein Beispiel für ein solches Feld, das zuvor für den Export unterstützt wurde, ist `personalEmail.address`:`johndoe@acme.org`.

Andere Feldtypen im Experience Platform umfassen Array-Felder. Mehr dazu [Verwalten von Array-Feldern in der Experience Platform-Benutzeroberfläche](/help/xdm/ui/fields/array.md). Zusätzlich zu den zuvor unterstützten Feldtypen können Sie nun Array-Objekte exportieren, z. B.: `organizations:[marketing, sales, engineering]`. Siehe weiter unten [ausführliche Beispiele](#examples) wie Sie verschiedene Funktionen verwenden können, um auf Elemente von Arrays zuzugreifen, Array-Elemente in einer Zeichenfolge zu verknüpfen und mehr.

## Bekannte Einschränkungen {#known-limitations}

Beachten Sie die folgenden bekannten Einschränkungen für die Beta-Version dieser Funktion:

* Der Export in JSON- oder Parquet-Dateien mit hierarchischen Schemata wird derzeit nicht unterstützt. Sie können Arrays nur in CSV-, JSON- und Parquet-Dateien mit flachen Schemas exportieren.
* Zu diesem Zeitpunkt *Sie können nur einfache Arrays (oder Arrays mit primitiven Werten) in Cloud-Speicher-Ziele exportieren.*. Dies bedeutet, dass Sie Array-Objekte exportieren können, die string-, int- oder boolesche Werte enthalten. Sie können keine Maps oder Arrays von Maps oder Objekten exportieren. Das modale Fenster der berechneten Felder zeigt nur die Arrays an, die Sie exportieren können.

## Voraussetzungen {#prerequisites}

Fortschritte durch [Aktivierungsschritte für Cloud-Speicher-Ziele](/help/destinations/ui/activate-batch-profile-destinations.md) und gehen Sie zu [Mapping](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) Schritt.

## Berechnete Felder exportieren {#how-to-export-calculated-fields}

Wählen Sie im Zuordnungsschritt des Aktivierungs-Workflows für Cloud-Speicher-Ziele die Option **[!UICONTROL (Beta) Berechnetes Feld hinzufügen]**.

![Berechnetes Feld zum Export hinzufügen](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

Dadurch wird ein modales Fenster geöffnet, in dem Sie Attribute auswählen können, die Sie zum Exportieren von Attributen aus Experience Platform verwenden können.

>[!IMPORTANT]
>
>Nur einige der Felder aus Ihrem XDM-Schema sind im **[!UICONTROL Feld]** anzeigen. Zeichenfolgenwerte und Arrays von String-, int- und booleschen Werten werden angezeigt. Beispiel: die `segmentMembership` -Array nicht angezeigt, da es andere Array-Werte enthält.

![Modal-Fenster 1](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

Verwenden Sie beispielsweise die `join` -Funktion auf der `loyaltyID` wie unten gezeigt, um ein Array von Treueprogramm-IDs als Zeichenfolge zu exportieren, die mit einem Unterstrich in einer CSV-Datei verkettet ist. Ansicht [Weitere Informationen hierzu und weitere Beispiele weiter unten](#join-function-export-arrays).

![Modal-Fenster 2](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

Auswählen **[!UICONTROL Speichern]** um das berechnete Feld beizubehalten und zum Zuordnungsschritt zurückzukehren.

![Modal-Fenster 3](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

Füllen Sie im Zuordnungsschritt des Workflows den **[!UICONTROL Zielfeld]** mit dem Wert der Spaltenüberschrift, die Sie für dieses Feld in den exportierten Dateien verwenden möchten.

![Zielfeld 1 auswählen](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![Zielfeld 2 auswählen](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

Wenn Sie bereit sind, wählen Sie **[!UICONTROL Nächste]** um mit dem nächsten Schritt des Aktivierungs-Workflows fortzufahren.

![Weiter auswählen](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## Unterstützte -Funktionen {#supported-functions}

Beachten Sie, dass in der Beta-Version der berechneten Felder und der Array-Unterstützung für Ziele nur die folgenden Funktionen unterstützt werden:

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

In den folgenden Abschnitten finden Sie Beispiele und weitere Informationen zu einigen der oben aufgeführten Funktionen. Die übrigen aufgelisteten Funktionen finden Sie im Abschnitt [Dokumentation zu allgemeinen Funktionen im Abschnitt &quot;Datenvorbereitung&quot;](/help/data-prep/functions.md).

### `join` Funktion zum Exportieren von Arrays {#join-function-export-arrays}

Verwenden Sie die `join` -Funktion zum Verketten der Elemente eines Arrays in einer Zeichenfolge mithilfe eines gewünschten Trennzeichens, z. B. `_` oder `|`.

Sie können beispielsweise die folgenden XDM-Felder wie im Screenshot der Zuordnung gezeigt kombinieren, indem Sie eine `join('_',loyalty.loyaltyID)` Syntax:

* `"organizations": ["Marketing","Sales,"Finance"]` array
* `person.name.firstName` Zeichenfolge
* `person.name.lastName` Zeichenfolge
* `personalEmail.address` Zeichenfolge

![Mapping-Screenshot](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-join-function.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus. Beachten Sie, wie die drei Elemente des Arrays mithilfe der `_` Zeichen.

```
`First_Name,Last_Name,Organization
John,Doe,"Marketing_Sales_Finance"
```

### `coalesce` Funktion zum Exportieren von Arrays {#coalesce-function-export-arrays}

Verwenden Sie die `coalesce` -Funktion, um auf das erste Element eines Arrays, das nicht null ist, zuzugreifen und es in eine Zeichenfolge zu exportieren.

Sie können beispielsweise die folgenden XDM-Felder wie im Screenshot der Zuordnung gezeigt kombinieren, indem Sie eine `coalesce(subscriptions.hasPromotion)` -Syntax, um den ersten &quot;true of false&quot;-Wert im Array zurückzugeben:

* `"subscriptions.hasPromotion": [null, true, null, false, true]` array
* `person.name.firstName` Zeichenfolge
* `person.name.lastName` Zeichenfolge
* `personalEmail.address` Zeichenfolge

![Mapping-Screenshot für die Koalesce-Funktion](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-coalesce-function.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus. Beachten Sie, wie die ersten Nicht-Null-Werte `true` -Wert im Array wird in die Datei exportiert.

```
First_Name,Last_Name,hasPromotion
John,Doe,true
```


### `size_of` Funktion zum Exportieren von Arrays {#sizeof-function-export-arrays}

Verwenden Sie die `size_of` -Funktion, um anzugeben, wie viele Elemente in einem Array vorhanden sind. Wenn Sie beispielsweise eine `purchaseTime` Array-Objekt mit mehreren Zeitstempeln, können Sie die `size_of` -Funktion, um anzugeben, wie viele separate Käufe von einer Person getätigt wurden.

Sie können beispielsweise die folgenden XDM-Felder wie im Screenshot der Zuordnung gezeigt kombinieren.

* `"purchaseTime": ["1538097126","1569633126,"1601255526","1632791526","1664327526"]` Array, das fünf separate Kaufzeiten durch den Kunden angibt
* `personalEmail.address` Zeichenfolge

![Mapping-Screenshot für size_of-Funktion](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-size-of-function.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus. Beachten Sie, wie die zweite Spalte die Anzahl der Elemente im Array anzeigt, die der Anzahl der separaten Käufe des Kunden entsprechen.

```
`Personal_Email,Times_Purchased
johndoe@acme.org,"5"
```

### Indexbasierter Array-Zugriff {#index-based-array-access}

Sie können auf einen Index eines Arrays zugreifen, um ein einzelnes Element aus dem Array zu exportieren. Beispielsweise ähnlich dem obigen Beispiel für die `size_of` verwenden, können Sie `purchaseTime[0]` das erste Element des Zeitstempels zu exportieren, `purchaseTime[1]` das zweite Element des Zeitstempels zu exportieren, `purchaseTime[2]` um das dritte Element des Zeitstempels zu exportieren usw.

![Mapping-Screenshot für den Zugriff auf den Index](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-index.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus:

```
`Personal_Email,First_Purchase
johndoe@acme.org,"1538097126"
```

### `first` und `last` Funktionen zum Exportieren von Arrays {#first-and-last-functions-export-arrays}

Verwenden Sie die `first` und `last` -Funktionen, um das erste oder letzte Element in ein Array zu exportieren. Beispiel: Fahren Sie mit dem `purchaseTime` -Array-Objekt mit mehreren Zeitstempeln aus den vorherigen Beispielen verwenden, können Sie diese verwenden, um die erste oder letzte von einer Person getätigte Kaufzeit zu exportieren.

![Mapping-Screenshot für die ersten und letzten Funktionen](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-first-last-functions.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus:

```
`Personal_Email,First_Purchase, Last_Purchase
johndoe@acme.org,"1538097126","1664327526"
```

<!--

### `iif` function to export arrays {#iif-function-export-arrays}

Here are some examples of how you could use the `iif` function to access and export arrays and other fields: (STILL TO DO)

-->

### `md5` und `sha256` Hashing-Funktionen {#hashing-functions}

Zusätzlich zu den spezifischen Funktionen für den Export von Arrays oder Elementen aus einem Array können Sie Hash-Funktionen für Hash-Attribute verwenden. Wenn Sie beispielsweise persönlich identifizierbare Informationen in Attributen haben, können Sie diese Felder beim Exportieren hash.

Sie können Zeichenfolgenwerte direkt hash, z. B. `md5(personalEmail.address)`. Falls gewünscht, können Sie auch einzelne Elemente von Array-Feldern hashen, z. B.: `md5(purchaseTime[0])`



