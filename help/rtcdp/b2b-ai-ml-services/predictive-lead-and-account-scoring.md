---
title: Prädiktives Lead- und Konto-Scoring in Real-Time CDP B2B
type: Documentation
description: Einen Überblick und weitere Informationen zur Funktion der prädiktiven Lead- und Konto-Bewertung in Experience Platform CDP B2B.
feature: Profiles, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: d3afbabb-005d-4537-831a-857c88043759
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 11%

---

# Prädiktives Lead- und Konto-Scoring in Real-Time CDP B2B

B2B-Marketing-Experten stehen im Marketing-Trichter vor mehreren Herausforderungen. Um effektiv zu sein, benötigen B2B-Marketer eine automatisierte Möglichkeit, die große Anzahl von Personen zu qualifizieren, damit sie sich auf die hochwertigen Ziele konzentrieren können. Die Qualifizierung sollte auf das endgültige Verkaufsergebnis abgestimmt sein, nicht nur auf die Marketing-Konversion.

Konten sind die letztendlichen Entitäten, die B2B-Produkte und -Services erwerben. Um effektiv zu vermarkten und zu verkaufen, müssen B2B-Marketer nicht nur die Kaufwahrscheinlichkeit einer Person kennen, sondern auch die Kaufwahrscheinlichkeit des Kontos.

Kontobasiertes Marketing, insbesondere strategische Konten als Marketingziele. Die Werte für die Kontenneigung zum Kaufen helfen den B2B-Marketing-Experten, bei den Accounts Prioritäten zu setzen, um den ROI zu maximieren.

Der prädiktive Lead- und Konto-Scoring-Service löst die oben genannten Herausforderungen, indem er aus Opportunity-Konversionsereignissen lernt und diese vorhersagt und Personenaktivitäten auf Kontoebene aggregiert, um Kontobewertungen zu generieren. Die Bewertungen sind als benutzerdefinierte Felder für Personenprofile und Kontoprofile jederzeit verfügbar und können einfach als Segmentkriterien aufgenommen werden, um Ihre Audience zu verfeinern. Die wichtigsten Einflussfaktoren sind sowohl auf aggregierter Ebene als auch auf Einheitenebene verfügbar, damit B2B-Marketing-Fachleute besser verstehen können, welche Elemente zu den Bewertungen geführt haben.

## Verstehen von prädiktivem Lead- und Konto-Scoring {#how-it-works}

>[!NOTE]
>
>[!DNL Marketo] Datenquelle ist derzeit erforderlich, da sie die einzige Datenquelle ist, die die Konversionsereignisse auf Personenprofilebene bereitstellen kann.

Beim prädiktiven Lead- und Konto-Scoring wird eine auf Baumstrukturen (Random Forest/Gradienten-Boosting) basierende maschinelle Lernmethode zum Erstellen des prädiktiven Lead-Scoring-Modells verwendet.

Administratoren haben die Möglichkeit, mehrere Profilbewertungsziele zu konfigurieren, auch als Modelle bezeichnet, ein für jedes konfigurierte Konversionsereignis, sodass für jedes konfigurierte Ziel separate Bewertungen generiert werden können.

Die prädiktive Lead- und Konto-Bewertung unterstützt die folgenden Konversionszieltypen und -felder:

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
>Der Algorithmus prüft nur `sourceAccountKey.sourceKey` Feld in der Feldergruppe Person:personComponents .

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

Es werden mehrere Modelle unterstützt, wobei die folgenden harten Beschränkungen gelten:

* Jede Produktions-Sandbox hat die Berechtigung für fünf Modelle.
* Jede Entwicklungs-Sandbox hat die Berechtigung für ein Modell.

Die Anforderungen an die Datenqualität lauten wie folgt:

* Idealerweise gibt es die neuesten Daten für Trainingszwecke für zwei Jahre.
* Die erforderliche Mindestlänge von Daten beträgt sechs Monate plus Prognosefenster.
* Für jedes Prognoseziel sind mindestens 10 qualifizierte Konversionsereignisse erforderlich.

