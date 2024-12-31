---
title: Schemafeldgruppe „XDM Business Campaign Member Details“
description: Erfahren Sie mehr über die Schemafeldgruppe „XDM Business Campaign Member Details“.
exl-id: 597629c8-7f41-4c1c-95b6-aed5e16cee72
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 3%

---

# [!UICONTROL XDM Business Campaign Member Details] Schemafeldgruppe

[!UICONTROL XDM Business Campaign Member Details] ist eine Standardschemafeldgruppe für die Klasse [[!UICONTROL XDM Business Campaign Members], ](../../classes/b2b/business-campaign-members.md) detaillierte Informationen über eine Unternehmenskampagne erfasst.

![Die Struktur der Feldergruppe „XDM Business Campaign Member Details“, wie sie in der Benutzeroberfläche angezeigt wird](../../images/field-groups/b2b/business-campaign-member-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `acquiredByCampaignKey` | [[!UICONTROL B2B-Source]](../../data-types/b2b-source.md) | Die zusammengesetzte ID der Kampagne, die dieses Kampagnenmitglied erworben hat. |
| `acquiredByCampaignID` | [!UICONTROL String] | Eine Zeichenfolgenkennung für die Kampagne, die dieses Kampagnenmitglied erworben hat. |
| `firstRespondedDate` | [!UICONTROL DateTime] | Ein ISO 8601-Zeitstempel, der angibt, wann die Person zum ersten Mal auf die Kampagne reagiert hat. |
| `hasReachedSuccess` | [!UICONTROL Boolesch] | Gibt an, ob dieses Kampagnenmitglied zu einer erfolgreichen Konversion geführt hat. |
| `hasResponded` | [!UICONTROL Boolesch] | Gibt an, ob dieses Kampagnenmitglied auf die Kampagne reagiert hat. |
| `isDeleted` | [!UICONTROL Boolesch] | Gibt an, ob dieses Kampagnenmitglied auf Marketo Engage gelöscht wurde.<br><br>Bei Verwendung des [Marketo-Quell](../../../sources/connectors/adobe-applications/marketo/marketo.md)Connectors werden alle in Marketo gelöschten Datensätze automatisch im Echtzeit-Kundenprofil angezeigt. Datensätze, die sich auf diese Profile beziehen, können jedoch weiterhin im Data Lake vorhanden sein. Wenn Sie `isDeleted` auf `true` setzen, können Sie das Feld verwenden, um herauszufiltern, welche Datensätze aus Ihren Quellen gelöscht wurden, wenn Sie den Data Lake abfragen. |
| `isExhausted` | [!UICONTROL Boolesch] | Gibt an, ob dieses Kampagnenmitglied alle Kampagneninteraktionen ausgeschöpft hat. |
| `lastStatus` | [!UICONTROL String] | Der letzte Status für das Kampagnenmitglied. |
| `memberStatus` | [!UICONTROL String] | Der aktuelle Status für das Kampagnenmitglied. |
| `memberStatusReason` | [!UICONTROL String] | Der Grund für den aktuellen Status des Kampagnenmitglieds. |
| `membershipDate` | [!UICONTROL DateTime] | Der Grund für den aktuellen Status des Kampagnenmitglieds. |
| `nurtureCadence` | [!UICONTROL String] | Der Zeitraum, in dem kampagnenbezogene Informationen dem Kampagnenmitglied angezeigt werden. |
| `nurtureTrackName` | [!UICONTROL String] | Der Name des Pflegeprogramms, dem dieses Kampagnenmitglied unterliegt. |
| `reachedSuccessDate` | [!UICONTROL DateTime] | Ein ISO 8601-Zeitstempel für den Zeitpunkt, zu dem eine erfolgreiche Konversion für das Kampagnenmitglied durchgeführt wurde. |
| `webinarConfirmationUrl` | [!UICONTROL String] | Die Webinar-Bestätigungs-URL für das Kampagnenmitglied. |
| `webinarRegistrationID` | [!UICONTROL String] | Die Webinar-Registrierungs-ID für das Kampagnenmitglied. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.schema.json)
