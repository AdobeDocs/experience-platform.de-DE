---
title: Advertising Details-Berichtdatentyp
description: Erfahren Sie mehr über den Datentyp Advertising Details Reporting Experience-Datenmodell (XDM) .
exl-id: fbca5b2a-a9bd-4f76-a494-d682cb2cbfbc
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 12%

---

# [!UICONTROL Advertising Details] Berichtdatentyp

[!UICONTROL Advertising Details] -Berichterstellung ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der Schlüsselattribute im Zusammenhang mit Anzeigen erfasst. Dazu gehören Informationen wie die Anzeigen-ID, Advertiser- und Kampagnen-IDs, Länge, Position innerhalb einer Sequenz, Details zum Rendering der Anzeige durch den Player usw. Sie können diesen Datentyp verwenden, um verschiedene Aspekte der Anzeigenleistung und -interaktion zu verfolgen und zu analysieren und Einblicke in die Interaktion und Reaktion von Zielgruppen mit verschiedenen Anzeigen zu erhalten.

+++Auswählen , um ein Diagramm des Datentyps Advertising Details Reporting anzuzeigen.
![Ein Diagramm des Advertising Details-Berichtdatentyps.](../images/data-types/advertising-details-information.png)
+++

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|----------------------------------------|-----------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL Anzeigenname] | `friendlyName` | Zeichenfolge | Der für Menschen lesbare Name der Anzeige. In Berichten ist &quot;Anzeigenname&quot;die Classification und &quot;Anzeigenname (Variable)&quot;der eVar. |
| [!UICONTROL Anzeigen-ID] | `name` | Zeichenfolge | Die ID der Anzeige. Jede Integer- und/oder Buchstaben-Kombination. |
| [!UICONTROL Anzeigenlänge/-dauer] | `length` | integer | Die Länge der Videoanzeige in Sekunden. |
| [!UICONTROL Anzeigenposition innerhalb der Werbeunterbrechung (Anzeigenstart)] | `podPosition` | integer | Der Index der Anzeige innerhalb des übergeordneten Anzeigenstarts, z. B. die erste Anzeige hat den Index 0 und die zweite Anzeige den Index 1. |
| [!UICONTROL Name des Anzeigenplayers] | `playerName` | Zeichenfolge | Der Name des Players, der für das Rendering der Werbeanzeige verantwortlich ist. |
| [!UICONTROL Ad Advertiser] | `advertiser` | Zeichenfolge | Das Unternehmen oder die Marke, deren Produkt in der Anzeige vorgestellt wird. |
| [!UICONTROL Anzeigenkampagne] | `campaignID` | Zeichenfolge | Die ID der Anzeigenkampagne. |
| [!UICONTROL Kreative Anzeigen-ID] | `creativeID` | Zeichenfolge | Die ID des Kreativinhalts der Anzeige. |
| [!UICONTROL Anzeigen-Site-ID] | `siteID` | Zeichenfolge | Die ID der Anzeigen-Site. |
| [!UICONTROL Kreative Anzeigen-URL] | `creativeURL` | Zeichenfolge | Die URL des Kreativinhalts der Anzeige. |
| [!UICONTROL Anzeigen-Platzierungs-ID] | `placementID` | Zeichenfolge | Die Platzierungs-ID der Anzeige. |
| [!UICONTROL  Anzeige abgeschlossen] | `isCompleted` | Boolescher Wert | Verfolgt, ob die Anzeige abgeschlossen wurde. |
| [!UICONTROL Ad Started] | `isStarted` | Boolescher Wert | Verfolgt, ob die Anzeige gestartet wurde. |
| [!UICONTROL  Anzeigenzeit wiedergegeben] | `timePlayed` | integer | Die insgesamt mit der Wiedergabe der Anzeige verbrachte Zeit in Sekunden (also die Anzahl der wiedergegebenen Sekunden). |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im [öffentlichen XDM-Repository](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json)
