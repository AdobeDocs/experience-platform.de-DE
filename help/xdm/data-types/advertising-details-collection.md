---
title: Datenerfassungstyp für Anzeigendetails
description: Erfahren Sie mehr über den Datentyp "Experience-Datenmodell (XDM) der Advertising Details-Sammlung".
source-git-commit: fe239bee3c853d43c04200092f59537dfeb00c87
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 12%

---

# [!UICONTROL Werbedetails] Sammlungsdatentyp

[!UICONTROL Werbedetails] Sammlung ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Schlüsselattribute im Zusammenhang mit Werbung erfasst. Dazu gehören Informationen wie die Anzeigen-ID, Advertiser- und Kampagnen-IDs, Länge, Position innerhalb einer Sequenz, Details zum Rendering der Anzeige durch den Player usw. Sie können diesen Datentyp verwenden, um verschiedene Aspekte der Anzeigenleistung und -interaktion zu verfolgen und zu analysieren und Einblicke in die Interaktion und Reaktion von Zielgruppen mit verschiedenen Anzeigen zu erhalten. Diese Informationen werden zur Verfolgung Ihrer Streaming-Daten verwendet.

++ + Wählen Sie diese Option aus, um ein Diagramm des Datentyps &quot;Sammlung von Werbedetails&quot;anzuzeigen.
![Ein Diagramm des Datentyps der Sammlung von Werbedetails.](../images/data-types/advertising-details-collection.png)
+++

>[!NOTE]
>
>Jeder Anzeigename enthält einen Link zu weiteren Informationen zu den Audio- und Videoparametern. Die verknüpften Seiten enthalten Details zu den von Adobe erfassten Videoanzeigendaten, Implementierungswerten, Netzwerkparametern, Berichten und wichtigen Aspekten.

| Anzeigename | Eigenschaft | Datentyp | Erforderlich | Beschreibung |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|-----------|----------------------------------------------------------------------------------------------------------------------------------|
| [[!UICONTROL Advertiser]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#advertiser) | `advertiser` | Zeichenfolge | Nein | Das Unternehmen oder die Marke, deren Produkt in der Anzeige vorgestellt wird. |
| [[!UICONTROL Anzeigenkampagne]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#campaign-id) | `campaignID` | Zeichenfolge | Nein | Die ID der Anzeigenkampagne. |
| [[!UICONTROL Kreativ-ID der Anzeige]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#creative-id) | `creativeID` | Zeichenfolge | Nein | Die ID des Anzeigenmotivs. |
| [[!UICONTROL Kreative Anzeigen-URL]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#creative-url) | `creativeURL` | Zeichenfolge | Nein | Die URL des Anzeigenmotivs. |
| [[!UICONTROL Anzeigenposition innerhalb der Werbeunterbrechung (Anzeigenstart)]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-start) | `podPosition` | integer | Ja | Der Index der Anzeige innerhalb des übergeordneten Anzeigenstarts, z. B. die erste Anzeige hat den Index 0 und die zweite Anzeige den Index 1. |
| [[!UICONTROL Anzeigenlänge oder -dauer]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-length) | `length` | integer | Ja | Die Länge der Videoanzeige in Sekunden. |
| [[!UICONTROL Anzeigenname]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-name) | `friendlyName` | Zeichenfolge | Ja | Der für Menschen lesbare Name der Anzeige. In Berichten stellt „Anzeigenname“ die Klassifizierung und „Anzeigenname (Variable)“ das eVar dar. |
| [[!UICONTROL Anzeigenplatzierungs-ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#placement-id) | `placementID` | Zeichenfolge | Nein | Die Platzierungs-ID der Anzeige. |
| [[!UICONTROL Name des Anzeigenplayers]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-player-name) | `playerName` | Zeichenfolge | Ja | Der Name des Players, der für die Wiedergabe der Anzeige verantwortlich ist. |
| [[!UICONTROL Anzeigen-Site-ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#site-id) | `siteID` | Zeichenfolge | Nein | Die ID der Anzeigen-Site. |
