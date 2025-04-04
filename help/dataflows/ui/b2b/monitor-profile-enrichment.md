---
description: Verwenden Sie das Dashboard [!UICONTROL Profilanreicherung] um zu verstehen, ob Profilanreicherungsaufträge erfolgreich ausgeführt und abgeschlossen wurden, und um die grundlegenden Metriken anzuzeigen, um die Effektivität der Anreicherungen zu messen.
solution: Experience Platform
title: Überwachen von Profilanreicherungsaufträgen
type: Tutorial
exl-id: 096a2212-ed7f-4419-8ead-fa1ca01c2804
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 4%

---

# Überwachen von Aufträgen zur Profilanreicherung in der Benutzeroberfläche {#monitor-profile-enrichment}

Verwenden Sie das Dashboard [!UICONTROL Profilanreicherung] um zu verstehen, ob Profilanreicherungsaufträge erfolgreich ausgeführt und abgeschlossen wurden, und um die grundlegenden Metriken anzuzeigen, um die Effektivität der Anreicherungen zu messen.

Wählen Sie in der [Experience Platform](https://platform.adobe.com)-Benutzeroberfläche **[!UICONTROL Monitoring]** in der linken Navigationsleiste aus, um auf das Dashboard [!UICONTROL Monitoring] zuzugreifen. Wählen Sie in der Ansichtsauswahl die Option **B2B-Fluss** aus, um die für [Real-Time CDP B2B](/help/rtcdp/b2b-overview.md) spezifischen Dashboard-Elemente anzuzeigen.  Das [!UICONTROL Monitoring]-Dashboard enthält die grundlegenden Metriken der letzten erfolgreichen Ausführung und den täglichen Auftragsstatus, der bis zu 90 Tage in der Vergangenheit lag.

## Profilanreicherung für verwandte Konten {#related-accounts}

Das Dashboard [!UICONTROL Verknüpfte Konten] zeigt die grundlegenden Metriken und den Status des täglichen Auftrags an, der spezifisch für die Profilanreicherung [Verknüpfte Konten](/help/rtcdp/b2b-ai-ml-services/related-accounts.md) ist.

![Visueller Hinweis darauf, wie Sie in der Experience Platform-Benutzeroberfläche zum Bildschirm Überwachung von Vorgängen zur Profilanreicherung gelangen.](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

Die Daten in der Karte **[!UICONTROL Metriken]** enthalten die grundlegenden Metriken aus der letzten erfolgreichen Ausführung des Vorgangs für verwandte Konten.

Die folgenden Metriken sind für Vorgänge zur Profilanreicherung bei verwandten Konten verfügbar:

| Metrik | Beschreibung |
| --------- | ---------- |
| **[!UICONTROL Kontoprofile insgesamt]** | Gibt die Gesamtzahl der Kontoprofile an, auf die Ihre Organisation Zugriff hat. |
| **[!UICONTROL Kontogruppen]** | Gibt die Anzahl der Kontogruppen an, die durch den zugehörigen Auftrag für maschinelles Lernen für Konten in einem Cluster zusammengefasst wurden. |
| **[!UICONTROL Einzelkontengruppen]** | Gibt die Anzahl der Konten an, die nicht mit anderen Konten gruppiert sind. |
| **[!UICONTROL Größte Gruppengröße]** | Gibt die Größe der größten verwandten Kontogruppe an. Die maximal zulässige Gruppengröße ist 30. |
| **[!UICONTROL Mediane Gruppengröße]** | Gibt die durchschnittliche Größe verwandter Kontogruppen in Ihrer Organisation an. |
| **[!UICONTROL Letzter erfolgreicher Durchgang]** | Gibt das Datum und die Uhrzeit der letzten erfolgreichen Ausführung des Vorgangs für verwandte Konten an. |
| **[!UICONTROL Status]** | Gibt den Status (erfolgreich, fehlgeschlagen oder Verarbeitung) des zugehörigen Kontoauftrags an. |
| **[!UICONTROL Nachricht]** | Gibt eine Fehler- oder Warnmeldung für einen bestimmten Auftragsdurchgang an. |

## Lead-Konto-Zuordnung Profilanreicherung {#lead-to-account-matching}

Das Dashboard [!UICONTROL Lead-Konto] zeigt die grundlegenden Metriken und den täglichen Auftragsausführungsstatus an, die für die Profilanreicherung [Lead-Konto-Zuordnung](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md) spezifisch sind.

![Lead-Konto-Matching-Profilanreicherung](/help/dataflows/assets/ui/b2b/mpc-lead-to-account-matching.png)

Die folgenden Metriken sind für Vorgänge zur Lead-Konto-Zuordnung von Profilanreicherungen verfügbar:

| Metrik | Beschreibung |
| --------- | ---------- |
| **[!UICONTROL Personen mit Konten insgesamt]** | Gibt die Gesamtzahl der Personen an, die mit einem Konto verknüpft sind. |
| **[!UICONTROL Konten insgesamt]** | Gibt die Gesamtzahl der Konten an. |
| **[!UICONTROL Vorhandene Personen mit Konten]** | Gibt die Anzahl der Personen an, die bereits über die Datenquellen mit einem Konto verknüpft sind. |
| **[!UICONTROL Zugeordnete Personen]** | Gibt die Anzahl der Personen an, die einem Konto zugeordnet wurden. |
| **[!UICONTROL Personen ohne Zuordnung]** | Gibt die Anzahl der Personen an, die keinem Konto zugeordnet wurden. |
| **[!UICONTROL Letzter erfolgreicher Durchgang]** | Gibt das Datum und die Uhrzeit des letzten erfolgreichen Lead-Konto-Matching-Vorgangs an. |
| **[!UICONTROL Status]** | Gibt den Status (erfolgreich, fehlgeschlagen oder Verarbeitung) des Lead-Konto-Abgleichauftrags an. |

## Anreicherung des prädiktiven Lead- und Konto-Scoring-Profils {#predictive-lead-to-account-scoring}

Das Dashboard [!UICONTROL Prädiktives Lead- und Konto] zeigt die grundlegenden Metriken und den täglichen Auftragsausführungsstatus an, die für die Profilanreicherung [Prädiktives Lead- und Konto](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md) spezifisch sind.

![Prädiktive Lead- und Konto-Scoring-Profilanreicherung](/help/dataflows/assets/ui/b2b/predictive-lead-and-account-scoring.png)

Die folgenden Metriken sind für prädiktive Lead- und Konto-Scoring-Profilanreicherungsaufträge verfügbar:

| Metrik | Beschreibung |
| --------- | ---------- |
| **[!UICONTROL Auftragsstart]** | Gibt das Startdatum und die Startzeit des prädiktiven Lead- und Konto-Scoring-Vorgangs an. |
| **[!UICONTROL Verarbeitungszeit]** | Die Gesamtzeit, die für den Abschluss des Auftrags benötigt wurde. |
| **[!UICONTROL Score-Name]** | Der Bewertungsname des Vorgangs. |
| **[!UICONTROL Profiltyp]** | Der Typ der Bewertung: <ul><li>Person</li><li>Konto</li></ul>. |
| **[!UICONTROL Vorgangstyp]** | Der Typ des Auftrags:<ul><li>Bewertung</li><li>Training</li>. |
| **[!UICONTROL Status]** | Gibt den Status (erfolgreich, fehlgeschlagen oder Verarbeitung) des prädiktiven Lead- und Konto-Scoring-Auftrags an. |

## Benutzeroberflächen-Steuerelemente {#ui-controls}

In diesem Abschnitt werden verschiedene Benutzeroberflächenoptionen (UI) in der Monitoring-Benutzeroberfläche beschrieben, mit denen Sie die auf der Seite angezeigten Metriken filtern können.

Verwenden Sie das Pfeilsymbol (![Pfeilsymbol](/help/images/icons/chevron-up.png)), um die Karte am oberen Bildschirmrand zu erweitern oder zu schließen, die Informationen zu den Aufträgen zur Profilanreicherung auf einen Blick anzeigt.

![Bildschirmaufzeichnung, die das Pfeilsymbol „UI-Steuerelement“ anzeigt.](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

Verwenden Sie den Umschalter **[!UICONTROL Metriken und Diagramme]** um die Ansicht zu schließen, die die neuesten Metriken anzeigt.

![Bildschirmaufzeichnung, die den Umschalter für Metriken und Diagramme anzeigt.](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

Verwenden Sie den Umschalter **[!UICONTROL Nur Fehler anzeigen]**, um nur die fehlgeschlagenen Profilanreicherungsaufträge anzuzeigen.

![Bildschirmaufzeichnung, die den Umschalter Nur Fehler anzeigen anzeigt.](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## Nächste Schritte {#next-steps}

Mithilfe dieses Tutorials können Sie jetzt erfolgreich Metriken für Aufträge zur Profilanreicherung überwachen und verstehen. Weiterführende Informationen finden Sie in folgenden Dokumenten:

* [Verwandte Konten in Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [Registerkarte „Verwandte Konten“ im Handbuch zur Benutzeroberfläche für Kontoprofile](/help/rtcdp/accounts/account-profile-ui-guide.md)
* [Lead-Konto-Zuordnung in Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)
* [Prädiktives Lead- und Konto-Scoring in Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
