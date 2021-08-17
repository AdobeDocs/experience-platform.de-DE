---
keywords: Experience Platform;Startseite;beliebte Themen;CSV zuordnen;CSV-Datei zuordnen;CSV-Datei zu xdm zuordnen;CSV zu xdm zuordnen;ui-Handbuch;Mapper;Zuordnung;Datenvorbereitung;Datenvorbereitung;Vorbereiten von Daten;
solution: Experience Platform
title: Datenvorbereitung – Übersicht
topic-legacy: overview
description: Dieses Dokument führt in die Datenvorbereitung in Adobe Experience Platform ein.
exl-id: f15eeb50-a531-4560-a524-1a670fbda706
source-git-commit: 2cc72708b77396e70d006ecd1e21fd2d495ddf61
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 19%

---


# Berechnete Felder

Berechnete Felder ermöglichen die Erstellung von Werten anhand der Attribute im Eingabeschema. Diese Werte können dann Attributen im Zielschema zugewiesen und mit einem Namen und einer Beschreibung versehen werden, um eine einfachere Referenz zu ermöglichen.

Um ein berechnetes Feld zu erstellen, wählen Sie **[!UICONTROL Berechnetes Feld hinzufügen]** aus.

![](./images/calculated-fields/add-calculated-field.png)

Das Bedienfeld **[!UICONTROL Berechnetes Feld erstellen]** wird angezeigt. Das linke Dialogfeld enthält die Felder, Funktionen und Operatoren, die in berechneten Feldern unterstützt werden. Wählen Sie eine der Registerkarten aus, um dem Ausdruckseditor Funktionen, Felder oder Operatoren hinzuzufügen.

![](./images/calculated-fields/create-calculated-field.png)

| Tab | Beschreibung |
| --- | ----------- |
| Funktion | Im Tab Funktionen werden die Funktionen aufgelistet, die zur Transformation der Daten verfügbar sind. Weitere Informationen zu den Funktionen, die Sie in berechneten Feldern verwenden können, finden Sie im Handbuch [Verwendung der Datenvorbereitung (Mapper)-Funktionen](./functions.md). |
| Feld | Auf der Registerkarte Felder werden die im Quellschema verfügbaren Felder und Attribute aufgelistet. |
| Operator | Im Tab Operatoren werden die zur Transformation der Daten verfügbaren Operatoren aufgelistet. |

Mithilfe des Ausdruckseditors in der Mitte können Sie manuell Felder, Funktionen und Operatoren hinzufügen. Wählen Sie den Editor aus, um mit der Erstellung eines Ausdrucks zu beginnen.

![](./images/calculated-fields/write-calculated-field.png)

Wählen Sie **[!UICONTROL Save]** aus, um fortzufahren.

Der Zuordnungsbildschirm wird mit dem neu erstellten Quellfeld erneut angezeigt. Wenden Sie das entsprechende Zielfeld an und wählen Sie **[!UICONTROL Beenden]** aus, um die Zuordnung abzuschließen.

![](./images/calculated-fields/new-calculated-field.png)