---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;Felder;Schemas;Schemas;Abonnement;Datentyp;Datentyp; Datentyp;
solution: Experience Platform
title: Abonnement-Datentyp
topic-legacy: overview
description: Dieses Dokument bietet eine Übersicht über den Datentyp des Abonnement Experience Data Model (XDM).
exl-id: 6fd1e073-441b-45f0-bb4f-54f51ab18694
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 27%

---

#  Abonnementdatentyp

[!UICONTROL &quot;] Abonnement&quot;ist ein standardmäßiger XDM-Datentyp (Experience Data Model), der lizenzierte Berechtigungen für Software, Dienste oder Güter beschreibt, die basierend auf der Zeit oder Verwendung verwendet werden.

<img src="../images/data-types/subscription-data-type.png" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `device` | [[!UICONTROL Gerät]](./device.md) | Beschreibt Details zum Gerät, das mit dem Abonnement verknüpft ist. |
| `environment` | [[!UICONTROL Umgebung]](./environment.md) | Enthält Informationen über die Umgebung, in der das Ereignis beobachtet wurde, insbesondere Informationen über vorübergehende Informationen wie Netzwerk- oder Softwareversionen. |
| `subscriber` | [[!UICONTROL Person]](./person.md) | Beschreibt eine einzelne Person. Dies kann auch eine Person darstellen, die in verschiedenen Rollen handelt, z. B. ein Kunde, ein Kontakt oder ein Eigentümer. |
| `SKU` | Zeichenfolge | Die Bestandsbuchhaltungseinheit (SKU), eine eindeutige Kennung für ein Produkt. |
| `billingPeriod` | Zeichenfolge | Die Zeitdauer zwischen Rechnungen. |
| `billingStartDate` | Datum | Das Datum, an dem die erste Rechnung fällig wird. Das Datumsformat (ohne Uhrzeit) sollte dem Standard [RFC 3339, Abschnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) entsprechen. |
| `category` | Zeichenfolge | Die wichtigste Kategorisierung dieser Art von Abonnement auf oberster Ebene. |
| `chargeMethod` | Zeichenfolge | Die Art und Weise, wie die Abrechnung eingerichtet wird, um den Kunden zu belasten. |
| `contractID` | Zeichenfolge | Die eindeutige ID für den Vertrag, der für dieses Abonnement gilt. |
| `country` | Zeichenfolge | Das Land, in dem die vertraglichen und vertraglichen Bedingungen des Abonnements verwurzelt sind. |
| `endDate` | Datum | Das Datum, an dem das aktuelle Abonnement endet. Das Datumsformat (ohne Uhrzeit) sollte dem Standard [RFC 3339, Abschnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) entsprechen. |
| `paymentMethod` | Zeichenfolge | Die Zahlungsmethode für wiederkehrende Zahlungen. |
| `paymentStatus` | Zeichenfolge | Die Zahlungsfähigkeit des Kontos. |
| `planName` | Zeichenfolge | Der für Menschen lesbare Name des Abonnements. |
| `reason` | Zeichenfolge | Die allgemeine Absicht des Mitglieds für die Verwendung des Abonnements. |
| `renew` | Zeichenfolge | Die vereinbarte Art und Weise, wie das Abonnement nach dem Enddatum fortgesetzt werden kann. |
| `revision` | Zeichenfolge | Die Identifikation zwischen gleichnamigen Abonnements und der Kategoriehierarchie. |
| `startDate` | Datum | Das Datum, an dem das Abonnement beginnt. Das Datumsformat (ohne Uhrzeit) sollte dem Standard [RFC 3339, Abschnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) entsprechen. |
| `status` | Zeichenfolge | Der aktuelle Status des Abonnements. |
| `subCategory` | Zeichenfolge | Die spezifische Unterkategorisierung des Abonnements. |
| `term` | Ganzzahl | Der numerische Wert des Abonnement-Begriffs. |
| `termUnitOfTime` | Zeichenfolge | Die Zeiteinheit für den Zeitraum. |
| `topUp` | Zeichenfolge | Beschreibt die vereinbarten Bedingungen für den Rückkauf verbrauchbarer Aspekte eines Abonnements während eines Abrechnungszeitraums. |
| `type` | Zeichenfolge | Der Umfang des Anspruchs in Bezug auf die Anzahl der Personen, die unter das Abonnement fallen. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)
