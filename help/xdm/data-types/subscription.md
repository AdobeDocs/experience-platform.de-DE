---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Abonnement; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Abonnementdatentyp
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über den Datentyp "Abonnement-Experience-Datenmodell (XDM)".
exl-id: 6fd1e073-441b-45f0-bb4f-54f51ab18694
source-git-commit: d99ddc65849a88350bf61977b399b07989554426
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 28%

---

# [!UICONTROL Abonnement] Datentyp

[!UICONTROL Abonnement] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der lizenzierte Berechtigungen für Software, Dienste oder Güter beschreibt, die basierend auf der Zeit oder Nutzung verwendet werden.

<img src="../images/data-types/subscription-data-type.png" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `device` | [[!UICONTROL Gerät]](./device.md) | Beschreibt Details zu dem Gerät, das mit dem Abonnement verknüpft ist. |
| `environment` | [[!UICONTROL Umgebung]](./environment.md) | Enthält Informationen über die Umgebungssituation, in der das Ereignis beobachtet wurde, insbesondere Informationen zu vorübergehenden Informationen wie Netzwerk- oder Softwareversionen. |
| `subscriber` | [[!UICONTROL Person]](./person.md) | Beschreibt eine Person. Dabei kann es sich auch um eine Person handeln, die in verschiedenen Rollen agiert, z. B. Kunde, Kontakt oder Eigentümer. |
| `SKU` | Zeichenfolge | Die Bestandseinheit (Stock-Management Unit, SKU), eine eindeutige Kennung für ein Produkt. |
| `billingPeriod` | Zeichenfolge | Die Zeitdauer zwischen Rechnungen. |
| `billingStartDate` | Datum | Das Datum, an dem die erste Rechnung fällig wird. Das Datumsformat (ohne Uhrzeit) sollte dem [RFC 3339, Abschnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) Standard. |
| `category` | Zeichenfolge | Die wichtigste Kategorisierung dieser Art von Abonnement auf oberster Ebene. |
| `chargeMethod` | Zeichenfolge | Die Art und Weise, wie die Abrechnung eingerichtet ist, um den Kunden zu belasten. |
| `contractID` | Zeichenfolge | Die eindeutige ID für den Vertrag, der für dieses Abonnement gilt. |
| `country` | Zeichenfolge | Das Land, in dem die vertraglichen und vertraglichen Bedingungen der Abonnements verwurzelt sind. |
| `endDate` | Datum | Das Datum, an dem das aktuelle Abonnement endet. Das Datumsformat (ohne Uhrzeit) sollte dem [RFC 3339, Abschnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) Standard. |
| `paymentMethod` | Zeichenfolge | Die Zahlungsmethode für wiederkehrende Zahlungen. |
| `paymentStatus` | Zeichenfolge | Die Zahlungsbilanz des Kontos. |
| `planName` | Zeichenfolge | Der für Menschen lesbare Name des Abonnements. |
| `reason` | Zeichenfolge | Die allgemeine Absicht des Mitglieds für die Verwendung des Abonnements. |
| `renew` | Zeichenfolge | Die vereinbarte Art und Weise, wie das Abonnement nach dem Enddatum fortgesetzt werden kann. |
| `revision` | Zeichenfolge | Die Identifikation zwischen gleichnamigen Abonnements und der Kategoriehierarchie. |
| `startDate` | Datum | Das Datum, an dem das Abonnement beginnt. Das Datumsformat (ohne Uhrzeit) sollte dem [RFC 3339, Abschnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) Standard. |
| `status` | Zeichenfolge | Der aktuelle Status des Abonnements. |
| `subCategory` | Zeichenfolge | Die spezifische Unterkategorisierung des Abonnements. |
| `term` | Ganzzahl | Der numerische Wert des Abonnementbegriffs. |
| `termUnitOfTime` | Zeichenfolge | Die Zeiteinheit für den Zeitraum. |
| `topUp` | Zeichenfolge | Beschreibt die vereinbarten Bedingungen dafür, wie verbrauchbare Aspekte eines Abonnements während eines Abrechnungszeitraums zurückgekauft werden. |
| `type` | Zeichenfolge | Der Umfang des Anspruchs in Bezug auf die Anzahl der Personen, die vom Abonnement abgedeckt werden. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)
