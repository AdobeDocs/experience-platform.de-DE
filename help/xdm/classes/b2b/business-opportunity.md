---
title: XDM Business Opportunity-Klasse
description: Dieses Dokument bietet einen Überblick über die XDM Business Opportunity-Klasse im Experience-Datenmodell (XDM).
source-git-commit: d83ad2870b6099d3c6359dcc7cd000ecad8a238f
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 8%

---

# [!UICONTROL XDM Business ] Opportunityclass (Beta)

>[!IMPORTANT]
>
>Diese Klasse ist als Teil der Echtzeit-Kundendatenplattform B2B Edition verfügbar, die sich derzeit in der Betaphase befindet. Dokumentation und Funktionalität können sich ändern.

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

Informationen dazu, wie diese Klasse konzeptionell mit anderen B2B-Klassen in Beziehung steht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können, finden Sie im Handbuch zu [Schemabeziehungen in der Echtzeit-Kundendatenplattform B2B Edition](../../tutorials/relationship-b2b.md).
