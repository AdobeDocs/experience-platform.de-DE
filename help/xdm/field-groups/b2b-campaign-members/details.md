---
title: XDM Business Campaign-Schema-Feldergruppe "Mitgliederdetails"
description: Erfahren Sie mehr über die Schemafeldgruppe XDM Business Campaign Member Details .
exl-id: 597629c8-7f41-4c1c-95b6-aed5e16cee72
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 3%

---

# Schemafeldgruppe [!UICONTROL XDM Business Campaign Member Details]

[!UICONTROL XDM Business Campaign Member Details] ist eine Standardschemafeldgruppe für die [[!UICONTROL XDM Business Campaign Members] class](../../classes/b2b/business-campaign-members.md) , die detaillierte Informationen zu einer Geschäftskampagne erfasst.

![Die Struktur der XDM Business Campaign Member Details -Feldergruppe, wie sie in der Benutzeroberfläche angezeigt wird](../../images/field-groups/b2b/business-campaign-member-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `acquiredByCampaignKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Die zusammengesetzte ID der Kampagne, die dieses Kampagnenmitglied erworben hat. |
| `acquiredByCampaignID` | [!UICONTROL String] | Eine Zeichenfolgenkennung für die Kampagne, die dieses Kampagnenmitglied erworben hat. |
| `firstRespondedDate` | [!UICONTROL DateTime] | Ein ISO 8601-Zeitstempel, der angibt, wann die Person zum ersten Mal auf die Kampagne reagiert hat. |
| `hasReachedSuccess` | [!UICONTROL Boolean] | Gibt an, ob dieses Kampagnenmitglied zu einer erfolgreichen Konvertierung geführt hat. |
| `hasResponded` | [!UICONTROL Boolean] | Gibt an, ob dieses Kampagnenmitglied auf die Kampagne reagiert hat. |
| `isDeleted` | [!UICONTROL Boolean] | Gibt an, ob dieses Kampagnenmitglied unter Marketo Engage gelöscht wurde.<br><br>Bei Verwendung des [Marketo-Quell-Connectors](../../../sources/connectors/adobe-applications/marketo/marketo.md) werden alle in Marketo gelöschten Datensätze automatisch im Echtzeit-Kundenprofil angezeigt. Datensätze, die sich auf diese Profile beziehen, können jedoch im Data Lake bestehen bleiben. Durch Festlegen von `isDeleted` auf `true` können Sie mithilfe des Felds herausfiltern, welche Datensätze bei der Abfrage des Data Lake aus Ihren Quellen gelöscht wurden. |
| `isExhausted` | [!UICONTROL Boolean] | Gibt an, ob dieses Kampagnenmitglied alle Kampagneninteraktionen ausgeschöpft hat. |
| `lastStatus` | [!UICONTROL String] | Der letzte Status für das Kampagnenmitglied. |
| `memberStatus` | [!UICONTROL String] | Der aktuelle Status für das Kampagnenmitglied. |
| `memberStatusReason` | [!UICONTROL String] | Der Grund für den aktuellen Status des Kampagnenmitglieds. |
| `membershipDate` | [!UICONTROL DateTime] | Der Grund für den aktuellen Status des Kampagnenmitglieds. |
| `nurtureCadence` | [!UICONTROL String] | Die Zeitspanne, in der dem Kampagnenmitglied kampagnenbezogene Informationen angezeigt werden. |
| `nurtureTrackName` | [!UICONTROL String] | Der Name des Pflegeprogramms, dem dieses Kampagnenmitglied unterliegt. |
| `reachedSuccessDate` | [!UICONTROL DateTime] | Ein ISO 8601-Zeitstempel für den Zeitpunkt, zu dem eine erfolgreiche Konvertierung für das Kampagnenmitglied durchgeführt wurde. |
| `webinarConfirmationUrl` | [!UICONTROL String] | Die Webinar-Bestätigungs-URL für das Kampagnenmitglied. |
| `webinarRegistrationID` | [!UICONTROL String] | Die Webinar-Registrierungs-ID für das Kampagnenmitglied. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.schema.json)
