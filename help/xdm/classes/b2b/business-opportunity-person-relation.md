---
title: XDM Business Opportunity Person Relation Class
description: Dieses Dokument bietet einen Überblick über die XDM Business Opportunity Person Relation-Klasse im Experience-Datenmodell (XDM).
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 4%

---

# [!UICONTROL XDM Business Opportunity Person ] Relationclass

>[!NOTE]
>
>Diese Klasse ist nur für Unternehmen verfügbar, die Zugriff auf die B2B-Edition der Echtzeit-Kundendatenplattform haben.

[!UICONTROL XDM Business Opportunity Person ] Relationation ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die die erforderlichen Mindesteigenschaften einer Person erfasst, die mit einer Geschäftschance verknüpft ist.

![](../../images/classes/b2b/business-opportunity-person-relation.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Audit-Attribute des externen Quellsystems]](../../data-types/external-source-system-audit-attributes.md) | Wenn die geschäftliche Personenbeziehung aus einem externen Quellsystem stammt, erfasst dieses Objekt Prüfattribute für dieses System. |
| `opportunityKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Gelegenheit in der Opportunity-Person-Beziehung. |
| `opportunityPersonKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Entität der Opportunity-Person-Beziehung. |
| `personKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Person in der Opportunity-Person-Beziehung. |
| `_id` | Zeichenfolge | Eine eindeutige Kennung für den Datensatz. Dies ist ein systemgenerierter Wert, der von den anderen von der Klasse erfassten ID-Feldern getrennt ist. |
| `opportunityID` | Zeichenfolge | Eine eindeutige Kennung für die Gelegenheit in der Opportunity-Person-Beziehung. |
| `opportunityPersonID` | Zeichenfolge | Eine eindeutige Kennung für die Entität der Opportunity-Person-Beziehung |
| `isPrimary` | Boolesch | Gibt an, ob die Person der Hauptkontakt für diese Gelegenheit ist. |
| `personID` | Zeichenfolge | Eine eindeutige Kennung für die Person in der Opportunity-Person-Beziehung. |
| `personRole` | Zeichenfolge | Die Rolle der Person in der Beziehung zwischen Opportunity und Person. |
