---
title: Medikationsklasse
description: Erfahren Sie mehr über die Mediationsklasse im Experience-Datenmodell (XDM).
exl-id: e5786241-dd6e-450f-98c8-2de46affb3e2
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 4%

---

# [!UICONTROL Medizin] class

Im Experience-Datenmodell (XDM) wird die [!UICONTROL Medizin] Klasse erfasst die Mindesteigenschaften, die einen Stoff definieren, der für die medizinische Behandlung verwendet wird, insbesondere ein Arzneimittel oder ein Medikament.

![Klassenstruktur](../images/classes/medication.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_id` | [!UICONTROL String] | Eine eindeutige, systemgenerierte Zeichenfolgenkennung für den Datensatz. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Datensatzes zu verfolgen, Datenduplizierung zu verhindern und diesen Datensatz in nachgelagerten Diensten nachzuschlagen.<br><br>Da dieses Feld systemgeneriert ist, wird bei der Datenerfassung kein expliziter Wert angegeben. Sie können jedoch weiterhin Ihre eigenen eindeutigen ID-Werte angeben, wenn Sie möchten. |
| `medicationId` | [!UICONTROL String] | Eine eindeutige Kennung für das Medikament. |
| `medicationName` | [!UICONTROL String] | Der Name des Arzneimittels. |

{style="table-layout:auto"}

Die Klasse kann mit der [[!UICONTROL Medizin] Feldergruppe](../field-groups/medication/healthcare-medication.md) zur Beschreibung weiterer Details über das Arzneimittel oder Arzneimittel.
