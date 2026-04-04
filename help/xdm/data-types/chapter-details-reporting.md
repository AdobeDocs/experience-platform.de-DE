---
title: Datentyp für Berichterstellung zu Kapiteldetails
description: Erfahren Sie mehr über den Datentyp „Chapter Details Reporting Experience Data Model (XDM)“.
exl-id: 73ebfbe3-66c3-4ef9-9944-d9cb5772127b
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 9%

---

# [!UICONTROL Chapter Details] Reporting-Datentyp

[!UICONTROL Chapter Details] Reporting ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der verschiedene Attribute beschreibt, die sich auf Kapitel oder Segmente innerhalb von Medieninhalten beziehen. Verwenden Sie den Datentyp &quot;[!UICONTROL Chapter Details] Reporting“, um Details wie Kapitelname, Dauer, Position, ID, Wiedergabestatus (Gestartet/Abgeschlossen) und die für jedes Kapitel aufgewendete Zeit zu erfassen. Medienberichterstellungsfelder werden von Adobe-Services verwendet, um die von Benutzenden gesendeten Mediensammlungsfelder zu analysieren. Diese Daten werden zusammen mit anderen spezifischen Benutzermetriken berechnet und in Berichten erfasst.

![Abbildung des Datentyps für die Berichterstellung zu Kapiteldetails.](../images/data-types/chapter-details-reporting.png)

>[!NOTE]
>
>Jeder Anzeigename enthält einen Link zu weiteren Informationen zu den Audio- und Videoparametern. Die verknüpften Seiten enthalten Details zu den von Adobe erfassten Video- und Anzeigendaten, Implementierungswerten, Netzwerkparametern, Berichten und wichtigen Überlegungen.

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------|--------------------------------------------------------------|
| [[!UICONTROL Chapter Completed]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=de#chapter-complete) | `isCompleted` | boolean | Ob das Kapitel abgeschlossen wurde oder nicht. |
| [[!UICONTROL Chapter ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=de#chapter) | `ID` | string | Die automatisch generierte ID des Kapitels. |
| [[!UICONTROL Chapter Length Or Duration]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=de#chapter-length) | `length` | integer | Die Länge des Kapitels in Sekunden. |
| [[!UICONTROL Chapter Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=de#chapter-name) | `friendlyName` | string | Der Name des Kapitels und/oder Segments. |
| [[!UICONTROL Chapter Offset]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=de#chapter-offset) | `offset` | integer | Der Versatz des Kapitels im Inhalt (in Sekunden) vom Start. |
| [[!UICONTROL Chapter Position]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=de#chapter-position) | `index` | integer | Die Position (Index, Ganzzahl) des Kapitels im Inhalt. |
| [[!UICONTROL Chapter Started]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=de#chapter-start) | `isStarted` | boolean | Gibt an, ob das Kapitel bereits begonnen hat oder nicht. |
| [[!UICONTROL Chapter Time Played]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=de#chapter-time-spent) | `timePlayed` | integer | Die für das Kapitel aufgewendete Zeit in Sekunden. |
