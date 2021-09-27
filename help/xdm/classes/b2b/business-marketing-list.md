---
title: XDM Business Marketing List-Klasse
description: Dieses Dokument bietet einen Überblick über die XDM Business Marketing List-Klasse im Experience-Datenmodell (XDM).
source-git-commit: 5fd82b02eb25f3d575de695c2f2b14a5e5b18400
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 4%

---

# [!UICONTROL XDM Business Marketing ] Listclass

>[!NOTE]
>
>Diese Klasse ist nur für Unternehmen verfügbar, die Zugriff auf die Echtzeit-Kundendatenplattform B2B Edition haben.

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

Informationen dazu, wie diese Klasse konzeptionell mit anderen B2B-Klassen in Beziehung steht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können, finden Sie im Handbuch zu [Schemabeziehungen in der Echtzeit-Kundendatenplattform B2B Edition](../../tutorials/relationship-b2b.md).
