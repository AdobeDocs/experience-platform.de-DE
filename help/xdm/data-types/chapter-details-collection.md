---
title: Datentyp der Kapiteldetails-Sammlung
description: Erfahren Sie mehr über den Datentyp Experience-Datenmodell (XDM) der Kapiteldetails-Sammlung.
exl-id: 4f841f5a-3840-4da5-a3a4-ceecde87c684
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 12%

---

# Datentyp der [!UICONTROL Chapter Details]

[!UICONTROL Chapter Details] Sammlung ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der verschiedene Attribute beschreibt, die sich auf Kapitel oder Segmente innerhalb von Medieninhalten beziehen. Verwenden Sie den Datentyp &quot;[!UICONTROL Chapter Details]&quot;, um Details wie Kapitelnamen, Versatz, Dauer und den Kapitelindex zu erfassen. Mediensammlungsfelder erfassen Daten und senden sie zur weiteren Verarbeitung an andere Adobe-Services.

![Abbildung des Datentyps der Kapiteldetails-Sammlung.](../images/data-types/chapter-details-collection.png)

>[!NOTE]
>
>Jeder Anzeigename enthält einen Link zu weiteren Informationen zu den Audio- und Videoparametern. Die verknüpften Seiten enthalten Details zu den von Adobe erfassten Video- und Anzeigendaten, Implementierungswerten, Netzwerkparametern, Berichten und wichtigen Überlegungen.

| Anzeigename | Eigenschaft | Datentyp | Erforderlich | Beschreibung |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------|----------|---------------------------------------------------|
| [[!UICONTROL Chapter Length Or Duration]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=de#chapter-length) | `length` | integer | Ja | Die Länge des Kapitels in Sekunden. |
| [[!UICONTROL Chapter Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=de#chapter-name) | `friendlyName` | string | Nein | Der Name des Kapitels und/oder Segments. |
| [[!UICONTROL Chapter Offset]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=de#chapter-offset) | `offset` | integer | Ja | Der Versatz des Kapitels im Inhalt (in Sekunden) vom Start. |
| [[!UICONTROL Chapter Position]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=de#chapter-position) | `index` | integer | Ja | Die Position (Index, Ganzzahl) des Kapitels im Inhalt. |

{style="table-layout:auto"}
