---
title: Modelldetails für KI-Modelltransparenz in Adobe Experience Platform
description: Erfahren Sie mehr über Modelldetails in Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: 74a8ef82-cff9-4a7e-95c8-f915eb664eda
source-git-commit: 6623c7dad0fc4ddb7cb79e8f474b824915f130fc
workflow-type: tm+mt
source-wordcount: '3171'
ht-degree: 0%

---

# Modelldetails für KI-Modelltransparenz in Adobe Experience Platform

Ein KI-Modelldetail ist das Standardformat, mit dem die Transparenz eines KI-Modells kommuniziert wird. Modelldetails bieten umfassende Informationen über das zugrunde liegende Modell, auf dem ein bestimmtes KI-Tool basiert. Zu den Modelldetails gehören Informationen wie der Zweck eines KI-Tools, Schulungsdaten, Leistungsmetriken, Einschränkungen und ethische Überlegungen. Sie können die Transparenz nutzen, die Modelldetails bieten, um die Funktionen und Einschränkungen des Modells besser zu verstehen und eine verantwortungsvolle und faire Verwendung von KI besser zu fördern.

Modelldetails sind öffentlich und sollen sowohl bestehenden als auch potenziellen Kunden das Verständnis der von Adobe verwendeten KI-Modelle erleichtern. Modelldetails sind im Allgemeinen statisch. Es gibt jedoch mehrere Aspekte von KI-Modellen, die sich im Laufe der Zeit ändern können, einschließlich Herkunft, Verzerrung und andere Transparenzattribute.

Lesen Sie dieses Dokument, um mehr über Modelldetails in Adobe Experience Platform zu erfahren.

## Modelldetailabschnitte {#model-detail-sections}

Ein Modelldetail besteht aus einer Vielzahl verschiedener Abschnitte, die sich jeweils auf einen bestimmten Aspekt des KI-Modells konzentrieren.

Im Folgenden finden Sie eine Anleitung zu den verschiedenen Abschnitten eines Modelldetails, einschließlich Informationen zu den von ihnen behandelten Fragen.

### Modellübersicht {#model-overview}

Die Modellübersicht enthält allgemeine Informationen zu einem KI-Modell. Verwenden Sie diesen Abschnitt, um Informationen wie den Namen, den Zweck und den Typ Ihres KI-Modells bereitzustellen. Darüber hinaus können Sie diesen Abschnitt verwenden, um Ihre vorgesehenen Benutzenden zu identifizieren und die Integration Ihres Modells mit Experience Platform zu erläutern.

+++Fragen und Beispielantworten anzeigen

| Question | Erforderliche Informationen | Beispielantwort |
| --- | --- | --- |
| Wie heißt das Modell? | Der offizielle Name und die Version des KI-Modells | **CustomerAI Tendenz-Scoring-Modell v2** 0<br>CustomerAI ist ein KI-gestütztes Modell, das entwickelt wurde, um Tendenz-Scores für Benutzende basierend auf früheren Verhaltensweisen und Interaktionen mit einem Unternehmen zu generieren. Es hilft bei der Vorhersage der Wahrscheinlichkeit, dass ein Kunde bestimmte Aktionen durchführt, z. B. einen Kauf tätigt, mit Inhalten interagiert oder abwandert. Dieses Modell wird innerhalb von Adobe Experience Platform bereitgestellt und lässt sich mit verschiedenen Marketing- und Kundenanalyse-Workflows integrieren.</br> |
| Was ist der Zweck des Modells? | Eine kurze Beschreibung dessen, wofür das Modell entwickelt wurde. | Das Modell soll Marketing-Experten und Kundeninteraktions-Teams umsetzbare Einblicke bieten, indem die Wahrscheinlichkeit vorhergesagt wird, dass eine Kundin oder ein Kunde eine bestimmte Aktion ausführt, z. B. einen Kauf tätigt, sich für ein Abonnement anmeldet oder mit einer E-Mail-Kampagne interagiert. Die Ergebnisse ermöglichen es Unternehmen, die Zielgruppensegmentierung zu optimieren und Kundeninteraktionen basierend auf prognostizierten Verhaltensweisen zu personalisieren. |
| Welche Art von Modell ist es? | Der Typ des Modells, z. B. Klassifizierung, Regression, generativ usw. | Dies ist ein **Learning Classification-Modell** das die Wahrscheinlichkeit vorhersagt, dass ein Ereignis (z. B. Kauf, Abwanderung, Interaktion) aufgrund historischer Kundendaten eintritt. Es wird mithilfe von Gradienten-verstärkenden Entscheidungsbäumen (GBDT) mit logistischer Regression trainiert, um Tendenzwerte zu modellieren. |
| Wer sind die vorgesehenen Benutzer? | Die internen und externen Benutzergruppen, für die das Modell vorgesehen ist. | Die wichtigsten Benutzer dieses Modells sind Marketing-Experten, Datenanalysten und Kundeninteraktions-Teams, die Adobe Experience Platform zur Förderung datengesteuerter Marketing-Strategien nutzen. |
| Wie lässt sich dieses Modell mit Adobe Experience Platform integrieren? | Die Integrationsdetails und verwendeten APIs sowie wie sie in die Workflows passen. | CustomerAI lässt sich direkt in die KI-Services von **Adobe Experience Platform integrieren** sodass Benutzende über vordefinierte APIs und Dashboards auf Modellausgaben zugreifen können. Die vom Modell generierten Tendenz-Scores können in **Adobe Journey Optimizer**, **und Adobe Real-Time CDP** verwendet werden, um die Zielgruppensegmentierung zu verfeinern und Marketing-Strategien anzupassen. |

