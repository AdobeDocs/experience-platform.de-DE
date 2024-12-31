---
title: XDM Business Opportunity Person Relation-Klasse
description: Erfahren Sie mehr über die Klasse XDM Business Opportunity Person Relation im Experience-Datenmodell (XDM).
exl-id: 7be193d2-52eb-4b28-953b-5e0fc21d8f93
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 3%

---

# [!UICONTROL XDM Business Opportunity Person Relation]-Klasse

>[!IMPORTANT]
>
>Diese Klasse ist für die Verwendung durch Organisationen vorgesehen, die Zugriff auf [Adobe Real-time Customer Data Platform B2B edition](../../../rtcdp/b2b-overview.md) haben. Sie müssen Zugriff auf Real-Time CDP B2B edition haben, damit diese Klasse am Echtzeit[Kundenprofil teilnehmen ](../../../profile/home.md).

[!UICONTROL XDM Business Opportunity Person Relation] ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die die erforderlichen Mindesteigenschaften einer Person erfasst, die einer Geschäftschance zugeordnet ist.

![Die Struktur der XDM Business Opportunity Person -Klasse, wie sie in der Benutzeroberfläche angezeigt wird](../../images/classes/b2b/business-opportunity-person-relation.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Audit-Attribute des externen Source-Systems]](../../data-types/external-source-system-audit-attributes.md) | Wenn die Geschäftspersonenbeziehung von einem externen Quellsystem stammt, erfasst dieses Objekt Audit-Attribute für dieses System. |
| `opportunityKey` | [[!UICONTROL B2B-Source]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Opportunity in der Opportunity-Person-Beziehung. |
| `opportunityPersonKey` | [[!UICONTROL B2B-Source]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Opportunity-Person-Beziehungsentität. |
| `personKey` | [[!UICONTROL B2B-Source]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Person in der Opportunity-Person-Beziehung. |
| `_id` | String | Eine eindeutige Kennung für den Datensatz. Dies ist ein systemgenerierter Wert, der von den anderen ID-Feldern, die von der Klasse erfasst werden, getrennt ist. |
| `isDeleted` | Boolesch | Gibt an, ob diese Marketing-Listenentität auf Marketo Engage gelöscht wurde.<br><br>Bei Verwendung des [Marketo-Quell](../../../sources/connectors/adobe-applications/marketo/marketo.md)Connectors werden alle in Marketo gelöschten Datensätze automatisch im Echtzeit-Kundenprofil angezeigt. Datensätze, die sich auf diese Profile beziehen, können jedoch weiterhin im Data Lake vorhanden sein. Wenn Sie `isDeleted` auf `true` setzen, können Sie das Feld verwenden, um herauszufiltern, welche Datensätze aus Ihren Quellen gelöscht wurden, wenn Sie den Data Lake abfragen. |
| `isPrimary` | Boolesch | Gibt an, ob die Person der primäre Ansprechpartner für diese Opportunity ist. |
| `opportunityID` | String | Eine eindeutige Kennung für die Opportunity in der Opportunity-Person-Beziehung. |
| `opportunityPersonID` | String | Eine eindeutige Kennung für die Opportunity-Person-Beziehungsentität |
| `personID` | String | Eine eindeutige Kennung für die Person in der Opportunity-Person-Beziehung. |
| `personRole` | String | Die Rolle der Person in der Opportunity-Person-Beziehung. |

{style="table-layout:auto"}

Lesen Sie das Handbuch zu [Schemabeziehungen in Real-Time CDP B2B edition](../../tutorials/relationship-b2b.md), um zu erfahren, wie sich diese Klasse konzeptionell auf die anderen B2B-Klassen bezieht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können.
