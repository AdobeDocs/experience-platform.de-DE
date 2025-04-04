---
keywords: Katalog-Service; Fragen; häufig gestellte Fragen; FAQ; Datensätze FAQ
title: Häufig gestellte Fragen
description: Antworten auf die am häufigsten gestellten Fragen zu Adobe Experience Platform Catalog Service und Datensätzen.
exl-id: 70d2a352-75bd-4bbc-98e6-aeea16306f63
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# Häufig gestellte Fragen {#faq}

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zum Adobe Experience Platform-Katalog-Service und zu Datensätzen. Fragen und Fehlerbehebungen für andere Experience Platform-Services, einschließlich Problemen in allen Experience Platform-APIs, finden Sie im [Handbuch zur Fehlerbehebung bei Experience Platform](../landing/troubleshooting.md).

## Aufbewahrungsrichtlinien und -regeln {#retention-policies-and-rules}

### Auf welche Arten von Datensätzen kann ich Regeln für Aufbewahrungsrichtlinien anwenden?

+++Antwort

Sie können Aufbewahrungsrichtlinien für Datensätze einrichten, die mithilfe der ExperienceEvent-XDM-Klasse erstellt wurden. Für den Profil-Service können Aufbewahrungsrichtlinien nur auf ExperienceEvent-Datensätze angewendet werden, nachdem sie für das Profil aktiviert wurden.

+++

### Kann ich unterschiedliche Aufbewahrungsrichtlinien für den Data Lake und den Profil-Service festlegen?

+++Antwort

Ja, Sie können unterschiedliche Aufbewahrungsrichtlinien für den Data Lake und den Profil-Service anwenden.

+++

## Ausführung und Timing von Aufbewahrungsaufträgen {#retention-job-execution-and-timing}

### Wie bald löscht der Datensatz-Aufbewahrungsauftrag Daten aus Data-Lake-Services?

+++Antwort

Datensatzgültigkeiten werden wöchentlich ausgewertet und verarbeitet, wobei alle abgelaufenen Datensätze gelöscht werden. Ein Ereignis wird als abgelaufen betrachtet, wenn es länger als 30 Tage in Experience Platform aufgenommen wurde (Aufnahmedatum > 30 Tage) und sein Ereignisdatum den definierten Aufbewahrungszeitraum überschreitet.

+++

### Wie bald löscht der Datensatzaufbewahrungsauftrag Daten aus Profil-Services?

+++Antwort

Nach dem Festlegen einer Aufbewahrungsrichtlinie werden vorhandene Ereignisse sofort aus Experience Platform gelöscht, wenn ihr Ereigniszeitstempel die Aufbewahrungsfrist überschreitet. Neue Ereignisse werden gelöscht, sobald ihr Zeitstempel die Aufbewahrungsfrist überschreitet.

Wenn Sie beispielsweise am 15. Mai eine 30-Tage-Gültigkeit anwenden, passiert Folgendes:

- Neue Ereignisse erhalten bei ihrer Aufnahme eine Gültigkeit von 30 Tagen.
- Vorhandene Ereignisse mit einem Zeitstempel, der älter als der 15. April ist, werden sofort gelöscht.
- Vorhandene Ereignisse mit einem Zeitstempel nach dem 15. April laufen 30 Tage nach ihrem Zeitstempel ab. Zum Beispiel würde ein Ereignis vom 18. April am 18. Mai gelöscht.

+++

## Nutzung und Überwachung von Datensätzen

### Wie kann ich meine aktuelle Datensatznutzung überprüfen?

+++Antwort

Sie können die neueste Speichergröße auf Datensatzebene in Data Lake und Profil als separate Metriken auf der Inventarseite [!UICONTROL Datensätze] anzeigen. Sie können auch die Spalten sortieren, um die größten Datensätze zu identifizieren und sicherzustellen, dass Aufbewahrungsrichtlinien angewendet werden. Die Verwendung auf Sandbox-Ebene ist im Dashboard Lizenznutzung verfügbar. Weitere Informationen finden Sie [ „Dokumentation zur ](../dashboards/guides/license-usage.md)&quot;.

+++

### Wie kann ich überprüfen, ob der Datenaufbewahrungsauftrag erfolgreich war?

+++Antwort

Sie können den Zeitstempel des letzten Datenaufbewahrungsauftrags in der [Benutzeroberfläche für die Datensatzaufbewahrungskonfiguration](./datasets/user-guide.md#data-retention-policy) und auf der Inventarseite [!UICONTROL Datensätze] überprüfen. Berichte zur historischen Datensatznutzung sind derzeit nicht verfügbar, sind aber für zukünftige Versionen geplant.

+++

## Datenwiederherstellung {#data-recovery}

### Kann ich gelöschte Daten wiederherstellen?

+++Antwort

Nein, nach Anwendung der Aufbewahrungsrichtlinie werden alle Daten, die älter als die Aufbewahrungsfrist sind, dauerhaft gelöscht und können nicht wiederhergestellt werden.

+++
