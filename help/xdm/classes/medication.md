---
title: Medikationsklasse
description: Dieses Dokument bietet einen Überblick über die Mediationsklasse im Experience-Datenmodell (XDM).
source-git-commit: cf39f943e27cd11b0eabbc344774fa12482a8f92
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 6%

---

# [!UICONTROL Medizin] class

Im Experience-Datenmodell (XDM) wird die [!UICONTROL Medizin] Klasse erfasst die Mindesteigenschaften, die einen Stoff definieren, der für die medizinische Behandlung verwendet wird, insbesondere ein Arzneimittel oder ein Medikament.

![Klassenstruktur](../images/classes/medication.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_id` | [!UICONTROL Zeichenfolge] | Eine eindeutige, systemgenerierte Zeichenfolgenkennung für den Datensatz. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Datensatzes zu verfolgen, Datenduplizierung zu verhindern und diesen Datensatz in nachgelagerten Diensten nachzuschlagen.<br><br>Da dieses Feld systemgeneriert wird, wird bei der Datenerfassung kein expliziter Wert angegeben. Sie können jedoch weiterhin Ihre eigenen eindeutigen ID-Werte angeben, wenn Sie möchten. |
| `medicationId` | [!UICONTROL Zeichenfolge] | Eine eindeutige Kennung für das Medikament. |
| `medicationName` | [!UICONTROL Zeichenfolge] | Der Name des Arzneimittels. |

{style=&quot;table-layout:auto&quot;}

Die Klasse kann mit der [[!UICONTROL Arzneimittel] Feldergruppe](../field-groups/medication/healthcare-medication.md) zur Beschreibung weiterer Details über das Arzneimittel oder Arzneimittel.
