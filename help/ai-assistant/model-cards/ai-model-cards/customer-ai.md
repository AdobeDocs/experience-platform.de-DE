---
title: Karte des Kunden-KI-Tendenz-Bewertungsmodells
description: Erfahren Sie mehr über das KI-Modell, das für Kunden-KI verwendet wird.
hide: true
hidefromtoc: true
exl-id: b2eeb1d2-3c2b-40a0-b5cd-91e99d99a906
source-git-commit: 63d95be281d1bc3867e4e24b9e7aadeecc64ac52
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 7%

---

# Karte des Kunden-KI-Tendenz-Bewertungsmodells

## Modellübersicht {#model-overview}

* Das Tendenz-Scoring-Modell der Kundinnen- und Kunden-KI bietet Marketing-Experten und Kundeninteraktions-Teams umsetzbare Einblicke, indem es die Wahrscheinlichkeit vorhersagt, dass eine Kundin oder ein Kunde eine bestimmte Aktion ausführen wird, z. B. einen Kauf tätigen, sich für ein Abonnement anmelden oder mit einer E-Mail-Kampagne interagieren. Die Ergebnisse ermöglichen es Unternehmen, die Zielgruppensegmentierung zu optimieren und Kundeninteraktionen basierend auf prognostizierten Verhaltensweisen zu personalisieren.
* Die wichtigsten Benutzer dieses Modells sind Marketing-Experten, Datenanalysten und Kundeninteraktions-Teams, die [Real-Time CDP](../../../rtcdp/home.md) nutzen, um datengesteuerte Marketing-Strategien zu fördern.
* Dieses Modell wird hauptsächlich für die Kundensegmentierung, zielgerichtetes Marketing und Abwanderungsvorhersagen verwendet. Unternehmen nutzen dieses Modell, um die Kaufabsicht ihrer Kunden vorherzusagen, Marketing-Kampagnen zu optimieren und ihren Personalisierungsaufwand zu steigern. Beispielsweise könnte ein E-Commerce-Unternehmen das Modell verwenden, um Kundinnen und Kunden mit hohen Absichten zu identifizieren und ihnen exklusive Aktionen anzubieten.
* Marketing-Experten haben oft Schwierigkeiten damit, die richtigen Kundinnen und Kunden für das Targeting und die Optimierung der Interaktion zu identifizieren. Dieses Modell reduziert Ratschläge, indem es einen datengesteuerten Ansatz für das Kunden-Targeting bereitstellt und sicherstellt, dass Marketing-Ressourcen effizient zugewiesen werden.
* Das Modell sollte nicht für Entscheidungen mit hohem Risiko verwendet werden, z. B. für finanzielle Kreditbewertung, medizinische Diagnostik oder rechtliche Bewertungen. Darüber hinaus ist es aufgrund potenzieller ethischer Bedenken nicht für die Verwendung bei der Vorhersage persönlich sensibler Verhaltensweisen (z. B. gesundheitliche Bedingungen, politische Präferenzen) vorgesehen.

## Modelldetails {#model-details}

* Dies ist ein überwachtes Lernklassifizierungsmodell, das die Wahrscheinlichkeit des Eintretens eines Ereignisses (Kauf, Abwanderung, Interaktion) anhand historischer Kundendaten vorhersagt. Es wird mithilfe von Gradienten-verstärkenden Entscheidungsbäumen (GBDT) mit logistischer Regression trainiert, um Tendenzwerte zu modellieren.
* Das Modell verarbeitet Kundenverhaltensdaten, demografische Attribute und historische Interaktionen. Dazu gehören Daten wie die Häufigkeit der Website-Besuche, der Kaufverlauf in der Vergangenheit, die Interaktion mit Marketing-E-Mails und demografische Informationen.
* Das Modell gibt einen Score zwischen 0 und 100 aus, wobei höhere Werte eine höhere Wahrscheinlichkeit für das prognostizierte Ereignis in der bewerteten Populationskohorte angeben. Darüber hinaus bietet es Funktionen und Wichtigkeitswerte, sodass Benutzende verstehen können, welche Faktoren die Prognose beeinflusst haben.

