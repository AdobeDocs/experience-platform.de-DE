---
title: Berichtdatentyp für Kapiteldetails
description: Erfahren Sie mehr über den Datentyp "Chapter Details Reporting Experience Data Model (XDM)".
source-git-commit: fe239bee3c853d43c04200092f59537dfeb00c87
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 8%

---

# [!UICONTROL Kapiteldetails] Berichtdatentyp

[!UICONTROL Kapiteldetails] Die Berichterstellung ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der verschiedene Attribute beschreibt, die sich auf Kapitel oder Segmente in Medieninhalten beziehen. Verwenden Sie die [!UICONTROL Kapiteldetails] Berichtdatentyp zum Erfassen von Details wie Kapitelname, Dauer, Position, ID, Wiedergabestatus (gestartet/abgeschlossen) und Besuchszeit für jedes Kapitel. Die Felder für die Medienberichte werden von Adobe-Diensten verwendet, um die von Benutzern gesendeten Mediensammlungsfelder zu analysieren. Diese Daten werden zusammen mit anderen spezifischen Benutzermetriken berechnet und in Berichten verwendet.

![Ein Diagramm des Datentyps für die Kapiteldetails-Berichterstellung .](../images/data-types/chapter-details-reporting.png)

>[!NOTE]
>
>Jeder Anzeigename enthält einen Link zu weiteren Informationen zu den Audio- und Videoparametern. Die verknüpften Seiten enthalten Details zu den von Adobe erfassten Videoanzeigendaten, Implementierungswerten, Netzwerkparametern, Berichten und wichtigen Aspekten.

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------|--------------------------------------------------------------|
| [[!UICONTROL Kapitel abgeschlossen]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-complete) | `isCompleted` | Boolescher Wert | Ob das Kapitel abgeschlossen ist oder nicht. |
| [[!UICONTROL Kapitel-ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter) | `ID` | Zeichenfolge | Die automatisch generierte ID des Kapitels. |
| [[!UICONTROL Kapitellänge oder -dauer]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-length) | `length` | integer | Die Länge des Kapitels in Sekunden. |
| [[!UICONTROL Kapitelname]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-name) | `friendlyName` | Zeichenfolge | Der Name des Kapitels und/oder Segments. |
| [[!UICONTROL Kapiteloffset]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-offset) | `offset` | integer | Der Versatz des Kapitels innerhalb des Inhalts ab Beginn (in Sekunden). |
| [[!UICONTROL Kapitelposition]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-position) | `index` | integer | Die Position (Index, Integer) des Kapitels im Inhalt. |
| [[!UICONTROL Kapitel gestartet]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-start) | `isStarted` | Boolescher Wert | Ob das Kapitel gestartet wurde oder nicht. |
| [[!UICONTROL Wiedergabe des Kapitels]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-time-spent) | `timePlayed` | integer | Die mit dem Kapitel verbrachte Zeit in Sekunden. |
