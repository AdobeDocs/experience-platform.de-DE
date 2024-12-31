---
title: Datentyp der Advertising-Detailsammlung
description: Erfahren Sie mehr über den Datentyp Advertising Details Collection Experience Data Model (XDM).
exl-id: 3f6bf1f9-c728-46af-804a-cb41eb29951b
source-git-commit: 9350cfc299c20bd63a2a559c177b3af02739e5b9
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 14%

---

# [!UICONTROL Advertising-Details] Sammlungsdatentyp

[!UICONTROL Advertising Details]-Sammlung ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der wichtige Attribute im Zusammenhang mit Anzeigen erfasst. Sie enthält Informationen wie die Werbe-ID, Advertiser- und Kampagnen-IDs, Länge, Position innerhalb einer Sequenz, Details zum Player, der die Anzeige rendert, und so weiter. Sie können diesen Datentyp verwenden, um verschiedene Aspekte der Anzeigenleistung und -interaktion zu verfolgen und zu analysieren und Einblicke in die Interaktion von Zielgruppen mit verschiedenen Anzeigen und ihre Reaktion darauf zu gewähren. Diese von Ihnen bereitgestellten Informationen werden zum Tracking Ihrer Streaming-Daten verwendet.

+++Wählen Sie diese Option aus, um ein Diagramm des Datentyps Advertising-Detailsammlung anzuzeigen.
![Abbildung des Datentyps der Advertising-Detailauflistung.](../images/data-types/advertising-details-collection.png)
+++

>[!NOTE]
>
>Jeder Anzeigename enthält einen Link zu weiteren Informationen zu den Audio- und Videoparametern. Die verknüpften Seiten enthalten Details zu den von Adobe erfassten Video-Anzeigendaten, Implementierungswerten, Netzwerkparametern, Berichten und wichtigen Überlegungen.

| Anzeigename | Eigenschaft | Datentyp | Erforderlich | Beschreibung |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|-----------|----------|-----------------------------------------------------------------------------------------------------------------------|
| [[!UICONTROL Werbekunde]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#advertiser) | `advertiser` | Zeichenfolge | Nein | Die Firma oder Marke, deren Produkt in der Anzeige zu sehen ist. |
| [[!UICONTROL Anzeigenkampagne]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#campaign-id) | `campaignID` | Zeichenfolge | Nein | Die ID der Anzeigenkampagne. |
| [[!UICONTROL Werbemittel-ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#creative-id) | `creativeID` | Zeichenfolge | Nein | Die ID des Kreativinhalts der Anzeige. |
| [[!UICONTROL Ad Creative URL]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#creative-url) | `creativeURL` | Zeichenfolge | Nein | Die URL des Kreativinhalts der Anzeige. |
| [[!UICONTROL Anzeige in Pod-Position (Anzeigenstart)]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-start) | `podPosition` | integer | Ja | Der Index der Anzeige innerhalb des übergeordneten Anzeigenstarts, z. B. hat die erste Anzeige den Index 0 und die zweite Anzeige den Index 1. |
| [[!UICONTROL Länge oder Dauer der Anzeige]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-length) | `length` | integer | Ja | Die Länge der Videoanzeige in Sekunden. |
| [[!UICONTROL Anzeigenname]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-name) | `friendlyName` | Zeichenfolge | Ja | Der für Menschen lesbare Name der Anzeige. In Berichten ist „Anzeigename“ die Klassifizierung und „Anzeigename (Variable)“ die eVar. |
| [[!UICONTROL Anzeigenplatzierungs-ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#placement-id) | `placementID` | Zeichenfolge | Nein | Die Platzierungs-ID der Anzeige. |
| [[!UICONTROL Anzeigenplayer-Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-player-name) | `playerName` | Zeichenfolge | Ja | Der Name des Players, der für das Rendering der Werbeanzeige verantwortlich ist. |
| [[!UICONTROL Anzeigen-Site-ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#site-id) | `siteID` | Zeichenfolge | Nein | Die ID der Anzeigen-Site. |

{style="table-layout:auto"}
