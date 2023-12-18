---
title: Warenkorbdatentyp
description: Erfahren Sie mehr über den Datentyp des Experience-Datenmodells für Warenkorb (XDM).
source-git-commit: c3590dc2cfe47eb634136eeb88578f965598760d
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 7%

---

# [!UICONTROL Warenkorb] Datentyp

[!UICONTROL Warenkorb] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Eigenschaften für einen Warenkorb bereitstellt. Verwenden Sie diesen Datentyp, um die vom Verkäufer zugewiesene eindeutige Kennung zu erfassen (`Cart ID`) und der Quelle (`Cart Source`), wobei ein oder mehrere Produkte dem Warenkorb hinzugefügt wurden.

![Ein Diagramm des [!UICONTROL Warenkorb] Datentyp.](../images/data-types/cart.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|----------------|-------------------|-----------|------------------------------------------------------------|
| [!UICONTROL Warenkorb-ID] | `cartID` | Zeichenfolge | Vom Verkäufer für den Warenkorb zugewiesene eindeutige Kennung. |
| [!UICONTROL Warenkorbquelle] | `cartSource` | Zeichenfolge | wenn ein oder mehrere Erzeugnisse aus dem Warenkorb hinzugefügt wurden. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json)
