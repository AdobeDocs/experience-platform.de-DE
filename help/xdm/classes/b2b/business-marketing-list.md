---
title: XDM Business Marketing List-Klasse
description: Dieses Dokument bietet einen Überblick über die XDM Business Marketing List-Klasse im Experience-Datenmodell (XDM).
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 4%

---

# [!UICONTROL XDM Business Marketing ] Listclass

>[!NOTE]
>
>Diese Klasse ist nur für Unternehmen verfügbar, die Zugriff auf die B2B-Edition der Echtzeit-Kundendatenplattform haben.

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
