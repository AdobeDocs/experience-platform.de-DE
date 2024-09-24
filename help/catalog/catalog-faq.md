---
keywords: Katalogdienst; Fragen; häufig gestellte Fragen; FAQ; Datensätze FAQ
title: Häufig gestellte Fragen
description: Antworten auf die am häufigsten gestellten Fragen zu Adobe Experience Platform Catalog Service und Datensätzen.
source-git-commit: 0bb10754e2f5bc289567368c803d4397cec77bf6
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 1%

---

# Häufig gestellte Fragen {#faq}

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Adobe Experience Platform Catalog Service und Datensätzen. Fragen und Informationen zur Fehlerbehebung bei anderen Platform-Diensten, einschließlich Problemen, die in allen Platform-APIs aufgetreten sind, finden Sie im [Handbuch zur Fehlerbehebung bei Experience Platform](../landing/troubleshooting.md).

## Bindungsrichtlinien und -regeln {#retention-policies-and-rules}

### Auf welche Arten von Datensätzen kann ich Aufbewahrungsrichtlinien anwenden?

+++Antwort

Sie können Aufbewahrungsrichtlinien für Datensätze einrichten, die mit der ExperienceEvent XDM-Klasse erstellt wurden. Für den Profildienst können Aufbewahrungsrichtlinien nur auf ExperienceEvent-Datensätze angewendet werden, nachdem sie für Profile aktiviert wurden.

+++

### Kann ich verschiedene Aufbewahrungsrichtlinien für den Data Lake und den Profildienst festlegen?

+++Antwort

Ja, Sie können verschiedene Aufbewahrungsrichtlinien für den Data Lake und den Profildienst anwenden.

+++

## Ausführung und zeitlicher Ablauf von Treueaufträgen {#retention-job-execution-and-timing}

### Wie bald werden Daten aus Data Lake-Diensten durch den Datenspeicherungsauftrag gelöscht?

+++Antwort

Die Datensatzabläufe werden wöchentlich ausgewertet und verarbeitet, wodurch alle abgelaufenen Datensätze gelöscht werden. Ein Ereignis gilt als abgelaufen, wenn es mehr als 30 Tage in Platform aufgenommen wurde (Erfassungsdatum > 30 Tage) und sein Ereignisdatum den festgelegten Aufbewahrungszeitraum überschreitet.

+++

### Wie bald werden Daten aus den Profildiensten durch den Auftrag zur Aufbewahrung von Datensätzen gelöscht?

+++Antwort

Sobald eine Aufbewahrungsrichtlinie festgelegt ist, werden vorhandene Ereignisse sofort aus Platform gelöscht, wenn ihr Ereignis-Zeitstempel die Aufbewahrungsfrist überschreitet. Neue Ereignisse werden gelöscht, sobald ihr Zeitstempel die Aufbewahrungsfrist überschreitet.

Wenn Sie beispielsweise am 15. Mai eine Ablaufrichtlinie von 30 Tagen anwenden, geschieht Folgendes:

- Neue Ereignisse erhalten bei ihrer Erfassung eine Gültigkeit von 30 Tagen.
- Vorhandene Ereignisse mit einem Zeitstempel, der älter als der 15. April ist, werden sofort gelöscht.
- Vorhandene Ereignisse mit einem Zeitstempel nach dem 15. April laufen 30 Tage nach ihrem Zeitstempel ab. Beispielsweise würde ein Ereignis vom 18. April am 18. Mai gelöscht.

+++

## Nutzung und Überwachung von Datensätzen

### Wie kann ich die aktuelle Datensatznutzung überprüfen?

+++Antwort

Sie können die neueste Speichergröße auf Datensatzebene im Data Lake und Profil als separate Metriken auf der Inventarseite [!UICONTROL Datensätze] anzeigen. Sie können die Spalten auch sortieren, um die größten Datensätze zu identifizieren und sicherzustellen, dass die Aufbewahrungsrichtlinien angewendet werden. Die Verwendung auf Sandbox-Ebene ist im Dashboard zur Lizenznutzung verfügbar. Weitere Informationen finden Sie in der Dokumentation zur [Lizenznutzung](../dashboards/guides/license-usage.md) .

+++

### Wie kann ich überprüfen, ob der Datenspeicherungsauftrag erfolgreich war?

+++Antwort

Sie können den Zeitstempel des letzten Datenspeicherungsauftrags in der Konfigurationsoberfläche für die Datensatzbeibehaltung ](./datasets/user-guide.md#data-retention-policy) und auf der Inventarseite für [!UICONTROL Datensätze] überprüfen. [ Berichte zur Verwendung historischer Datensätze sind derzeit nicht verfügbar, sind aber für künftige Versionen geplant.

+++

## Datenwiederherstellung {#data-recovery}

### Kann ich gelöschte Daten wiederherstellen?

+++Antwort

Nein, nach Anwendung der Aufbewahrungsrichtlinie werden alle Daten, die älter als die Aufbewahrungsfrist sind, dauerhaft gelöscht und können nicht wiederhergestellt werden.

+++

