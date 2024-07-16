---
title: XDM Business Campaign-Schema-Feldergruppe
description: Erfahren Sie mehr über die Schemafeldgruppe XDM Business Campaign Details .
exl-id: 3ef6c0b9-cba1-449e-8868-46446c00465f
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 5%

---

# Schemafeldgruppe [!UICONTROL XDM Business Campaign Details]

[!UICONTROL XDM Business Campaign Details der Geschäftskampagne] ist eine Standardschemafeldgruppe für die [[!UICONTROL XDM Business Campaign] -Klasse](../../classes/b2b/business-campaign.md), die detaillierte Informationen zu einer Geschäftskampagne erfasst.

![Die Struktur der XDM Business Campaign Details-Feldergruppe, wie sie in der Benutzeroberfläche angezeigt wird](../../images/field-groups/b2b/business-campaign-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `actualCost` | [[!UICONTROL Währung]](../../data-types/currency.md) | Stellt die tatsächlichen Kosten der Unternehmenskampagne dar. |
| `budgetedCost` | [[!UICONTROL Währung]](../../data-types/currency.md) | Stellt die budgetierten Kosten der Unternehmenskampagne dar. |
| `expectedRevenue` | [[!UICONTROL Währung]](../../data-types/currency.md) | Stellt den Umsatz dar, den die Geschäftskampagne voraussichtlich generieren wird. |
| `parentCampaignKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Die zusammengesetzte ID einer übergeordneten Kampagne, falls zutreffend. |
| `campaignEndDate` | [!UICONTROL DateTime] | Ein ISO 8601-Zeitstempel, der angibt, wann die Kampagne beendet wurde oder beendet wird. |
| `campaignProgressionName` | [!UICONTROL String] | Der Name des Kampagnenfortschritts. |
| `campaignStartDate` | [!UICONTROL DateTime] | Ein ISO 8601-Zeitstempel, der angibt, wann die Kampagne gestartet wurde oder beginnt. |
| `campaignStatus` | [!UICONTROL String] | Der aktuelle Status der Kampagne. |
| `channelName` | [!UICONTROL String] | Der Name des dieser Kampagne zugeordneten Kanals. |
| `expectedResponse` | [!UICONTROL String] | Die erwartete Antwort für die Kampagne. |
| `integrationPartnerName` | [!UICONTROL String] | Der Name des Partners, der in diese Kampagne integriert hat. |
| `isActive` | [!UICONTROL Boolean] | Gibt an, ob diese Kampagne aktiv ist. |
| `isDeleted` | [!UICONTROL Boolean] | Gibt an, ob diese Kampagne im Marketo Engage gelöscht wurde.<br><br>Bei Verwendung des [Marketo-Quell-Connectors](../../../sources/connectors/adobe-applications/marketo/marketo.md) werden alle in Marketo gelöschten Datensätze automatisch im Echtzeit-Kundenprofil angezeigt. Datensätze, die sich auf diese Profile beziehen, können jedoch im Data Lake bestehen bleiben. Durch Festlegen von `isDeleted` auf `true` können Sie mithilfe des Felds herausfiltern, welche Datensätze bei der Abfrage des Data Lake aus Ihren Quellen gelöscht wurden. |
| `lastActivityDate` | [!UICONTROL DateTime] | Ein ISO 8601-Zeitstempel der letzten mit der Kampagne verknüpften Aktivität. |
| `timeZone` | [!UICONTROL String] | Die Zeitzone, in der die Kampagne ausgeführt wird. |
| `timeZoneDelivery` | [!UICONTROL String] | Die Zeitzone des Versands, in der die Kampagne ausgeführt wird. |
| `timeZoneName` | [!UICONTROL String] | Der Name der Zeitzone, in der die Kampagne ausgeführt wird. |
| `webinarHistorySyncDate` | [!UICONTROL DateTime] | Ein ISO 8601-Zeitstempel der letzten Synchronisation des Webinarverlaufs für diese Kampagne. |
| `webinarHistorySyncStatus` | [!UICONTROL String] | Der Status der Synchronisation des Webinarverlaufs für diese Kampagne. |
| `webinarSessionDescription` | [!UICONTROL String] | Eine Beschreibung der mit dieser Kampagne verknüpften Webinarsitzung. |
| `webinarSessionName` | [!UICONTROL String] | Ein Name der Webinar-Sitzung, die mit dieser Kampagne verbunden ist. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im [öffentlichen XDM-Repository](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign/campaign-details.schema.json).