**Beispieleingabe**

```json
{ 
  "customer_id": 12345, 
  "past_purchases": 3, 
  "last_visit_days": 7,
  "email_click_rate": 0.4 
}
```

**Beispielausgabe**

```json
{ 
  "customer_id": 12345,
  "SCORE": 89 
}
```

## Modellschulung {#model-training}

* Der Schulungsdatensatz für jeden Kunden wird direkt aus den eigenen Daten in Experience Platform bezogen. Dazu gehören die historischen Interaktionen des Kunden, Transaktionsdatensätze, Verhaltensinteraktionslogs und demografischen Informationen, die in seiner Experience Platform-Instanz erfasst und gespeichert werden. Der Datensatz nutzt kundenspezifische Daten über den ausgewählten Zeitraum und erfasst deren einzigartige saisonale Trends und Interaktionsmuster. Vor der Verwendung wird der Datensatz jedes Kunden einer auf seine Datenmerkmale zugeschnittenen Vorverarbeitung unterzogen, einschließlich der Handhabung fehlender Werte, der Kategoriekodierung, der Funktionsskalierung, der Ausreißererkennung und der Funktionsentwicklung, um eine optimale Qualität und Nutzbarkeit für seinen spezifischen Anwendungsfall sicherzustellen.
* Das Modell nutzt [!DNL LightGBM] mit [!DNL GBM], die für strukturierte Daten optimiert sind. Es wird auf historischen Kundenereignissequenzen trainiert, um prädiktive Verhaltensmuster zu identifizieren.
* Das Modell wurde mit [!DNL LightGBM] und [!DNL scikit-learn] entwickelt und ist in der Adobe AI-Cloud-Infrastruktur geschult.
* Die für das Modell-Training verwendeten Computerressourcen sind [!DNL Databricks].

## Modellauswertung {#model-evaluation}

* Die Effektivität des Modells wird mithilfe von [!DNL AUC-ROC] gemessen. Da Kunden-KI auf eine sehr breite Palette von Kunden-Nutzungsszenarien abzielt, kann der Einsatzbereich nicht bekannt sein. Daher wird die [!DNL AUC] verwendet, da sie unabhängig von Reichweite und Budget ist.
* Die Auswertungsdaten enthalten Holdout-Kundendatensätze und werden ähnlich wie Schulungsdaten mit Funktionsnormalisierung, Kodierung und Bereinigungsschritten vorverarbeitet, um den Erwartungen an das Eingabeformat zu entsprechen. Nach Ablauf des Ergebnisfensters kann die endgültige Leistungsbewertung durchgeführt werden.

## Modellbereitstellung {#model-deployment}

* Das Modell wird auf Experience Platform-KI-Services gehostet und in verschiedene Adobe-Programme integriert. Sie ist über API-Endpunkte verfügbar und ermöglicht so den nahtlosen Zugriff für Echtzeit-Prognosen und Batch-Verarbeitung in Marketing- und Kundeninteraktions-Workflows.
* Das Modell wird kontinuierlich über die Modellüberwachung überwacht, um die Abweichung vom Trainings-Setup zu sehen. Periodische Umschulungen (einmal in 3 Monaten) werden automatisch durchgeführt.
* Das Modell wird einmal in mehreren Monaten (maximal einmal in 6 Monaten) neu trainiert, wobei aktualisierte Kundeninteraktionsdaten verwendet werden, um eine kontinuierliche Relevanz zu gewährleisten. Periodische Umschulungen tragen dazu bei, Datenabweichungen und saisonale Schwankungen zu minimieren, die sich auf die Prognosegenauigkeit auswirken könnten.

## Erklärbarkeit {#explainability}

