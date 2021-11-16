---
title: XDM Business Opportunity-Klasse
description: Dieses Dokument bietet einen Überblick über die XDM Business Opportunity-Klasse im Experience-Datenmodell (XDM).
exl-id: d816b0f9-fd37-45da-aa55-247f7f662da0
source-git-commit: 8718512a9768158183b9fb6b9e336081e47cd889
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 5%

---

# [!UICONTROL XDM-Geschäftschancen] class

>[!IMPORTANT]
>
>Diese Klasse ist für Organisationen mit Zugriff auf [Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Sie müssen Zugriff auf die Echtzeit-CDP B2B Edition haben, damit diese Klasse an [Echtzeit-Kundenprofil](../../../profile/home.md).

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
