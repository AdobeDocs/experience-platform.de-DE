---
title: Planungsklasse
description: Erfahren Sie mehr über die Klasse Plan im Experience-Datenmodell (XDM).
exl-id: ccff962d-3104-482c-8d65-d2bd2602a9be
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 4%

---

# [!UICONTROL Plan] Klasse

Im Experience-Datenmodell (XDM) erfasst die [!UICONTROL Plan]-Klasse den Mindestsatz von Eigenschaften, die einen Plan definieren, z. B. einen Krankenversicherungsplan oder einen Versicherungsplan.

![Klassenstruktur](../images/classes/plan.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_id` | [!UICONTROL String] | Eine eindeutige, systemgenerierte Zeichenfolgenkennung für den Datensatz. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Datensatzes nachzuverfolgen, Doppelungen von Daten zu verhindern und diesen Datensatz in nachgelagerten Services nachzuschlagen.<br><br>Da dieses Feld systemgeneriert ist, wird bei der Datenaufnahme kein expliziter Wert bereitgestellt. Sie können jedoch auch weiterhin eigene eindeutige ID-Werte angeben, wenn Sie dies wünschen. |
| `planId` | [!UICONTROL String] | Eine eindeutige Kennung für den Plan. |
| `planName` | [!UICONTROL String] | Der Name des Plans. |

{style="table-layout:auto"}

Die Klasse kann mit der Feldergruppe [[!UICONTROL Details zum Gesundheitsplan] erweitert werden, &#x200B;](../field-groups/plan/healthcare-plan-details.md) weitere Details zu einem Krankenversicherungsplan zu beschreiben.
