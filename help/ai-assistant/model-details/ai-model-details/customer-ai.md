---
title: Details des Kunden-KI-Tendenz-Bewertungsmodells
description: Erfahren Sie mehr über das KI-Modell, das für Kunden-KI verwendet wird.
hide: true
hidefromtoc: true
exl-id: b2eeb1d2-3c2b-40a0-b5cd-91e99d99a906
source-git-commit: 6623c7dad0fc4ddb7cb79e8f474b824915f130fc
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# Details des Kunden-KI-Tendenz-Bewertungsmodells

## Modellübersicht {#model-overview}

* **Modellname und -version**: Tendenz-Bewertungsmodell für Kunden-KI
* **Modellzweck**: Das Modell bietet Marketing-Experten und Kundeninteraktions-Teams umsetzbare Einblicke, indem vorhergesagt wird, mit welcher Wahrscheinlichkeit ein Kunde eine bestimmte Aktion ausführen wird, z. B. einen Kauf tätigen, sich für ein Abonnement anmelden oder mit einer E-Mail-Kampagne interagieren. Die Ergebnisse ermöglichen es Unternehmen, die Zielgruppensegmentierung zu optimieren und Verbraucherinteraktionen basierend auf prognostizierten Verhaltensweisen zu personalisieren.
* **Vorgesehene Benutzer**: Die primären Benutzer dieses Modells sind Marketing-Experten, Datenanalysten und Kundeninteraktions-Teams, die [Real-Time CDP](../../../rtcdp/home.md) zur Förderung datengesteuerter Marketing-Strategien nutzen.
* **Anwendungsfälle**: Dieses Modell wird hauptsächlich für die Verbrauchersegmentierung, das zielgerichtete Marketing und die Prognose von Abwanderungen verwendet. Unternehmen nutzen dieses Modell, um die Kaufabsicht von Verbrauchern vorherzusagen, Marketing-Kampagnen zu optimieren und den Personalisierungsaufwand zu verbessern. Beispielsweise könnte ein E-Commerce-Unternehmen das Modell verwenden, um Kundinnen und Kunden mit hohen Absichten zu identifizieren und ihnen exklusive Aktionen anzubieten.
* **Probleme**: Marketing-Experten haben oft Schwierigkeiten damit, die richtigen Verbraucher für das Targeting und die Optimierung ihrer Interaktion zu ermitteln. Dieses Modell reduziert Rätselraten, indem es einen datengesteuerten Ansatz für das Verbraucher-Targeting bereitstellt und sicherstellt, dass Marketing-Ressourcen effizient zugewiesen werden.
* **Potenzieller Missbrauch**: Das Modell sollte nicht für Anwendungsfälle mit hohem Risiko verwendet werden, wie z. B. finanzielle Kreditbewertung, medizinische Diagnostik oder rechtliche Bewertungen. Darüber hinaus sollte das Modell nicht für die Vorhersage persönlich sensibler Verhaltensweisen (wie Gesundheitszustände, politische Präferenzen) verwendet werden.

## Modelldetails {#model-details}

* **Modelltyp**: Dies ist ein überwachtes Lernklassifizierungsmodell, das die Wahrscheinlichkeit des Eintretens eines Ereignisses (z. B. Kauf, Abwanderung, Interaktion) anhand historischer Kundendaten vorhersagt. Es wird mithilfe von Gradienten-verstärkenden Entscheidungsbäumen (GBDT) mit logistischer Regression trainiert, um Tendenzwerte zu modellieren.
* **Input**: Das Modell verarbeitet Verhaltensdaten von Verbrauchern, demografische Attribute und historische Interaktionen. Dazu gehören Daten wie die Häufigkeit der Website-Besuche, der Kaufverlauf in der Vergangenheit, die Interaktion mit Marketing-E-Mails und demografische Informationen.
* **Ausgabe**: Das Modell gibt einen Score zwischen 0 und 100 aus, wobei höhere Werte eine höhere Wahrscheinlichkeit für das Auftreten des prognostizierten Ereignisses in der bewerteten Populationskohorte angeben. Darüber hinaus bietet es Funktionen und Wichtigkeitswerte, die es Marketing-Experten ermöglichen zu verstehen, welche Faktoren die Prognose beeinflusst haben.

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