{style="table-layout:auto"}

+++

### Vorgesehene Verwendung {#intended-use}

Der Abschnitt „Verwendungszweck“ enthält Informationen zu den primären Anwendungsfällen Ihres KI-Modells. In diesem Abschnitt können Sie die Probleme, die Ihr Modell lösen soll, die Branchen und/oder Domains, für die Ihr Modell relevant ist, und die Missbrauchsfälle erläutern, die bei der Verwendung Ihres KI-Modells vermieden werden sollten.

+++Fragen und Beispielantworten anzeigen

| Question | Erforderliche Informationen | Beispielantwort |
| --- | --- | --- |
| Was sind die wichtigsten Anwendungsfälle? | Die Szenarien, in denen das Modell voraussichtlich verwendet wird. | Dieses Modell wird in erster Linie für **Kundensegmentierung, zielgerichtetes Marketing und Abwanderungsvorhersagen)**. Unternehmen nutzen dieses Modell, um **Kaufabsicht von Kunden vorherzusagen, Marketing-Kampagnen zu optimieren und Personalisierungsbemühungen zu**. Beispielsweise könnte ein E-Commerce-Unternehmen das Modell verwenden, um Kundinnen und Kunden mit hohen Absichten zu identifizieren und ihnen exklusive Aktionen anzubieten. |
| Welche Probleme löst dieses Modell? | Die wichtigsten vom Modell angesprochenen Probleme. | Marketing-Experten haben oft Schwierigkeiten damit **die richtigen Kundinnen und Kunden für eine Zielgruppenbestimmung zu identifizieren** die Interaktionsbemühungen **optimieren**. Dieses Modell **reduziert**, indem es einen **datengestützten Ansatz) für das Kunden-Targeting**, um sicherzustellen, dass Marketing-Ressourcen effizient zugewiesen werden. |
| Für welche Branchen oder Bereiche ist dieses Modell relevant? | Eine Liste der anwendbaren Branchen. | Das Modell ist in verschiedenen Branchen anwendbar, einschließlich **E-Commerce, Einzelhandel, Finanzdienstleistungen, Telekommunikation und Medien**. Jedes Unternehmen, das sich auf Kundeninteraktion und personalisiertes Marketing stützt, kann von diesem Modell profitieren. |
| Wie sollte dieses Modell nicht verwendet werden? | Alle Fälle von Missbrauch, die vermieden werden sollten. | Das Modell **sollte nicht für Entscheidungen mit hohem Risiko verwendet werden** z. B. **finanzielle Kreditbewertung, medizinische Diagnostik oder rechtliche Bewertungen**. Darüber hinaus ist es aufgrund potenzieller ethischer Bedenken nicht für die Verwendung bei **Vorhersage von persönlich sensiblen** (wie z. B. gesundheitliche Bedingungen, politische Präferenzen) vorgesehen. |

