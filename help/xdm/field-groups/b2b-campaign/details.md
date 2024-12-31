---
title: Schemafeldgruppe „XDM Business Campaign Details“
description: Erfahren Sie mehr über die Schemafeldgruppe „XDM Business Campaign Details“.
exl-id: 3ef6c0b9-cba1-449e-8868-46446c00465f
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 5%

---

# [!UICONTROL XDM Business Campaign Details] Schemafeldgruppe

[!UICONTROL XDM Business Campaign Details] ist eine Standardschemafeldgruppe für die [[!UICONTROL XDM Business Campaign]-Klasse](../../classes/b2b/business-campaign.md) die detaillierte Informationen über eine Unternehmenskampagne erfasst.

![Die Struktur der Feldergruppe „XDM Business Campaign Details“, wie sie in der Benutzeroberfläche angezeigt wird](../../images/field-groups/b2b/business-campaign-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `actualCost` | [[!UICONTROL Währung]](../../data-types/currency.md) | Stellt die tatsächlichen Kosten der Unternehmenskampagne dar. |
| `budgetedCost` | [[!UICONTROL Währung]](../../data-types/currency.md) | Stellt die budgetierten Kosten der Geschäftskampagne dar. |
| `expectedRevenue` | [[!UICONTROL Währung]](../../data-types/currency.md) | Stellt den Umsatz dar, den die Geschäftskampagne voraussichtlich generieren wird. |
| `parentCampaignKey` | [[!UICONTROL B2B-Source]](../../data-types/b2b-source.md) | Die zusammengesetzte ID für eine übergeordnete Kampagne, falls zutreffend. |
| `campaignEndDate` | [!UICONTROL DateTime] | Ein ISO 8601-Zeitstempel, der angibt, wann die Kampagne beendet wurde oder endet. |
| `campaignProgressionName` | [!UICONTROL String] | Der Name des Kampagnenverlaufs. |
| `campaignStartDate` | [!UICONTROL DateTime] | Ein ISO 8601-Zeitstempel, der angibt, wann die Kampagne gestartet wurde oder beginnen wird. |
| `campaignStatus` | [!UICONTROL String] | Der aktuelle Status der Kampagne. |
| `channelName` | [!UICONTROL String] | Der Name des Kanals, der mit dieser Kampagne verknüpft ist. |
| `expectedResponse` | [!UICONTROL String] | Die erwartete Antwort für die Kampagne. |
| `integrationPartnerName` | [!UICONTROL String] | Der Name des Partners, der sich in diese Kampagne integriert hat. |
| `isActive` | [!UICONTROL Boolesch] | Gibt an, ob diese Kampagne aktiv ist. |
| `isDeleted` | [!UICONTROL Boolesch] | Gibt an, ob diese Kampagne auf Marketo Engage gelöscht wurde.<br><br>Bei Verwendung des [Marketo-Quell](../../../sources/connectors/adobe-applications/marketo/marketo.md)Connectors werden alle in Marketo gelöschten Datensätze automatisch im Echtzeit-Kundenprofil angezeigt. Datensätze, die sich auf diese Profile beziehen, können jedoch weiterhin im Data Lake vorhanden sein. Wenn Sie `isDeleted` auf `true` setzen, können Sie das Feld verwenden, um herauszufiltern, welche Datensätze aus Ihren Quellen gelöscht wurden, wenn Sie den Data Lake abfragen. |
| `lastActivityDate` | [!UICONTROL DateTime] | Ein ISO 8601-Zeitstempel der letzten Aktivität, die mit der Kampagne verknüpft ist. |
| `timeZone` | [!UICONTROL String] | Die Zeitzone, in der die Kampagne ausgeführt wird. |
| `timeZoneDelivery` | [!UICONTROL String] | Die Zeitzone des Versands, in der die Kampagne ausgeführt wird. |
| `timeZoneName` | [!UICONTROL String] | Der Name der Zeitzone, in der die Kampagne ausgeführt wird. |
| `webinarHistorySyncDate` | [!UICONTROL DateTime] | Ein ISO 8601-Zeitstempel der letzten Webinar-Verlaufssynchronisierung für diese Kampagne. |
| `webinarHistorySyncStatus` | [!UICONTROL String] | Der Status der Webinar-Verlaufssynchronisierung für diese Kampagne. |
| `webinarSessionDescription` | [!UICONTROL String] | Eine Beschreibung der Webinar-Sitzung, die mit dieser Kampagne verbunden ist. |
| `webinarSessionName` | [!UICONTROL String] | Ein Name der Webinar-Sitzung, die mit dieser Kampagne verknüpft ist. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie unter [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign/campaign-details.schema.json).
