---
title: XDM Business Campaign-Schema-Feldergruppe "Mitgliederdetails"
description: Dieses Dokument bietet einen Überblick über die Schemakonzerne XDM Business Campaign Member Details .
exl-id: 597629c8-7f41-4c1c-95b6-aed5e16cee72
source-git-commit: 7805e4c45a48070adefbaba25a57140efc3e86b1
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 6%

---

# [!UICONTROL Details zu XDM-Business-Campaign-Mitgliedern] Schemafeldgruppe

[!UICONTROL Details zu XDM-Business-Campaign-Mitgliedern] ist eine Standardschemafeldgruppe für die [[!UICONTROL XDM Business Campaign-Mitglieder] class](../../classes/b2b/business-campaign-members.md), das detaillierte Informationen zu einer Geschäftskampagne erfasst.

![Die Struktur der Feldergruppe &quot;XDM Business Campaign Member Details&quot;, wie sie in der Benutzeroberfläche angezeigt wird](../../images/field-groups/b2b/business-campaign-member-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `acquiredByCampaignKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Die zusammengesetzte ID der Kampagne, die dieses Kampagnenmitglied erworben hat. |
| `acquiredByCampaignID` | [!UICONTROL Zeichenfolge] | Eine Zeichenfolgenkennung für die Kampagne, die dieses Kampagnenmitglied erworben hat. |
| `firstRespondedDate` | [!UICONTROL DateTime] | Ein ISO 8601-Zeitstempel, der angibt, wann die Person zum ersten Mal auf die Kampagne reagiert hat. |
| `hasReachedSuccess` | [!UICONTROL Boolesch] | Gibt an, ob dieses Kampagnenmitglied zu einer erfolgreichen Konvertierung geführt hat. |
| `hasResponded` | [!UICONTROL Boolesch] | Gibt an, ob dieses Kampagnenmitglied auf die Kampagne reagiert hat. |
| `isDeleted` | [!UICONTROL Boolesch] | Gibt an, ob dieses Kampagnenmitglied in Marketo Engage gelöscht wurde.<br><br>Bei Verwendung von [Marketo-Quell-Connector](../../../sources/connectors/adobe-applications/marketo/marketo.md), werden alle in Marketo gelöschten Datensätze automatisch im Echtzeit-Kundenprofil angezeigt. Datensätze, die sich auf diese Profile beziehen, können jedoch im Data Lake bestehen bleiben. Durch Festlegen von `isDeleted` nach `true`können Sie mithilfe des Felds herausfiltern, welche Datensätze bei der Abfrage des Data Lake aus Ihren Quellen gelöscht wurden. |
| `isExhausted` | [!UICONTROL Boolesch] | Gibt an, ob dieses Kampagnenmitglied alle Kampagneninteraktionen ausgeschöpft hat. |
| `lastStatus` | [!UICONTROL Zeichenfolge] | Der letzte Status für das Kampagnenmitglied. |
| `memberStatus` | [!UICONTROL Zeichenfolge] | Der aktuelle Status für das Kampagnenmitglied. |
| `memberStatusReason` | [!UICONTROL Zeichenfolge] | Der Grund für den aktuellen Status des Kampagnenmitglieds. |
| `membershipDate` | [!UICONTROL DateTime] | Der Grund für den aktuellen Status des Kampagnenmitglieds. |
| `nurtureCadence` | [!UICONTROL Zeichenfolge] | Die Zeitspanne, in der dem Kampagnenmitglied kampagnenbezogene Informationen angezeigt werden. |
| `nurtureTrackName` | [!UICONTROL Zeichenfolge] | Der Name des Pflegeprogramms, dem dieses Kampagnenmitglied unterliegt. |
| `reachedSuccessDate` | [!UICONTROL DateTime] | Ein ISO 8601-Zeitstempel für den Zeitpunkt, zu dem eine erfolgreiche Konvertierung für das Kampagnenmitglied durchgeführt wurde. |
| `webinarConfirmationUrl` | [!UICONTROL Zeichenfolge] | Die Webinar-Bestätigungs-URL für das Kampagnenmitglied. |
| `webinarRegistrationID` | [!UICONTROL Zeichenfolge] | Die Webinar-Registrierungs-ID für das Kampagnenmitglied. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.schema.json)
