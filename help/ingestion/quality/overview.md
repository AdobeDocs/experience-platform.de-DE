---
keywords: Experience Platform;Startseite;beliebte Themen;Datenqualität;Qualität;Qualität;Unterstützte Validierung;Validierung;Unterstützte Validierung;
solution: Experience Platform
title: Datenqualität
topic-legacy: overview
description: Das folgende Dokument enthält eine Zusammenfassung der unterstützten Prüf- und Prüfverhaltensweisen für die Batch- und Streaming-Erfassung in Adobe Experience Platform.
exl-id: 7ef40859-235a-4759-9492-c63e5fd80c8e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 76%

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

Sowohl die Batch- als auch die Streaming-Erfassung verhindern, dass fehlerhafte Daten nach unten gelangen, indem fehlerhafte Daten für den Abruf und die Analyse in [!DNL Data Lake] verschoben werden. Die Datenerfassung bietet die folgenden Validierungen für die Batch- und Streaming-Erfassung.

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

Weitere Informationen darüber, wie [!DNL Platform] Daten überwacht und validiert, finden Sie in der [Dokumentation zu Überwachungsdatenströmen](./monitor-data-ingestion.md).
