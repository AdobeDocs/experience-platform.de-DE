---
title: KI-Assistent Natürliche Sprache zu SQL-Modellkarte
description: Erfahren Sie mehr über das KI-Modell des KI-Assistenten für die natürliche Sprache in SQL.
hide: true
hidefromtoc: true
source-git-commit: 70b705a7c6df24ad9549c46832ff4898253670ac
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# KI-Assistent Operative Einblicke Natürliche Sprache zu SQL-Modellkarte

## Modellübersicht {#model-overview}

* Der offizielle Name des Modells ist AI Assistant Operational Insights Natural Language to SQL Model ([!DNL NL2SQL]) und wurde in der neuesten GA-Version im Februar 2025 veröffentlicht.
* Das Modell ist so konzipiert, dass es die natürlichen Sprachabfragen von Kunden über betriebliche Einblicke in SQL-Abfragen übersetzt. Diese SQL-Abfragen werden über das Adobe Experience Platform-Wissensdiagramm ausgeführt, das Metadaten zu den Experience Platform-Entitäten der Kundinnen und Kunden enthält - z. B. Schemata, Datensätze, Zielgruppen, Ziele und Journey. Die Ergebnisse der SQL-Abfragen werden dann verwendet, um Antworten auf die ursprünglichen Fragen der natürlichen Sprache des Kunden zu generieren.
* Die Hauptanwender dieses Modells sind Marketing-Experten, Datenanalysten oder Kunden-Journey-Manager, die versuchen, operative Erkenntnisse in Experience Platform mithilfe natürlicher Sprache zu verstehen und darauf zu reagieren. Möglicherweise sind sie keine Experten in SQL oder Data Engineering, benötigen aber schnelle, präzise Antworten auf ihre Experience Platform-Entitäten, um fundierte Entscheidungen zu treffen und Kundenerlebnisse zu optimieren.
* Dieses Modell ist Teil des KI-Assistenten für operative Einblicke, mit dem es Benutzenden hilft, auf Metadaten über ihre Experience Platform-Entitäten zuzugreifen, z. B. Zielgruppen, Journey, Schemata, Attribute, Datensätze und Ziele. Benutzende können Fragen in natürlicher Sprache stellen, z. B. welche Zielgruppen aktiviert sind oder welche Zielgruppen ein bestimmtes Schema verwenden, und das Modell übersetzt diese in SQL-Abfragen über das Experience Platform-Wissensdiagramm. Auf diese Weise können Benutzer schnell operative Transparenz erlangen und fundierte Entscheidungen treffen, ohne das System manuell untersuchen oder abfragen zu müssen.
* Dieses Modell behandelt wichtige Probleme, mit denen Geschäftsbenutzer und Analysten, die mit Experience Platform arbeiten, konfrontiert sind, z. B. die Komplexität der Navigation durch große Mengen miteinander verbundener Metadaten, die Notwendigkeit, SQL-Abfragen manuell zu schreiben, um betriebliche Einblicke abzurufen, und die mangelnde Sichtbarkeit der Art und Weise, wie Experience Platform-Entitäten wie Zielgruppen, Datensätze und Journey miteinander verbunden sind oder funktionieren. Durch die Aktivierung des Zugriffs auf Metadaten in natürlicher Sprache und die Automatisierung der SQL-Generierung reduziert das Modell die Abhängigkeit von technischen Ressourcen, verkürzt die insight-Erkennungszeit und ermöglicht Anwendern schnellere, datengestützte Entscheidungen.
* Das Modell sollte nicht für den Zugriff auf oder die Ableitung von personenbezogenen Daten (PII) wie Kundennamen, E-Mail-Adressen oder Telefonnummern verwendet werden, selbst wenn solche Daten in der Plattform vorhanden sind.
* Darüber hinaus sollten Compliance- oder Governance-Prüfungen, z. B. die Validierung von Richtlinien zur Datenaufbewahrung, Zugriffskontrollregeln oder Einverständnisstatus, nicht damit durchgeführt werden. Diese Aufgaben erfordern spezielle Systeme und Strategien.

## Modelldetails {#model-details}

* Der Modelltyp ist LLM Prompt with Dynamic In-Context Learning (LLM-Eingabeaufforderung mit dynamischem Lernen im Kontext).
* Bei den Modelleingaben handelt es sich um Abfragen in natürlicher Sprache.
* Das Modell gibt SQL-Abfragen in [!DNL Snowflake] Syntax aus, die über Experience Platform Knowledge Graph ausgeführt werden.

