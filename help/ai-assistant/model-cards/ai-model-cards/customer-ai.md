---
title: Karte des Kunden-KI-Tendenz-Bewertungsmodells
description: Erfahren Sie mehr über das KI-Modell, das für Kunden-KI verwendet wird.
hide: true
hidefromtoc: true
source-git-commit: 21a95bd678cf83c72a08213b647ef778cfb49cfc
workflow-type: tm+mt
source-wordcount: '1629'
ht-degree: 0%

---

# Karte des Kunden-KI-Tendenz-Bewertungsmodells

Im Rahmen von [Intelligent Services in Adobe Experience Platform](../../../intelligent-services/home.md) können Sie [Kunden-KI](../../../intelligent-services/customer-ai/overview.md) verwenden, um individuelle Kundenprognosen und -erklärungen zu generieren.

Mithilfe von Einflussfaktoren können Sie mithilfe von Kunden-KI vorhersagen, was ein Kunde wahrscheinlich tun wird und warum. Darüber hinaus können Sie von Prognosen und Insights durch Kunden-KI profitieren, um Kundenerlebnisse durch Bereitstellung der am besten geeigneten Angebote und Botschaften zu personalisieren.

In dieser Modellkarte finden Sie Informationen zum KI-Modell, das für Kunden-KI verwendet wird.

## Modellübersicht {#model-overview}

* Kunden-KI ist ein KI-gestütztes Modell, das entwickelt wurde, um Tendenzwerte für Benutzende basierend auf ihren früheren Verhaltensweisen und Interaktionen mit einem Unternehmen zu generieren. Verwenden Sie Kunden-KI, um die Wahrscheinlichkeit vorherzusagen, mit der eine Kundin oder ein Kunde bestimmte Aktionen durchführt, z. B. einen Kauf tätigt, mit Inhalten interagiert oder abwandert. Dieses Modell wird innerhalb von Experience Platform bereitgestellt und lässt sich mit verschiedenen Marketing- und Kundenanalyse-Workflows integrieren.
* Das Modell soll Marketing-Experten und Kundeninteraktions-Teams umsetzbare Einblicke bieten, indem die Wahrscheinlichkeit vorhergesagt wird, dass eine Kundin oder ein Kunde eine bestimmte Aktion ausführt, z. B. einen Kauf tätigt, sich für ein Abonnement anmeldet oder mit einer E-Mail-Kampagne interagiert. Die Ergebnisse ermöglichen es Unternehmen, die Zielgruppensegmentierung zu optimieren und Kundeninteraktionen basierend auf prognostizierten Verhaltensweisen zu personalisieren.
* Dies ist ein **überwachtes Lernklassifizierungsmodell** das die Wahrscheinlichkeit des Eintretens eines Ereignisses (Kauf, Abwanderung, Interaktion) anhand historischer Kundendaten vorhersagt. Es wird mithilfe von Gradienten-verstärkenden Entscheidungsbäumen (GBDT) mit logistischer Regression trainiert, um Tendenzwerte zu modellieren.
* Die wichtigsten Benutzer dieses Modells sind Marketing-Experten, Datenanalysten und Kundeninteraktions-Teams, die Experience Platform zur Förderung datengesteuerter Marketing-Strategien nutzen.
* Kunden-KI lässt sich direkt in die KI-Services von Experience Platform integrieren und ermöglicht es Benutzenden, über vordefinierte APIs und Dashboards auf Modellausgaben zuzugreifen. Die vom Modell generierten Tendenz-Scores können in [Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/get-started) und [Real-Time CDP](../../../rtcdp/home.md) verwendet werden, um die Zielgruppensegmentierung zu verfeinern und Marketing-Strategien anzupassen.

## Vorgesehene Verwendung {#intended-use}

* Dieses Modell wird in erster Linie für **Kundensegmentierung, zielgerichtetes Marketing und Abwanderungsvorhersagen)**. Unternehmen nutzen dieses Modell, um **Kaufabsicht von Kunden vorherzusagen, Marketing-Kampagnen zu optimieren und Personalisierungsbemühungen zu**. Beispielsweise könnte ein E-Commerce-Unternehmen das Modell verwenden, um Kundinnen und Kunden mit hohen Absichten zu identifizieren und ihnen exklusive Aktionen anzubieten.
* Marketing-Experten haben oft Schwierigkeiten damit **die richtigen Kundinnen und Kunden für eine Zielgruppenbestimmung zu identifizieren** die Interaktionsbemühungen **optimieren**. Dieses Modell **reduziert**, indem es einen datengesteuerten Ansatz für das Kunden-Targeting bereitstellt und sicherstellt, dass Marketing-Ressourcen effizient zugewiesen werden.
* Das Modell ist auf mehrere Branchen anwendbar, einschließlich E-Commerce, Einzelhandel, Finanzdienstleistungen, Telekommunikation und Medien. Jedes Unternehmen, das sich auf Kundeninteraktion und personalisiertes Marketing stützt, kann von diesem Modell profitieren.
* Das Modell **sollte nicht für Entscheidungen mit hohem Risiko verwendet werden,**. B. für finanzielle Kreditbewertung, medizinische Diagnostik oder rechtliche Bewertungen. Darüber hinaus ist es nicht für die Verwendung bei der Vorhersage persönlich sensibler Verhaltensweisen (Gesundheitszustand, politische Präferenzen) aufgrund potenzieller ethischer Bedenken vorgesehen.

