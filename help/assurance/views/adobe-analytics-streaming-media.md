---
title: Adobe Analytics für Streaming-Medien-Ansicht in Assurance
description: In diesem Handbuch wird die Verwendung von Adobe Analytics für Streaming-Medien mit Adobe Experience Platform Assurance erläutert.
exl-id: 9a9c2c64-e9ed-4d58-b936-d802f1c3b7d3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

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

Weiterführende Informationen zur Installation von Assurance in Ihrer Anwendung finden Sie im [Implementierungshandbuch für Assurance](../tutorials/implement-assurance.md).

## Verwenden von Assurance mit Adobe Analytics für Streaming-Medien

Nachdem Sie eine Verbindung hergestellt und Ihre App für Adobe Analytics eingerichtet haben, können Sie sie für Streaming Media Analytics konfigurieren. Wählen Sie unten im linken Bereich **[!UICONTROL Konfigurieren]** aus, um die Ansicht &quot;Media Analytics Events&quot;hinzuzufügen, und **Speichern** Sie sie.

![Konfigurieren](./images/adobe-analytics-streaming-media/configure.png)

Wählen Sie nach dem Hinzufügen die Ansicht **[!UICONTROL Media Analytics-Ereignisse]** im Abschnitt **[!UICONTROL Adobe Analytics]** aus, um das Sitzungs-Tracking zu überprüfen.

![Select](./images/adobe-analytics-streaming-media/select.png)

In der Ansicht **[!UICONTROL Media Analytics-Ereignisse]** können Sie nach Sitzungs-ID (VSID) suchen und filtern, um eine bestimmte Mediensitzung anzuzeigen. Um weitere Ereignisdetails anzuzeigen, wählen Sie ein bestimmtes Ereignis aus.

![Medienereignisse](./images/adobe-analytics-streaming-media/media-events.png)

Für eine präzisere Ansicht von API-Aufrufen können Sie auch die Aktualisierungsereignisse der Abspielleiste ausblenden, indem Sie den Filter **[!UICONTROL Ereignisse der Abspielleistenaktualisierung ausblenden]** auswählen.

![Abspielleiste ausblenden](./images/adobe-analytics-streaming-media/hide-playhead.png)

>[!INFO]
>
>Für die Anzeige von nachbearbeiteten Medienanalysedaten müssen SDK-Versionen verwendet werden: Android Media 2.1.2 und iOS AGPedia 3.0.1 (oder höher).

Um nachverarbeitete Daten anzuzeigen, suchen Sie das Sitzungsstartereignis und überprüfen Sie in der Statusspalte, in der die Sitzung abgeschlossen wurde. Wenn Sie fertig sind, klicken Sie auf das Ereignis, um eine Zusammenfassung der Mediensitzung in der Detailansicht des Ereignisses anzuzeigen. Für weitere Details scrollen Sie nach unten, um die Details nach der Verarbeitung zu finden.

![Ansicht mit Post-Verarbeitung](./images/adobe-analytics-streaming-media/post-processed-view.png)
