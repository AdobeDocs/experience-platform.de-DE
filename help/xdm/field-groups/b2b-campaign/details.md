---
title: XDM Business Campaign-Schema-Feldergruppe
description: Dieses Dokument bietet einen Überblick über die Schemakontrollgruppe XDM Business Campaign Details .
exl-id: 3ef6c0b9-cba1-449e-8868-46446c00465f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 7%

---

# [!UICONTROL XDM-Geschäftskampagnendetails] Schemafeldgruppe

[!UICONTROL XDM-Geschäftskampagnendetails] ist eine Standardschemafeldgruppe für die [[!UICONTROL XDM Business Campaign] class](../../classes/b2b/business-campaign.md), das detaillierte Informationen zu einer Geschäftskampagne erfasst.

![Die Struktur der XDM Business Campaign Details -Feldergruppe, wie sie in der Benutzeroberfläche angezeigt wird](../../images/field-groups/b2b/business-campaign-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `actualCost` | [[!UICONTROL Währung]](../../data-types/currency.md) | Stellt die tatsächlichen Kosten der Unternehmenskampagne dar. |
| `budgetedCost` | [[!UICONTROL Währung]](../../data-types/currency.md) | Stellt die budgetierten Kosten der Unternehmenskampagne dar. |
| `expectedRevenue` | [[!UICONTROL Währung]](../../data-types/currency.md) | Stellt den Umsatz dar, den die Geschäftskampagne voraussichtlich generieren wird. |
| `parentCampaignKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Die zusammengesetzte ID für eine übergeordnete Kampagne, falls zutreffend. |
| `campaignEndDate` | [!UICONTROL DateTime] | Ein ISO 8601-Zeitstempel, der angibt, wann die Kampagne beendet wurde oder beendet wird. |
| `campaignProgressionName` | [!UICONTROL String] | Der Name des Kampagnenfortschritts. |
| `campaignStartDate` | [!UICONTROL DateTime] | Ein ISO 8601-Zeitstempel, der angibt, wann die Kampagne gestartet wurde oder beginnt. |
| `campaignStatus` | [!UICONTROL String] | Der aktuelle Status der Kampagne. |
| `channelName` | [!UICONTROL String] | Der Name des mit dieser Kampagne verknüpften Kanals. |
| `expectedResponse` | [!UICONTROL String] | Die erwartete Antwort für die Kampagne. |
| `integrationPartnerName` | [!UICONTROL String] | Der Name des Partners, der in diese Kampagne integriert hat. |
| `isActive` | [!UICONTROL Boolesch] | Gibt an, ob diese Kampagne aktiv ist. |
| `isDeleted` | [!UICONTROL Boolesch] | Gibt an, ob diese Kampagne in Marketo Engage gelöscht wurde.<br><br>Bei Verwendung von [Marketo-Quell-Connector](../../../sources/connectors/adobe-applications/marketo/marketo.md), werden alle in Marketo gelöschten Datensätze automatisch in das Echtzeit-Kundenprofil übernommen. Datensätze, die sich auf diese Profile beziehen, können jedoch im Data Lake bestehen bleiben. Durch Festlegen von `isDeleted` nach `true`können Sie mithilfe des Felds herausfiltern, welche Datensätze bei der Abfrage des Data Lake aus Ihren Quellen gelöscht wurden. |
| `lastActivityDate` | [!UICONTROL DateTime] | Ein ISO 8601-Zeitstempel der letzten mit der Kampagne verknüpften Aktivität. |
| `timeZone` | [!UICONTROL String] | Die Zeitzone, in der die Kampagne ausgeführt wird. |
| `timeZoneDelivery` | [!UICONTROL String] | Die Zeitzone des Versands, in der die Kampagne ausgeführt wird. |
| `timeZoneName` | [!UICONTROL String] | Der Name der Zeitzone, in der die Kampagne ausgeführt wird. |
| `webinarHistorySyncDate` | [!UICONTROL DateTime] | Ein ISO 8601-Zeitstempel der letzten Synchronisation des Webinarverlaufs für diese Kampagne. |
| `webinarHistorySyncStatus` | [!UICONTROL String] | Der Status der Synchronisation des Webinarverlaufs für diese Kampagne. |
| `webinarSessionDescription` | [!UICONTROL String] | Eine Beschreibung der mit dieser Kampagne verknüpften Webinarsitzung. |
| `webinarSessionName` | [!UICONTROL String] | Ein Name der Webinar-Sitzung, die mit dieser Kampagne verbunden ist. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im Abschnitt [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign/campaign-details.schema.json).
