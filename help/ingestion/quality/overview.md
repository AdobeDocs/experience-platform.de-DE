---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Qualität der Datenverarbeitung
topic: overview
translation-type: tm+mt
source-git-commit: 24df962656706d769a7034020d96a545e8f905ca
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 6%

---


# Datenqualität in Adobe Experience Platform

Adobe Experience Platform bietet klar definierte Garantien für Vollständigkeit, Genauigkeit und Konsistenz von Daten, die über Batch- oder Streaming-Vorgänge hochgeladen werden. Das folgende Dokument enthält eine Zusammenfassung der unterstützten Prüf- und Prüfverhaltensweisen für die Batch- und Streaming-Erfassung in Experience Platform.

## Unterstützte Prüfungen

|   | Batch Ingestion | Streaming-Ingestion |
| ------ | --------------- | ------------------- |
| Datentypprüfung | Ja | Ja |
| Enum-Prüfung | Ja | Ja |
| Bereichsprüfung (min, max.) | Ja | Ja |
| Erforderliche Feldüberprüfung | Ja | Ja |
| Musterprüfung | Nein | Ja  |
| Formatprüfung | Nein | Ja |

## Unterstützte Überprüfungsverhalten

Sowohl die Batch- als auch die Streaming-Erfassung verhindern, dass Daten mit Fehlern nach unten gelangen, indem fehlerhafte Daten zum Abrufen und zur Analyse in Data Lake verschoben werden. Die Datenerfassung bietet die folgenden Überprüfungen für die Batch- und Streaming-Erfassung.

### Stapelverarbeitung

Die folgenden Überprüfungen werden für die Stapelverarbeitung durchgeführt:

| Überprüfungsbereich | Beschreibung |
| --------------- | ----------- |
| Schema | Stellt sicher, dass das Schema **nicht** leer ist und einen Verweis auf das Schema &quot;Vereinigung&quot;enthält, wie folgt: `"meta:immutableTags": ["union"]` |
| `identityField` | Stellt sicher, dass alle gültigen Identitätsdeskriptoren definiert sind. |
| `createdUser` | Stellt sicher, dass der Benutzer, der den Stapel aufgenommen hat, den Stapel aufnehmen darf. |

### Streaming-Erfassung

Die folgenden Überprüfungen werden für die Streaming-Erfassung durchgeführt:

| Überprüfungsbereich | Beschreibung |
| --------------- | ----------- |
| Schema | Stellt sicher, dass das Schema **nicht** leer ist und einen Verweis auf das Schema &quot;Vereinigung&quot;enthält, wie folgt: `"meta:immutableTags": ["union"]` |
| `identityField` | Stellt sicher, dass alle gültigen Identitätsdeskriptoren definiert sind. |
| JSON | Stellt sicher, dass die JSON gültig ist. |
| IMS-Organisation | Stellt sicher, dass die aufgelistete IMS-Organisation eine gültige Organisation ist. |
| Quellname | Stellt sicher, dass der Name der Datenquelle angegeben ist. |
| Datenbestand | Stellt sicher, dass der Datensatz angegeben, aktiviert und nicht entfernt wurde. |
| Kopfzeile | Stellt sicher, dass die Kopfzeile angegeben wurde und gültig ist. |

Weitere Informationen darüber, wie Daten von der Plattform überwacht und validiert werden, finden Sie in der Dokumentation [zu](./monitor-data-flows.md)Überwachungsdatenströmen.