Das Modell nutzt [!DNL SHapley Additive Explanations] (SHAP), um die Auswirkungen jeder Eingabefunktion auf ihre Prognosen zu quantifizieren und Transparenz darüber zu schaffen, wie Kundenattribute die Tendenzwerte beeinflussen. SHAP-Werte ermöglichen sowohl die globale Interpretierbarkeit, d. h. die Identifizierung der einflussreichsten Faktoren für alle Prognosen, als auch die lokale Interpretierbarkeit, wodurch individuelle Prognosen für bestimmte Kunden erklärt werden. Das Modell unterstützt auch [!DNL Local Interpretable Model-Agnostic Explanations] (LIME).

## Fairness und Voreingenommenheit {#fairness-and-bias}

* Dieses Modell basiert auf anonymisierten Verhaltensdaten, die mit Cookie-IDs verknüpft sind, ohne Zugriff auf geschützte demografische Attribute wie Alter, Geschlecht oder ethnische Zugehörigkeit. Daher ist eine direkte Messung der Fairness zwischen sensiblen Gruppen nicht möglich. Zu den Bemühungen zur Minderung der Verzerrung gehören die Normalisierung der Häufigkeit der Benutzeraktivitäten, die Unterdrückung übermäßig dominanter Funktionen und die Durchführung von Score-Kalibrierungsprüfungen in allen Kohorten.
* Das Modell berücksichtigt Verzerrungen aufgrund von Neuigkeit und überwacht Verzerrungen durch Exposition, indem es Modellprognosen für randomisierten Holdout-Traffic auswertet. Laufende Auswertungen sind vorhanden, um die Verzerrungsverstärkung und Rückkopplungsschleifen während der Modellbereitstellung zu erkennen und zu reduzieren.
* Der Datensatz wird hauptsächlich von Benutzern mit hoher Interaktion bezogen, was zu Selektionsverzerrungen führen kann. Um dies abzuschwächen, wendet das Modell Stichprobenstrategien an.

## Stärke {#robustness}

Das Modell behält eine starke Verallgemeinerung auf neue Kundendatensätze bei. Die Leistung bleibt in verschiedenen Kundensegmenten stabil, verschlechtert sich jedoch geringfügig, wenn das Benutzerverhalten erheblich von historischen Mustern abweicht.

## Überlegungen zum Datenschutz und zur Sicherheit {#privacy-and-security-considerations}

* Das Modell verarbeitet oder speichert keine persönlich identifizierbaren Informationen (PII), und alle für das Training verwendeten Daten werden anonymisiert und aggregiert. Sie befolgt die strikte Einhaltung der DSGVO, des CCPA und der internen Adobe-Datenschutzrichtlinien. Das Modell umfasst verschiedene Datenschutztechniken, Hashing, Anonymisierung und Tokenisierung, um den Datenschutz sicherzustellen.
* Kunden-KI respektiert die von Ihnen festgelegten Einverständniseinstellungen. Sobald Sie Ihre [Einverständnisrichtlinie eingerichtet und aktiviert](../../../data-governance/policies/user-guide.md#create-a-consent-policy) haben, hält sich Kunden-KI an die zu Ihnen erfassten einverständisbezogenen Daten. Zum Scoring des Modells in nachfolgenden Ausführungen des Modells werden nur die Daten verwendet, die mit Ihrem Einverständis erfasst wurden. Die neuen Werte ersetzen die alten Werte und können bei der Segmentierung verwendet werden. Diese Funktion ist derzeit nur für Kundinnen und Kunden von HealthCare Shield sowie Privacy und Security Shield verfügbar.

## Ethische Überlegungen {#ethical-considerations}

Das Modell könnte bei der Entscheidungsfindung möglicherweise zu Verzerrungen führen. Im Bestreben, dies zu verhindern, folgt Experience Platform den Richtlinien für verantwortungsvolle KI, um sicherzustellen, dass Modelle vor der Bereitstellung Verzerrungs-Audits, Fairness-Tests und menschliche Aufsicht unterzogen werden.
