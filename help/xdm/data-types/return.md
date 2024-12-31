---
title: Rückgabedatentyp
description: Erfahren Sie mehr über den Datentyp „Rückgabe-Experience-Datenmodell (XDM)“.
exl-id: 1fd99a25-547f-49e7-8980-dda7db2ebb8a
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 8%

---

# [!UICONTROL Zurück] Datentyp

[!UICONTROL Return] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der die wesentlichen Informationen im Zusammenhang mit einer Warenrücksendeautorisierung (Return Merchandise Authorization, RMA) erfasst.

![Ein Diagramm zum Datentyp „Return“.](../images/data-types/return.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|----------------------------------|----------------------|-----------|--------------------------------------------------|
| [!UICONTROL Rückgabe-ID] | `returnID` | Zeichenfolge | Die eindeutige Kennung für diese RMA. |
| [!UICONTROL Rückgabestatus] | `returnStatus` | Zeichenfolge | Der aktuelle Status der RMA (z. B. ausstehend oder geschlossen). |
| [!UICONTROL Bestellungs-ID] | `purchaseID` | Zeichenfolge | Die eindeutige Kennung der Bestellung/Bestellung, zu der die Rücksendung gehört. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/return.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/return.schema.json)
