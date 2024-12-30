---
title: Virtueller Service - Detaildatentyp
description: Erfahren Sie mehr über den Datentyp Virtual Service Detail Experience Data Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: bde7363c-43b7-402d-96b2-7aa0160cd2ea
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 5%

---

# [!UICONTROL Virtual Service Detail] Datentyp

[!UICONTROL Virtual Service Detail] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der die Kontaktdetails des virtuellen Services beschreibt. Dieser Datentyp wird gemäß den HL7 FHIR Release 5-Spezifikationen erstellt.

![Datentypstruktur „Virtual Service Detail“](../../../images/healthcare/data-types/virtual-service-detail.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Adresse Kontaktstelle] | `addressContactPoint` | [[!UICONTROL Kontaktstelle]](../data-types/contact-point.md) | Die Details einer technologievermittelten Kontaktstelle, z. B. Telefon, Fax oder E-Mail. |
| [!UICONTROL Erweiterte Kontaktdaten der Adresse] | `addressExtendedContactDetail` | [[!UICONTROL Erweiterte Kontaktdetails]](../data-types/extended-contact-detail.md) | Erweiterte Kontaktinformationen. |
| [!UICONTROL Kanaltyp] | `channelType` | [[!UICONTROL Kodierung]](../data-types/coding.md) | Der Typ des virtuellen Services, mit dem eine Verbindung hergestellt werden soll, z. B. Teams, Zoom oder WhatsApp. |
| [!UICONTROL Zusätzliche Informationen] | `additionalInfo` | Zeichenfolgen-Array | Die Adresse, an die alternative Verbindungsdetails, dargestellt als URI, angezeigt werden. |
| [!UICONTROL Adresszeichenfolge] | `addressString` | String | Die Adresse, die für die Verbindung mit dem virtuellen Service verwendet werden soll. |
| [!UICONTROL Adresse URL] | `addressUrl` | String | Die URL, die für die Verbindung mit dem virtuellen Service verwendet werden soll und als URI dargestellt wird. |
| [!UICONTROL Max Teilnehmer] | `maxParticipants` | Ganzzahl | Die maximale Anzahl der unterstützten Teilnehmer mit einem Mindestwert von `0`. |
| [!UICONTROL Sitzungsschlüssel] | `sessionKey` | String | Der für den virtuellen Service erforderliche Sitzungsschlüssel. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.schema.json)
