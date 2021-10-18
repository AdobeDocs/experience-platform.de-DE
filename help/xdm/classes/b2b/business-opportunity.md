---
title: XDM Business Opportunity-Klasse
description: Dieses Dokument bietet einen Überblick über die XDM Business Opportunity-Klasse im Experience-Datenmodell (XDM).
exl-id: d816b0f9-fd37-45da-aa55-247f7f662da0
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 9%

---

# [!UICONTROL XDM Business ] Opportunityclass (Beta)

>[!IMPORTANT]
>
>Diese Klasse ist als Teil der Real-time Customer Data Platform B2B Edition verfügbar, die sich derzeit in der Beta-Phase befindet. Dokumentation und Funktionalität können sich ändern.

[!UICONTROL XDM Business ] Opportunityist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die die erforderlichen Mindesteigenschaften einer Geschäftschance erfasst.

![](../../images/classes/b2b/business-opportunity.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für das Konto, mit dem diese Gelegenheit verknüpft ist. |
| `extSourceSystemAudit` | [[!UICONTROL Audit-Attribute des externen Quellsystems]](../../data-types/external-source-system-audit-attributes.md) | Wenn die Möglichkeit von einem externen Quellsystem stammt, erfasst dieses Objekt Prüfattribute für dieses System. |
| `opportunityKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Opportunity. |
| `_id` | Zeichenfolge | Eine eindeutige Kennung für den Datensatz. Dies ist ein systemgenerierter Wert, der von `opportunityID` getrennt ist. |
| `accountID` | Zeichenfolge | Eine eindeutige ID für das Konto, mit dem diese Gelegenheit verknüpft ist. |
| `opportunityDescription` | Zeichenfolge | Eine Beschreibung der Gelegenheit. |
| `opportunityID` | Zeichenfolge | Eine eindeutige ID für die Opportunity. |
| `opportunityName` | Zeichenfolge | Der Name der Gelegenheit. |
| `opportunityStage` | Zeichenfolge | Die Verkaufsphase der Chance. |
| `opportunityType` | Zeichenfolge | Die Art von Gelegenheit. |

{style=&quot;table-layout:auto&quot;}

Informationen dazu, wie diese Klasse konzeptionell mit anderen B2B-Klassen in Beziehung steht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können, finden Sie im Handbuch zu [Schemabeziehungen in der Echtzeit-Kundendatenplattform B2B Edition](../../tutorials/relationship-b2b.md).
