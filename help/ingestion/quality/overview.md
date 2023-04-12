---
keywords: Experience Platform; Startseite; beliebte Themen; Datenqualität; Qualität; Qualität; unterstützte Validierung; Validierung; unterstützte Validierung;
solution: Experience Platform
title: Datenqualität
description: Das folgende Dokument bietet eine Zusammenfassung der unterstützten Prüf- und Validierungsverfahren für die Batch- und Streaming-Erfassung in Adobe Experience Platform.
exl-id: 7ef40859-235a-4759-9492-c63e5fd80c8e
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 54%

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

Sowohl die Batch- als auch die Streaming-Erfassung verhindern, dass fehlerhafte Daten nachgelagert werden, indem fehlerhafte Daten zum Abrufen und zur Analyse in verschoben werden. [!DNL Data Lake]. Die Datenerfassung bietet die folgenden Validierungen für die Batch- und Streaming-Erfassung.

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
| Organisation | Stellt sicher, dass die aufgelistete Organisation eine gültige Organisation ist. |
| Name der Quelle | Stellt sicher, dass der Name der Datenquelle angegeben ist. |
| Datensatz | Stellt sicher, dass der Datensatz angegeben, aktiviert und nicht entfernt wurde. |
| Kopfzeile | Stellt sicher, dass die Kopfzeile angegeben und gültig ist. |

Weitere Informationen zum [!DNL Platform] Daten zu Monitoren und Validierungen finden Sie im Abschnitt [Dokumentation zur Überwachung von Datenflüssen](./monitor-data-ingestion.md).

## Überprüfung des Identitätswerts

In der folgenden Tabelle sind die vorhandenen Regeln aufgeführt, die Sie befolgen müssen, um eine erfolgreiche Überprüfung Ihres Identitätswerts sicherzustellen.

| Namespace | Validierungsregel | Systemverhalten bei Verletzung einer Regel |
| --- | --- | --- |
| ECID | <ul><li>Der Identitätswert einer ECID muss genau 38 Zeichen betragen.</li><li>Der Identitätswert einer ECID darf nur aus Zahlen bestehen.</li></ul> | <ul><li>Wenn der Identitätswert der ECID nicht genau 38 Zeichen beträgt, wird der Datensatz übersprungen.</li><li>Wenn der Identitätswert der ECID nicht numerische Zeichen enthält, wird der Datensatz übersprungen.</li></ul> |
| Nicht ECID | Der Identitätswert darf 1024 Zeichen nicht überschreiten. | Wenn der Identitätswert 1024 Zeichen überschreitet, wird der Datensatz übersprungen. |

Weitere Informationen finden Sie unter [!DNL Identity Service] Limits, siehe [[!DNL Identity Service] Limits - Übersicht](../../identity-service/guardrails.md).
