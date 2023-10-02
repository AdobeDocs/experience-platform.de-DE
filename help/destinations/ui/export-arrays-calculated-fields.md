---
title: (Beta) Verwenden Sie berechnete Felder, um Arrays in flachen Schemadateien zu exportieren
type: Tutorial
description: Erfahren Sie, wie Sie berechnete Felder verwenden können, um Arrays in flachen Schemadateien aus Real-Time CDP in Cloud-Speicher-Ziele zu exportieren.
badge: Beta
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: 8b8abea65ee0448594113ca77f75b84293646146
workflow-type: tm+mt
source-wordcount: '1479'
ht-degree: 2%

---

# (Beta) Verwenden Sie berechnete Felder, um Arrays in flachen Schemadateien zu exportieren {#use-calculated-fields-to-export-arrays-in-flat-schema-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="(Beta) Unterstützung von Export-Arrays"
>abstract="Verwenden Sie die **Berechnetes Feld hinzufügen** -Steuerelement zum Exportieren einfacher Arrays von int-, string- oder booleschen Werten von Experience Platform in Ihr gewünschtes Cloud-Speicher-Ziel. Es gelten einige Einschränkungen. In der Dokumentation finden Sie ausführliche Beispiele und unterstützte Funktionen."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#examples" text="Beispiele"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#known-limitations" text="Bekannte Einschränkungen"

>[!AVAILABILITY]
>
>* Die Funktion zum Exportieren von Arrays über berechnete Felder ist derzeit als Beta-Version verfügbar. Dokumentation und Funktionalitäten können sich ändern.

Erfahren Sie, wie Sie Arrays über berechnete Felder aus Real-Time CDP in flachen Schemadateien nach exportieren. [Cloud-Speicher-Ziele](/help/destinations/catalog/cloud-storage/overview.md). Lesen Sie dieses Dokument, um die durch diese Funktion aktivierten Anwendungsfälle zu verstehen.

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

[Verbinden](/help/destinations/ui/connect-destination.md) zu einem gewünschten Cloud-Speicher-Ziel gelangen, indem Sie durch die [Aktivierungsschritte für Cloud-Speicher-Ziele](/help/destinations/ui/activate-batch-profile-destinations.md) und gehen Sie zu [Mapping](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) Schritt.

## Berechnete Felder exportieren {#how-to-export-calculated-fields}

Wählen Sie im Zuordnungsschritt des Aktivierungs-Workflows für Cloud-Speicher-Ziele die Option **[!UICONTROL (Beta) Berechnetes Feld hinzufügen]**.