Bewertungsaufträge werden täglich ausgeführt und die Ergebnisse werden als Profilattribute und Kontoattribute gespeichert, die dann in Segmentdefinitionen und in der Personalisierung verwendet werden können. Vorkonfigurierte Analytics-Einblicke sind auch im Dashboard zur Kontoübersicht verfügbar.

Weitere Informationen finden Sie in der Dokumentation zum [Verwalten von prädiktivem Lead- und Konto-Scoring](/help/rtcdp/b2b-ai-ml-services/manage-predictive-lead-and-account-scoring.md)Service.

## Anzeigen prädiktiver Lead- und Konto-Bewertungsergebnisse {#how-to-view}

Nach dem Auftragsdurchgang werden die Ergebnisse für jedes Modell in einem neuen Systemdatensatz unter dem Namen `LeadsAI.Scores` gespeichert - ***Score-Name***. Jede Score-Feldergruppe befindet sich unter `{CUSTOM_FIELD_GROUP}.LeadsAI.the_score_name`.

| Attribut | Beschreibung |
| --- | --- |
| Ergebnis | Die relative Wahrscheinlichkeit, dass ein Profil das prognostizierte Ziel innerhalb des definierten Zeitraums erreicht. Dieser Wert ist nicht als Wahrscheinlichkeitsprozentsatz zu behandeln, sondern als die Wahrscheinlichkeit eines Profils im Vergleich zur Gesamtpopulation. Dieser Wert liegt im Bereich von 0 bis 100. |
| Perzentil | Dieser Wert enthält Informationen zur Performance eines Profils im Vergleich zu anderen Profilen mit ähnlichen Werten. Die Perzentile liegen zwischen 1 und 100. |
| Modelltyp | Der ausgewählte Modelltyp gibt an, ob es sich um eine Personen- oder Kontobewertung handelt. |
| Datum der Auswertung | Das Datum, an dem die Auswertung erfolgte. |
| Einflussfaktoren | Prognostizierte Gründe für die wahrscheinliche Konversion eines Profils. Die Faktoren bestehen aus den folgenden Attributen:<ul><li>Code: Das Profil- oder Verhaltensattribut, das das prognostizierte Ergebnis eines Profils positiv beeinflusst.</li><li>Wert: Der Wert des Profil- oder Verhaltensattributs.</li><li>Wichtigkeit: Gibt die Gewichtung an, die das Profil- oder Verhaltensattribut in Bezug auf den prognostizierten Wert hat (niedrig, mittel, hoch).</li></ul> |

### Anzeigen der Bewertungen von Kundenprofilen

Um die prädiktiven Bewertungen für ein Personenprofil anzuzeigen, wählen Sie **[!UICONTROL Profile]** im Abschnitt Kunde im linken Bereich aus und geben Sie dann den Identity-Namespace und den Identitätswert ein. Klicken Sie abschließend auf **[!UICONTROL Anzeigen]**.

Wählen Sie anschließend das Profil aus der Liste aus.

![Kundenprofil](/help/rtcdp/accounts/images/b2b-view-customer-profile.png)

Die **[!UICONTROL Detail]**-Seite enthält jetzt die Prognosewerte. Klicken Sie auf das Diagrammsymbol neben dem Prognosewert.

![Prognosewert des Kundenprofils](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score.png)

In einem Popup-Dialogfeld werden die Punktzahl, die Gesamtpunktzahlverteilung, die wichtigsten Einflussfaktoren für diese Punktzahl und die Zielwertdefinition angezeigt.

![Details zur prädiktiven Bewertung des Kundenprofils](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score-details.png)

## Überwachen von prädiktiven Lead- und Konto-Scoring-Aufträgen {#monitoring-jobs}

Sie können grundlegende Metriken und den täglichen Auftragsausführungsstatus über das Dashboard überwachen. Zu den Metriken gehören:

* Gesamtzahl der bewerteten Personen-/Kontoprofile
* Nächster Scoring-Auftrag (Datum)
* Nächster Schulungsvorgang (Datum)

Weitere Informationen finden Sie in der Dokumentation unter [Überwachen von Aufträgen für prädiktives Lead- und Konto-Scoring](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
