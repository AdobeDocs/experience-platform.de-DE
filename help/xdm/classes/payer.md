---
title: Kostenstelle
description: Erfahren Sie mehr über die Player-Klasse im Experience-Datenmodell (XDM).
exl-id: 8d3e0a6d-41eb-4ffe-81dd-c7b7d532a531
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 5%

---

# [!UICONTROL Payer]-Klasse

Im Experience-Datenmodell (XDM) erfasst die [!UICONTROL Payer]-Klasse den Mindestsatz von Eigenschaften, die eine Geschäftseinheit des Zahlenden definieren, die Daten zu Versicherungsunternehmen (z. B. Krankenversicherungen) erfasst.

![Klassenstruktur](../images/classes/payer.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_id` | [!UICONTROL String] | Eine eindeutige, systemgenerierte Zeichenfolgenkennung für den Datensatz. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Datensatzes nachzuverfolgen, Doppelungen von Daten zu verhindern und diesen Datensatz in nachgelagerten Services nachzuschlagen.<br><br>Da dieses Feld systemgeneriert ist, wird bei der Datenaufnahme kein expliziter Wert bereitgestellt. Sie können jedoch auch weiterhin eigene eindeutige ID-Werte angeben, wenn Sie dies wünschen. |
| `payerId` | [!UICONTROL String] | Eine eindeutige Kennung für den Player. |
| `payerName` | [!UICONTROL String] | Der Name des Zahlers. |

{style="table-layout:auto"}
