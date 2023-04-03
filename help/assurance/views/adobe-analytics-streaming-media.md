---
title: Adobe Analytics für Streaming-Medien-Ansicht in Assurance
description: In diesem Handbuch wird die Verwendung von Adobe Analytics für Streaming-Medien mit Adobe Experience Platform Assurance erläutert.
source-git-commit: 07dc01c11c79ac2dad05d89309cabb5715c0b63c
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 2%

---


# Adobe Analytics für Streaming-Medien-Ansicht in Assurance

Durch die Integration zwischen Adobe Analytics für Streaming-Medien und Adobe Experience Platform Assurance können Sie jetzt die Media Analytics-Implementierung in Ihrer mobilen App validieren. Media Analytics-Ansichten zeigen an, was in der Mediensitzung verfolgt wird, z. B.:

- Sitzungsstartereignis, das alle Content-Core-, Standard-Metadaten- und benutzerdefinierten Metadateneigenschaften sowie Sitzungsende- und Sitzungsabschlussereignisse enthält.
- Ad Break Start- und Ad Start-Ereignisse mit allen angehängten Anzeigeneigenschaften sowie Skip- und Complete-Ereignisse für beide.
- Chapter Start mit allen angehängten Eigenschaften sowie Chapter Skip - und Chapter Complete -Ereignissen.
- Alle Wiedergabe-Änderungsereignisse (Wiedergabe, Pause, Puffer, Fehler, Bitratenänderung).
- Alle Player-Status ändern Tracking-Ereignisse (Start, Ende).

Sobald Daten in Analytics verarbeitet wurden, sind auch der Status und die Daten, die nach der Verarbeitung erfasst wurden, wie z. B. die Besuchszeit für Medien und die Pausierung insgesamt, in der Detailansicht des Ereignisses verfügbar.

## Erste Schritte

Bevor Sie fortfahren, stellen Sie bitte sicher, dass Sie über die folgenden Dienste verfügen:

- Die [Adobe Experience Platform-Datenerfassungs-Benutzeroberfläche](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

Informationen zum Installieren von Assurance in Ihrer Anwendung finden Sie unter [Implementieren des Zuverlässigkeitshandbuchs](../tutorials/implement-assurance.md).

## Verwenden von Assurance mit Adobe Analytics für Streaming-Medien

Nachdem Sie eine Verbindung hergestellt und Ihre App für Adobe Analytics eingerichtet haben, können Sie sie für Streaming Media Analytics konfigurieren. Wählen Sie unten im linken Bedienfeld die Option **[!UICONTROL Konfigurieren]** Hinzufügen der Media Analytics-Ereignisansicht und **Speichern** es.

![Konfigurieren](./images/adobe-analytics-streaming-media/configure.png)

Wählen Sie nach dem Hinzufügen die **[!UICONTROL Media Analytics-Ereignisse]** Ansicht in der **[!UICONTROL Adobe Analytics]** -Abschnitt zur Validierung Ihres Sitzungs-Trackings.

![Auswählen](./images/adobe-analytics-streaming-media/select.png)

Im **[!UICONTROL Media Analytics-Ereignisse]** anzeigen, können Sie nach Sitzungs-ID (VSID) suchen und filtern, um eine bestimmte Mediensitzung anzuzeigen. Um weitere Ereignisdetails anzuzeigen, wählen Sie ein bestimmtes Ereignis aus.

![Media-Ereignisse](./images/adobe-analytics-streaming-media/media-events.png)

Für eine genauere Anzeige von API-Aufrufen können Sie auch die Abspielleistenaktualisierungsereignisse ausblenden, indem Sie die Option **[!UICONTROL Ereignisse zum Aktualisieren der Abspielleiste ausblenden]** Filter.

![Abspielleiste ausblenden](./images/adobe-analytics-streaming-media/hide-playhead.png)

>[!INFO]
>
>Für die Anzeige von nach der Verarbeitung verarbeiteten Medienanalysedaten ist die Verwendung von SDK-Versionen erforderlich: Android Media 2.1.2 und iOS AGPedia 3.0.1 (oder höher)

Um nachverarbeitete Daten anzuzeigen, suchen Sie das Sitzungsstartereignis und überprüfen Sie in der Statusspalte, in der die Sitzung abgeschlossen wurde. Wenn Sie fertig sind, klicken Sie auf das Ereignis, um eine Zusammenfassung der Mediensitzung in der Detailansicht des Ereignisses anzuzeigen. Für weitere Details scrollen Sie nach unten, um die Details nach der Verarbeitung zu finden.

![Ansicht nach Verarbeitung](./images/adobe-analytics-streaming-media/post-processed-view.png)
