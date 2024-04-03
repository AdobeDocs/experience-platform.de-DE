---
title: Berichtdatentyp für Werbedetails
description: Erfahren Sie mehr über den Datentyp "Advertising Details Reporting Experience Data Model"(XDM).
source-git-commit: a604dc8b541784ace8aedef42030e5bd8b646c28
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 12%

---

# [!UICONTROL Werbedetails] Berichtdatentyp

[!UICONTROL Werbedetails] Die Berichterstellung ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Schlüsselattribute im Zusammenhang mit Werbung erfasst. Dazu gehören Informationen wie die Anzeigen-ID, Advertiser- und Kampagnen-IDs, Länge, Position innerhalb einer Sequenz, Details zum Rendering der Anzeige durch den Player usw. Sie können diesen Datentyp verwenden, um verschiedene Aspekte der Anzeigenleistung und -interaktion zu verfolgen und zu analysieren und Einblicke in die Interaktion und Reaktion von Zielgruppen mit verschiedenen Anzeigen zu erhalten.

+++Auswählen , um ein Diagramm des Datentyps Werbedetails anzuzeigen.
![Ein Diagramm des Datentyps Advertising Details Reporting .](../images/data-types/advertising-details-information.png)
+++

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|----------------------------------------|-----------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL Anzeigenname] | `friendlyName` | Zeichenfolge | Der für Menschen lesbare Name der Anzeige. In Berichten stellt „Anzeigenname“ die Klassifizierung und „Anzeigenname (Variable)“ das eVar dar. |
| [!UICONTROL Anzeigen-ID] | `name` | Zeichenfolge | Die ID der Anzeige. Beliebige Integer- und/oder Buchstaben-Kombination. |
| [!UICONTROL Anzeigenlänge oder -dauer] | `length` | integer | Die Länge der Videoanzeige in Sekunden. |
| [!UICONTROL Anzeigenposition innerhalb der Werbeunterbrechung (Anzeigenstart)] | `podPosition` | integer | Der Index der Anzeige innerhalb des übergeordneten Anzeigenstarts, z. B. die erste Anzeige hat den Index 0 und die zweite Anzeige den Index 1. |
| [!UICONTROL Name des Anzeigenplayers] | `playerName` | Zeichenfolge | Der Name des Players, der für die Wiedergabe der Anzeige verantwortlich ist. |
| [!UICONTROL Advertiser] | `advertiser` | Zeichenfolge | Das Unternehmen oder die Marke, deren Produkt in der Anzeige vorgestellt wird. |
| [!UICONTROL Anzeigenkampagne] | `campaignID` | Zeichenfolge | Die ID der Anzeigenkampagne. |
| [!UICONTROL Kreativ-ID der Anzeige] | `creativeID` | Zeichenfolge | Die ID des Anzeigenmotivs. |
| [!UICONTROL Anzeigen-Site-ID] | `siteID` | Zeichenfolge | Die ID der Anzeigen-Site. |
| [!UICONTROL Kreative Anzeigen-URL] | `creativeURL` | Zeichenfolge | Die URL des Anzeigenmotivs. |
| [!UICONTROL Anzeigenplatzierungs-ID] | `placementID` | Zeichenfolge | Die Platzierungs-ID der Anzeige. |
| [!UICONTROL Anzeige abgeschlossen] | `isCompleted` | Boolescher Wert | Verfolgt, ob die Anzeige abgeschlossen wurde. |
| [!UICONTROL Anzeigenstarts] | `isStarted` | Boolescher Wert | Verfolgt, ob die Anzeige gestartet wurde. |
| [!UICONTROL Wiedergabedauer der Anzeige] | `timePlayed` | integer | Die insgesamt mit der Wiedergabe der Anzeige verbrachte Zeit in Sekunden (also die Anzahl der wiedergegebenen Sekunden). |

{style="table-layout:auto"}

Weiterführende Informationen zur Feldergruppe finden Sie im Abschnitt [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json)
