---
title: Warenkorb-Datentyp
description: Erfahren Sie mehr über den Datentyp Cart Experience-Datenmodell (XDM) .
exl-id: 24ae3882-60f3-4962-b0b5-7dba48170da8
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 15%

---

# [!UICONTROL Warenkorb] Datentyp

[!UICONTROL Cart] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Eigenschaften für einen Warenkorb bereitstellt. Verwenden Sie diesen Datentyp, um die vom Verkäufer (`Cart ID`) zugewiesene eindeutige Kennung und die Quelle (`Cart Source`) zu erfassen, aus der ein oder mehrere Produkte zum Warenkorb hinzugefügt wurden.

![Ein Diagramm des Datentyps [!UICONTROL Warenkorb].](../images/data-types/cart.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|----------------|-------------------|-----------|------------------------------------------------------------|
| [!UICONTROL Warenkorb-ID] | `cartID` | Zeichenfolge | Vom Verkäufer dem Warenkorb zugewiesene eindeutige Kennung. |
| [!UICONTROL Warenkorb - Source] | `cartSource` | Zeichenfolge | Wenn ein oder mehrere Produkte aus dem Warenkorb hinzugefügt wurden. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json)
