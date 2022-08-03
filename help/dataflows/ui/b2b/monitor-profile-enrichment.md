---
description: Verwenden Sie die [!UICONTROL Profilanreicherung] Dashboard, um zu verstehen, ob die Profilanreicherungsaufträge erfolgreich ausgeführt und abgeschlossen wurden, und um die grundlegenden Metriken zur Messung der Effektivität der Anreicherungen anzuzeigen.
solution: Experience Platform
title: Überwachen von Profilanreicherungsaufträgen
type: Tutorial
exl-id: 096a2212-ed7f-4419-8ead-fa1ca01c2804
source-git-commit: 47a6cc9b77a0591d488d5ebc3929b465e1a6e6d2
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 4%

---

# Überwachen von Profilanreicherungsaufträgen in der Benutzeroberfläche {#monitor-profile-enrichment}

Verwenden Sie die [!UICONTROL Profilanreicherung] Dashboard, um zu verstehen, ob die Profilanreicherungsaufträge erfolgreich ausgeführt und abgeschlossen wurden, und um die grundlegenden Metriken zur Messung der Effektivität der Anreicherungen anzuzeigen.

Im [Platform-Benutzeroberfläche](https://platform.adobe.com)auswählen **[!UICONTROL Überwachung]** über die linke Navigationsleiste auf [!UICONTROL Überwachung] Dashboard. Wählen Sie in der Ansichtsauswahl **B2B-Fluss** um die Dashboard-Elemente anzuzeigen, die spezifisch für [Real-Time CDP B2B](/help/rtcdp/b2b-overview.md).  Die [!UICONTROL Überwachung] Das Dashboard enthält die grundlegenden Metriken aus der letzten erfolgreichen Ausführung sowie den täglichen Auftragsstatus von bis zu 90 Tagen in der Vergangenheit.

## Profilanreicherung für verwandte Konten (#related-accounts)

Die [!UICONTROL Verwandte Konten] Dashboard zeigt grundlegende Metriken und den Status des täglichen Auftrags an, der spezifisch für die [Verwandte Konten](/help/rtcdp/b2b-ai-ml-services/related-accounts.md) Profilanreicherung.

![Visuelle Angabe, wie Sie in der Experience Platform-Benutzeroberfläche zum Überwachungsbildschirm für Profilanreicherungsaufträge gelangen.](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

Die Daten im **[!UICONTROL Metriken]** -Karte enthält die grundlegenden Metriken aus der letzten erfolgreichen Ausführung des Auftrags &quot;Zugehörige Konten&quot;.

Die folgenden Metriken stehen für verwandte Profilanreicherungsaufträge zur Verfügung:

| Metrik | Beschreibung |
| --------- | ---------- |
| **[!UICONTROL Kontoprofile insgesamt]** | Gibt die Gesamtzahl der Kontoprofile an, auf die Ihr Unternehmen Zugriff hat. |
| **[!UICONTROL Kontogruppen]** | Gibt die Anzahl der Kontogruppen an, die durch den entsprechenden maschinellen Lernauftrag für Konten gruppiert wurden. |
| **[!UICONTROL Gruppen mit einem Konto]** | Gibt die Anzahl der Konten an, die nicht mit anderen Konten gruppiert sind. |
| **[!UICONTROL Größte Gruppengröße]** | Gibt die Größe der größten verbundenen Kontogruppe an. Die maximal zulässige Gruppengröße beträgt 30. |
| **[!UICONTROL mittlere Gruppengröße]** | Gibt die mittlere Größe verwandter Kontogruppen in Ihrer Organisation an. |
| **[!UICONTROL Letzte erfolgreiche Ausführung]** | Gibt Datum und Uhrzeit der letzten erfolgreichen Ausführung des verbundenen Kontoauftrags an. |
| **[!UICONTROL Status]** | Gibt den Status (erfolgreich, fehlgeschlagen oder Verarbeitung) des zugehörigen Kontoauftrags an. |
| **[!UICONTROL Nachricht]** | Gibt eine Fehler- oder Warnmeldung für eine bestimmte Auftragsausführung an. |

## Möglichkeit zur Profilanreicherung {#lead-to-account-matching}

Die [!UICONTROL Interessenten-Konto-Abgleich] Dashboard zeigt die grundlegenden Metriken und den täglichen Auftragslaufstatus an, die für die [Interessenten-Konto-Abgleich](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md) Profilanreicherung.

![Möglichkeit zur Profilanreicherung](/help/dataflows/assets/ui/b2b/mpc-lead-to-account-matching.png)

Die folgenden Metriken sind für Lead-Vorgänge verfügbar, bei denen Profile zugeordnet werden:

| Metrik | Beschreibung |
| --------- | ---------- |
| **[!UICONTROL Personen mit Konten insgesamt]** | Gibt die Gesamtzahl der Personen an, die mit einem Konto verknüpft sind. |
| **[!UICONTROL Konten insgesamt]** | Gibt die Gesamtanzahl der Konten an. |
| **[!UICONTROL Bestehende Personen mit Konten]** | Gibt die Anzahl der Personen an, die bereits mit einem Konto aus den Datenquellen verknüpft sind. |
| **[!UICONTROL Übereinstimmende Persons]** | Gibt die Anzahl der Personen an, die mit einem Konto abgeglichen wurden. |
| **[!UICONTROL Nicht übereinstimmende Persons]** | Gibt die Anzahl der Personen an, die keinem Konto zugeordnet wurden. |
| **[!UICONTROL Letzte erfolgreiche Ausführung]** | Gibt das Datum und die Uhrzeit des letzten erfolgreichen Leads an, zu dem der übereinstimmende Auftrag ausgeführt wurde. |
| **[!UICONTROL Status]** | Gibt den Status (erfolgreich, fehlgeschlagen oder Verarbeitung) des Leads an, der zu einem übereinstimmenden Konto führt. |

## UI-Steuerelemente {#ui-controls}

In diesem Abschnitt werden verschiedene Optionen der Benutzeroberfläche in der Monitoring-Oberfläche beschrieben, mit denen Sie die auf der Seite angezeigten Metriken filtern können.

Verwenden Sie das Pfeilsymbol (![Pfeilsymbol](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png)), um die Karte oben im Bildschirm zu erweitern oder zu schließen, die einen Überblick über die Profilanreicherungsvorgänge bietet.

![Bildschirmaufzeichnung, die das Steuerelement der Pfeilsymbolleiste anzeigt.](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

Verwenden Sie die **[!UICONTROL Metriken und Diagramme]** Umschalten, um die Ansicht zu schließen, die die neuesten Metriken anzeigt.

![Bildschirmaufzeichnung, die die Umschaltung zwischen Metriken und Diagrammen anzeigt.](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

Verwenden Sie die **[!UICONTROL Nur Fehler anzeigen]** umschalten, um nur die fehlgeschlagenen Profilanreicherungsaufträge anzuzeigen.

![Bildschirmaufzeichnung, bei der nur der Umschalter Fehler anzeigen angezeigt wird.](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## Nächste Schritte {#next-steps}

In diesem Tutorial können Sie jetzt Metriken für Profilanreicherungsaufträge erfolgreich überwachen und verstehen. Weiterführende Informationen finden Sie in folgenden Dokumenten:

* [Verwandte Konten in der Echtzeit-Kundendatenplattform B2B](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [Registerkarte „Verwandte Konten“ im Handbuch zur Benutzeroberfläche für Kontoprofile](/help/rtcdp/accounts/account-profile-ui-guide.md)
* [Lead zur Kontoübereinstimmung in der Echtzeit-Kundendatenplattform B2B](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)
