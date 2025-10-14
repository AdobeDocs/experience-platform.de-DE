---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;Felder;Schemata;Schemata;Telekommunikation;Abonnement;Datentyp;Datentyp;Datentyp;
solution: Experience Platform
title: Datentyp des Telekom-Abonnements
description: Erfahren Sie mehr über den Datentyp Telekom-Abonnement-Experience-Datenmodell (XDM).
exl-id: d67915b6-daaa-489f-81b4-bd3dbe0ffa44
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 20%

---

# Datentyp [!UICONTROL Telekom]Abonnement

[!UICONTROL Telekom-Abonnement] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Details für bestimmte Telekommunikationsabonnementtypen wie Internet, Mobile, Medien oder Festnetz beschreibt.

>[!NOTE]
>
>In diesem Dokument wird der Datentyp beschrieben. Informationen zur Feldergruppe mit demselben Namen finden Sie im Referenzhandbuch [[!UICONTROL Telekom-Abonnement] Feldergruppe &#x200B;](../field-groups/profile/telecom-subscription.md).
>
>Wenn Sie einen Abonnementtyp beschreiben, der nicht mit der Telekommunikationsbranche verbunden ist, verwenden Sie stattdessen den generischen [[!UICONTROL Abonnement]-Datentyp](./subscription.md).

![Telekom-Abonnementstruktur](../images/data-types/telecom-subscription/structure.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `devices` | Array von Objekten | Beschreibt eine Liste von Geräten und/oder Zubehör, die mit dem Plan verbunden sind. Siehe [Abschnitt unten](#devices) für Details zur erwarteten Struktur der einzelnen Array-Elemente. |
| `subscriber` | [[!UICONTROL Person]](./person.md) | Beschreibt den Inhaber des Abonnements. |
| `ID` | String | Eine eindeutige Kennung für die Abonnementinstanz. |
| `billingPeriod` | String | Die Zeitdauer zwischen Rechnungen. |
| `billingStartDate` | Datum | Das Datum, an dem der Abrechnungszeitraum beginnt. Das Datumsformat (ohne Zeit) sollte dem Standard [RFC 3339, Abschnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) entsprechen. |
| `chargeMethod` | String | Die Art und Weise, wie die Abrechnung eingerichtet wird, um den Kunden zu belasten. |
| `contractID` | String | Die eindeutige ID für den Vertrag, der für dieses Abonnement gilt. |
| `country` | String | Das Land, in dem die Vertragsbedingungen des Abonnements ihren Ursprung haben. |
| `endDate` | Datum | Das Datum, an dem die aktuelle Abonnementlaufzeit endet. Das Datumsformat (ohne Zeit) sollte dem Standard [RFC 3339, Abschnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) entsprechen. |
| `paymentDueDate` | Datum | Das Datum, an dem die Abonnementzahlung fällig ist. Das Datumsformat (ohne Zeit) sollte dem Standard [RFC 3339, Abschnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) entsprechen. |
| `paymentMethod` | String | Die Zahlungsmethode für wiederkehrende Zahlungen. |
| `paymentStatus` | String | Die Zahlungsfähigkeit des Kontos. |
| `planName` | String | Der für Menschen lesbare Name des Abonnements. |
| `reason` | String | Die allgemeine Absicht, die der Abonnent mit der Verwendung des Abonnements verfolgt. |
| `renew` | String | Die vereinbarte Art und Weise, wie das Abonnement nach dem Enddatum fortgesetzt werden kann. |
| `startDate` | Datum | Das Datum, an dem das Abonnement beginnt. Das Datumsformat (ohne Zeit) sollte dem Standard [RFC 3339, Abschnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) entsprechen. |
| `status` | String | Der aktuelle Status des Abonnements. |
| `subscriptionCategory` | String | Die wichtigste, übergeordnete Kategorisierung dieses Abonnementtyps. |
| `subscriptionSKU` | String | Die Lagerhaltungseinheit (SKU) für das Abonnement. |
| `subscriptionSubCategory` | String | Die spezifische Unterkategorie des Abonnements. |
| `term` | Ganzzahl | Der numerische Wert der Abonnementbedingung. |
| `termUnitOfTime` | String | Die Zeiteinheit für den Zeitraum. |
| `topUp` | String | Beschreibt die vereinbarten Bedingungen für den Rückkauf verbrauchbarer Aspekte eines Abonnements während eines Abrechnungszeitraums. |
| `type` | String | Der Umfang der Berechtigungen in Bezug auf die Anzahl der Personen, die im Abonnement enthalten sind. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)

## `devices` {#devices}

`devices` ist ein Array von Objekten, wobei jedes Objekt ein Gerät oder ein Zubehör beschreibt, das mit dem Abonnement verknüpft ist.

![Geräte-Array-Struktur](../images/data-types/telecom-subscription/devices.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `deviceFees` | Objekt | Ein Objekt, das alle Gerätegebühren für Elemente wie Router, Modems und Empfänger erfasst. Erwartet die folgenden Eigenschaften:<ul><li>`amount`: Der Geldbetrag in der Form, in der der `currencyCode` dargestellt wird.</li><li>`conversionDate`: Das Datum, an dem die Währungsumrechnung vorgenommen wurde.</li><li>`currencyCode`: Der [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html)-Währungscode für die `amount`.</li></ul> |
| `ID` | String | Eine eindeutige ID für das Gerät. |
| `OS` | String | Das Gerätebetriebssystem. |
| `deviceInsurance` | String | Zeigt an, ob ein Kunde sich für eine Versicherung für dieses Gerät entschieden hat. |
| `manufacturer` | String | Der Gerätehersteller. |
| `name` | String | Ein Name für das Gerät. |
| `paymentOptions` | String | Zeigt an, ob das Gerät in Raten oder zum vollen Verkaufspreis bezahlt wird. |
| `serialNumber` | String | Die Seriennummer des Geräts. |
| `status` | String | Der Gerätestatus. |
| `storageCapacity` | String | Die Speicherkapazität des Geräts. |
| `type` | String | Der Gerätetyp. |

{style="table-layout:auto"}