![Fügen Sie ein berechnetes Feld hinzu, das im Zuordnungsschritt des Batch-Aktivierungs-Workflows hervorgehoben ist.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

Dadurch wird ein modales Fenster geöffnet, in dem Sie Attribute auswählen können, die Sie zum Exportieren von Attributen aus Experience Platform verwenden können.

>[!IMPORTANT]
>
>Nur einige der Felder aus Ihrem XDM-Schema sind im **[!UICONTROL Feld]** anzeigen. Zeichenfolgenwerte und Arrays von String-, int- und booleschen Werten werden angezeigt. Beispiel: die `segmentMembership` -Array nicht angezeigt, da es andere Array-Werte enthält.

![Modales Fenster der Funktion für berechnete Felder, für das noch keine Funktion ausgewählt wurde.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

Verwenden Sie beispielsweise die `join` -Funktion auf der `loyaltyID` wie unten gezeigt, um ein Array von Treueprogramm-IDs als Zeichenfolge zu exportieren, die mit einem Unterstrich in einer CSV-Datei verkettet ist. Ansicht [Weitere Informationen hierzu und weitere Beispiele weiter unten](#join-function-export-arrays).

![Modales Fenster der berechneten Feldfunktionalität mit ausgewählter Join-Funktion.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

Auswählen **[!UICONTROL Speichern]** um das berechnete Feld beizubehalten und zum Zuordnungsschritt zurückzukehren.

![Modales Fenster der berechneten Feldfunktionalität mit ausgewählter Join-Funktion und hervorgehobenem Speichermodul.](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

Füllen Sie im Zuordnungsschritt des Workflows den **[!UICONTROL Zielfeld]** mit dem Wert der Spaltenüberschrift, die Sie für dieses Feld in den exportierten Dateien verwenden möchten.

![Zuordnungsschritt mit hervorgehobenem Zielfeld.](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![Zielfeld 2 auswählen](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

Wenn Sie bereit sind, wählen Sie **[!UICONTROL Nächste]** um mit dem nächsten Schritt des Aktivierungs-Workflows fortzufahren.

![Zuordnungsschritt mit hervorgehobenem Zielfeld und ausgefülltem Zielwert.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

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

![Zuordnungsbeispiel, einschließlich der Join-Funktion.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-join-function.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus. Beachten Sie, wie die drei Elemente des Arrays mithilfe der `_` Zeichen.

```
`First_Name,Last_Name,Personal_Email,Organization
John,Doe,johndoe@acme.org, "Marketing_Sales_Finance"
```

### `iif` Funktion zum Exportieren von Arrays {#iif-function-export-arrays}

Verwenden Sie die `iif` -Funktion, um Elemente eines Arrays unter bestimmten Bedingungen zu exportieren. Beispiel: Fahren Sie mit dem `organizations` Array-Objekt von oben können Sie eine einfache bedingte Funktion wie `iif(organizations[0].equals("Marketing"), "isMarketing", "isNotMarketing")`.

![Zuordnungsbeispiel, einschließlich der if -Funktion.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-iif-function.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus. In diesem Fall ist das erste Element des Arrays Marketing, sodass die Person Mitglied der Marketing-Abteilung ist.

```
`First_Name,Last_Name, Personal_Email, Is_Member_Of_Marketing_Dept
John,Doe, johndoe@acme.org, "isMarketing"
```

### `add_to_array` Funktion zum Exportieren von Arrays {#add-to-array-function-export-arrays}

Verwenden Sie die `add_to_array` -Funktion, um einem exportierten Array Elemente hinzuzufügen. Sie können diese Funktion mit dem `join` weiter oben beschrieben.

Fortfahren mit der `organizations` Array-Objekt von oben können Sie eine Funktion wie `source: join('_', add_to_array(organizations,"2023"))`zurück und gibt die Organisationen zurück, denen eine Person im Jahr 2023 angehört.

![Zuordnungsbeispiel, einschließlich der Funktion add_to_array .](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-add-to-array-function.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus. Beachten Sie, wie die drei Elemente des Arrays mithilfe der `_` -Zeichen und 2023 werden auch am Ende der Zeichenfolge angehängt.

```
`First_Name,Last_Name,Personal_Email,Organization_Member_2023
John,Doe, johndoe@acme.org,"Marketing_Sales_Finance_2023"
```

### `coalesce` Funktion zum Exportieren von Arrays {#coalesce-function-export-arrays}

Verwenden Sie die `coalesce` -Funktion, um auf das erste Element eines Arrays, das nicht null ist, zuzugreifen und es in eine Zeichenfolge zu exportieren.

Sie können beispielsweise die folgenden XDM-Felder wie im Screenshot der Zuordnung gezeigt kombinieren, indem Sie eine `coalesce(subscriptions.hasPromotion)` -Syntax, um die erste `true` von `false` -Wert im Array:

* `"subscriptions.hasPromotion": [null, true, null, false, true]` array
* `person.name.firstName` Zeichenfolge
* `person.name.lastName` Zeichenfolge
* `personalEmail.address` Zeichenfolge

![Zuordnungsbeispiel, einschließlich der Coalesce-Funktion.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-coalesce-function.png)

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

![Zuordnungsbeispiel, einschließlich der Funktion size_of .](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-size-of-function.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus. Beachten Sie, wie die zweite Spalte die Anzahl der Elemente im Array anzeigt, die der Anzahl der separaten Käufe des Kunden entsprechen.

```
`Personal_Email,Times_Purchased
johndoe@acme.org,"5"
```

### Indexbasierter Array-Zugriff {#index-based-array-access}

Sie können auf einen Index eines Arrays zugreifen, um ein einzelnes Element aus dem Array zu exportieren. Beispielsweise ähnlich dem obigen Beispiel für die `size_of` verwenden, können Sie `purchaseTime[0]` das erste Element des Zeitstempels zu exportieren, `purchaseTime[1]` das zweite Element des Zeitstempels zu exportieren, `purchaseTime[2]` um das dritte Element des Zeitstempels zu exportieren usw.

![Zuordnungsbeispiel, das zeigt, wie auf ein Element eines Arrays zugegriffen werden kann.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-index.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus und exportiert den Kunden zum ersten Mal, wenn er einen Kauf tätigt:

```
`Personal_Email,First_Purchase
johndoe@acme.org,"1538097126"
```

### `first` und `last` Funktionen zum Exportieren von Arrays {#first-and-last-functions-export-arrays}

Verwenden Sie die `first` und `last` -Funktionen, um das erste oder letzte Element in ein Array zu exportieren. Beispiel: Fahren Sie mit dem `purchaseTime` -Array-Objekt mit mehreren Zeitstempeln aus den vorherigen Beispielen verwenden, können Sie diese verwenden, um die erste oder letzte von einer Person getätigte Kaufzeit zu exportieren.

![Zuordnungsbeispiel, einschließlich der ersten und letzten Funktionen.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-first-last-functions.png)

In diesem Fall sieht Ihre Ausgabedatei wie folgt aus und exportiert das erste und letzte Mal, dass der Kunde einen Kauf tätigt:

```
`Personal_Email,First_Purchase, Last_Purchase
johndoe@acme.org,"1538097126","1664327526"
```

### `md5` und `sha256` Hashing-Funktionen {#hashing-functions}

Zusätzlich zu den spezifischen Funktionen für den Export von Arrays oder Elementen aus einem Array können Sie Hash-Funktionen für Hash-Attribute verwenden. Wenn Sie beispielsweise persönlich identifizierbare Informationen in Attributen haben, können Sie diese Felder beim Exportieren hash.

Sie können Zeichenfolgenwerte direkt hash, z. B. `md5(personalEmail.address)`. Falls gewünscht, können Sie auch einzelne Elemente von Array-Feldern hashen, z. B.: `md5(purchaseTime[0])`