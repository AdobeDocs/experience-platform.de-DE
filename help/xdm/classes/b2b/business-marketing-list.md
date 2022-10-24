---
title: XDM Business Marketing List-Klasse
description: Dieses Dokument bietet einen Überblick über die XDM Business Marketing List-Klasse im Experience-Datenmodell (XDM).
exl-id: 510c5608-054d-4bed-91eb-22d84b5dc625
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 6%

---

# [!UICONTROL XDM Business Marketing List] class

>[!IMPORTANT]
>
>Diese Klasse ist für Organisationen mit Zugriff auf [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Sie müssen Zugriff auf Real-Time CDP B2B Edition haben, damit diese Klasse an [Echtzeit-Kundenprofil](../../../profile/home.md).

[!UICONTROL XDM Business Marketing List] ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die die erforderlichen Mindesteigenschaften einer Marketing-Liste erfasst. Marketinglisten ermöglichen es Ihnen, potenzielle Kunden zu priorisieren, die Ihr Produkt am ehesten kaufen.

![Die Struktur der XDM Business Marketing List-Klasse, wie sie in der Benutzeroberfläche angezeigt wird](../../images/classes/b2b/business-marketing-list.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Audit-Attribute des externen Quellsystems]](../../data-types/external-source-system-audit-attributes.md) | Wenn die Marketing-Liste aus einem externen Quellsystem stammt, erfasst dieses Objekt Prüfattribute für dieses System. |
| `marketingListKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Marketing-Listenentität. |
| `_id` | Zeichenfolge | Eine eindeutige Kennung für den Datensatz. Dies ist ein systemgenerierter Wert, der getrennt vom `marketingListID`. |
| `isDeleted` | Boolesch | Gibt an, ob diese Entität der Marketingliste in Marketo Engage gelöscht wurde.<br><br>Bei Verwendung von [Marketo-Quell-Connector](../../../sources/connectors/adobe-applications/marketo/marketo.md), werden alle in Marketo gelöschten Datensätze automatisch im Echtzeit-Kundenprofil angezeigt. Datensätze, die sich auf diese Profile beziehen, können jedoch im Data Lake bestehen bleiben. Durch Festlegen von `isDeleted` nach `true`können Sie mithilfe des Felds herausfiltern, welche Datensätze bei der Abfrage des Data Lake aus Ihren Quellen gelöscht wurden. |
| `marketingListDescription` | Zeichenfolge | Eine Beschreibung für die Marketing-Liste. |
| `marketingListID` | Zeichenfolge | Eine eindeutige ID für die Marketing-Listenentität. |
| `marketingListName` | Zeichenfolge | Der Name der Marketing-Liste. |

{style=&quot;table-layout:auto&quot;}

Siehe Handbuch unter [Schemabeziehungen in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) um zu erfahren, wie diese Klasse konzeptionell mit den anderen B2B-Klassen in Beziehung steht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können.
