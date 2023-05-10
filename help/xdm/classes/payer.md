---
title: Player-Klasse
description: Dieses Dokument bietet einen Überblick über die Payer-Klasse im Experience-Datenmodell (XDM).
exl-id: 8d3e0a6d-41eb-4ffe-81dd-c7b7d532a531
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 5%

---

# [!UICONTROL Player] class

Im Experience-Datenmodell (XDM) wird die [!UICONTROL Player] -Klasse erfasst den Mindestsatz von Eigenschaften, die eine Zahler-Geschäftsentität definieren, die Daten über Versicherungsunternehmen erfasst (z. B. Krankenversicherungen).

![Klassenstruktur](../images/classes/payer.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_id` | [!UICONTROL String] | Eine eindeutige, systemgenerierte Zeichenfolgenkennung für den Datensatz. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Datensatzes zu verfolgen, Datenduplizierung zu verhindern und diesen Datensatz in nachgelagerten Diensten nachzuschlagen.<br><br>Da dieses Feld systemgeneriert wird, wird bei der Datenerfassung kein expliziter Wert angegeben. Sie können jedoch weiterhin Ihre eigenen eindeutigen ID-Werte angeben, wenn Sie möchten. |
| `payerId` | [!UICONTROL String] | Eine eindeutige ID für den Player. |
| `payerName` | [!UICONTROL String] | Der Name des Zahlers. |

{style="table-layout:auto"}
