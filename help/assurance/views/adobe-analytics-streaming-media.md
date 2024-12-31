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

Durch die Integration zwischen Adobe Analytics für Streaming-Medien und Adobe Experience Platform Assurance können Sie jetzt die Media Analytics-Implementierung in Ihrer Mobile App validieren. In Media Analytics-Ansichten wird angezeigt, was in der Mediensitzung verfolgt wird, z. B.:

- Sitzungsstartereignis, das alle Core-Inhalte, Standard-Metadaten und benutzerdefinierten Metadateneigenschaften sowie Ereignisse zum Sitzungsende und zum Abschluss der Sitzung enthält.
- Start- und Start-Ereignisse für Anzeigenunterbrechungen mit allen angefügten Anzeigeneigenschaften sowie Ereignis „Überspringen“ und „Abschließen“ für beide Ereignisse.
- Kapitelstart mit allen angehängten Eigenschaften sowie die Ereignisse „Kapitelüberspringen“ und „Kapitelabschluss“.
- Alle Wiedergabeveränderungsereignisse (Wiedergabe, Pause, Puffer, Fehler, Bitratenänderung).
- Alle Player-Status ändern Tracking-Ereignisse (Start, Ende).

Sobald Daten in Analytics verarbeitet wurden, sind Status und Daten nach der Verarbeitung, wie z. B. die mit Medien verbrachte Zeit und die gesamte Pausendauer, auch in der Ereignisdetailansicht verfügbar.

## Erste Schritte

Bevor Sie fortfahren, stellen Sie sicher, dass Sie über die folgenden Services verfügen:

- Die Datenerfassungs-Benutzeroberfläche von [Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

Informationen zum Installieren von Assurance in Ihrer Anwendung finden Sie im [Implementierungshandbuch für Assurance](../tutorials/implement-assurance.md).

## Verwenden von Assurance mit Adobe Analytics für Streaming-Medien

Nachdem Sie die Verbindung hergestellt und Ihre App für Adobe Analytics eingerichtet haben, können Sie sie für Streaming Media Analytics konfigurieren. Wählen Sie unten im linken Bedienfeld die Option **[!UICONTROL Konfigurieren]**, um die Ansicht „Media Analytics-Ereignisse“ hinzuzufügen und **Speichern**.

![Konfigurieren](./images/adobe-analytics-streaming-media/configure.png)

Wählen Sie nach dem Hinzufügen die Ansicht **[!UICONTROL Media Analytics-Ereignisse]** im Abschnitt **[!UICONTROL Adobe Analytics]** aus, um Ihr Sitzungs-Tracking zu validieren.

![Auswählen](./images/adobe-analytics-streaming-media/select.png)

In der **[!UICONTROL Media Analytics-Ereignisse]** können Sie nach Sitzungs-ID (VSID) suchen und filtern, um eine bestimmte Mediensitzung anzuzeigen. Um zusätzliche Ereignisdetails anzuzeigen, wählen Sie ein bestimmtes Ereignis aus.

![Medienereignisse](./images/adobe-analytics-streaming-media/media-events.png)

Um eine kürzere Ansicht der API-Aufrufe zu erhalten, können Sie auch die Abspielkopf-Aktualisierungsereignisse ausblenden, indem Sie den Filter **[!UICONTROL Abspielkopf-Aktualisierungsereignisse ausblenden]** auswählen.

![Abspielkopf ausblenden](./images/adobe-analytics-streaming-media/hide-playhead.png)

>[!INFO]
>
>Für die Anzeige nachbearbeiteter Medienanalysedaten müssen SDK-Versionen verwendet werden: Android Media 2.1.2 und iOS AEPMedia 3.0.1 (oder höher)

Um nachverarbeitete Daten anzuzeigen, suchen Sie das Sitzungsstartereignis und überprüfen Sie in der Spalte Status , ob die Sitzung abgeschlossen wurde. Wenn Sie fertig sind, klicken Sie auf das Ereignis, um eine Zusammenfassung der Mediensitzungen in der Ansicht „Ereignisdetails“ anzuzeigen. Für weitere Details scrollen Sie nach unten, um die nachbearbeiteten Details zu finden.

![Nachbearbeitungsansicht](./images/adobe-analytics-streaming-media/post-processed-view.png)
