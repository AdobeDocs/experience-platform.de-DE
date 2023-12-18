---
title: XDM Business Opportunity Person Relation Class
description: Erfahren Sie mehr über die Klasse "XDM Business Opportunity Person Relation"im Experience-Datenmodell (XDM).
exl-id: 7be193d2-52eb-4b28-953b-5e0fc21d8f93
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 3%

---

# [!UICONTROL XDM Business Opportunity-Personenbeziehung] class

>[!IMPORTANT]
>
>Diese Klasse ist für Organisationen mit Zugriff auf [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Sie müssen Zugriff auf Real-Time CDP B2B Edition haben, damit diese Klasse an [Echtzeit-Kundenprofil](../../../profile/home.md).

[!UICONTROL XDM Business Opportunity-Personenbeziehung] ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die die erforderlichen Mindesteigenschaften einer Person erfasst, die mit einer Geschäftschance verknüpft ist.

![Die Struktur der XDM Business Opportunity Person-Klasse, wie sie in der Benutzeroberfläche angezeigt wird](../../images/classes/b2b/business-opportunity-person-relation.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Audit-Attribute des externen Quellsystems]](../../data-types/external-source-system-audit-attributes.md) | Wenn die geschäftliche Personenbeziehung aus einem externen Quellsystem stammt, erfasst dieses Objekt Prüfattribute für dieses System. |
| `opportunityKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Gelegenheit in der Opportunity-Person-Beziehung. |
| `opportunityPersonKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Entität der Opportunity-Person-Beziehung. |
| `personKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Person in der Opportunity-Person-Beziehung. |
| `_id` | Zeichenfolge | Eine eindeutige Kennung für den Datensatz. Dies ist ein systemgenerierter Wert, der von den anderen von der Klasse erfassten ID-Feldern getrennt ist. |
| `isDeleted` | Boolesch | Gibt an, ob diese Entität der Marketingliste im Marketo Engage gelöscht wurde.<br><br>Bei Verwendung von [Marketo-Quell-Connector](../../../sources/connectors/adobe-applications/marketo/marketo.md), werden alle in Marketo gelöschten Datensätze automatisch in das Echtzeit-Kundenprofil übernommen. Datensätze, die sich auf diese Profile beziehen, können jedoch im Data Lake bestehen bleiben. Durch Festlegen von `isDeleted` nach `true`können Sie mithilfe des Felds herausfiltern, welche Datensätze bei der Abfrage des Data Lake aus Ihren Quellen gelöscht wurden. |
| `isPrimary` | Boolesch | Gibt an, ob die Person der Hauptkontakt für diese Gelegenheit ist. |
| `opportunityID` | Zeichenfolge | Eine eindeutige Kennung für die Gelegenheit in der Opportunity-Person-Beziehung. |
| `opportunityPersonID` | Zeichenfolge | Eine eindeutige Kennung für die Entität der Opportunity-Person-Beziehung |
| `personID` | Zeichenfolge | Eine eindeutige Kennung für die Person in der Opportunity-Person-Beziehung. |
| `personRole` | Zeichenfolge | Die Rolle der Person in der Beziehung zwischen Opportunity und Person. |

{style="table-layout:auto"}

Siehe Handbuch unter [Schemabeziehungen in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) um zu erfahren, wie diese Klasse konzeptionell mit den anderen B2B-Klassen in Beziehung steht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können.
