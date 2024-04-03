---
title: Sammlungsdatentyp für Kapiteldetails
description: Erfahren Sie mehr über den Datentyp "Chapter Details Collection Experience Data Model (XDM)".
source-git-commit: c6108bb692c80c79e115ac7b1488d95a7039ffcf
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 11%

---

# [!UICONTROL Kapiteldetails] Sammlungsdatentyp

[!UICONTROL Kapiteldetails] Die Sammlung ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der verschiedene Attribute beschreibt, die sich auf Kapitel oder Segmente in Medieninhalten beziehen. Verwenden Sie die [!UICONTROL Kapiteldetails] Sammlungsdatentyp zum Erfassen von Details wie Kapitelname, Offset, Dauer und Kapitelindex. Medienerfassungsfelder erfassen Daten und senden sie zur weiteren Verarbeitung an andere Adobe-Dienste.

![Ein Diagramm des Datentyps der Kapiteldetails-Sammlung.](../images/data-types/chapter-details-collection.png)

>[!NOTE]
>
>Jeder Anzeigename enthält einen Link zu weiteren Informationen zu den Audio- und Videoparametern. Die verknüpften Seiten enthalten Details zu den von Adobe erfassten Videoanzeigendaten, Implementierungswerten, Netzwerkparametern, Berichten und wichtigen Aspekten.

| Anzeigename | Eigenschaft | Datentyp | Erforderlich | Beschreibung |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------|----------|---------------------------------------------------|
| [[!UICONTROL Kapitellänge oder -dauer]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-length) | `length` | integer | Ja | Die Länge des Kapitels in Sekunden. |
| [[!UICONTROL Kapitelname]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-name) | `friendlyName` | Zeichenfolge | Nein | Der Name des Kapitels und/oder Segments. |
| [[!UICONTROL Kapiteloffset]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-offset) | `offset` | integer | Ja | Der Versatz des Kapitels innerhalb des Inhalts ab Beginn (in Sekunden). |
| [[!UICONTROL Kapitelposition]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-position) | `index` | integer | Ja | Die Position (Index, Integer) des Kapitels im Inhalt. |

{style="table-layout:auto"}
