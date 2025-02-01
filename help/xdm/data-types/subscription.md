---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;Felder;Schemata;Schemata;Abonnement;Datentyp;Datentyp;Datentyp;
solution: Experience Platform
title: Datentyp des Abonnements
description: Erfahren Sie mehr über den Datentyp Abonnement-Experience-Datenmodell (XDM).
exl-id: 6fd1e073-441b-45f0-bb4f-54f51ab18694
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 29%

---

# [!UICONTROL Abonnement] Datentyp

[!UICONTROL Subscription] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der lizenzierte Berechtigungen für Software, Services oder Waren beschreibt, die basierend auf Zeit oder Nutzung genutzt werden.

![](../images/data-types/subscription-data-type.png){width=500}

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `device` | [[!UICONTROL Gerät]](./device.md) | Beschreibt Details über das Gerät, das mit dem Abonnement verknüpft ist. |
| `environment` | [[!UICONTROL Umgebung]](./environment.md) | Enthält Informationen über die Umgebungssituation, in der die Ereignisbeobachtung stattgefunden hat, insbesondere mit Details zu vorübergehenden Informationen wie Netzwerk- oder Softwareversionen. |
| `subscriber` | [[!UICONTROL Person]](./person.md) | Beschreibt eine einzelne Person. Dies kann auch eine Person darstellen, die in verschiedenen Rollen agiert, z. B. als Kunde, Kontakt oder Inhaber. |
| `SKU` | String | Die Lagerhaltungseinheit (SKU), eine eindeutige Kennung für ein Produkt. |
| `billingPeriod` | String | Die Zeitdauer zwischen Rechnungen. |
| `billingStartDate` | Datum | Das Datum, an dem die erste Rechnung fällig wird. Das Datumsformat (ohne Zeit) sollte dem Standard [RFC 3339, Abschnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) entsprechen. |
| `category` | String | Die wichtigste, übergeordnete Kategorisierung dieses Abonnementtyps. |
| `chargeMethod` | String | Die Art und Weise, wie die Abrechnung eingerichtet wird, um den Kunden zu belasten. |
| `contractID` | String | Die eindeutige ID für den Vertrag, der für dieses Abonnement gilt. |
| `country` | String | Das Land, in dem die Vertragsbedingungen des Abonnements ihren Ursprung haben. |
| `endDate` | Datum | Das Datum, an dem die aktuelle Abonnementlaufzeit endet. Das Datumsformat (ohne Zeit) sollte dem Standard [RFC 3339, Abschnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) entsprechen. |
| `paymentMethod` | String | Die Zahlungsmethode für wiederkehrende Zahlungen. |
| `paymentStatus` | String | Die Zahlungsfähigkeit des Kontos. |
| `planName` | String | Der für Menschen lesbare Name des Abonnements. |
| `reason` | String | Die allgemeine Absicht, die der Abonnent mit der Verwendung des Abonnements verfolgt. |
| `renew` | String | Die vereinbarte Art und Weise, wie das Abonnement nach dem Enddatum fortgesetzt werden kann. |
| `revision` | String | Die Identifikation zwischen gleichnamigen Abonnements und der Kategoriehierarchie. |
| `startDate` | Datum | Das Datum, an dem das Abonnement beginnt. Das Datumsformat (ohne Zeit) sollte dem Standard [RFC 3339, Abschnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) entsprechen. |
| `status` | String | Der aktuelle Status des Abonnements. |
| `subCategory` | String | Die spezifische Unterkategorie des Abonnements. |
| `term` | Ganzzahl | Der numerische Wert der Abonnementbedingung. |
| `termUnitOfTime` | String | Die Zeiteinheit für den Zeitraum. |
| `topUp` | String | Beschreibt die vereinbarten Bedingungen für den Rückkauf verbrauchbarer Aspekte eines Abonnements während eines Abrechnungszeitraums. |
| `type` | String | Der Umfang der Berechtigungen in Bezug auf die Anzahl der Personen, die im Abonnement enthalten sind. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)
