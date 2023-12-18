---
title: Datentyp "Rückgabeelement"
description: Erfahren Sie mehr über den Datentyp "Return Item Experience Data Model (XDM)".
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 7%

---

# [!UICONTROL Rückgabeelement] Datentyp

[!UICONTROL Rückgabeelement] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der wichtige Details zum Rückgabeverfahren für einen gekauften Artikel erfasst.

![Ein Diagramm des Datentyps Rückgabeelement .](../images/data-types/return-item.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|-----------------------------|------------------------------|-----------|--------------------------------------------------------|
| [!UICONTROL Rückkehrstatus] | `returnStatus` | Zeichenfolge | Der Status des zurückgegebenen Elements (z. B. Ausstehend oder Genehmigt). |
| [!UICONTROL Rückkehrgrund] | `returnReason` | Zeichenfolge | Der Grund, warum die Rückgabe für den Artikel angefordert wurde. |
| [!UICONTROL Bedingung für Rückgabeelement] | `returnItemCondition` | Zeichenfolge | Die Bedingung des Elements, für das die Rückgabe angefordert wird. |
| [!UICONTROL Rückgabeauflösung] | `returnResolution` | Zeichenfolge | Die gewünschte Auflösung oder das Ergebnis, das von der Rückkehr erwartet wird (z. B. Rückerstattung oder Exchange). |
| [!UICONTROL Anforderte Rückgabemenge] | `returnQuantityRequested` | integer | Die Menge des Artikels, zu dem der Käufer die Rückgabe angefordert hat. |
| [!UICONTROL Zugelassene Rückgabenmenge] | `returnQuantityAuthorized` | integer | Die Menge des zu versendenden Artikels. |
| [!UICONTROL Erhaltene Rückgabemenge] | `returnQuantityReceived` | integer | Die Menge der zurückgegebenen Artikel, die empfangen wurden. |
| [!UICONTROL Genehmigte Rückgabenmenge] | `returnQuantityApproved` | integer | Die Menge des Artikels mit einer Rückgabe ist vollständig abgeschlossen und genehmigt. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.schema.json)