## Modellein- und -ausgänge {#model-inputs-and-outputs}

* Das Modell verarbeitet Kundenverhaltensdaten, demografische Attribute und historische Interaktionen. Dazu gehören Daten wie die Häufigkeit der Website-Besuche, der Kaufverlauf in der Vergangenheit, die Interaktion mit Marketing-E-Mails und demografische Informationen.
* Eingabedaten müssen als JSON-Objekte strukturiert sein, die Kundenattribute und Verhaltenssignale enthalten. Für die Batch-Verarbeitung akzeptiert das Modell CSV-Dateien, die gemäß den Datenerfassungsstandards von Experience Platform formatiert sind.
* Das Modell gibt einen Neigungs-Score zwischen 0 und 1 aus, wobei höhere Werte eine höhere Wahrscheinlichkeit für das Auftreten des prognostizierten Ereignisses angeben. Darüber hinaus bietet es Funktionen und Wichtigkeitswerte, sodass Benutzende verstehen können, welche Faktoren die Prognose beeinflusst haben.

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
  "propensity_score": 0.82
}
```

## Trainings-Daten

* Das Modell wurde auf **über Experience Platform erfassten anonymisierten Kundeninteraktionsdaten** Erstanbietern trainiert. Sie enthält historische **(Verhaltensdaten, Transaktionsdatensätze, E-Mail-Interaktionen und Interaktionsmetriken** in verschiedenen Branchen.
* Der Schulungsdatensatz besteht aus **10 Millionen Kundendatensätzen** die von einer Vielzahl von Experience Platform-Kunden bezogen werden. Zu diesen Datensätzen gehören **historische Kundeninteraktionen, Transaktionsdaten, Protokolle zu Verhaltensaktivitäten und demografische Informationen** aus verschiedenen Branchen wie Einzelhandel, E-Commerce, Telekommunikation und Finanzen. Die Daten wurden über einen Zeitraum von 24 Monaten erhoben, um eine ausreichende Darstellung saisonaler Trends und langfristiger Interaktionsmuster zu gewährleisten.
* Der Datensatz wird hauptsächlich von Benutzern mit hoher Interaktion bezogen, was zu Selektionsverzerrungen führen kann. Um dies abzuschwächen, wendet das Modell stratifizierte Stichprobenverfahren, Verzerrungs-Auditing-Techniken und Datenaugmentationsstrategien an.
* Der Datensatz wird einer umfassenden Vorverarbeitung unterzogen, um Konsistenz, Qualität und Benutzerfreundlichkeit der Daten sicherzustellen.
   * **Umgang mit fehlenden Werten**: Fehlende Werte werden mithilfe einer Kombination aus mittlerer Imputation (für numerische Felder), Modusimputation (für kategoriale Felder) und prädiktiver Modellierung (für komplexe fehlende Fälle) adressiert.
   * **Kategoriale Kodierung**: Kategoriale Variablen wie Kundensegmente und Kaufkategorien werden durch einmalige Kodierungs- und Zielcodierungstechniken in numerische Darstellungen konvertiert.
   * **Funktionsskalierung und Normalisierung**: Die Min-Max-Skalierung wird auf gebundene Variablen (Alter, Einkommen) angewendet, während die Z-Score-Standardisierung für normal verteilte Funktionen verwendet wird.
   * **Zusätzliche Vorverarbeitung**: Die Pipeline umfasst die Erkennung und Entfernung von Ausreißern, die Filterung von Duplikaten, die Standardisierung von Zeitstempeln und das Feature Engineering, um die prädiktive Modellierung zu verbessern.

## Modellarchitektur und Schulung

* Das Modell nutzt **[!DNL Gradient Boosting Decision Trees](GBDT) mithilfe von[!DNL XGBoost]**, die für strukturierte Daten optimiert sind. Es wird auf historischen Kundenereignissequenzen trainiert, um prädiktive Verhaltensmuster zu identifizieren.
* Das Modell basiert auf einem überwachten Lernansatz und nutzt GBDT mit [!DNL XGBoost] als primären Lernalgorithmus. Darüber hinaus wird die logistische Regression als Basismodell für das Benchmarking der Prognosegenauigkeit integriert.
* Das Modell wurde mit **[!DNL TensorFlow]**, **[!DNL XGBoost]** und **[!DNL scikit-learn]** entwickelt. Trainings-Läufe für die Adobe AI-Cloud-Infrastruktur mit **[!DNL NVIDIA V100]GPUs**, die große Datensätze unterstützen.
* [!DNL NVIDIA V100 GPUs], trainiert in der Google Cloud-Infrastruktur.
* [!DNL AUC-ROC], Präzisions-Rückruf und Kreuzvalidierung.

## Leistung und Bewertung

* Das Modell wurde mit einem Holdout-Validierungsansatz getestet, bei dem 80 % der Daten für das Training verwendet wurden und 20 % für die Auswertung reserviert waren.
* Die Effektivität des Modells wird mit [!DNL AUC-ROC] (0,85), Precision-Recall (0,78) und F1-Score (0,80) gemessen. Diese Metriken helfen bei der Beurteilung der Prognosefähigkeit des Modells in verschiedenen Segmenten.
* Geringere Genauigkeit für neue Kundensegmente mit eingeschränkten historischen Daten.
* Bei Kunden mit begrenzten historischen Daten kann das Modell die Leistung beeinträchtigen (Kaltstart-Problem). Darüber hinaus können saisonale Effekte (Urlaubstrends) häufige Umschulungen erfordern, um die Genauigkeit zu gewährleisten.

## Fairness und Voreingenommenheit

* Das Modell wurde **demografischen Paritätstests** und **kontradiktorischen Fairness-Bewertungen** unterzogen, um Leistungsunterschiede zwischen verschiedenen Benutzersegmenten zu erkennen.
* Die Analyse ergab einen Leistungsabfall von **5 % bei Benutzenden mit niedrigen historischen Interaktionsdaten**. Um diesem Problem zu begegnen, verwendet das Modell während des Trainings neue Gewichtungstechniken.
* Der Datensatz wird stratifiziert, um eine proportionale Repräsentation verschiedener Kundendemografiken zu gewährleisten, und während des Trainings werden Fairness-Einschränkungen eingeführt, um zu verhindern, dass das Modell eine bestimmte Gruppe bevorzugt. Regelmäßige Verzerrungsaudits werden unter Verwendung der demografischen Paritätsanalyse durchgeführt, die Anpassungen ermöglicht, wenn Leistungsunterschiede festgestellt werden.

## Erklärbarkeit und Interpretierbarkeit

* Das Modell nutzt **[!DNL SHapley Additive Explanations](SHAP)** um die Auswirkungen jeder Eingabefunktion auf ihre Prognosen zu quantifizieren und Transparenz darüber zu schaffen, wie Kundenattribute die Tendenzwerte beeinflussen. SHAP-Werte ermöglichen sowohl die globale Interpretierbarkeit, d. h. die Identifizierung der einflussreichsten Faktoren für alle Prognosen, als auch die lokale Interpretierbarkeit, wodurch individuelle Prognosen für bestimmte Kunden erklärt werden.
* Das Modell unterstützt **[!DNL Local Interpretable Model-Agnostic Explanations](LIME)** und SHAP, um Einblicke zu gewähren, wie Eingabefunktionen Prognosen beeinflussen. LIME erzeugt lokale Erklärungen, indem es gestörte Versionen der Eingabedaten erstellt und Änderungen der Vorhersagen beobachtet, während SHAP jedem Merkmal Beitragswerte zuweist, was sowohl globale als auch lokale Interpretationsmöglichkeiten von Modellentscheidungen bietet.

## Robustheit und Verallgemeinerung

* Das Modell behält beim Testen von nicht angezeigten Datensätzen 80 % [!DNL AUC-ROC] bei und zeigt so eine starke Verallgemeinerung auf neue Kundendatensätze. Die Leistung bleibt in verschiedenen Kundensegmenten stabil, verschlechtert sich jedoch geringfügig, wenn das Benutzerverhalten erheblich von historischen Mustern abweicht.
* Das Modell wurde hinsichtlich gestörter und kontraproduktiver Eingaben, einschließlich fehlender Daten, Ausreißer-Injektion und absichtlicher Falschkennzeichnung, bewertet. Während die Leistung unter normalen Bedingungen stabil bleibt, wurde bei extremen unerwünschten Veränderungen eine geringfügige Genauigkeitsverschlechterung (ca. 3-5 %) beobachtet.

## Überlegungen zu Sicherheit und Datenschutz

* Das Modell **verarbeitet oder speichert keine persönlich identifizierbaren Informationen (PII)** und alle für das Training verwendeten Daten werden anonymisiert und aggregiert. Sie befolgt die strikte Einhaltung der DSGVO-, CCPA- und internen Adobe-Datenschutzrichtlinien, um eine verantwortungsvolle Datennutzung sicherzustellen.
* Das Modell beinhaltet verschiedene Datenschutztechniken, um kontrolliertes Rauschen zu den Daten hinzuzufügen und so eine erneute Identifizierung von Personen zu verhindern. Darüber hinaus **Methoden (Hashing, Anonymisierung und Tokenisierung) verwendet, um personenbezogene Daten zu entfernen** bevor Modell-Trainings und Rückschlüsse gezogen werden.

## Bereitstellung und Integration

* Das Modell wird auf Adobe Experience Platform-KI-Services gehostet und in verschiedene Adobe-Programme integriert. Sie ist über API-Endpunkte verfügbar und ermöglicht so den nahtlosen Zugriff für Echtzeit-Prognosen und Batch-Verarbeitung in Marketing- und Kundeninteraktions-Workflows.
* Das Modell wird auf einer **[!DNL Kubernetes]-basierten Bereitstellung mit** Funktionen zur automatischen Skalierung ausgeführt, um unterschiedliche Arbeitslasten effizient zu bewältigen. Zu den Compute-Ressourcen gehören [!DNL NVIDIA V100] GPUs für Schulungen und optimierte CPU-basierte Rückschlüsse für Echtzeit-Skalierbarkeit.

## Überwachung und Wartung

* Das Modell wird kontinuierlich **über[!DNL WatsonX]** überwacht, um wichtige Leistungsindikatoren wie Genauigkeitsabweichungen, Änderungen der Wichtigkeit von Funktionen und Prognosestabilität zu verfolgen. Mechanismen zur Anomalieerkennung und -warnung benachrichtigen das Team, wenn erhebliche Abweichungen vom erwarteten Verhalten auftreten.
* Das Modell wird monatlich mit aktualisierten Daten zur Kundeninteraktion neu trainiert, um eine kontinuierliche Relevanz zu gewährleisten. Periodische Umschulungen tragen dazu bei, Datenabweichungen und saisonale Schwankungen zu minimieren, die sich auf die Prognosegenauigkeit auswirken könnten

## Ethische Belange und verantwortungsvolle KI

* Das Modell könnte bei nicht ordnungsgemäßer Überwachung zu Verzerrungen bei der Entscheidungsfindung führen. Wenn beispielsweise bestimmte demografische Daten in den Schulungsdaten überrepräsentiert sind, kann das Modell bestimmte Kundengruppen ungerecht bevorzugen.
* Experience Platform befolgt die Richtlinien für verantwortungsvolle KI und stellt sicher, dass Modelle vor **Bereitstellung (Bias-Audits** Fairness-Tests und menschlicher Aufsicht) unterzogen werden.

## Bekannte Einschränkungen

* Das Modell kann Schwierigkeiten bei der genauen Prognose von Ergebnissen für neu eingeführte Produkte oder Kundensegmente haben, wenn keine ausreichenden historischen Daten verfügbar sind. Darüber hinaus können saisonale Schwankungen im Kundenverhalten zu Schwankungen in der Prognosegenauigkeit führen, wenn sie bei Umschulungen nicht berücksichtigt werden.
* Die Leistung sinkt, wenn die Kundenhistorie spärlich ist, z. B. bei Erstkäufern oder Benutzern mit minimalen Interaktionsdaten. Wenn sich das Kundenverhalten **aufgrund externer Faktoren wie Konjunkturabschwünge oder Branchentrends) ändert** kann das Modell außerdem eine schnelle Anpassung erfordern, um die Genauigkeit aufrechtzuerhalten.

## Künftige Verbesserungen

* Künftige Iterationen umfassen Transfer-Lerntechniken, um die Leistung für Kaltstart-Benutzer zu verbessern und die Anpassungsfähigkeit an sich ändernde Kundenverhaltensweisen zu verbessern. Darüber hinaus wird die Echtzeit-Datenintegration eingeführt, um die Reaktionsfähigkeit und Genauigkeit von Modellen in dynamischen Marketing-Umgebungen zu verbessern.
