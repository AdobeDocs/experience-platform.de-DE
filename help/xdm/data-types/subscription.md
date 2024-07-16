---
keywords: Experience Platform; home; beliebte Themen; schema; XDM; Felder; Schemas; Schemas; Abonnement; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Abonnementdatentyp
description: Erfahren Sie mehr über den Datentyp des Abonnement-Experience-Datenmodells (XDM).
exl-id: 6fd1e073-441b-45f0-bb4f-54f51ab18694
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 29%

---

# Datentyp [!UICONTROL Abonnement]

[!UICONTROL Abonnement] ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der lizenzierte Berechtigungen für Software, Dienste oder Güter beschreibt, die basierend auf der Zeit oder Verwendung verwendet werden.

<img src="../images/data-types/subscription-data-type.png" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `device` | [[!UICONTROL Gerät]](./device.md) | Beschreibt Details zu dem Gerät, das mit dem Abonnement verknüpft ist. |
| `environment` | [[!UICONTROL Umgebung]](./environment.md) | Enthält Informationen über die Umgebungssituation, in der das Ereignis beobachtet wurde, insbesondere Informationen zu vorübergehenden Informationen wie Netzwerk- oder Softwareversionen. |
| `subscriber` | [[!UICONTROL Person]](./person.md) | Beschreibt eine Person. Dabei kann es sich auch um eine Person handeln, die in verschiedenen Rollen agiert, z. B. Kunde, Kontakt oder Eigentümer. |
| `SKU` | Zeichenfolge | Die Bestandseinheit (Stock-Management Unit, SKU), eine eindeutige Kennung für ein Produkt. |
| `billingPeriod` | Zeichenfolge | Die Zeitdauer zwischen Rechnungen. |
| `billingStartDate` | Datum | Das Datum, an dem die erste Rechnung fällig wird. Das Datumsformat (ohne Uhrzeit) sollte dem Standard [RFC 3339, Abschnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) entsprechen. |
| `category` | Zeichenfolge | Die wichtigste Kategorisierung dieser Art von Abonnement auf oberster Ebene. |
| `chargeMethod` | Zeichenfolge | Die Art und Weise, wie die Abrechnung eingerichtet ist, um den Kunden zu belasten. |
| `contractID` | Zeichenfolge | Die eindeutige ID für den Vertrag, der für dieses Abonnement gilt. |
| `country` | Zeichenfolge | Das Land, in dem die Vertragsbedingungen des Abonnements ihren Ursprung haben. |
| `endDate` | Datum | Das Datum, an dem der aktuelle Abonnementzeitraum endet. Das Datumsformat (ohne Uhrzeit) sollte dem Standard [RFC 3339, Abschnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) entsprechen. |
| `paymentMethod` | Zeichenfolge | Die Zahlungsmethode für wiederkehrende Zahlungen. |
| `paymentStatus` | Zeichenfolge | Die Zahlungsbilanz des Kontos. |
| `planName` | Zeichenfolge | Der für Menschen lesbare Name des Abonnements. |
| `reason` | Zeichenfolge | Die allgemeine Absicht, die der Abonnent mit der Verwendung des Abonnements verfolgt. |
| `renew` | Zeichenfolge | Die vereinbarte Art und Weise, wie das Abonnement nach dem Enddatum fortgesetzt werden kann. |
| `revision` | Zeichenfolge | Die Identifikation zwischen gleichnamigen Abonnements und der Kategoriehierarchie. |
| `startDate` | Datum | Das Datum, an dem das Abonnement beginnt. Das Datumsformat (ohne Uhrzeit) sollte dem Standard [RFC 3339, Abschnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) entsprechen. |
| `status` | Zeichenfolge | Der aktuelle Status des Abonnements. |
| `subCategory` | Zeichenfolge | Die spezifische Unterkategorisierung des Abonnements. |
| `term` | Ganzzahl | Der numerische Wert des Abonnementbegriffs. |
| `termUnitOfTime` | Zeichenfolge | Die Zeiteinheit für den Zeitraum. |
| `topUp` | Zeichenfolge | Beschreibt die vereinbarten Bedingungen dafür, wie verbrauchbare Aspekte eines Abonnements während eines Abrechnungszeitraums zurückgekauft werden. |
| `type` | Zeichenfolge | Der Umfang der Berechtigungen in Bezug auf die Anzahl der Personen, die im Abonnement enthalten sind. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)