{style="table-layout:auto"}

+++

### Modellein- und -ausgänge {#model-inputs-and-outputs}

Der Abschnitt Modelleingaben und -ausgaben enthält Informationen zu den unterstützten Datentypen, die Ihr Modell als Eingabe verwendet und als Ausgabe zurückgibt. In diesem Abschnitt finden Sie Beispiele für die Dateneingaben und -ausgaben, die für Ihr KI-Modell relevant sind.

+++Fragen und Beispielantworten anzeigen

| Question | Erforderliche Informationen | Beispielantwort |
| --- | --- | --- |
| Welche Datentypen nimmt das Modell als Eingabe? | Die Datentypen, die das Modell als Eingabe verwendet, darunter: Datenfunktionen, Formate und Quellen. | Das Modell verarbeitet **Kundenverhaltensdaten, demografische Attribute und historische Interaktionen**. Dazu gehören Daten wie die Häufigkeit der Website-Besuche, der Kaufverlauf in der Vergangenheit, die Interaktion mit Marketing-E-Mails und demografische Informationen. |
| In welchem Format sollten die Eingaben erfolgen? | Die akzeptierten Eingabeformate. | Eingabedaten müssen als JSON **Objekte strukturiert sein,** Kundenattribute und Verhaltenssignale enthalten. Für die Batch-Verarbeitung akzeptiert das Modell **CSV** Dateien, die gemäß den Datenerfassungsstandards von Adobe Experience Platform formatiert sind. |
| Was gibt das Modell aus? | Der Typ der vom Modell generierten Ausgabe. | Das Modell gibt einen Neigungs-Score zwischen 0 und 1 aus, wobei höhere Werte eine höhere Wahrscheinlichkeit für das Auftreten des prognostizierten Ereignisses angeben. Darüber hinaus bietet es Funktionen und Wichtigkeitswerte, sodass Benutzende verstehen können, welche Faktoren die Prognose beeinflusst haben. |
| Was sind einige Beispieleingaben und -ausgaben? | Eine Beispieleingabe und entsprechende Ausgabe. | <ul><li>**Beispieleingabe:** json { „customer_id“: 12345, „last_purchases“: 3, „last_visit_days“: 7, „email_click_rate“: 0.4 }</li><li>**Beispielausgabe:** json { „customer_id“: 12345, „propensity_score“: 0.82 }</li></ul> |

{style="table-layout:auto"}

+++

### Trainings-Daten {#training-data}

Der Abschnitt Trainingsdaten enthält Informationen zu den Datensätzen, die zum Trainieren eines bestimmten KI-Modells verwendet wurden. In diesem Abschnitt können Sie die Größe und Quelle der Trainings-Daten, die im Datensatz identifizierten Verzerrungen und die Art der Vorverarbeitung von Daten erläutern.

+++Fragen und Beispielantworten anzeigen

