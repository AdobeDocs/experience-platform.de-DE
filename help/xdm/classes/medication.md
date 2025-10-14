---
title: Medikationsklasse
description: Erfahren Sie mehr über die Klasse Medizin im Experience-Datenmodell (XDM).
exl-id: e5786241-dd6e-450f-98c8-2de46affb3e2
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 4%

---

# [!UICONTROL Medizin] Klasse

Im Experience-Datenmodell (XDM) erfasst die Klasse [!UICONTROL Medizin] den Mindestsatz von Eigenschaften, die eine für die medizinische Behandlung verwendete Substanz definieren, insbesondere ein Arzneimittel oder ein Medikament.

![Klassenstruktur](../images/classes/medication.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_id` | [!UICONTROL String] | Eine eindeutige, systemgenerierte Zeichenfolgenkennung für den Datensatz. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Datensatzes nachzuverfolgen, Doppelungen von Daten zu verhindern und diesen Datensatz in nachgelagerten Services nachzuschlagen.<br><br>Da dieses Feld systemgeneriert ist, wird bei der Datenaufnahme kein expliziter Wert bereitgestellt. Sie können jedoch auch weiterhin eigene eindeutige ID-Werte angeben, wenn Sie dies wünschen. |
| `medicationId` | [!UICONTROL String] | Eine eindeutige Kennung für das Medikament. |
| `medicationName` | [!UICONTROL String] | Der Name des Medikaments. |

{style="table-layout:auto"}

Die Klasse kann mit der Feldergruppe [[!UICONTROL Healthcare Medication] erweitert werden, &#x200B;](../field-groups/medication/healthcare-medication.md) weitere Details über das Medikament oder Medikament zu beschreiben.
