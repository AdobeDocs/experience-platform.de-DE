---
title: Datentyp für Advertising-Detailberichte
description: Erfahren Sie mehr über den Datentyp Advertising Details Reporting Experience Data Model (XDM).
exl-id: fbca5b2a-a9bd-4f76-a494-d682cb2cbfbc
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 12%

---

# [!UICONTROL Advertising-Details] Reporting-Datentyp

[!UICONTROL Advertising-]: Reporting ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der wichtige Attribute im Zusammenhang mit Anzeigen erfasst. Sie enthält Informationen wie die Werbe-ID, Advertiser- und Kampagnen-IDs, Länge, Position innerhalb einer Sequenz, Details zum Player, der die Anzeige rendert, und so weiter. Sie können diesen Datentyp verwenden, um verschiedene Aspekte der Anzeigenleistung und -interaktion zu verfolgen und zu analysieren und Einblicke in die Interaktion von Zielgruppen mit verschiedenen Anzeigen und ihre Reaktion darauf zu gewähren.

+++Wählen Sie diese Option aus, um ein Diagramm des Datentyps für Advertising-Detailberichte anzuzeigen.
![Abbildung des Datentyps für Advertising-Detailberichte.](../images/data-types/advertising-details-information.png)
+++

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|----------------------------------------|-----------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL Anzeigenname] | `friendlyName` | Zeichenfolge | Der für Menschen lesbare Name der Anzeige. In Berichten ist „Anzeigename“ die Klassifizierung und „Anzeigename (Variable)“ die eVar. |
| [!UICONTROL Werbe-ID] | `name` | Zeichenfolge | Die ID der Anzeige. Beliebige Ganzzahl und/oder Buchstabenkombination. |
| [!UICONTROL Länge oder Dauer der Anzeige] | `length` | integer | Die Länge der Videoanzeige in Sekunden. |
| [!UICONTROL Anzeige in Pod-Position (Anzeigenstart)] | `podPosition` | integer | Der Index der Anzeige innerhalb des übergeordneten Anzeigenstarts, z. B. hat die erste Anzeige den Index 0 und die zweite Anzeige den Index 1. |
| [!UICONTROL Anzeigenplayer-Name] | `playerName` | Zeichenfolge | Der Name des Players, der für das Rendering der Werbeanzeige verantwortlich ist. |
| [!UICONTROL Werbekunde] | `advertiser` | Zeichenfolge | Die Firma oder Marke, deren Produkt in der Anzeige zu sehen ist. |
| [!UICONTROL Anzeigenkampagne] | `campaignID` | Zeichenfolge | Die ID der Anzeigenkampagne. |
| [!UICONTROL Werbemittel-ID] | `creativeID` | Zeichenfolge | Die ID des Kreativinhalts der Anzeige. |
| [!UICONTROL Anzeigen-Site-ID] | `siteID` | Zeichenfolge | Die ID der Anzeigen-Site. |
| [!UICONTROL Ad Creative URL] | `creativeURL` | Zeichenfolge | Die URL des Kreativinhalts der Anzeige. |
| [!UICONTROL Anzeigenplatzierungs-ID] | `placementID` | Zeichenfolge | Die Platzierungs-ID der Anzeige. |
| [!UICONTROL Anzeige abgeschlossen] | `isCompleted` | Boolescher Wert | Verfolgt, ob die Anzeige abgeschlossen wurde. |
| [!UICONTROL Anzeige gestartet] | `isStarted` | Boolescher Wert | Verfolgt, ob die Anzeige gestartet wurde. |
| [!UICONTROL Anzeigenspielzeit] | `timePlayed` | integer | Die Gesamtzeit in Sekunden, die mit dem Anzeigen verbracht wurde (d. h. die Anzahl der wiedergegebenen Sekunden). |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im [öffentlichen XDM-Repository](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json)
