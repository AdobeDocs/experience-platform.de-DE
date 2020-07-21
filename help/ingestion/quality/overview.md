---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Qualität der Datenerfassung
topic: overview
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 86%

---


# Datenqualität in Adobe Experience Platform

Adobe Experience Platform bietet klar definierte Garantien für Vollständigkeit, Genauigkeit und Konsistenz von Daten, die über Batch- oder Streaming-Erfassung hochgeladen werden. Das folgende Dokument enthält eine Zusammenfassung der unterstützten Prüf- und Validierungsverfahren für die Batch- und Streaming-Erfassung in Adobe [!DNL Experience Platform].

## Unterstützte Prüfungen

|   | Batch-Erfassung | Streaming-Erfassung |
| ------ | --------------- | ------------------- |
| Datentypprüfung | Ja | Ja |
| Aufzählungsprüfung | Ja | Ja |
| Bereichsprüfung (min, max.) | Ja | Ja |
| Prüfung auf erforderliche Felder | Ja | Ja |
| Musterprüfung | Nein | Ja |
| Formatprüfung | Nein | Ja |

## Unterstützte Validierungsverfahren

Both batch and streaming ingestion prevent failed data from going downstream by moving bad data for retrieval and analysis in [!DNL Data Lake]. Die Datenerfassung bietet die folgenden Validierungen für die Batch- und Streaming-Erfassung.

### Batch-Erfassung

Die folgenden Validierungen werden für die Batch-Erfassung durchgeführt:

| Validierungsbereich | Beschreibung |
| --------------- | ----------- |
| Schema | Stellt sicher, dass das Schema **nicht** leer ist und wie folgt einen Verweis auf das Schema „Vereinigung“ enthält: `"meta:immutableTags": ["union"]` |
| `identityField` | Stellt sicher, dass alle gültigen Identitätsdeskriptoren definiert sind. |
| `createdUser` | Stellt sicher, dass der Benutzer, der den Batch erfasst hat, diesen auch erfassen darf. |

### Streaming-Erfassung

Die folgenden Validierungen werden für die Streaming-Erfassung durchgeführt:

| Validierungsbereich | Beschreibung |
| --------------- | ----------- |
| Schema | Stellt sicher, dass das Schema **nicht** leer ist und wie folgt einen Verweis auf das Schema „Vereinigung“ enthält: `"meta:immutableTags": ["union"]` |
| `identityField` | Stellt sicher, dass alle gültigen Identitätsdeskriptoren definiert sind. |
| JSON | Stellt sicher, dass die JSON gültig ist. |
| IMS-Organisation | Stellt sicher, dass die aufgelistete IMS-Organisation eine gültige Organisation ist. |
| Name der Quelle | Stellt sicher, dass der Name der Datenquelle angegeben ist. |
| Datensatz | Stellt sicher, dass der Datensatz angegeben, aktiviert und nicht entfernt wurde. |
| Kopfzeile | Stellt sicher, dass die Kopfzeile angegeben und gültig ist. |

More information about how [!DNL Platform] monitors and validates data can be found in the [monitoring data flows documentation](./monitor-data-flows.md).
