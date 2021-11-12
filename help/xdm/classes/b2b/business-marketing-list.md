---
title: XDM Business Marketing List-Klasse
description: Dieses Dokument bietet einen Überblick über die XDM Business Marketing List-Klasse im Experience-Datenmodell (XDM).
exl-id: 510c5608-054d-4bed-91eb-22d84b5dc625
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 5%

---

# [!UICONTROL XDM Business Marketing List] class

[!UICONTROL XDM Business Marketing List] ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die die erforderlichen Mindesteigenschaften einer Marketing-Liste erfasst. Marketinglisten ermöglichen es Ihnen, potenzielle Kunden zu priorisieren, die Ihr Produkt am ehesten kaufen.

![](../../images/classes/b2b/business-marketing-list.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Audit-Attribute des externen Quellsystems]](../../data-types/external-source-system-audit-attributes.md) | Wenn die Marketing-Liste aus einem externen Quellsystem stammt, erfasst dieses Objekt Prüfattribute für dieses System. |
| `marketingListKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Marketing-Listenentität. |
| `_id` | Zeichenfolge | Eine eindeutige Kennung für den Datensatz. Dies ist ein systemgenerierter Wert, der getrennt vom `marketingListID`. |
| `marketingListDescription` | Zeichenfolge | Eine Beschreibung für die Marketing-Liste. |
| `marketingListID` | Zeichenfolge | Eine eindeutige ID für die Marketing-Listenentität. |
| `marketingListName` | Zeichenfolge | Der Name der Marketing-Liste. |

{style=&quot;table-layout:auto&quot;}

Siehe Handbuch unter [Schemabeziehungen in der Echtzeit-Kundendatenplattform B2B Edition](../../tutorials/relationship-b2b.md) um zu erfahren, wie diese Klasse konzeptionell mit den anderen B2B-Klassen in Beziehung steht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können.
