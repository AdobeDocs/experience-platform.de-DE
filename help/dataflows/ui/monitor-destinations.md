---
keywords: Experience Platform; Startseite; beliebte Themen; Konten überwachen; Datenflüsse überwachen; Datenflüsse; Ziele
description: Mit Zielen können Sie Ihre Daten von Adobe Experience Platform für unzählige externe Partner aktivieren. In diesem Tutorial erfahren Sie, wie Sie mithilfe der Experience Platform-Benutzeroberfläche Datenflüsse für Ihre Ziele überwachen können.
solution: Experience Platform
title: Überwachen von Datenflüssen für Ziele in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
exl-id: 8eb7bb3c-f2dc-4dbc-9cf5-3d5d3224f5f1
source-git-commit: 1d40ef02bd0bdb48bb999c3308f78824f75e3459
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 4%

---

# Überwachen von Datenflüssen auf Ziele in der Benutzeroberfläche

Mit Zielen können Sie Ihre Daten von Adobe Experience Platform für unzählige externe Partner aktivieren. In diesem Tutorial erfahren Sie, wie Sie mithilfe der Experience Platform-Benutzeroberfläche Datenflüsse für Ihre Ziele überwachen können.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Ziele](../../destinations/home.md): Ziele sind vordefinierte Integrationen mit häufig verwendeten Anwendungen, die die nahtlose Aktivierung von Daten aus Platform für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle ermöglichen.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

## Überwachen von Datenflüssen

Navigieren Sie im Arbeitsbereich **[!UICONTROL Ziele]** der Platform-Benutzeroberfläche zur Registerkarte **[!UICONTROL Durchsuchen]** und wählen Sie den Namen eines Ziels aus, das Sie anzeigen möchten.

![](../assets/ui/monitor-destinations/select-destination.png)

Eine Liste der vorhandenen Datenflüsse wird angezeigt. Auf dieser Seite finden Sie eine Liste sichtbarer Datenflüsse, einschließlich Informationen zu Ziel, Benutzername, Anzahl der Datenflüsse und Status.

Weitere Informationen zu Status finden Sie in der folgenden Tabelle:

| Status | Beschreibung |
| ------ | ----------- |
| Aktiviert | Der Status `Enabled` zeigt an, dass ein Datenfluss aktiv ist und Daten gemäß dem Zeitplan erfasst, der ihm bereitgestellt wurde. |
| Deaktiviert | Der Status `Disabled` zeigt an, dass ein Datenfluss inaktiv ist und keine Daten erfasst. |
| Verarbeitung | Der Status `Processing` zeigt an, dass ein Datenfluss noch nicht aktiv ist. Dieser Status tritt oft unmittelbar nach der Erstellung eines neuen Datenflusses auf. |
| Fehler | Der Status `Error` zeigt an, dass der Aktivierungsprozess eines Datenflusses unterbrochen wurde. |

## Datenfluss-Ausführungen für Streaming-Ziele

Für Streaming-Ziele bietet die Registerkarte [!UICONTROL Datenfluss-Läufe] eine stündliche Aktualisierung für Metrikdaten in Ihren Datenfluss-Läufen. Die auffälligsten gekennzeichneten Statistiken sind für Identitäten.

Identitäten stellen die verschiedenen Facetten eines Profils dar. Wenn beispielsweise ein Profil sowohl eine Telefonnummer als auch eine E-Mail-Adresse enthält, hat dieses Profil zwei Identitäten.

Es wird eine Liste einzelner Ausführungen und der jeweiligen Metriken mit den folgenden Gesamtwerten für Identitäten angezeigt:

- **[!UICONTROL Aktivierte]** Identitäten: Die Gesamtzahl der Profilidentitäten, die zur Aktivierung erstellt oder aktualisiert wurden.
- **[!UICONTROL Ausgeschlossene]** Identitäten: Die Gesamtzahl der Profilidentitäten, die zur Aktivierung aufgrund fehlender Attribute und Zustimmungsverstoßes übersprungen werden.
- **[!UICONTROL Identitäten fehlgeschlagen]**: Die Gesamtzahl der Profilidentitäten, die aufgrund von Fehlern nicht für das Ziel aktiviert werden.