| Question | Erforderliche Informationen | Beispielantwort |
| --- | --- | --- |
| Welche Datensätze wurden zum Trainieren des Modells verwendet? | Eine Beschreibung der Datenquellen. | Das Modell wurde auf First-Party-Kundeninteraktionsdaten trainiert, die über Adobe Experience Platform erfasst wurden. Sie enthält historische Kundenverhaltensdaten, Transaktionsdatensätze, E-Mail-Interaktionen und Interaktionsmetriken aus verschiedenen Branchen. |
| Wie groß und aus welcher Quelle werden die Daten gespeichert? | Volumen und Herkunft des Trainings-Datensatzes. | Der Schulungsdatensatz besteht aus 10 Millionen Kundendatensätzen, die von einer Vielzahl von Adobe Experience Platform-Kunden bezogen werden. Zu diesen Datensätzen gehören historische Kundeninteraktionen, Transaktionsdaten, Protokolle zu Verhaltensdaten und demografische Informationen aus verschiedenen Branchen wie Einzelhandel, E-Commerce, Telekommunikation und Finanzen. Die Daten wurden über einen Zeitraum von 24 Monaten erhoben, um eine ausreichende Darstellung saisonaler Trends und langfristiger Interaktionsmuster zu gewährleisten. |
| Gibt es bekannte Verzerrungen im Datensatz? | Voreingenommenheit und Minderungsbemühungen. | Der Datensatz wird hauptsächlich von Benutzern mit hoher Interaktion bezogen, was zu Selektionsverzerrungen führen kann. Um dies abzuschwächen, wendet das Modell stratifizierte Stichprobenverfahren, Verzerrungs-Auditing-Techniken und Datenaugmentationsstrategien an. |
| Wie werden die Daten vorverarbeitet? | Schritte zur Bereinigung und Vorbereitung der Daten. | Der Datensatz wird einer umfassenden Vorverarbeitung unterzogen, um Konsistenz, Qualität und Benutzerfreundlichkeit der Daten sicherzustellen. <ol><li>**Umgang mit fehlenden Werten**: Fehlende Werte werden mithilfe einer Kombination aus mittlerer Imputation (für numerische Felder), Modusimputation (für kategoriale Felder) und prädiktiver Modellierung (für komplexe fehlende Fälle) adressiert.</li><li>**Kategoriale Kodierung:** Kategoriale Variablen wie Kundensegmente und Kaufkategorien werden durch einmalige Kodierungs- und Zielcodierungstechniken in numerische Darstellungen konvertiert.</li><li>**Funktionsskalierung und Normalisierung:** Min-Max-Skalierung wird auf gebundene Variablen (z. B. Alter, Einkommen) angewendet, während die Z-Score-Standardisierung für normal verteilte Funktionen verwendet wird.</li><li>**Zusätzliche Vorverarbeitung:** Die Pipeline umfasst die Erkennung und Entfernung von Ausreißern, die Filterung von Duplikaten, die Standardisierung von Zeitstempeln und die Entwicklung von Funktionen, um die Vorhersagefunktion zu verbessern.</li></ol> |

{style="table-layout:auto"}

+++

### Modellarchitektur und Schulung {#model-architecture-and-training}

Im Abschnitt Modellarchitektur und Training wird der Blueprint Ihres KI-Modells beschrieben. Dieser Abschnitt bezieht sich auf die Struktur und das Design des KI-Modells, einschließlich Details zum Typ des verwendeten Algorithmus und der verwendeten Auswertungsmethoden. Sie können diesen Abschnitt auch verwenden, um Informationen über die verwendeten Trainings-Frameworks sowie über die Compute-Ressourcen bereitzustellen, die bei Schulungen verwendet wurden.

+++Fragen und Beispielantworten anzeigen

| Question | Erforderliche Informationen | Beispielantwort |
| --- | --- | --- |
| Welche Architektur verwendet das Modell? | Der Typ des neuronalen Netzwerks, Ensemble-Methode usw. | Das Modell nutzt mithilfe von XGBost Entscheidungsbäume zur Verlaufssteigerung (Gradient Boosting Decision Trees, GBDT), die für strukturierte Daten optimiert sind. Es wird auf historischen Kundenereignissequenzen trainiert, um prädiktive Verhaltensmuster zu identifizieren. |
| Welche Algorithmen wurden angewendet? | Die verwendeten Techniken des maschinellen Lernens. | Das Modell basiert auf einem überwachten Lernansatz und nutzt Gradient Boosting Decision Trees (GBDT) mit XGBoost als primären Lernalgorithmus. Darüber hinaus wird die logistische Regression als Basismodell für das Benchmarking der Prognosegenauigkeit integriert. |
| Welche Trainings-Frameworks wurden verwendet? | Die für das Training verwendeten Bibliotheken oder Plattformen. | Das Modell wurde mit TensorFlow, XGBoost und Scikit-Learn entwickelt. Trainings-Läufe für die Adobe AI-Cloud-Infrastruktur mit NVIDIA V100-GPUs, die große Datensätze unterstützen. |
| Welche Compute-Ressourcen wurden für das Training verwendet? | Die Hardware- und Cloud-Ressourcen, die für das Training verwendet wurden. | NVIDIA V100 GPUs, geschult in der Google Cloud-Infrastruktur. |
| Welche Auswertungsmethoden wurden verwendet? | Die Metriken und Testverfahren, die für die Bewertung verwendet wurden. | AUC-ROC, Präzisions-Rückruf und Kreuzvalidierung. |

