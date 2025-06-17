---
title: Details zum KI-Assistenten für SQL-Modell in natürlicher Sprache
description: Erfahren Sie mehr über das KI-Modell des KI-Assistenten für die natürliche Sprache in SQL.
exl-id: ca157945-5f74-45d0-9d40-c65d09a8e80d
source-git-commit: 26d05e9519491ef2e8f239cba6a2cde43cff941c
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# KI-Assistent Betriebskenntnisse Natürliche Sprache zu SQL-Modell Details

>[!IMPORTANT]
>
>Adobe veröffentlicht aktiv weitere Modelldetails. Sobald Experience League verfügbar ist, wird zusätzliche Dokumentation hinzugefügt.

## Modellübersicht {#model-overview}

* **Modellname und -version**: Adobe Experience Platform AI Assistant Operational Insights Natural Language to SQL-Modell ([!DNL NL2SQL]).
* **Modellveröffentlichungsdatum**: Februar 2025
* **Modellzweck**: Das Modell ist so konzipiert, dass es die Abfragen von Kunden in natürlicher Sprache zu operativen Einblicken in SQL-Abfragen übersetzt. Diese SQL-Abfragen werden über das Adobe Experience Platform-Wissensdiagramm ausgeführt, das Metadaten zu den Experience Platform-Entitäten der Kundinnen und Kunden enthält - z. B. Schemata, Datensätze, Zielgruppen, Ziele und Journey. Die Ergebnisse der SQL-Abfragen werden dann verwendet, um Antworten auf die ursprünglichen Fragen der natürlichen Sprache des Kunden zu generieren.
* **Vorgesehene Benutzer**: Die Hauptbenutzer dieses Modells sind Marketing-Experten, Datenanalysten oder Kunden-Journey-Manager, die versuchen, operative Erkenntnisse in Experience Platform mithilfe natürlicher Sprache zu verstehen und darauf zu reagieren. Möglicherweise sind sie keine Experten in SQL oder Data Engineering, benötigen aber schnelle, präzise Antworten auf ihre Experience Platform-Entitäten, um fundierte Entscheidungen zu treffen und Kundenerlebnisse zu optimieren.
* **Anwendungsfälle**: Dieses Modell hilft Benutzenden, auf Metadaten über ihre Experience Platform-Entitäten zuzugreifen, z. B. Zielgruppen, Journey, Schemata, Attribute, Datensätze und Ziele. Benutzende können Fragen in natürlicher Sprache stellen, z. B. welche Zielgruppen aktiviert sind oder welche Zielgruppen ein bestimmtes Schema verwenden, und das Modell übersetzt diese in SQL-Abfragen über das Experience Platform-Wissensdiagramm. Auf diese Weise können Benutzer schnell operative Transparenz erlangen und fundierte Entscheidungen treffen, ohne das System manuell untersuchen oder abfragen zu müssen.
* **Probleme**: Dieses Modell behandelt wichtige Probleme, mit denen Geschäftsbenutzer und Analysten, die mit Experience Platform arbeiten, konfrontiert sind, z. B. die Komplexität der Navigation durch große Mengen miteinander verbundener Metadaten, die Notwendigkeit, SQL-Abfragen manuell zu schreiben, um betriebliche Einblicke abzurufen, und die fehlende Sichtbarkeit der Art und Weise, wie Experience Platform-Entitäten wie Zielgruppen, Datensätze und Journey miteinander verbunden sind oder funktionieren. Durch die Aktivierung des Zugriffs auf Metadaten in natürlicher Sprache und die Automatisierung der SQL-Generierung reduziert das Modell die Abhängigkeit von technischen Ressourcen, verkürzt die insight-Erkennungszeit und ermöglicht Anwendern schnellere, datengestützte Entscheidungen.

## Modelldetails {#model-details}

* **Modelltyp**: LLM-Eingabeaufforderung mit dynamischem Lernen im Kontext
* **Input**: Abfragen in natürlicher Sprache von Benutzern.
* **Ausgabe**: Das Modell gibt SQL-Abfragen in [!DNL Snowflake] Syntax aus, die über das Experience Platform-Wissensdiagramm ausgeführt werden.

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

## Modellauswertung {#model-evaluation}

* **Auswertungsmetriken und -**: Das Modell wird bewertet, indem die [!DNL NL2SQL] Anforderungen betrachtet und bewertet werden, wie viele Anforderungen die richtigen SQL-Ergebnisse liefern. Der Bewertungsprozess ist eine Kombination aus regelbasiertem Matching (SQL-Standardisierung und dann direkter SQL-Zeichenfolgenabgleich), LLM-basiertem SQL-Solver und menschlicher Auswertung.
* **Auswertungsdaten und Vorverarbeitung**: Wir verwenden offene Sets für Regressionstests und wir haben auch wöchentliche Anmerkungsprojekte, um die Leistung des Modells durch erfassten realen Kunden-Traffic zu überwachen.

## Modellbereitstellung {#model-deployment}

* **Modellüberwachung**: Das Basismodell wird von [!DNL Azure] gehostet.
* **Modellaktualisierung**: Das Adobe Experience Platform AI Assistant Operational Insights Natural Language to SQL-Modell wird regelmäßig (wöchentlich) durch die Erweiterung der Fragenbank aktualisiert. Das Modell wird bei Bedarf auch durch neue Aufforderungsstrategien und Anweisungen aktualisiert.

## Fairness und Voreingenommenheit {#fairness-and-bias}

* **Modellgerechtigkeit**: Um sicherzustellen, dass das Modell Abfragen konsistent über verschiedene Benutzerinteressen und sprachliche Varianten hinweg interpretiert und generiert, ohne Verzerrungen oder Stereotypen zu verstärken, verwendet Adobe eine sofortige Prüfung, Erklärbarkeit und Schutzmaßnahmen gegen die Erzeugung von verzerrten oder unethischen Ausgaben.
* **Datenverzerrung**: Die Modellausgabe wird durch die Beispiele für kontextbezogenes Lernen und die Auswahl der Elemente in der Eingabeaufforderung beeinflusst. Die Fragebankbeispiele enthalten Beispiele, die aus Sicht des Produktmanagements als repräsentativ gelten. Je nach Anwendungsfall sollten Kunden überlegen, wie potenzielle Verzerrungen in den Modellausgaben mit ihrer beabsichtigten Anwendung übereinstimmen oder sich darauf auswirken können.

## Ethische Überlegungen {#ethical-considerations}

**Ethische Überlegungen im Zusammenhang mit dem Modell**: Um die Offenlegung von personenbezogenen Daten oder sensiblen Attributen zu vermeiden, wurde das Modell so konzipiert, dass bestehende Datenverzerrungen nicht verstärkt werden und die Zugriffssteuerungsgrenzen eingehalten werden. Dazu gehören Filtern, Taggen und Prüfen von Schemafeldern auf eine verantwortungsvolle Verwendung.
