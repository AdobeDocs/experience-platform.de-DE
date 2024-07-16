---
description: Verwenden Sie das Dashboard [!UICONTROL Profilanreicherung] , um zu verstehen, ob die Profilanreicherungsaufträge erfolgreich ausgeführt und abgeschlossen wurden, und um die grundlegenden Metriken zur Messung der Effektivität der Anreicherungen anzuzeigen.
solution: Experience Platform
title: Überwachen von Profilanreicherungsaufträgen
type: Tutorial
exl-id: 096a2212-ed7f-4419-8ead-fa1ca01c2804
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 4%

---

# Überwachen von Profilanreicherungsaufträgen in der Benutzeroberfläche {#monitor-profile-enrichment}

Verwenden Sie das Dashboard [!UICONTROL Profilanreicherung] , um zu verstehen, ob die Profilanreicherungsaufträge erfolgreich ausgeführt und abgeschlossen wurden, und um die grundlegenden Metriken zur Messung der Effektivität der Anreicherungen anzuzeigen.

Wählen Sie in der [Platform-Benutzeroberfläche](https://platform.adobe.com) im linken Navigationsbereich die Option **[!UICONTROL Überwachung]** aus, um auf das Dashboard [!UICONTROL Überwachung] zuzugreifen. Wählen Sie in der Ansichtsauswahl **B2B Flow** aus, um die für [Real-Time CDP B2B](/help/rtcdp/b2b-overview.md) spezifischen Dashboard-Elemente anzuzeigen.  Das Dashboard [!UICONTROL Überwachung] enthält die grundlegenden Metriken aus der letzten erfolgreichen Ausführung sowie den täglichen Auftragsstatus von bis zu 90 Tagen in der Vergangenheit.

## Profilanreicherung für verwandte Konten {#related-accounts}

Das Dashboard [!UICONTROL Zugehörige Konten] enthält grundlegende Metriken und den Status des täglichen Auftrags, der spezifisch für die Profilanreicherung [Zugehörige Konten](/help/rtcdp/b2b-ai-ml-services/related-accounts.md) ist.

![ Visuelle Angabe, wie Sie in der Experience Platform-Benutzeroberfläche zum Überwachungsbildschirm für Profilanreicherungsaufträge gelangen.](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

Die Daten auf der Karte **[!UICONTROL Metriken]** enthalten die grundlegenden Metriken aus der letzten erfolgreichen Ausführung des Auftrags &quot;Zugehörige Konten&quot;.

Die folgenden Metriken stehen für verwandte Profilanreicherungsaufträge zur Verfügung:

| Metrik | Beschreibung |
| --------- | ---------- |
| **[!UICONTROL Kontoprofile insgesamt]** | Gibt die Gesamtzahl der Kontoprofile an, auf die Ihr Unternehmen Zugriff hat. |
| **[!UICONTROL Kontogruppen]** | Gibt die Anzahl der Kontogruppen an, die durch den entsprechenden maschinellen Lernauftrag für Konten gruppiert wurden. |
| **[!UICONTROL Gruppen mit einzelnen Konten]** | Gibt die Anzahl der Konten an, die nicht mit anderen Konten gruppiert sind. |
| **[!UICONTROL Größte Gruppengröße]** | Gibt die Größe der größten verbundenen Kontogruppe an. Die maximal zulässige Gruppengröße beträgt 30. |
| **[!UICONTROL mittlere Gruppengröße]** | Gibt die mittlere Größe verwandter Kontogruppen in Ihrer Organisation an. |
| **[!UICONTROL Letzter erfolgreicher Lauf]** | Gibt Datum und Uhrzeit der letzten erfolgreichen Ausführung des verbundenen Kontoauftrags an. |
| **[!UICONTROL Status]** | Gibt den Status (erfolgreich, fehlgeschlagen oder Verarbeitung) des zugehörigen Kontoauftrags an. |
| **[!UICONTROL Message]** | Gibt eine Fehler- oder Warnmeldung für eine bestimmte Auftragsausführung an. |

## Möglichkeit zur Profilanreicherung {#lead-to-account-matching}

Das Dashboard [!UICONTROL Lead zum Abgleich von Konten] zeigt die grundlegenden Metriken und den täglichen Auftragslaufstatus an, die für die [Lead zum Abgleichen der Profilanreicherung](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md) spezifisch sind.

![Lead zur Berücksichtigung der Profilanreicherung](/help/dataflows/assets/ui/b2b/mpc-lead-to-account-matching.png)

Die folgenden Metriken sind für Lead-Vorgänge verfügbar, bei denen Profile zugeordnet werden:

| Metrik | Beschreibung |
| --------- | ---------- |
| **[!UICONTROL Personen mit Konten insgesamt]** | Gibt die Gesamtzahl der Personen an, die mit einem Konto verknüpft sind. |
| **[!UICONTROL Konten insgesamt]** | Gibt die Gesamtanzahl der Konten an. |
| **[!UICONTROL Vorhandene Personen mit Konten]** | Gibt die Anzahl der Personen an, die bereits mit einem Konto aus den Datenquellen verknüpft sind. |
| **[!UICONTROL Entsprechende Personen]** | Gibt die Anzahl der Personen an, die mit einem Konto abgeglichen wurden. |
| **[!UICONTROL Nicht übereinstimmende Personen]** | Gibt die Anzahl der Personen an, die keinem Konto zugeordnet wurden. |
| **[!UICONTROL Letzter erfolgreicher Lauf]** | Gibt das Datum und die Uhrzeit des letzten erfolgreichen Leads an, zu dem der übereinstimmende Auftrag ausgeführt wurde. |
| **[!UICONTROL Status]** | Gibt den Status (erfolgreich, fehlgeschlagen oder Verarbeitung) des Leads an, der zu einem übereinstimmenden Konto führt. |

## Prädiktive Profilanreicherung für Lead- und Kontobewertung {#predictive-lead-to-account-scoring}

Das Dashboard [!UICONTROL Prädiktive Lead- und Kontobewertung] zeigt die grundlegenden Metriken und den täglichen Auftragslaufstatus an, die für die Profilanreicherung [Prädiktiver Lead und Kontoauswertung](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md) spezifisch sind.

![Anreicherung des prädiktiven Lead- und Kontoauswertungsprofils](/help/dataflows/assets/ui/b2b/predictive-lead-and-account-scoring.png)

Die folgenden Metriken sind für prädiktive Anreicherungsaufträge für Lead- und Kontobewertungsprofile verfügbar:

| Metrik | Beschreibung |
| --------- | ---------- |
| **[!UICONTROL Auftragsstart]** | Gibt das Startdatum und die Startzeit des prädiktiven Lead- und Kontoauswertungsauftrags an. |
| **[!UICONTROL Verarbeitungszeit]** | Die Gesamtdauer, die zum Abschluss des Auftrags benötigt wurde. |
| **[!UICONTROL Score name]** | Der Bewertungsname des Auftrags. |
| **[!UICONTROL Profiltyp]** | Der Typ der Punktzahl: <ul><li>Person</li><li>Konto</li></ul>. |
| **[!UICONTROL Auftragstyp]** | Der Auftragstyp:<ul><li>Bewertung</li><li>Training</li>. |
| **[!UICONTROL Status]** | Gibt den Status (erfolgreich, fehlgeschlagen oder Verarbeitung) des prädiktiven Lead- und Kontobewertungsauftrags an. |

## UI-Steuerelemente {#ui-controls}

In diesem Abschnitt werden verschiedene Optionen der Benutzeroberfläche in der Monitoring-Oberfläche beschrieben, mit denen Sie die auf der Seite angezeigten Metriken filtern können.

Verwenden Sie das Pfeilsymbol (![Pfeilsymbol](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png)), um die Karte oben im Bildschirm zu erweitern oder zu schließen, die einen Überblick über die Profilanreicherungsvorgänge bietet.

![Bildschirmaufzeichnung, die das Benutzeroberflächensteuerelement mit dem Pfeilsymbol anzeigt.](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

Mit dem Umschalter **[!UICONTROL Metriken und Diagramme]** können Sie die Ansicht schließen, die die neuesten Metriken anzeigt.

![Bildschirmaufzeichnung, die die Umschaltung der Metriken und Diagramme anzeigt.](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

Verwenden Sie den Umschalter **[!UICONTROL Nur Fehler anzeigen]** , um nur die fehlgeschlagenen Profilanreicherungsaufträge anzuzeigen.

![Bildschirmaufzeichnung, die nur den Umschalter Fehler anzeigen anzeigt.](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## Nächste Schritte {#next-steps}

In diesem Tutorial können Sie jetzt Metriken für Profilanreicherungsaufträge erfolgreich überwachen und verstehen. Weiterführende Informationen finden Sie in folgenden Dokumenten:

* [Verwandte Konten in Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [Registerkarte „Verwandte Konten“ im Handbuch zur Benutzeroberfläche für Kontoprofile](/help/rtcdp/accounts/account-profile-ui-guide.md)
* [Lead zur Kontoübereinstimmung in Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)
* [Prädiktive Lead- und Kontobewertung in Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