{style="table-layout:auto"}

+++

### Leistung und Bewertung {#performance-and-evaluation}

Der Abschnitt Leistung und Bewertung enthält Informationen zu den Metriken und Methoden, mit denen bewertet wird, wie gut das Modell seine beabsichtigten Aufgaben erfüllt. In diesem Abschnitt erhalten Sie Informationen zu den verwendeten Auswertungsmetriken sowie zu identifizierten Schwächen oder Fehlerfällen.

+++Fragen und Beispielantworten anzeigen

| Question | Erforderliche Informationen | Beispielantwort |
| --- | --- | --- |
| Wie wurde das Modell getestet? | Die zur Validierung der Leistung verwendeten Methoden. | Das Modell wurde mit einem Holdout-Validierungsansatz getestet, bei dem 80 % der Daten für das Training verwendet wurden und 20 % für die Auswertung reserviert waren. |
| Welche Auswertungsmetriken wurden verwendet? | Die wichtigsten Leistungsindikatoren. | Die Effektivität des Modells wird mit **AUC-ROC (0,85)**, **Precision-Recall (0,78)** und **F1-Score (0,80)** gemessen. Diese Metriken helfen bei der Beurteilung der Prognosefähigkeit des Modells in verschiedenen Segmenten. |
| Wie variiert die Leistung in verschiedenen Szenarien? | Die kontextspezifischen Leistungsvarianten. | Geringere Genauigkeit für neue Kundensegmente mit eingeschränkten historischen Daten. |
| Gibt es bekannte Schwächen oder Fälle von Fehlschlägen? | Alle Einschränkungen oder Fehlerpunkte. | Bei Kunden mit begrenzten historischen Daten kann das Modell die Leistung beeinträchtigen (Kaltstart-Problem). Darüber hinaus können saisonale Effekte, z. B. Urlaubstrends, häufige Umschulungen erfordern, um die Genauigkeit zu gewährleisten. |

{style="table-layout:auto"}

+++

### Fairness und Voreingenommenheit {#fairness-and-bias}

Der Abschnitt Fairness und Bias enthält Informationen darüber, wie das KI-Modell in Bezug auf Fairness- und Bias-Metriken abgeschnitten hat. Fairness bezieht sich auf die Fähigkeit des Modells, gerechte Ergebnisse für verschiedene demografische Gruppen und Anwendungsfälle bereitzustellen, während Bias sich auf systematische Fehler bezieht, die zu unfairen Ergebnissen führen. In diesem Abschnitt erfahren Sie mehr über die durchgeführten Fairness-Prüfungen und darüber, wie das Modell Verzerrungen verringert.

+++Fragen und Beispielantworten anzeigen

| Question | Erforderliche Informationen | Beispielantwort |
| --- | --- | --- |
| Welche Fairness-Prüfungen wurden durchgeführt? | Die durchgeführten Prozesse zur Verzerrungsanalyse und Risikominderung. | Das Modell wurde demografischen Paritätstests und gegenseitigen Fairness-Bewertungen unterzogen, um Leistungsunterschiede zwischen verschiedenen Benutzersegmenten zu erkennen. |
| Hat das Modell unverhältnismäßige Auswirkungen auf bestimmte Gruppen? | etwaige festgestellte Leistungsunterschiede. | Die Analyse ergab einen Leistungsabfall von 5 % bei Benutzenden mit niedrigen historischen Interaktionsdaten. Um diesem Problem zu begegnen, beinhaltet das Modell während des Trainings neue Gewichtungstechniken. |
| Wie mindert das Modell die Verzerrung? | Die zur Beseitigung von Verzerrungen verwendeten Techniken. | Der Datensatz wird stratifiziert, um eine proportionale Repräsentation verschiedener Kundendemografiken zu gewährleisten, und während des Trainings werden Fairness-Einschränkungen eingeführt, um zu verhindern, dass das Modell eine bestimmte Gruppe bevorzugt. Regelmäßige Verzerrungsaudits werden unter Verwendung der demografischen Paritätsanalyse durchgeführt, die Anpassungen ermöglicht, wenn Leistungsunterschiede festgestellt werden. |

