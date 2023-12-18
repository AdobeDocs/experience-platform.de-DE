---
title: Datentyp zurückgeben
description: Erfahren Sie mehr über den XDM-Datentyp (Return Experience Data Model).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 8%

---

# [!UICONTROL Rückgabe] Datentyp

[!UICONTROL Rückgabe] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der die wesentlichen Informationen zu einer Return Merchandise Authorization (RMA) erfasst.

![Ein Diagramm des Datentyps Rückgabe .](../images/data-types/return.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|----------------------------------|----------------------|-----------|--------------------------------------------------|
| [!UICONTROL Rückgabe-ID] | `returnID` | Zeichenfolge | Die eindeutige Kennung für diese RMA. |
| [!UICONTROL Rückkehrstatus] | `returnStatus` | Zeichenfolge | Der aktuelle Status des RMA (z. B. Ausstehend oder Geschlossen). |
| [!UICONTROL Bestell-ID] | `purchaseID` | Zeichenfolge | Die eindeutige Kennung der Bestellung/des Kaufs, auf die sich der RMA bezieht. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/return.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/return.schema.json)

