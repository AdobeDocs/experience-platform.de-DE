---
title: XDM Business Campaign-Klasse
description: Erfahren Sie mehr über die Klasse „XDM Business Campaign“ im Experience-Datenmodell (XDM).
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 3%

---

# [!UICONTROL XDM Business Campaign]-Klasse

>[!IMPORTANT]
>
>Diese Klasse ist für die Verwendung durch Organisationen vorgesehen, die Zugriff auf [Adobe Real-time Customer Data Platform B2B edition](../../../rtcdp/b2b-overview.md) haben. Sie müssen Zugriff auf Real-Time CDP B2B edition haben, damit diese Klasse am Echtzeit[Kundenprofil teilnehmen ](../../../profile/home.md).

[!UICONTROL XDM Business Campaign] ist eine Standardklasse des Experience-Datenmodells (XDM), die die erforderlichen Mindesteigenschaften einer Unternehmenskampagne erfasst.

![Die Struktur der Klasse XDM Business Campaign , wie sie in der Benutzeroberfläche angezeigt wird](../../images/classes/b2b/business-campaign.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B-Source]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Kampagnenentität. |
| `extSourceSystemAudit` | [[!UICONTROL Audit-Attribute des externen Source-Systems]](../../data-types/external-source-system-audit-attributes.md) | Wenn die Kampagne von einem externen Quellsystem stammt, erfasst dieses Objekt Audit-Attribute für dieses System. |
| `_id` | String | Eine eindeutige Kennung für den Datensatz. Dies ist ein vom System generierter Wert, der vom `campaignID` getrennt ist. |
| `campaignDescription` | String | Eine Beschreibung für die Kampagne. |
| `campaignID` | String | Eine eindeutige Kennung für die Kampagnenentität. |
| `campaignName` | String | Der Name der Kampagne. |
| `campaignType` | String | Kampagnentyp oder Zielgruppe. |

{style="table-layout:auto"}

Informationen dazu, wie sich diese Klasse konzeptionell auf die anderen B2B-Klassen bezieht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können, finden Sie im Handbuch zu [Schemabeziehungen in Real-Time CDP B2B edition](../../tutorials/relationship-b2b.md)

Weitere Felder, die mit dieser Klasse kompatibel sind, finden Sie in der Referenz für Feldergruppen für [[!UICONTROL XDM Business Campaign Details]](../../field-groups/b2b-campaign/details.md).
