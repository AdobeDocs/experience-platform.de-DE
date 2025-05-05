---
title: Datentyp des zurückgegebenen Elements
description: Erfahren Sie mehr über den Datentyp „Rückgabeelement-Experience-Datenmodell (XDM)“.
exl-id: e703d65b-a133-484e-96d6-6b1f50fc1e48
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 7%

---

# [!UICONTROL &#x200B; Datentyp &#x200B;]Rückgabeelement“

[!UICONTROL Rückgabeartikel] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der wichtige Details im Zusammenhang mit dem Rückgabeprozess für einen gekauften Artikel erfasst.

![Ein Diagramm zum Datentyp „Rückgabeelement“.](../images/data-types/return-item.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|-----------------------------|------------------------------|-----------|--------------------------------------------------------|
| [!UICONTROL Rückgabestatus] | `returnStatus` | Zeichenfolge | Der Status des zurückgegebenen Elements (z. B. Ausstehend oder Genehmigt). |
| [!UICONTROL Grund für die Rücksendung] | `returnReason` | Zeichenfolge | Der Grund, warum die Rücksendung für den Artikel angefordert wurde. |
| [!UICONTROL Bedingung für die Rücksendung des Artikels] | `returnItemCondition` | Zeichenfolge | Die Bedingung des Elements, für das die Rücksendung angefordert wird. |
| [!UICONTROL Rückgabeauflösung] | `returnResolution` | Zeichenfolge | Die gewünschte Lösung oder das gewünschte Ergebnis, das von der Rückgabe erwartet wird (z. B. Rückerstattung oder Umtausch). |
| [!UICONTROL Rückgabemenge angefordert] | `returnQuantityRequested` | integer | Die Menge des Artikels, den der Einkäufer zurückgeben wollte. |
| [!UICONTROL Rücklieferungsmenge zulässig] | `returnQuantityAuthorized` | integer | Die Menge des Artikels, die zurückgegeben werden darf. |
| [!UICONTROL Retourenmenge erhalten] | `returnQuantityReceived` | integer | Die Anzahl der zurückgegebenen empfangenen Artikel. |
| [!UICONTROL Rückliefermenge genehmigt] | `returnQuantityApproved` | integer | Die Menge des Artikels mit einer vollständig abgeschlossenen und genehmigten Rücksendung. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.schema.json)
