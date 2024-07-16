---
title: Datentyp "Rückgabeelement"
description: Erfahren Sie mehr über den Datentyp "Return Item Experience Data Model (XDM)".
exl-id: e703d65b-a133-484e-96d6-6b1f50fc1e48
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 7%

---

# Datentyp [!UICONTROL Rückgabeelement]

[!UICONTROL Rückgabeelement] ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der wichtige Details zum Rückgabeverfahren für einen gekauften Artikel erfasst.

![Ein Diagramm des Datentyps &quot;Rückgabeelement&quot;.](../images/data-types/return-item.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|-----------------------------|------------------------------|-----------|--------------------------------------------------------|
| [!UICONTROL Rückkehrstatus] | `returnStatus` | Zeichenfolge | Der Status des zurückgegebenen Elements (z. B. Ausstehend oder Genehmigt). |
| [!UICONTROL Rückkehrgrund] | `returnReason` | Zeichenfolge | Der Grund, warum die Rückgabe für den Artikel angefordert wurde. |
| [!UICONTROL Rückgabeelementbedingung] | `returnItemCondition` | Zeichenfolge | Die Bedingung des Elements, für das die Rückgabe angefordert wird. |
| [!UICONTROL Rückgabeauflösung] | `returnResolution` | Zeichenfolge | Die gewünschte Auflösung oder das Ergebnis, das von der Rückkehr erwartet wird (z. B. Rückerstattung oder Exchange). |
| [!UICONTROL Zurückgegebene Menge angefordert] | `returnQuantityRequested` | integer | Die Menge des Artikels, zu dem der Käufer die Rückgabe angefordert hat. |
| [!UICONTROL Zurückgeben der autorisierten Menge ] | `returnQuantityAuthorized` | integer | Die Menge des zu versendenden Artikels. |
| [!UICONTROL Zurückgegebene Menge zurückgeben] | `returnQuantityReceived` | integer | Die Menge der zurückgegebenen Artikel, die empfangen wurden. |
| [!UICONTROL Zurückgeben der genehmigten Menge] | `returnQuantityApproved` | integer | Die Menge des Artikels mit einer Rückgabe ist vollständig abgeschlossen und genehmigt. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.schema.json)
