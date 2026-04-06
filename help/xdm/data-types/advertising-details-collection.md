---
title: Datentyp der Advertising-Detailsammlung
description: Erfahren Sie mehr über den Datentyp Advertising Details Collection Experience Data Model (XDM).
exl-id: 3f6bf1f9-c728-46af-804a-cb41eb29951b
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 8%

---

# Datentyp der [!UICONTROL Advertising Details]

[!UICONTROL Advertising Details] Sammlung ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der wichtige Attribute im Zusammenhang mit Anzeigen erfasst. Sie enthält Informationen wie die Werbe-ID, Advertiser- und Kampagnen-IDs, Länge, Position innerhalb einer Sequenz, Details zum Player, der die Anzeige rendert, und so weiter. Sie können diesen Datentyp verwenden, um verschiedene Aspekte der Anzeigenleistung und -interaktion zu verfolgen und zu analysieren und Einblicke in die Interaktion von Zielgruppen mit verschiedenen Anzeigen und ihre Reaktion darauf zu gewähren. Diese von Ihnen bereitgestellten Informationen werden zum Tracking Ihrer Streaming-Daten verwendet.

+++Wählen Sie diese Option aus, um ein Diagramm des Datentyps Advertising-Detailsammlung anzuzeigen.
![Abbildung des Datentyps der Advertising-Detailauflistung.](../images/data-types/advertising-details-collection.png)
+++

>[!NOTE]
>
>Jeder Anzeigename enthält einen Link zu weiteren Informationen zu den Audio- und Videoparametern. Die verknüpften Seiten enthalten Details zu den von Adobe erfassten Video- und Anzeigendaten, Implementierungswerten, Netzwerkparametern, Berichten und wichtigen Überlegungen.

| Anzeigename | Eigenschaft | Datentyp | Erforderlich | Beschreibung |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|-----------|----------|-----------------------------------------------------------------------------------------------------------------------|
| [[!UICONTROL Ad Advertiser]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#advertiser) | `advertiser` | string | Nein | Die Firma oder Marke, deren Produkt in der Anzeige zu sehen ist. |
| [[!UICONTROL Ad Campaign]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#campaign-id) | `campaignID` | string | Nein | Die ID der Anzeigenkampagne. |
| [[!UICONTROL Ad Creative ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#creative-id) | `creativeID` | string | Nein | Die ID des Kreativinhalts der Anzeige. |
| [[!UICONTROL Ad Creative URL]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#creative-url) | `creativeURL` | string | Nein | Die URL der kreativen Anzeige. |
| [[!UICONTROL Ad In Pod Position (Ad Start)]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-start) | `podPosition` | integer | Ja | Der Index der Anzeige innerhalb des übergeordneten Anzeigenstarts, z. B. hat die erste Anzeige den Index 0 und die zweite Anzeige den Index 1. |
| [[!UICONTROL Ad Length Or Duration]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-length) | `length` | integer | Ja | Die Länge der Videoanzeige in Sekunden. |
| [[!UICONTROL Ad Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-name) | `friendlyName` | string | Ja | Der für Menschen lesbare Name der Anzeige. Beim Reporting ist „Anzeigename“ die Klassifizierung und „Anzeigename (Variable)“ die eVar. |
| [[!UICONTROL Ad Placement ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#placement-id) | `placementID` | string | Nein | Die Platzierungs-ID der Anzeige. |
| [[!UICONTROL Ad Player Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-player-name) | `playerName` | string | Ja | Der Name des Players, der für das Rendering der Anzeige verantwortlich ist. |
| [[!UICONTROL Ad Site ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#site-id) | `siteID` | string | Nein | Die ID der Anzeigen-Site. |

{style="table-layout:auto"}