![](../assets/ui/monitor-destinations/dataflow-runs-stream.png)

Jeder einzelne Datenfluss zeigt die folgenden Details an:

- **[!UICONTROL Start]** des Datenflusses: Die Zeit, zu der der Datenfluss gestartet wurde.
- **[!UICONTROL Verarbeitungszeit]**: Die Zeitdauer, die die Verarbeitung des Datenflusses dauerte.
- **[!UICONTROL Vorgenommene]** Profile: Die Gesamtzahl der im Datenfluss empfangenen Profile.
- **[!UICONTROL Aktivierte]** Identitäten: Die Gesamtzahl der Profilidentitäten, die erfolgreich für das ausgewählte Ziel aktiviert wurden.
- **[!UICONTROL Ausgeschlossene]** Identitäten: Die Gesamtzahl der Profilidentitäten, die zur Aktivierung aufgrund fehlender Attribute und Zustimmungsverstoßes ausgeschlossen sind.
- **[!UICONTROL Identitäten]** fehlgeschlagenDie Gesamtzahl der Profilidentitäten, die aufgrund von Fehlern nicht für das Ziel aktiviert werden.
- **[!UICONTROL Aktivierungsrate]**: Der Prozentsatz der empfangenen Identitäten, die erfolgreich aktiviert oder übersprungen wurden. Die folgende Formel zeigt, wie dieser Wert berechnet wird:
   ![](../assets/ui/monitor-destinations/activation-rate-formula.png)
- **[!UICONTROL Status]**: Stellt den Status dar, in dem sich der Datenfluss befindet: entweder   Abgeschlossen oder  [!UICONTROL Verarbeitung].  Abgeschlossen bedeutet, dass alle Identitäten für den entsprechenden Datenfluss innerhalb des Zeitraums von einer Stunde erfasst wurden.  Verarbeitung bedeutet, dass die Ausführung des Datenflusses noch nicht abgeschlossen ist.

Um die Details eines bestimmten Datenfluss-Laufs anzuzeigen, wählen Sie die Startzeit der Ausführung aus der Liste aus.

Die Detailseite für einen Datenfluss-Lauf enthält zusätzliche Informationen wie die Anzahl der empfangenen Profile, die Anzahl der aktivierten Identitäten, die Anzahl der fehlgeschlagenen Identitäten und die Anzahl der ausgeschlossenen Identitäten.

![](../assets/ui/monitor-destinations/dataflow-details-stream.png)

Auf der Detailseite wird auch eine Liste mit fehlgeschlagenen Identitäten und ausgeschlossenen Identitäten angezeigt. Es werden Informationen für die fehlgeschlagenen und ausgeschlossenen Identitäten angezeigt, einschließlich Fehlercode, Identitätsanzahl und Beschreibung. Standardmäßig werden in der Liste die fehlgeschlagenen Identitäten angezeigt. Um übersprungene Identitäten anzuzeigen, wählen Sie den Umschalter **[!UICONTROL Ausgeschlossene Identitäten]** aus.

![](../assets/ui/monitor-destinations/dataflow-records-stream.png)

## Datenfluss-Ausführung für Batch-Ziele

Bei Batch-Zielen stellt die Registerkarte [!UICONTROL Datenflüsse] Metrikdaten zu Ihren Datenflug-Ausführungen bereit. Es wird eine Liste einzelner Ausführungen und der jeweiligen Metriken mit den folgenden Gesamtwerten für Identitäten angezeigt:

- **[!UICONTROL Aktivierte]** Identitäten: Die Anzahl der einzelnen Profilidentitäten, die erfolgreich für das ausgewählte Ziel aktiviert wurden.
- **[!UICONTROL Ausgeschlossene]** Identitäten: Die Anzahl der einzelnen Profilidentitäten, die für die Aktivierung für das ausgewählte Ziel ausgeschlossen sind, basierend auf fehlenden Attributen und einer Verletzung der Einwilligung.

