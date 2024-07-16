---
title: Sammlungsdatentyp für Kapiteldetails
description: Erfahren Sie mehr über den Datentyp "Chapter Details Collection Experience Data Model (XDM)".
exl-id: 4f841f5a-3840-4da5-a3a4-ceecde87c684
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 11%

---

# [!UICONTROL Kapiteldetails] Sammlungsdatentyp

[!UICONTROL Kapiteldetails] Sammlung ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der verschiedene Attribute beschreibt, die sich auf Kapitel oder Segmente in Medieninhalten beziehen. Verwenden Sie den Sammlungsdatentyp [!UICONTROL Kapiteldetails] , um Details wie Kapitelname, Offset, Dauer und Kapitelindex zu erfassen. Medienerfassungsfelder erfassen Daten und senden sie zur weiteren Verarbeitung an andere Adobe-Dienste.

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
