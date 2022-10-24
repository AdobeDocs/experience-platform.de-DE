---
title: XDM Business Campaign-Klasse
description: Dieses Dokument bietet einen Überblick über die XDM Business Campaign-Klasse im Experience-Datenmodell (XDM).
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 8%

---

# [!UICONTROL XDM Business Campaign] class

>[!IMPORTANT]
>
>Diese Klasse ist für Organisationen mit Zugriff auf [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Sie müssen Zugriff auf Real-Time CDP B2B Edition haben, damit diese Klasse an [Echtzeit-Kundenprofil](../../../profile/home.md).

[!UICONTROL XDM Business Campaign] ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die die erforderlichen Mindesteigenschaften einer Geschäftskampagne erfasst.

![Die Struktur der XDM Business Campaign-Klasse, wie sie in der Benutzeroberfläche angezeigt wird](../../images/classes/b2b/business-campaign.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Kampagnenentität. |
| `extSourceSystemAudit` | [[!UICONTROL Audit-Attribute des externen Quellsystems]](../../data-types/external-source-system-audit-attributes.md) | Wenn die Kampagne aus einem externen Quellsystem stammt, erfasst dieses Objekt Prüfattribute für dieses System. |
| `_id` | Zeichenfolge | Eine eindeutige Kennung für den Datensatz. Dies ist ein systemgenerierter Wert, der getrennt vom `campaignID`. |
| `campaignDescription` | Zeichenfolge | Eine Beschreibung der Kampagne. |
| `campaignID` | Zeichenfolge | Eine eindeutige Kennung für die Kampagnenentität. |
| `campaignName` | Zeichenfolge | Der Name der Kampagne. |
| `campaignType` | Zeichenfolge | Kampagnentyp oder Zielgruppe. |

{style=&quot;table-layout:auto&quot;}

Informationen dazu, wie diese Klasse konzeptionell mit den anderen B2B-Klassen verknüpft ist und wie Sie diese Beziehungen in der Benutzeroberfläche von Adobe Experience Platform herstellen können, finden Sie im Handbuch unter [Schemabeziehungen in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md)

Weitere Felder, die mit dieser Klasse kompatibel sind, finden Sie in der Feldergruppenreferenz für [[!UICONTROL XDM-Geschäftskampagnendetails]](../../field-groups/b2b-campaign/details.md).
