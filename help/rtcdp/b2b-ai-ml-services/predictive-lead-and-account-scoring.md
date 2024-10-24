---
title: Prädiktive Lead- und Kontobewertung in Real-Time CDP B2B
type: Documentation
description: Eine Übersicht und weitere Informationen zur prädiktiven Lead- und Kontoauswertungsfunktion in der Experience Platform CDP B2B.
feature: Profiles, B2B
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: d3afbabb-005d-4537-831a-857c88043759
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 11%

---

# Prädiktive Lead- und Kontobewertung in Real-Time CDP B2B

B2B-Marketer stehen oben im Marketing-Trichter vor mehreren Herausforderungen. Um effektiv zu sein, benötigen B2B-Marketer eine automatisierte Möglichkeit, die große Anzahl von Personen zu qualifizieren, sodass sie sich auf die hochwertigen Ziele konzentrieren können. Die Qualifizierung sollte an dem endgültigen Verkaufsergebnis ausgerichtet werden, nicht nur an der Marketing-Konversion.

Konten, sind die ultimativen Einheiten, die B2B-Produkte und -Dienstleistungen erwerben. Um effektiv zu vermarkten und zu verkaufen, müssen B2B-Marketer nicht nur die Wahrscheinlichkeit kennen, mit der die Person, sondern auch das Konto, kaufen kann.

Kontenbasiertes Marketing, insbesondere die strategische Ausrichtung von Konten als Marketingziele. Die Neigung zum Kauf von Konten hilft den B2B-Marketingexperten bei der Priorisierung der Konten, um ihre Rendite zu maximieren.

Der prädiktive Lead- und Kontoauswertungsdienst behebt die oben genannten Herausforderungen, indem er aus den Konversion-Ereignissen der Opportunitätsstufe lernt und diese vorhersagt und Personenaktivitäten auf Kontoebene aggregiert, um die Kontobewertungen zu erhalten. Die Punktzahlen stehen in benutzerdefinierten Feldern zu Personenprofilen und Kontoprofilen zur Verfügung und können einfach als Segmentkriterien eingefügt werden, um Ihre Zielgruppe zu verfeinern. Wichtigste Einflussfaktoren sind sowohl auf der Aggregat- als auch auf der Einheitenebene verfügbar, damit B2B-Marketer besser verstehen können, welche Elemente zu den Werten geführt haben.

## Prädiktive Lead- und Kontobewertung verstehen {#how-it-works}

>[!NOTE]
>
>[!DNL Marketo] -Datenquelle ist derzeit erforderlich, da dies die einzige Datenquelle ist, die die Konversionsereignisse auf der Ebene des Personenprofils bereitstellen kann.

Die prädiktive Lead- und Kontobewertung verwendet eine baumbasierte (zufällige Forest-/Gradientenverstärkung) maschinelle Lernmethode, um das prädiktive Lead-Scoring-Modell zu erstellen.

Administratoren haben die Möglichkeit, für jedes konfigurierte Konversionsereignis mehrere Profile-Scoring-Ziele zu konfigurieren, die auch als Modelle bezeichnet werden. So können für jedes konfigurierte Ziel separate Bewertungen generiert werden.

Die prädiktive Lead- und Kontoauswertung unterstützt die folgenden Konversionszieltypen und -felder:

| Zieltyp | Felder |
| --- | --- |
| `leadOperation.convertLead` | <ul><li>`leadOperation.convertLead.convertedStatus`</li><li>`leadOperation.convertLead.assignTo`</li></ul> |
| `opportunityEvent.opportunityUpdated` | <ul><li>`opportunityEvent.dataValueChanges.attributeName`</li><li>`opportunityEvent.dataValueChanges.newValue`</li><li>`opportunityEvent.dataValueChanges.oldValue`</li>Beispiel: `opportunityEvent.dataValueChanges.attributeName` gleich `Stage` und `opportunityEvent.dataValueChanges.newValue` gleich `Contract`</ul> |

Der Algorithmus berücksichtigt die folgenden Attribute und Eingabedaten:

* Personenprofil

| XDM-Feld | Erforderlich/Optional |
| --- | --- |
| `personComponents.sourceAccountKey.sourceKey` | Erforderlich |
| `workAddress.country` | Optional |
| `extSourceSystemAudit.createdDate` | Erforderlich |
| `extendedWorkDetails.jobTitle` | Optional |

>[!NOTE]
> 
>Der Algorithmus prüft nur das Feld `sourceAccountKey.sourceKey` in der Feldergruppe Person:personComponents .

* Kontoprofil

| XDM-Feld | Erforderlich/Optional |
| --- | --- |
| `accountKey.sourceKey` | Erforderlich |
| `extSourceSystemAudit.createdDate` | Erforderlich |
| `accountOrganization.industry` | Optional |
| `accountOrganization.numberOfEmployees` | Optional |
| `accountOrganization.annualRevenue.amount` | Optional |

* Erlebnisereignis

