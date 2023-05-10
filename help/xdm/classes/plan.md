---
title: Planungsklasse
description: Dieses Dokument bietet einen Überblick über die Planklasse im Experience-Datenmodell (XDM).
exl-id: ccff962d-3104-482c-8d65-d2bd2602a9be
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 4%

---

# [!UICONTROL Plan] class

Im Experience-Datenmodell (XDM) wird die [!UICONTROL Plan] -Klasse erfasst den Mindestsatz von Eigenschaften, die einen Plan definieren, wie z. B. einen Krankenversicherungsplan oder einen Versicherungsplan.

![Klassenstruktur](../images/classes/plan.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_id` | [!UICONTROL String] | Eine eindeutige, systemgenerierte Zeichenfolgenkennung für den Datensatz. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Datensatzes zu verfolgen, Datenduplizierung zu verhindern und diesen Datensatz in nachgelagerten Diensten nachzuschlagen.<br><br>Da dieses Feld systemgeneriert wird, wird bei der Datenerfassung kein expliziter Wert angegeben. Sie können jedoch weiterhin Ihre eigenen eindeutigen ID-Werte angeben, wenn Sie möchten. |
| `planId` | [!UICONTROL String] | Eine eindeutige Kennung für den Plan. |
| `planName` | [!UICONTROL String] | Der Name des Plans. |

{style="table-layout:auto"}

Die Klasse kann mit der [[!UICONTROL Details zum Gesundheitsplan] Feldergruppe](../field-groups/plan/healthcare-plan-details.md) weitere Einzelheiten über einen Krankenversicherungsplan.
