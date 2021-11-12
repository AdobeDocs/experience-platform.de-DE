---
title: XDM Business Opportunity Person Relation Class
description: Dieses Dokument bietet einen Überblick über die XDM Business Opportunity Person Relation-Klasse im Experience-Datenmodell (XDM).
exl-id: 7be193d2-52eb-4b28-953b-5e0fc21d8f93
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 5%

---

# [!UICONTROL XDM Business Opportunity-Personenbeziehung] class

[!UICONTROL XDM Business Opportunity-Personenbeziehung] ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die die erforderlichen Mindesteigenschaften einer Person erfasst, die mit einer Geschäftschance verknüpft ist.

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

{style=&quot;table-layout:auto&quot;}

Siehe Handbuch unter [Schemabeziehungen in der Echtzeit-Kundendatenplattform B2B Edition](../../tutorials/relationship-b2b.md) um zu erfahren, wie diese Klasse konzeptionell mit den anderen B2B-Klassen in Beziehung steht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können.