* **Schulungsdaten und Vorverarbeitung**: Der Schulungsdatensatz für jede Kundin und jeden Kunden wird direkt aus den eigenen Daten in Adobe Experience Platform bezogen. Dazu gehören historische Kundeninteraktionen, Transaktionsdatensätze, Verhaltensinteraktionslogs und demografische Informationen, die in der Adobe Experience Platform-Instanz erfasst und gespeichert werden. Der Datensatz nutzt kundenspezifische Daten über den ausgewählten Zeitraum und erfasst deren einzigartige saisonale Trends und Interaktionsmuster. Vor der Verwendung wird der Datensatz jedes Kunden einer auf seine Datenmerkmale zugeschnittenen Vorverarbeitung unterzogen, einschließlich der Handhabung fehlender Werte, der Kategoriekodierung, der Funktionsskalierung, der Ausreißererkennung und der Funktionsentwicklung, um eine optimale Qualität und Nutzbarkeit für seinen spezifischen Anwendungsfall sicherzustellen
* **Schulungsspezifikationen**: Das Modell nutzt [!DNL LightGBM] mithilfe von [!DNL GBM], die für strukturierte Daten optimiert sind. Es wird auf historischen Kundenereignissequenzen trainiert, um prädiktive Verhaltensmuster zu identifizieren.
* **Trainings-Frameworks**: Das Modell wurde mithilfe von [!DNL LightGBM] und [!DNL scikit-learn] entwickelt und basiert auf der Adobe AI-Cloud-Infrastruktur.
* **Schulungsinfrastruktur**: [!DNL Databricks].

## Modellauswertung {#model-evaluation}

* **Evaluierungsmetriken und -verfahren**: Die Effektivität des Modells wird mithilfe von [!DNL AUC-ROC] gemessen. Da Kunden-KI auf eine sehr breite Palette von Kunden-Nutzungsszenarien abzielt, kann der Einsatzbereich nicht bekannt sein. Also verwenden wir ein [!DNL AUC], das unabhängig von Reichweite und Budget ist.
* **Auswertungsdaten und Vorverarbeitung**: Auswertungsdaten enthalten Holdout-Verbraucherdatensätze und werden ähnlich wie Schulungsdaten mit Funktionsnormalisierung, Kodierung und Bereinigungsschritten vorverarbeitet, um den Erwartungen an das Eingabeformat zu entsprechen. Nachdem das Ergebnisfenster bestanden ist, können wir eine abschließende Leistungsbewertung durchführen.

## Modellbereitstellung {#model-deployment}

* **Modellbereitstellung**: Das Modell wird auf Adobe Experience Platform-KI-Services gehostet und in verschiedene Adobe-Programme integriert. Sie ist über API-Endpunkte verfügbar und ermöglicht so den nahtlosen Zugriff für Echtzeit-Prognosen und Batch-Verarbeitung in Marketing- und Verbraucherinteraktions-Workflows.
* **Modellüberwachung**: Das Modell wird kontinuierlich über die Modellüberwachung überwacht, um die Abweichung von der Trainings-Einrichtung zu sehen. Regelmäßige Umschulungen (einmal in 3 Monaten) werden automatisch durchgeführt.
* **Modellaktualisierung**: Das Modell wird einmal in mehreren Monaten (maximal einmal in 6 Monaten) neu trainiert, wobei aktualisierte Daten zu Verbraucherinteraktionen verwendet werden, um eine kontinuierliche Relevanz zu gewährleisten. Periodische Umschulungen tragen dazu bei, Datenabweichungen und saisonale Schwankungen zu minimieren, die sich auf die Prognosegenauigkeit auswirken könnten.

