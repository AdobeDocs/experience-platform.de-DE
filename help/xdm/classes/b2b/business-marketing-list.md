---
title: XDM Business Marketing List-Klasse
description: Erfahren Sie mehr über die Klasse XDM Business Marketing List im Experience-Datenmodell (XDM).
exl-id: 510c5608-054d-4bed-91eb-22d84b5dc625
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 3%

---

# [!UICONTROL XDM Business Marketing List]-Klasse

>[!IMPORTANT]
>
>Diese Klasse ist für die Verwendung durch Organisationen vorgesehen, die Zugriff auf [Adobe Real-time Customer Data Platform B2B edition](../../../rtcdp/b2b-overview.md) haben. Sie müssen Zugriff auf Real-Time CDP B2B edition haben, damit diese Klasse am Echtzeit[Kundenprofil teilnehmen ](../../../profile/home.md).

[!UICONTROL XDM Business Marketing List] ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die die erforderlichen Mindesteigenschaften einer Marketing-Liste erfasst. Mithilfe von Marketing-Listen können Sie sich auf potenzielle Kunden konzentrieren, die am ehesten Ihr Produkt kaufen würden.

![Die Struktur der Klasse XDM Business Marketing List , wie sie in der Benutzeroberfläche angezeigt wird](../../images/classes/b2b/business-marketing-list.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Audit-Attribute des externen Source-Systems]](../../data-types/external-source-system-audit-attributes.md) | Wenn die Marketing-Liste von einem externen Quellsystem stammt, erfasst dieses Objekt Audit-Attribute für dieses System. |
| `marketingListKey` | [[!UICONTROL B2B-Source]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Marketing-Listenentität. |
| `_id` | String | Eine eindeutige Kennung für den Datensatz. Dies ist ein vom System generierter Wert, der vom `marketingListID` getrennt ist. |
| `isDeleted` | Boolesch | Gibt an, ob diese Marketing-Listenentität auf Marketo Engage gelöscht wurde.<br><br>Bei Verwendung des [Marketo-Quell](../../../sources/connectors/adobe-applications/marketo/marketo.md)Connectors werden alle in Marketo gelöschten Datensätze automatisch im Echtzeit-Kundenprofil angezeigt. Datensätze, die sich auf diese Profile beziehen, können jedoch weiterhin im Data Lake vorhanden sein. Wenn Sie `isDeleted` auf `true` setzen, können Sie das Feld verwenden, um herauszufiltern, welche Datensätze aus Ihren Quellen gelöscht wurden, wenn Sie den Data Lake abfragen. |
| `marketingListDescription` | String | Eine Beschreibung für die Marketing-Liste. |
| `marketingListID` | String | Eine eindeutige ID für die Marketing-Listenentität. |
| `marketingListName` | String | Der Name der Marketing-Liste. |

{style="table-layout:auto"}

Lesen Sie das Handbuch zu [Schemabeziehungen in Real-Time CDP B2B edition](../../tutorials/relationship-b2b.md), um zu erfahren, wie sich diese Klasse konzeptionell auf die anderen B2B-Klassen bezieht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können.
