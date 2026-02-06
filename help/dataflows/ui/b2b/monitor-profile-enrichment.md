---
description: Verwenden Sie das [!UICONTROL Profile Enrichment]-Dashboard, um zu verstehen, ob Profilanreicherungsaufträge erfolgreich ausgeführt und abgeschlossen wurden, und um die grundlegenden Metriken anzuzeigen, um die Effektivität der Anreicherungen zu messen.
solution: Experience Platform
title: Überwachen von Profilanreicherungsaufträgen
type: Tutorial
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html#rtcdp-editions" newtab=true
exl-id: 096a2212-ed7f-4419-8ead-fa1ca01c2804
source-git-commit: 0e993f7d0791f5f6f9dce63eb3848609d892e788
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 4%

---

# Überwachen von Aufträgen zur Profilanreicherung in der Benutzeroberfläche {#monitor-profile-enrichment}

Verwenden Sie das [!UICONTROL Profile Enrichment]-Dashboard, um zu verstehen, ob Profilanreicherungsaufträge erfolgreich ausgeführt und abgeschlossen wurden, und um die grundlegenden Metriken anzuzeigen, um die Effektivität der Anreicherungen zu messen.

Wählen Sie in der [Experience Platform](https://platform.adobe.com)Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Monitoring]** aus, um auf das [!UICONTROL Monitoring]-Dashboard zuzugreifen. Wählen Sie in der Ansichtsauswahl die Option **B2B-Fluss** aus, um die für [Real-Time CDP B2B](/help/rtcdp/b2b-overview.md) spezifischen Dashboard-Elemente anzuzeigen.  Das [!UICONTROL Monitoring]-Dashboard enthält die grundlegenden Metriken aus der letzten erfolgreichen Ausführung und den täglichen Auftragsstatus von bis zu 90 Tagen in der Vergangenheit.

## Profilanreicherung für verwandte Konten {#related-accounts}

Im [!UICONTROL Related accounts]-Dashboard werden grundlegende Metriken und der Status des täglichen Auftrags für die Profilanreicherung [Verwandte Konten](/help/rtcdp/b2b-ai-ml-services/related-accounts.md) angezeigt.

![Visueller Hinweis darauf, wie Sie in der Experience Platform-Benutzeroberfläche zum Bildschirm Überwachung von Vorgängen zur Profilanreicherung gelangen.](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

Die Daten in der **[!UICONTROL Metrics]** enthalten die grundlegenden Metriken aus der letzten erfolgreichen Ausführung des Vorgangs für verwandte Konten.

Die folgenden Metriken sind für Vorgänge zur Profilanreicherung bei verwandten Konten verfügbar:

| Metrik | Beschreibung |
| --------- | ---------- |
| **[!UICONTROL Total account profiles]** | Gibt die Gesamtzahl der Kontoprofile an, auf die Ihre Organisation Zugriff hat. |
| **[!UICONTROL Account groups]** | Gibt die Anzahl der Kontogruppen an, die durch den zugehörigen Auftrag für maschinelles Lernen für Konten in einem Cluster zusammengefasst wurden. |
| **[!UICONTROL Single-account groups]** | Gibt die Anzahl der Konten an, die nicht mit anderen Konten gruppiert sind. |
| **[!UICONTROL Largest group size]** | Gibt die Größe der größten verwandten Kontogruppe an. Die maximal zulässige Gruppengröße ist 30. |
| **[!UICONTROL Median group size]** | Gibt die durchschnittliche Größe verwandter Kontogruppen in Ihrer Organisation an. |
| **[!UICONTROL Last successful run]** | Gibt das Datum und die Uhrzeit der letzten erfolgreichen Ausführung des Vorgangs für verwandte Konten an. |
| **[!UICONTROL Status]** | Gibt den Status (erfolgreich, fehlgeschlagen oder Verarbeitung) des zugehörigen Kontoauftrags an. |
| **[!UICONTROL Message]** | Gibt eine Fehler- oder Warnmeldung für einen bestimmten Auftragsdurchgang an. |

## Lead-Konto-Zuordnung Profilanreicherung {#lead-to-account-matching}

Im Dashboard [!UICONTROL Lead to account matching] werden die grundlegenden Metriken und der tägliche Auftragsausführungsstatus angezeigt, die für die Profilanreicherung [Lead-Konto-Zuordnung](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md) spezifisch sind.

![Lead-Konto-Matching-Profilanreicherung](/help/dataflows/assets/ui/b2b/mpc-lead-to-account-matching.png)

Die folgenden Metriken sind für Vorgänge zur Lead-Konto-Zuordnung von Profilanreicherungen verfügbar:

| Metrik | Beschreibung |
| --------- | ---------- |
| **[!UICONTROL Total persons with accounts]** | Gibt die Gesamtzahl der Personen an, die mit einem Konto verknüpft sind. |
| **[!UICONTROL Total accounts]** | Gibt die Gesamtzahl der Konten an. |
| **[!UICONTROL Existing persons with accounts]** | Gibt die Anzahl der Personen an, die bereits über die Datenquellen mit einem Konto verknüpft sind. |
| **[!UICONTROL Persons matched]** | Gibt die Anzahl der Personen an, die einem Konto zugeordnet wurden. |
| **[!UICONTROL Persons unmatched]** | Gibt die Anzahl der Personen an, die keinem Konto zugeordnet wurden. |
| **[!UICONTROL Last successful run]** | Gibt das Datum und die Uhrzeit des letzten erfolgreichen Lead-Konto-Matching-Vorgangs an. |
| **[!UICONTROL Status]** | Gibt den Status (erfolgreich, fehlgeschlagen oder Verarbeitung) des Lead-Konto-Abgleichauftrags an. |

## Anreicherung des prädiktiven Lead- und Konto-Scoring-Profils {#predictive-lead-to-account-scoring}

Im Dashboard [!UICONTROL Predictive lead and account scoring] werden die grundlegenden Metriken und der tägliche Auftragsausführungsstatus angezeigt, die für die Profilanreicherung [Prädiktiver Lead- und ](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)) spezifisch sind.

![Prädiktive Lead- und Konto-Scoring-Profilanreicherung](/help/dataflows/assets/ui/b2b/predictive-lead-and-account-scoring.png)

Die folgenden Metriken sind für prädiktive Lead- und Konto-Scoring-Profilanreicherungsaufträge verfügbar:

| Metrik | Beschreibung |
| --------- | ---------- |
| **[!UICONTROL Job start]** | Gibt das Startdatum und die Startzeit des prädiktiven Lead- und Konto-Scoring-Vorgangs an. |
| **[!UICONTROL Processing time]** | Die Gesamtzeit, die für den Abschluss des Auftrags benötigt wurde. |
| **[!UICONTROL Score name]** | Der Bewertungsname des Vorgangs. |
| **[!UICONTROL Profile type]** | Der Typ der Bewertung: <ul><li>Person</li><li>Konto</li></ul>. |
| **[!UICONTROL Job type]** | Der Typ des Auftrags:<ul><li>Bewertung</li><li>Training</li>. |
| **[!UICONTROL Status]** | Gibt den Status (erfolgreich, fehlgeschlagen oder Verarbeitung) des prädiktiven Lead- und Konto-Scoring-Auftrags an. |

## Benutzeroberflächen-Steuerelemente {#ui-controls}

In diesem Abschnitt werden verschiedene Benutzeroberflächenoptionen (UI) in der Monitoring-Benutzeroberfläche beschrieben, mit denen Sie die auf der Seite angezeigten Metriken filtern können.

Verwenden Sie das Pfeilsymbol (![Pfeilsymbol](/help/images/icons/chevron-up.png)), um die Karte am oberen Bildschirmrand zu erweitern oder zu schließen, die Informationen zu den Aufträgen zur Profilanreicherung auf einen Blick anzeigt.

![Bildschirmaufzeichnung, die das Pfeilsymbol „UI-Steuerelement“ anzeigt.](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

Verwenden Sie den Umschalter **[!UICONTROL Metrics and graphs]** , um die Ansicht zu schließen, die die neuesten Metriken anzeigt.

![Bildschirmaufzeichnung, die den Umschalter für Metriken und Diagramme anzeigt.](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

Verwenden Sie den Umschalter **[!UICONTROL Show failures only]** , um nur die fehlgeschlagenen Profilanreicherungsaufträge anzuzeigen.

![Bildschirmaufzeichnung, die den Umschalter Nur Fehler anzeigen anzeigt.](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## Nächste Schritte {#next-steps}

Mithilfe dieses Tutorials können Sie jetzt erfolgreich Metriken für Aufträge zur Profilanreicherung überwachen und verstehen. Weiterführende Informationen finden Sie in folgenden Dokumenten:

* [Verwandte Konten in Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [Registerkarte „Verwandte Konten“ im Handbuch zur Benutzeroberfläche für Kontoprofile](/help/rtcdp/accounts/account-profile-ui-guide.md)
* [Lead-Konto-Zuordnung in Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)
* [Prädiktives Lead- und Konto-Scoring in Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