**Beispieleingabe**

```console
How many datasets were created within the last 10 days?
```

**Beispielausgabe**

```SQL
SELECT
    COUNT(*) AS datasetCount 
FROM hkg_dim_dataset 
WHERE
    createdTime >= DATEADD(day, -10, CURRENT_DATE);
```

## Modellschulung {#model-training}

* [!DNL NL2SQL] verwendet [!DNL OpenAI] GPT-basierte Modelle für kontextbezogenes Lernen.
* Die [!DNL NL2SQL] Fragenbank enthält 428 Abfragen des [!DNL Operational Insights]-Teams und 524 Abfragen externer Teams für Alpha-Anwendungsfälle.

## Modellauswertung {#model-evaluation}

* Das Modell wird mit Genauigkeit bewertet. Beispielsweise gibt die Anzahl [!DNL NL2SQL] Anforderungen von allen Anforderungen die richtigen SQL-Ergebnisse zurück.
* Der Bewertungsprozess ist eine Kombination aus regelbasiertem Matching (SQL-Standardisierung und dann direkter SQL-Zeichenfolgenabgleich), LLM-basiertem SQL-Solver und menschlicher Auswertung
* Offene Sets werden für Regressionstests verwendet, und wöchentliche Anmerkungsprojekte überwachen die Leistung des Modells durch abgefragten echten Kunden-Traffic.
* Im Hinblick auf die kontradiktorische Bewertung gibt es ein separates Modell innerhalb und außerhalb des Geltungsbereichs, das als Leitplanke für [!DNL NL2SQL] dient.

## Modellbereitstellung {#model-deployment}

* Das LLM-Modell ist ein GPT-basiertes Modell, das von [!DNL Azure OpenAI] APIs gehostet wird.
* Das Basismodell wird von [!DNL Azure] gehostet.
* Das Modell wird regelmäßig wöchentlich durch die Erweiterung der Fragenbanken aktualisiert. Der Modus wird bei Bedarf auch durch neue Aufforderungsstrategien und Anweisungen aktualisiert.

## Erklärbarkeit {#explainability}

Das Modell verwendet ein separates Erklärungsmodell für SQL.

## Fairness und Voreingenommenheit {#fairness-and-bias}

* Um sicherzustellen, dass das Modell Abfragen konsistent über verschiedene Benutzerinteressen und sprachliche Variationen hinweg interpretiert und generiert, ohne Vorurteile einzuführen oder Stereotypen zu verstärken, verwendet Adobe eine sofortige Prüfung, Erklärbarkeit und Sicherheitsmechanismen, um verzerrte oder unethische Ausgaben zu vermeiden.
* Die Modellausgabe ist von den Beispielen für kontextbezogenes Lernen und den vom Abrufenden in der Eingabeaufforderung ausgewählten Elementen betroffen. Die Fragebankbeispiele enthalten Beispiele, die aus PM-Sicht als repräsentativ angesehen werden, und auch wir erweitern die Fragebanken auf Basis des realen Kundenverkehrs.

## Stärke {#robustness}

Da die meisten empfangenen Abfragen nicht in der Fragenbank behandelt werden, spiegelt die Genauigkeit des Produktions-Traffics die Robustheit des Modells wider.

## Überlegungen zum Datenschutz und zur Sicherheit {#privacy-and-security-considerations}

Das Modell verarbeitet oder speichert keine persönlich identifizierbaren Informationen (PII), und diese Informationen werden für die SQL-Generierung ausgeblendet. Für die attributbasierte Zugriffssteuerungs-Berechtigungsprüfung wird die generierte SQL vom Experience Platform Knowledge Graph-Team weiter verarbeitet, um die Qualität der Governance sicherzustellen.

## Ethische Überlegungen {#ethical-considerations}

Um das Offenlegen von personenbezogenen oder sensiblen Attributen zu vermeiden, wurde das Modell so konzipiert, dass es den Datenschutz unterstützt, die Verstärkung vorhandener Datenverzerrungen vermeidet und die Zugriffssteuerungsgrenzen einhält. Dazu gehören Filtern, Taggen und Prüfen von Schemafeldern auf eine verantwortungsvolle Verwendung.