## Erklärbarkeit {#explainability}

**Modellerklärbarkeit**: Das Modell nutzt [!DNL SHapley Additive Explanations] (SHAP), um die Auswirkungen der einzelnen Eingabefunktionen auf seine Prognosen zu quantifizieren und Transparenz darüber zu schaffen, wie Verbraucherattribute die Tendenzwerte beeinflussen. SHAP-Werte ermöglichen sowohl die globale Interpretierbarkeit, die Identifizierung der einflussreichsten Faktoren für alle Prognosen, als auch die lokale Interpretierbarkeit, die individuelle Prognosen für bestimmte Verbraucher erklärt. Das Modell unterstützt auch [!DNL Local Interpretable Model-Agnostic Explanations] (LIME).

## Fairness und Voreingenommenheit {#fairness-and-bias}

* **Modellfairness**: Dieses Modell wird auf anonymisierten Verhaltensdaten trainiert, die mit Cookie-IDs verknüpft sind, ohne Zugriff auf geschützte demografische Attribute wie Alter, Geschlecht oder ethnische Zugehörigkeit. Daher ist eine direkte Messung der Fairness zwischen sensiblen Gruppen nicht möglich. Zu den Bemühungen zur Minderung der Verzerrung gehören die Normalisierung der Häufigkeit der Benutzeraktivitäten, die Unterdrückung übermäßig dominanter Funktionen und die Durchführung von Score-Kalibrierungsprüfungen in allen Kohorten. Wir berücksichtigen die Tendenz zur Neuigkeit und überwachen die Tendenz zur Exposition, indem wir Modellprognosen für randomisierten Holdout-Traffic auswerten. Laufende Auswertungen sind vorhanden, um die Verzerrungsverstärkung und Rückkopplungsschleifen während der Modellbereitstellung zu erkennen und zu reduzieren.
* **Datenbias**: Der Datensatz wird hauptsächlich von Benutzern mit hoher Interaktion bezogen, was zu Selektionsverzerrungen führen kann. Um dies abzuschwächen, wendet das Modell Stichprobenstrategien an. Je nach Anwendungsfall sollten Kunden überlegen, wie potenzielle Verzerrungen in den Modellausgaben mit ihrer beabsichtigten Anwendung übereinstimmen oder sich darauf auswirken können.

## Stärke {#robustness}

**Modell-Robustheit**: Das Modell behält eine starke Generalisierung für neue Verbraucherdatensätze bei. Die Leistung bleibt in verschiedenen Verbrauchersegmenten stabil, verschlechtert sich jedoch geringfügig, wenn das Benutzerverhalten erheblich von historischen Mustern abweicht.

## Ethische Überlegungen {#ethical-considerations}

**Ethische Überlegungen im Zusammenhang mit dem Modell**: Dieses Modell ist für Marketing-Anwendungsfälle vorgesehen, und Kunden sollten erhöhte Vorsicht walten lassen, wenn sie es in sensiblen oder regulierten Bereichen wie Kredit oder Beschäftigung anwenden. Die Ergebnisse sind probabilistisch und werden aus Verhaltensdaten abgeleitet, die möglicherweise historische oder repräsentative Verzerrungen widerspiegeln. Kunden wird empfohlen, menschliche Aufsicht anzuwenden. Adobe Experience Platform folgt den Richtlinien für verantwortungsvolle KI, um sicherzustellen, dass Modelle vor der Bereitstellung Verzerrungsprüfungen, Fairness-Tests und menschliche Aufsicht unterzogen werden. Weitere Informationen finden Sie in den [Ethikgrundsätzen für die Adobe-KI](https://www.adobe.com/content/dam/cc/en/ai-ethics/pdfs/Adobe-AI-Ethics-Principles.pdf?msockid=0d85c8269eb36f0801d0ddb49fd16ebc).