{style="table-layout:auto"}

+++

### Erklärbarkeit und Interpretierbarkeit {#explainability-and-interpretability}

Der Abschnitt Erklärbarkeit und Interpretierbarkeit enthält Informationen zur Fähigkeit eines KI-Modells, klare und verständliche Erklärungen bereitzustellen, und zur Leichtigkeit, mit der ein menschlicher Benutzer verstehen kann, wie Eingabefunktionen Prognosen und Antworten beeinflussen. In diesem Abschnitt erfahren Sie, wie Benutzer besser verstehen können, warum Ihr Modell bestimmte Entscheidungen trifft und welche Tools oder Techniken für die Interpretation verfügbar sind.

+++Fragen und Beispielantworten anzeigen

| Question | Erforderliche Informationen | Beispielantwort |
| --- | --- | --- |
| Können Benutzende verstehen, warum das Modell bestimmte Entscheidungen trifft? | Die vom Modell verwendeten Interpretationsmethoden. | Das Modell nutzt **SHapley Additive Explanations (SHAP)** um die Auswirkungen der einzelnen Eingabefunktionen auf ihre Prognosen zu quantifizieren und Transparenz darüber zu schaffen, wie Kundenattribute die Tendenzwerte beeinflussen. SHAP-Werte ermöglichen sowohl die globale Interpretierbarkeit, d. h. die Identifizierung der einflussreichsten Faktoren für alle Prognosen, als auch die lokale Interpretierbarkeit, wodurch individuelle Prognosen für bestimmte Kunden erklärt werden. |
| Welche Instrumente oder Techniken stehen zur Interpretation zur Verfügung? | Die verfügbaren Erklärungstools. | Das Modell unterstützt **Local Interpretable Model-Agnostic Explanations (LIME)** und SHAP, um Einblicke in die Art und Weise zu gewähren, wie Eingabefunktionen Prognosen beeinflussen. LIME erzeugt lokale Erklärungen, indem es gestörte Versionen der Eingabedaten erstellt und Änderungen der Vorhersagen beobachtet, während SHAP jedem Merkmal Beitragswerte zuweist, was sowohl globale als auch lokale Interpretationsmöglichkeiten von Modellentscheidungen bietet. |

{style="table-layout:auto"}

+++

### Robustheit und Verallgemeinerung {#robustness-and-generalization}

Der Abschnitt Robustheit und Generalisierung enthält Informationen dazu, wie gut Ihr KI-Modell mit unsichtbaren Daten umgehen kann. Darüber hinaus können Sie in diesem Abschnitt erläutern, wie Ihr Modell seine Leistung und Genauigkeit bei unerwarteten oder anspruchsvollen Eingaben beibehält.

>[!TIP]
>
>In KI beziehen sich „nicht angesehene Daten“ auf Daten, die sich von den Daten unterscheiden, an denen ein bestimmtes Modell trainiert wurde.

+++Fragen und Beispielantworten anzeigen

| Question | Erforderliche Informationen | Beispielantwort |
| --- | --- | --- |
| Wie gut schneidet das Modell bei nicht angezeigten Daten ab? | Die Ergebnisse zu Leistungstests für die Generalisierung. | Das Modell behält **80 % AUC-ROC bei** wenn es an nicht gesehenen Datensätzen getestet wird, was eine starke Generalisierung zu neuen Kundendatensätzen zeigt. Die Leistung bleibt in verschiedenen Kundensegmenten stabil, verschlechtert sich jedoch geringfügig, wenn das Benutzerverhalten erheblich von historischen Mustern abweicht. |
| Wurde das Modell auf belastende Faktoren getestet? | Die Details aus der Robustheitsbewertung. | Das Modell wurde hinsichtlich gestörter und kontraproduktiver Eingaben, einschließlich fehlender Daten, Ausreißer-Injektion und absichtlicher Falschkennzeichnung, bewertet. Während die Leistung unter normalen Bedingungen stabil bleibt, wurde bei extremen unerwünschten Veränderungen eine geringfügige Genauigkeitsverschlechterung (ca. 3-5 %) beobachtet. |