| XDM-Feld | Erforderlich/Optional |
| --- | --- |
| `_id` | Erforderlich |
| `personKey.sourceKey` | Erforderlich |
| `timestamp` | Erforderlich |
| `eventType` | Erforderlich |

Es werden mehrere Modelle unterstützt, wobei die folgenden harten Grenzwerte festgelegt sind:

* Jede Produktions-Sandbox hat Anspruch auf fünf Modelle.
* Jede Entwicklungs-Sandbox ist für ein Modell berechtigt.

Die Datenqualitätsanforderungen lauten wie folgt:

* Idealerweise gibt es die zwei Jahre aktuellsten Daten für Schulungszwecke.
* Die erforderliche Mindestlänge der Daten beträgt sechs Monate plus Prognosefenster.
* Für jedes Prognoseziel sind mindestens 10 qualifizierte Konversionsereignisse erforderlich.

Scoring-Aufträge werden täglich ausgeführt und die Ergebnisse werden als Profilattribute und Kontoattribute gespeichert, die dann in Segmentdefinitionen und in der Personalisierung verwendet werden können. Native Analytics-Einblicke sind auch im Dashboard für die Kontoübersicht verfügbar.

Weitere Informationen zum Verwalten des prädiktiven Lead- und Kontoauswertungsdienstes ](/help/rtcdp/b2b-ai-ml-services/manage-predictive-lead-and-account-scoring.md) finden Sie in der Dokumentation .[

## Prognoseergebnisse für Lead- und Kontoauswertung anzeigen {#how-to-view}

Nach Ausführung des Auftrags werden die Ergebnisse in einem neuen Systemdatensatz für jedes Modell unter dem Namen `LeadsAI.Scores` - ***Bewertungsname*** gespeichert. Jede Feldergruppe mit Punktzahl kann sich unter `{CUSTOM_FIELD_GROUP}.LeadsAI.the_score_name` befinden.

| Attribut | Beschreibung |
| --- | --- |
| Ergebnis | Die relative Wahrscheinlichkeit, mit der ein Profil das prognostizierte Ziel innerhalb des definierten Zeitraums erreicht. Dieser Wert ist nicht als Prozentsatz der Wahrscheinlichkeit zu behandeln, sondern vielmehr als die Wahrscheinlichkeit eines Profils im Vergleich zur Gesamtpopulation. Dieser Wert liegt im Bereich von 0 bis 100. |
| Perzentil | Dieser Wert enthält Informationen zur Performance eines Profils im Vergleich zu anderen Profilen mit ähnlichen Werten. Die Perzentile liegen zwischen 1 und 100. |
| Modelltyp | Der ausgewählte Modelltyp gibt an, ob es sich um eine Person oder ein Kontoergebnis handelt. |
| Datum der Auswertung | Das Datum, an dem die Auswertung erfolgte. |
| Einflussfaktoren | Prognostizierte Gründe, warum ein Profil wahrscheinlich konvertiert wird. Die Faktoren bestehen aus den folgenden Attributen:<ul><li>Code: Das Profil- oder Verhaltensattribut, das das prognostizierte Ergebnis eines Profils positiv beeinflusst.</li><li>Wert: Der Wert des Profil- oder Verhaltensattributs.</li><li>Wichtigkeit: Gibt die Gewichtung an, die das Profil- oder Verhaltensattribut auf das prognostizierte Ergebnis hat (niedrig, mittel, hoch).</li></ul> |

### Anzeigen von Kundenprofilbewertungen

Um die Prognosewerte für ein Personenprofil anzuzeigen, wählen Sie im linken Bereich im Abschnitt &quot;Kunde&quot;die Option **[!UICONTROL Profile]** aus und geben Sie dann den Identitäts-Namespace und den Identitätswert ein. Wählen Sie danach **[!UICONTROL Ansicht]** aus.

Wählen Sie anschließend das Profil aus der Liste aus.

![Kundenprofil](/help/rtcdp/accounts/images/b2b-view-customer-profile.png)

Die Seite **[!UICONTROL Detail]** enthält jetzt die Prognosewerte. Klicken Sie auf das Diagrammsymbol neben dem Prädiktivwert.

![Vorhersagewert des Kundenprofils](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score.png)

Ein Popup-Dialogfeld zeigt die Punktzahl, die Verteilung des Gesamtergebnisses, die wichtigsten Einflussfaktoren für dieses Ergebnis und die Definition des Punktziels an.

![Prädiktive Ergebnisdetails des Kundenprofils](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score-details.png)

## Prognostizierende Lead- und Kontobewertungsaufträge überwachen {#monitoring-jobs}

Über das Dashboard können Sie grundlegende Metriken und den täglichen Ausführungsstatus von Aufträgen überwachen. Zu den Metriken gehören:

* Gesamtzahl der bewerteten Personen/Kontoprofile
* Nächster Scoring-Auftrag (Datum)
* Nächster Ausbildungsauftrag (Datum)

Weitere Informationen finden Sie in der Dokumentation zu [Überwachungsaufträgen für prädiktive Lead- und Kontobewertungen](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