![](../assets/ui/monitor-destinations/dataflow-runs-batch.png)

Jeder einzelne Datenfluss zeigt die folgenden Details an:

- **[!UICONTROL Start]** des Datenflusses: Die Zeit, zu der der Datenfluss gestartet wurde.
- **[!UICONTROL Verarbeitungszeit]**: Die Zeit, die für die Verarbeitung des Datenflusses benötigt wurde.
- **[!UICONTROL Vorgenommene]** Profile: Die Gesamtzahl der im Datenfluss empfangenen Profile. Dieser Wert wird alle 60 Minuten aktualisiert.
- **[!UICONTROL Aktivierte]** Identitäten: Die Gesamtzahl der Profilidentitäten, die erfolgreich für das ausgewählte Ziel aktiviert wurden.
- **[!UICONTROL Ausgeschlossene]** Identitäten: Die Gesamtzahl der Profilidentitäten, die zur Aktivierung aufgrund fehlender Attribute und Zustimmungsverstoßes ausgeschlossen sind.
- **[!UICONTROL Status]**: Stellt den Status dar, in dem sich der Datenfluss befindet. Dabei kann es sich um einen von drei Status handeln: [!UICONTROL Erfolg], [!UICONTROL Fehlgeschlagen] und [!UICONTROL Verarbeitung].  Erfolg bedeutet, dass der Datenfluss aktiv ist und Daten gemäß dem bereitgestellten Zeitplan erfasst.  Fehlgeschlagen bedeutet, dass die Aktivierung von Daten aufgrund von Fehlern ausgesetzt wurde.  Verarbeitung bedeutet, dass der Datenfluss noch nicht aktiv ist und im Allgemeinen beim Erstellen eines neuen Datenflusses auftritt.

Um Details zu einem bestimmten Datenfluss-Lauf anzuzeigen, wählen Sie die Startzeit der Ausführung aus der Liste aus.

>[!NOTE]
>
>Datenflüsse werden basierend auf der Zeitplanfrequenz des Zieldatenflusses generiert. Für jede auf ein Segment angewendete Zusammenführungsrichtlinie wird ein separater Datenfluss ausgeführt.

Auf der Detailseite für einen Datenfluss werden neben den Details, die in der Liste der Datenflüsse angezeigt werden, spezifischere Informationen zum Datenfluss angezeigt:

- **[!UICONTROL Datengröße]**: Die Größe des aufgenommenen Datenflusses.
- **[!UICONTROL Dateien insgesamt]**: Die Gesamtzahl der im Datenfluss erfassten Dateien.
- **[!UICONTROL Zuletzt aktualisiert]**: Die Zeit, zu der der Datenfluss zuletzt aktualisiert wurde.

![](../assets/ui/monitor-destinations/dataflow-batch.png)

Auf der Detailseite wird auch eine Liste mit fehlgeschlagenen Identitäten und ausgeschlossenen Identitäten angezeigt. Es werden Informationen für die fehlgeschlagenen und ausgeschlossenen Identitäten angezeigt, einschließlich Fehlercode und Beschreibung. Standardmäßig werden in der Liste die fehlgeschlagenen Identitäten angezeigt. Um ausgeschlossene Identitäten anzuzeigen, wählen Sie den Umschalter **[!UICONTROL Ausgeschlossene Identitäten]** aus.

![](../assets/ui/monitor-destinations/dataflow-records-batch.png)


## Nächste Schritte

In diesem Handbuch erfahren Sie jetzt, wie Sie Datenflüsse für Batch- und Streaming-Ziele überwachen können, einschließlich aller relevanten Informationen wie Verarbeitungszeit, Aktivierungsrate und Status. Weitere Informationen zu Datenflüssen in Platform finden Sie in der [Übersicht der Datenflüsse](../home.md). Weitere Informationen zu Zielen finden Sie in der [Zielübersicht](../../destinations/home.md).