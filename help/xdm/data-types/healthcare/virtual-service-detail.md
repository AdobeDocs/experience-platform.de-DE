---
title: Detaildatentyp "Virtueller Dienst"
description: Erfahren Sie mehr über den Datentyp des Experience-Datenmodells (XDM) für Virtual Service-Details.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 5%

---

# Datentyp [!UICONTROL Virtual Service Detail]

[!UICONTROL Virtual Service Detail] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Kontaktdetails für virtuelle Dienste beschreibt. Dieser Datentyp wird gemäß den Spezifikationen von HL7 FHIR Release 5 erstellt.

![Datenstruktur des Virtual Service-Detaildatentyps](../../images/data-types/healthcare/virtual-service-detail.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Kontaktpunkt der Adresse] | `addressContactPoint` | [[!UICONTROL Kontaktpunkt]](../healthcare/contact-point.md) | Die Details eines technologievermittelten Kontaktpunkts wie Telefon, Fax oder E-Mail. |
| [!UICONTROL Adresse - Erweiterte Kontaktdetails] | `addressExtendedContactDetail` | [[!UICONTROL Erweiterte Kontaktdetails]](../healthcare/extended-contact-detail.md) | Erweiterte Kontaktinformationen. |
| [!UICONTROL Kanaltyp] | `channelType` | [[!UICONTROL Kodierung]](../healthcare/coding.md) | Der Typ des virtuellen Dienstes, mit dem eine Verbindung hergestellt werden soll, z. B. Teams, Zoom oder WhatApp. |
| [!UICONTROL Zusätzliche Informationen] | `additionalInfo` | Zeichenfolgen-Array | Die Adresse, an die alternative Verbindungsdetails angezeigt werden sollen, dargestellt als URI. |
| [!UICONTROL Adresszeichenfolge] | `addressString` | String | Die Adresse, unter der eine Verbindung zum virtuellen Dienst hergestellt wird. |
| [!UICONTROL URL der Adresse] | `addressUrl` | String | Die URL, die für die Verbindung mit dem virtuellen Dienst verwendet werden soll, dargestellt als URI. |
| [!UICONTROL Max Participants] | `maxParticipants` | Ganzzahl | Die maximale Anzahl der unterstützten Teilnehmer mit einem Mindestwert von `0`. |
| [!UICONTROL Sitzungsschlüssel] | `sessionKey` | String | Der für den virtuellen Dienst erforderliche Sitzungsschlüssel. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.schema.json)
