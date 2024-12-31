---
title: XDM Business-Opportunity-Klasse
description: Erfahren Sie mehr über die Klasse „XDM Business Opportunity“ im Experience-Datenmodell (XDM).
exl-id: d816b0f9-fd37-45da-aa55-247f7f662da0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 3%

---

# [!UICONTROL XDM Business Opportunity] Klasse

>[!IMPORTANT]
>
>Diese Klasse ist für die Verwendung durch Organisationen vorgesehen, die Zugriff auf [Adobe Real-time Customer Data Platform B2B edition](../../../rtcdp/b2b-overview.md) haben. Sie müssen Zugriff auf Real-Time CDP B2B edition haben, damit diese Klasse am Echtzeit[Kundenprofil teilnehmen ](../../../profile/home.md).

[!UICONTROL XDM Business Opportunity] ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die die erforderlichen Mindesteigenschaften einer Business Opportunity erfasst.

![Die Struktur der Klasse XDM Business Opportunity , wie sie in der Benutzeroberfläche angezeigt wird](../../images/classes/b2b/business-opportunity.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B-Source]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für das Konto, mit dem diese Opportunity verknüpft ist. |
| `extSourceSystemAudit` | [[!UICONTROL Audit-Attribute des externen Source-Systems]](../../data-types/external-source-system-audit-attributes.md) | Wenn die Opportunity von einem externen Quellsystem stammt, erfasst dieses Objekt Audit-Attribute für dieses System. |
| `opportunityKey` | [[!UICONTROL B2B-Source]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Opportunity-Entität. |
| `_id` | String | Eine eindeutige Kennung für den Datensatz. Dies ist ein vom System generierter Wert, der vom `opportunityID` getrennt ist. |
| `accountID` | String | Eine eindeutige ID für das Konto, mit dem diese Opportunity verknüpft ist. |
| `isDeleted` | Boolesch | Gibt an, ob diese Marketing-Listenentität auf Marketo Engage gelöscht wurde.<br><br>Bei Verwendung des [Marketo-Quell](../../../sources/connectors/adobe-applications/marketo/marketo.md)Connectors werden alle in Marketo gelöschten Datensätze automatisch im Echtzeit-Kundenprofil angezeigt. Datensätze, die sich auf diese Profile beziehen, können jedoch weiterhin im Data Lake vorhanden sein. Wenn Sie `isDeleted` auf `true` setzen, können Sie das Feld verwenden, um herauszufiltern, welche Datensätze aus Ihren Quellen gelöscht wurden, wenn Sie den Data Lake abfragen. |
| `opportunityDescription` | String | Eine Beschreibung für die Opportunity. |
| `opportunityID` | String | Eine eindeutige ID für die Opportunity-Entität. |
| `opportunityName` | String | Der Name der Opportunity. |
| `opportunityStage` | String | Die Verkaufsphase der Opportunity. |
| `opportunityType` | String | Die Art der Opportunity. |

{style="table-layout:auto"}

Lesen Sie das Handbuch zu [Schemabeziehungen in Real-Time CDP B2B edition](../../tutorials/relationship-b2b.md), um zu erfahren, wie sich diese Klasse konzeptionell auf die anderen B2B-Klassen bezieht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können.
