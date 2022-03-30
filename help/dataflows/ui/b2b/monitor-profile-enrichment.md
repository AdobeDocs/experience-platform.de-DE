---
description: Verwenden Sie die [!UICONTROL Profilanreicherung] Dashboard, um zu verstehen, ob die Profilanreicherungsaufträge erfolgreich ausgeführt und abgeschlossen wurden, und um die grundlegenden Metriken zur Messung der Effektivität der Anreicherungen anzuzeigen.
solution: Experience Platform
title: Überwachen von Profilanreicherungsaufträgen
type: Tutorial
source-git-commit: f3389ef2c2bd9ff52ecde2a4f5fd55e5b86783fc
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 1%

---

# Überwachen von Profilanreicherungsaufträgen in der Benutzeroberfläche

Verwenden Sie die [!UICONTROL Profilanreicherung] Dashboard, um zu verstehen, ob die Profilanreicherungsaufträge erfolgreich ausgeführt und abgeschlossen wurden, und um die grundlegenden Metriken zur Messung der Effektivität der Anreicherungen anzuzeigen.

Im [Platform-Benutzeroberfläche](https://platform.adobe.com)auswählen **[!UICONTROL Überwachung]** über die linke Navigationsleiste auf [!UICONTROL Überwachung] Dashboard. Wählen Sie in der Ansichtsauswahl **B2B-Fluss** um die Dashboard-Elemente anzuzeigen, die spezifisch für [Real-Time CDP B2B](/help/rtcdp/b2b-overview.md).  Die [!UICONTROL Überwachung] Das Dashboard enthält die grundlegenden Metriken aus der letzten erfolgreichen Ausführung sowie den täglichen Auftragsstatus von bis zu 90 Tagen in der Vergangenheit. Die [!UICONTROL Verwandte Konten] Dashboard zeigt die grundlegenden Metriken und den täglichen Auftragsstatus an, die für die [Verwandte Konten](/help/rtcdp/b2b-ai-ml-services/related-accounts.md) Profilanreicherung.

![Visuelle Angabe, wie Sie in der Experience Platform-Benutzeroberfläche zum Überwachungsbildschirm für Profilanreicherungsaufträge gelangen.](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

Die Daten im **[!UICONTROL Metriken]** -Karte enthält die grundlegenden Metriken aus der letzten erfolgreichen Ausführung des Auftrags &quot;Zugehörige Konten&quot;.

Die folgenden Metriken stehen für verwandte Profilanreicherungsaufträge zur Verfügung:

| Metrik | Beschreibung |
---------|----------|
| **[!UICONTROL Kontoprofile insgesamt]** | Gibt die Gesamtzahl der Kontoprofile an, auf die Ihr Unternehmen Zugriff hat. |
| **[!UICONTROL Kontogruppen]** | Gibt die Anzahl der Kontogruppen an, die vom maschinellen Lernauftrag &quot;Ähnliche Konten&quot;geclustert wurden. |
| **[!UICONTROL Gruppen mit einem Konto]** | Gibt die Anzahl der Konten an, die nicht mit anderen Konten gruppiert sind. |
| **[!UICONTROL Größte Gruppengröße]** | Gibt die Größe der größten verbundenen Kontogruppe an. Die maximal zulässige Gruppengröße beträgt 30. |
| **[!UICONTROL mittlere Gruppengröße]** | Gibt die mittlere Größe verwandter Kontogruppen in Ihrer Organisation an. |
| **[!UICONTROL Letzte erfolgreiche Ausführung]** | Gibt Datum und Uhrzeit der letzten erfolgreichen Ausführung des Auftrags &quot;Zugehörige Konten&quot;an. |
| **[!UICONTROL Status]** | Gibt den Status (erfolgreich, fehlgeschlagen oder Verarbeitung) des Auftrags &quot;Zugehörige Konten&quot;an. |
| **[!UICONTROL Nachricht]** | Gibt eine Fehler- oder Warnmeldung für eine bestimmte Auftragsausführung an. |

## UI-Steuerelemente {#ui-controls}

In diesem Abschnitt werden verschiedene Optionen der Benutzeroberfläche in der Monitoring-Oberfläche beschrieben, mit denen Sie die auf der Seite angezeigten Metriken filtern können.

Verwenden Sie das Pfeilsymbol (![Pfeilsymbol](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png)), um die Karte oben im Bildschirm zu erweitern oder zu schließen, die einen Überblick über die Profilanreicherungsvorgänge bietet.

![Bildschirmaufzeichnung, die das Steuerelement der Pfeilsymbolleiste anzeigt.](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

Verwenden Sie die **[!UICONTROL Metriken und Diagramme]** Umschalten, um die Ansicht zu schließen, die die neuesten Metriken anzeigt.

![Bildschirmaufzeichnung, die die Umschaltung zwischen Metriken und Diagrammen anzeigt.](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

Verwenden Sie die **[!UICONTROL Nur Fehler anzeigen]** umschalten, um nur die fehlgeschlagenen Profilanreicherungsaufträge anzuzeigen.

![Bildschirmaufzeichnung, bei der nur der Umschalter Fehler anzeigen angezeigt wird.](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## Nächste Schritte {#next-steps}

Durch Befolgen dieses Tutorials können Sie jetzt Metriken für verwandte Profilanreicherungsaufträge für Konten erfolgreich überwachen und verstehen. Weitere Informationen finden Sie in den folgenden Dokumenten:

* [Verwandte Konten in der Echtzeit-Kundendatenplattform B2B](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [Registerkarte &quot;Zugehörige Konten&quot;im UI-Handbuch für Kontoprofile](/help/rtcdp/accounts/account-profile-ui-guide.md)