{style="table-layout:auto"}

+++

### Überlegungen zu Sicherheit und Datenschutz {#security-and-privacy-considerations}

Der Abschnitt Überlegungen zur Sicherheit und zum Datenschutz enthält Informationen zu den Maßnahmen und Praktiken, die zum Schutz sensibler Daten und zur Gewährleistung der sicheren Verwendung Ihres Modells implementiert wurden. In diesem Abschnitt können Sie Fragen dazu beantworten, wie Ihr Modell mit sensiblen Daten umgeht.

+++Fragen und Beispielantworten anzeigen

| Question | Erforderliche Informationen | Beispielantwort |
| --- | --- | --- |
| Verarbeitet das Modell vertrauliche Daten? | Alle Informationen, die mit den Datenschutzgesetzen in Einklang stehen. | Das Modell verarbeitet oder speichert keine persönlich identifizierbaren Informationen (PII), und alle für das Training verwendeten Daten werden anonymisiert und aggregiert. Sie befolgt die strikte Einhaltung der DSGVO-, CCPA- und internen Adobe-Datenschutzrichtlinien, um eine verantwortungsvolle Datennutzung sicherzustellen. |
| Welche Techniken zum Schutz der Privatsphäre wurden verwendet? | Die zur Gewährleistung der Datenschutzmaßnahmen verwendeten Techniken. | Das Modell beinhaltet verschiedene Datenschutztechniken, um kontrolliertes Rauschen zu den Daten hinzuzufügen und so eine erneute Identifizierung von Personen zu verhindern. Darüber hinaus werden Hash-, Anonymisierungs- und Tokenisierungsmethoden verwendet, um personenbezogene Daten vor dem Modell-Training und den Rückschlüssen zu entfernen. |

{style="table-layout:auto"}

+++

### Überwachung und Wartung {#monitoring-and-maintenance}

Der Abschnitt Überwachung und Wartung enthält Informationen darüber, wie die Leistung Ihres Modells im Laufe der Zeit überwacht wird und wie oft das Modell neu trainiert wird. Sie können diesen Abschnitt verwenden, um Informationen darüber bereitzustellen, wie Metriken wie Genauigkeit, Präzision, Rückruf und Latenz verfolgt werden.

+++Fragen und Beispielantworten anzeigen

| Question | Erforderliche Informationen | Beispielantwort |
| --- | --- | --- |
| Wie wird die Modellleistung im Zeitverlauf überwacht? | Details zu den für das Modell verwendeten Tracking-Mechanismen. | Das Modell wird kontinuierlich über WatsonX überwacht, wobei wichtige Leistungsindikatoren wie Genauigkeitsabweichungen, Änderungen der Wichtigkeit von Funktionen und Prognosestabilität verfolgt werden. Mechanismen zur Anomalieerkennung und -warnung benachrichtigen das Team, wenn erhebliche Abweichungen vom erwarteten Verhalten auftreten. |
| Wie oft wird das Modell umgeschult? | Die Häufigkeit der Aktualisierungen des Modells. | Das Modell wird monatlich mit aktualisierten Daten zur Kundeninteraktion neu trainiert, um eine kontinuierliche Relevanz zu gewährleisten. Periodische Umschulungen tragen dazu bei, Datenabweichungen und saisonale Schwankungen zu minimieren, die sich auf die Prognosegenauigkeit auswirken könnten. |

{style="table-layout:auto"}

+++

### Ethische Überlegungen und verantwortungsvolle KI {#ethical-considerations-and-responsible-ai}

