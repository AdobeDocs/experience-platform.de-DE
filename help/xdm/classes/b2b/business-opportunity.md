---
title: XDM Business Opportunity-Klasse
description: Dieses Dokument bietet einen Überblick über die XDM Business Opportunity-Klasse im Experience-Datenmodell (XDM).
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 6%

---

# [!UICONTROL XDM Business ] Opportunityclass

>[!NOTE]
>
>Diese Klasse ist nur für Unternehmen verfügbar, die Zugriff auf die B2B-Edition der Echtzeit-Kundendatenplattform haben.

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
