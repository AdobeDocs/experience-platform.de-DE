---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Telekom; Abonnement; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Datentyp "Telecom Subscription"
description: Dieses Dokument bietet einen Überblick über den Datentyp "Telecom Subscription Experience Data Model (XDM)".
exl-id: d67915b6-daaa-489f-81b4-bd3dbe0ffa44
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 19%

---

# [!UICONTROL Telekom-Abonnement] Datentyp

[!UICONTROL Telekom-Abonnement] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Details zu bestimmten Telekommunikations-Abonnementtypen wie Internet, Mobilgeräte, Medien oder Festnetz beschreibt.

>[!NOTE]
>
>In diesem Dokument wird der Datentyp beschrieben. Die gleichnamige Feldergruppe wird im Abschnitt [[!UICONTROL Telekom-Abonnement] Referenzhandbuch für Feldergruppen](../field-groups/profile/telecom-subscription.md).
>
>Wenn Sie einen Abonnementtyp beschreiben, der nicht mit der Telekommunikationsbranche in Verbindung steht, verwenden Sie bitte die generische [[!UICONTROL Abonnement] Datentyp](./subscription.md) anstatt.

![Struktur der Telekommunikationsmitgliedschaft](../images/data-types/telecom-subscription/structure.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `devices` | Array von Objekten | Beschreibt eine Liste von Geräten und/oder Zubehör, die mit dem Plan verbunden sind. Siehe [Abschnitt unten](#devices) für Details zur erwarteten Struktur der einzelnen Array-Elemente. |
| `subscriber` | [[!UICONTROL Person]](./person.md) | Beschreibt den Inhaber des Abonnements. |
| `ID` | Zeichenfolge | Eine eindeutige Kennung für die Abonnementinstanz. |
| `billingPeriod` | Zeichenfolge | Die Zeitdauer zwischen Rechnungen. |
| `billingStartDate` | Datum | Das Datum, an dem der Abrechnungszeitraum beginnt. Das Datumsformat (ohne Uhrzeit) sollte dem [RFC 3339, Abschnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) Standard. |
| `chargeMethod` | Zeichenfolge | Die Art und Weise, wie die Abrechnung eingerichtet ist, um den Kunden zu belasten. |
| `contractID` | Zeichenfolge | Die eindeutige ID für den Vertrag, der für dieses Abonnement gilt. |
| `country` | Zeichenfolge | Das Land, in dem die vertraglichen und vertraglichen Bedingungen der Abonnements verwurzelt sind. |
| `endDate` | Datum | Das Datum, an dem das aktuelle Abonnement endet. Das Datumsformat (ohne Uhrzeit) sollte dem [RFC 3339, Abschnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) Standard. |
| `paymentDueDate` | Datum | Das Datum, an dem die Abonnement-Zahlung fällig ist. Das Datumsformat (ohne Uhrzeit) sollte dem [RFC 3339, Abschnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) Standard. |
| `paymentMethod` | Zeichenfolge | Die Zahlungsmethode für wiederkehrende Zahlungen. |
| `paymentStatus` | Zeichenfolge | Die Zahlungsbilanz des Kontos. |
| `planName` | Zeichenfolge | Der für Menschen lesbare Name des Abonnements. |
| `reason` | Zeichenfolge | Die allgemeine Absicht des Mitglieds für die Verwendung des Abonnements. |
| `renew` | Zeichenfolge | Die vereinbarte Art und Weise, wie das Abonnement nach dem Enddatum fortgesetzt werden kann. |
| `startDate` | Datum | Das Datum, an dem das Abonnement beginnt. Das Datumsformat (ohne Uhrzeit) sollte dem [RFC 3339, Abschnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) Standard. |
| `status` | Zeichenfolge | Der aktuelle Status des Abonnements. |
| `subscriptionCategory` | Zeichenfolge | Die wichtigste Kategorisierung dieser Art von Abonnement auf oberster Ebene. |
| `subscriptionSKU` | Zeichenfolge | Die Bestandserhaltungseinheit (SKU) für das Abonnement. |
| `subscriptionSubCategory` | Zeichenfolge | Die spezifische Unterkategorisierung des Abonnements. |
| `term` | Ganzzahl | Der numerische Wert des Abonnementbegriffs. |
| `termUnitOfTime` | Zeichenfolge | Die Zeiteinheit für den Zeitraum. |
| `topUp` | Zeichenfolge | Beschreibt die vereinbarten Bedingungen dafür, wie verbrauchbare Aspekte eines Abonnements während eines Abrechnungszeitraums zurückgekauft werden. |
| `type` | Zeichenfolge | Der Umfang des Anspruchs in Bezug auf die Anzahl der Personen, die vom Abonnement abgedeckt werden. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)

## `devices` {#devices}

`devices` ist ein Array von Objekten, wobei jedes Objekt ein mit dem Abonnement verknüpftes Gerät oder Zubehör beschreibt.

![Geräte-Array-Struktur](../images/data-types/telecom-subscription/devices.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `deviceFees` | Objekt | Ein Objekt, das alle Gerätegebühren für Elemente wie Router, Modems und Empfänger erfasst. erwartet die folgenden Eigenschaften:<ul><li>`amount`: Der Geldbetrag, der sich aus dem `currencyCode`.</li><li>`conversionDate`: Das Datum, an dem die Währungsumrechnung vorgenommen wurde.</li><li>`currencyCode`: Die [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) Währungscode für `amount`.</li></ul> |
| `ID` | Zeichenfolge | Eine eindeutige ID für das Gerät. |
| `OS` | Zeichenfolge | Das Betriebssystem des Geräts. |
| `deviceInsurance` | Zeichenfolge | Gibt an, ob sich ein Kunde für eine Versicherung dieses Geräts entschieden hat. |
| `manufacturer` | Zeichenfolge | Der Gerätehersteller. |
| `name` | Zeichenfolge | Ein Name für das Gerät. |
| `paymentOptions` | Zeichenfolge | Gibt an, ob das Gerät in Raten oder im vollen Einzelhandelspreis bezahlt wird. |
| `serialNumber` | Zeichenfolge | Die Seriennummer des Geräts. |
| `status` | Zeichenfolge | Der Gerätestatus. |
| `storageCapacity` | Zeichenfolge | Die Speicherkapazität des Geräts. |
| `type` | Zeichenfolge | Der Gerätetyp. |

{style="table-layout:auto"}
