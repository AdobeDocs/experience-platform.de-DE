---
title: XDM Business Opportunity-Klasse
description: Dieses Dokument bietet einen Überblick über die XDM Business Opportunity-Klasse im Experience-Datenmodell (XDM).
exl-id: d816b0f9-fd37-45da-aa55-247f7f662da0
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 7%

---

# [!UICONTROL XDM-Geschäftschancen] class

[!UICONTROL XDM-Geschäftschancen] ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die die erforderlichen Mindesteigenschaften einer Geschäftschance erfasst.

![](../../images/classes/b2b/business-opportunity.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für das Konto, mit dem diese Gelegenheit verknüpft ist. |
| `extSourceSystemAudit` | [[!UICONTROL Audit-Attribute des externen Quellsystems]](../../data-types/external-source-system-audit-attributes.md) | Wenn die Möglichkeit von einem externen Quellsystem stammt, erfasst dieses Objekt Prüfattribute für dieses System. |
| `opportunityKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Opportunity. |
| `_id` | Zeichenfolge | Eine eindeutige Kennung für den Datensatz. Dies ist ein systemgenerierter Wert, der getrennt vom `opportunityID`. |
| `accountID` | Zeichenfolge | Eine eindeutige ID für das Konto, mit dem diese Gelegenheit verknüpft ist. |
| `opportunityDescription` | Zeichenfolge | Eine Beschreibung der Gelegenheit. |
| `opportunityID` | Zeichenfolge | Eine eindeutige ID für die Opportunity. |
| `opportunityName` | Zeichenfolge | Der Name der Gelegenheit. |
| `opportunityStage` | Zeichenfolge | Die Verkaufsphase der Chance. |
| `opportunityType` | Zeichenfolge | Die Art von Gelegenheit. |

{style=&quot;table-layout:auto&quot;}

Siehe Handbuch unter [Schemabeziehungen in der Echtzeit-Kundendatenplattform B2B Edition](../../tutorials/relationship-b2b.md) um zu erfahren, wie diese Klasse konzeptionell mit den anderen B2B-Klassen in Beziehung steht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können.