Der Abschnitt Ethische Überlegungen und Verantwortliche KI enthält Informationen zu allen ethischen Bedenken, die mit Ihrem KI-Modell verbunden sind. Dieser Abschnitt enthält auch Informationen dazu, wie gut Ihr Modell mit den Prinzipien verantwortungsvoller KI übereinstimmt. Verwenden Sie diesen Abschnitt, um Informationen zu den potenziellen ethischen Auswirkungen der Verwendung Ihres Modells bereitzustellen, einschließlich der Erkennung von Verzerrungen, der Gewährleistung von Fairness und der Vermeidung von Schäden für Einzelpersonen oder Gruppen.

+++Fragen und Beispielantworten anzeigen

| Question | Erforderliche Informationen | Beispielantwort |
| --- | --- | --- |
| Welche ethischen Bedenken sind mit diesem Modell verbunden? | Die ermittelten potenziellen Risiken. | Das Modell könnte bei nicht ordnungsgemäßer Überwachung zu Verzerrungen bei der Entscheidungsfindung führen. Wenn beispielsweise bestimmte demografische Daten in den Schulungsdaten überrepräsentiert sind, kann das Modell bestimmte Kundengruppen ungerecht bevorzugen. |
| Wie stimmt das Modell mit den Prinzipien von Responsible AI überein? | Informationen darüber, wie das Modell den KI-Ethikrichtlinien entspricht. | Adobe Experience Platform folgt den Richtlinien für verantwortungsvolle KI, um sicherzustellen, dass Modelle vor der Bereitstellung Verzerrungsprüfungen, Fairness-Tests und menschliche Aufsicht unterzogen werden. |

{style="table-layout:auto"}

+++

### Bekannte Einschränkungen {#known-limitations}

Der Abschnitt Bekannte Einschränkungen enthält Informationen zu den vorhandenen Einschränkungen, die für Ihr KI-Modell identifiziert wurden. Verwenden Sie diesen Abschnitt, um die Bedingungen hervorzuheben, unter denen Ihr KI-Modell möglicherweise schlecht abschneidet, und um die Einschränkungen zu umreißen, die Benutzende kennen müssen.

+++Fragen und Beispielantworten anzeigen

| Question | Erforderliche Informationen | Beispielantwort |
| --- | --- | --- |
| Welche Einschränkungen des Modells sind bekannt? | Alle identifizierten Einschränkungen bei Leistung oder Anwendungsfällen. | Das Modell kann Schwierigkeiten bei der genauen Prognose von Ergebnissen für neu eingeführte Produkte oder Kundensegmente haben, wenn keine ausreichenden historischen Daten verfügbar sind. Darüber hinaus können saisonale Schwankungen im Kundenverhalten zu Schwankungen in der Prognosegenauigkeit führen, wenn sie bei Umschulungen nicht berücksichtigt werden. |
| Unter welchen Bedingungen funktioniert das Modell schlecht? | Etwaige festgestellte Schwachstellen des Modells. | Die Leistung sinkt, wenn die Kundenhistorie spärlich ist, z. B. bei Erstkäufern oder Benutzern mit minimalen Interaktionsdaten. Wenn sich das Kundenverhalten aufgrund externer Faktoren wie Konjunkturabschwünge oder Branchentrends ändert, muss das Modell möglicherweise schnell angepasst werden, um die Genauigkeit zu gewährleisten. |

{style="table-layout:auto"}

+++

### Künftige Verbesserungen {#future-improvements}

Der Abschnitt Zukünftige Verbesserungen enthält Informationen zu Funktionsaktualisierungen, die für Ihr KI-Modell geplant sind. In diesem Abschnitt erfahren Sie mehr über Ihre Verbesserungs-Roadmap.

+++Fragen und Beispielantworten anzeigen

| Question | Erforderliche Informationen | Beispielantwort |
| --- | --- | --- |
| Welche Verbesserungen sind für zukünftige Iterationen geplant? | Der Fahrplan für Verbesserungen. | Künftige Iterationen umfassen Transfer-Lerntechniken, um die Leistung für Kaltstart-Benutzer zu verbessern und die Anpassungsfähigkeit an sich ändernde Kundenverhaltensweisen zu verbessern. Darüber hinaus wird die Echtzeit-Datenintegration eingeführt, um die Reaktionsfähigkeit und Genauigkeit von Modellen in dynamischen Marketing-Umgebungen zu verbessern. |

{style="table-layout:auto"}

+++
