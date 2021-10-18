---
title: XDM Business Marketing List-Klasse
description: Dieses Dokument bietet einen Überblick über die XDM Business Marketing List-Klasse im Experience-Datenmodell (XDM).
exl-id: 510c5608-054d-4bed-91eb-22d84b5dc625
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 8%

---

# [!UICONTROL XDM Business Marketing ] Listclass (Beta)

>[!IMPORTANT]
>
>Diese Klasse ist als Teil der Real-time Customer Data Platform B2B Edition verfügbar, die sich derzeit in der Beta-Phase befindet. Dokumentation und Funktionalität können sich ändern.

[!UICONTROL XDM Business Marketing ] Listet eine standardmäßige Experience-Datenmodell (XDM)-Klasse auf, die die erforderlichen Mindesteigenschaften einer Marketing-Liste erfasst. Marketinglisten ermöglichen es Ihnen, potenzielle Kunden zu priorisieren, die Ihr Produkt am ehesten kaufen.

![](../../images/classes/b2b/business-marketing-list.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Audit-Attribute des externen Quellsystems]](../../data-types/external-source-system-audit-attributes.md) | Wenn die Marketing-Liste aus einem externen Quellsystem stammt, erfasst dieses Objekt Prüfattribute für dieses System. |
| `marketingListKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Marketing-Listenentität. |
| `_id` | Zeichenfolge | Eine eindeutige Kennung für den Datensatz. Dies ist ein systemgenerierter Wert, der von `marketingListID` getrennt ist. |
| `marketingListDescription` | Zeichenfolge | Eine Beschreibung für die Marketing-Liste. |
| `marketingListID` | Zeichenfolge | Eine eindeutige ID für die Marketing-Listenentität. |
| `marketingListName` | Zeichenfolge | Der Name der Marketing-Liste. |

{style=&quot;table-layout:auto&quot;}

Informationen dazu, wie diese Klasse konzeptionell mit anderen B2B-Klassen in Beziehung steht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können, finden Sie im Handbuch zu [Schemabeziehungen in der Echtzeit-Kundendatenplattform B2B Edition](../../tutorials/relationship-b2b.md).
