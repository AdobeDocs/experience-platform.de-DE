---
title: XDM Business Campaign-Klasse
description: Dieses Dokument bietet einen Überblick über die XDM Business Campaign-Klasse im Experience-Datenmodell (XDM).
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 10%

---

# [!UICONTROL XDM Business ] Campaign-Klasse (Beta)

>[!IMPORTANT]
>
>Diese Klasse ist als Teil der Echtzeit-Kundendatenplattform B2B Edition verfügbar, die sich derzeit in der Betaphase befindet. Dokumentation und Funktionalität können sich ändern.

[!UICONTROL XDM Business ] Campaign ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die die erforderlichen Mindesteigenschaften einer Geschäftskampagne erfasst.

![](../../images/classes/b2b/business-campaign.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Kampagnenentität. |
| `extSourceSystemAudit` | [[!UICONTROL Audit-Attribute des externen Quellsystems]](../../data-types/external-source-system-audit-attributes.md) | Wenn die Kampagne aus einem externen Quellsystem stammt, erfasst dieses Objekt Prüfattribute für dieses System. |
| `_id` | Zeichenfolge | Eine eindeutige Kennung für den Datensatz. Dies ist ein systemgenerierter Wert, der von `campaignID` getrennt ist. |
| `campaignDescription` | Zeichenfolge | Eine Beschreibung der Kampagne. |
| `campaignID` | Zeichenfolge | Eine eindeutige Kennung für die Kampagnenentität. |
| `campaignName` | Zeichenfolge | Der Name der Kampagne. |
| `campaignType` | Zeichenfolge | Kampagnentyp oder Zielgruppe. |

{style=&quot;table-layout:auto&quot;}

Informationen dazu, wie diese Klasse konzeptionell mit anderen B2B-Klassen in Beziehung steht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können, finden Sie im Handbuch zu [Schemabeziehungen in der Echtzeit-Kundendatenplattform B2B Edition](../../tutorials/relationship-b2b.md).
