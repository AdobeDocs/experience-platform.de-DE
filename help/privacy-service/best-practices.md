---
title: Best Practices für Privacy Service
description: Erfahren Sie, wie Sie die Verarbeitungszeit und die Kosten reduzieren, die Ihrem Unternehmen beim Ausführen von Datenschutzanfragen entstehen, indem Sie diese optimalen Nutzungsrichtlinien befolgen.
exl-id: 1333d6c6-5ca0-41c1-9f9e-aa2a5a8b8a9c
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '1234'
ht-degree: 0%

---

# Best Practices für Privacy Service

Verwenden Sie Privacy Service, um die Einhaltung von Datenschutzbestimmungen zu automatisieren, wenn Kunden auf ihre personenbezogenen Daten in Ihren Datenspeichern zugreifen oder diese löschen möchten. Um diese sich wandelnden geschäftlichen Anforderungen zu erfüllen, bietet Privacy Service eine RESTful-API und -Benutzeroberfläche, mit der Zugriffs- und Löschanfragen für Kundendaten in Adobe Experience Cloud-Anwendungen eingereicht werden können.

In diesem Handbuch werden Best Practices für die effiziente Verarbeitung von Datenschutzanfragen und die Optimierung der Reaktionszeiten bei der Verwaltung von Kundendatenanfragen beschrieben.

## Erste Schritte {#getting-started}

Dieses Handbuch setzt ein Verständnis von [Privacy Service](./home.md) voraus und wie Sie damit Zugriffs- und Löschanfragen Ihrer Datensubjekte (Kunden) in allen Adobe Experience Cloud-Anwendungen verwalten können. Es wird außerdem empfohlen, das Handbuch zum Erstellen einer Datenschutzauftragsanforderung in der Benutzeroberfläche ](./ui/user-guide.md#create-a-new-privacy-job-request) oder [der API](./api/overview.md) zu lesen und zu verstehen, wie diese Vorgänge programmatisch ausgeführt werden.[

## Voraussetzungen {#prerequisites}

Der Zugriff auf den Adobe Experience Platform Privacy Service wird über granulare rollenbasierte Berechtigungen in Adobe Admin Console gesteuert. Sie benötigen die entsprechenden Berechtigungen in einem Produktprofil, um bestimmte Funktionen in der Privacy Service-Benutzeroberfläche und -API verwenden zu können. Wenden Sie sich an Ihren Systemadministrator, wenn Sie zusätzliche Berechtigungen benötigen.

Administratoren können das Handbuch zum [Verwalten von Berechtigungen für Privacy Service](./permissions.md) lesen, um weitere Informationen zu erhalten.

## Richtlinien zur Erstellung von Datenschutzaufträgen {#creation-guidelines}

Um die Anforderungsverarbeitung zu optimieren und die Antwortzeiten zu verbessern, beachten Sie beim Erstellen von Datenschutzaufträgen die folgenden Richtlinien. Dies gilt sowohl für die API- als auch für die UI-Methoden.

1. **Maximieren Sie die Datensubjekte pro Anforderung:** Nehmen Sie so viele Datensubjekte wie möglich auf, bis zu 1000 pro Anforderung.
2. **Gruppen-IDs für Effizienz:** Gruppieren Sie mehrere IDs für ein einzelnes Datensubjekt (bis zu neun) in jeder Anfrage. Die **IDs können aus verschiedenen Adobe-Diensten in derselben Anforderung stammen**.
3. **Kombinieren von Zugriffs- und Löschvorgängen:** Schließen Sie sowohl die Auftragstypen &quot;access&quot;als auch &quot;delete&quot;in einer Anfrage ein, falls dies vom Datensubjekt benötigt wird.
4. **Nur erforderliche Produkte einschließen:** Nur Produkte einschließen, die erforderlich oder lizenziert sind. Zusätzliche Produkte können die Verarbeitungszeit verkürzen und die Kosten erhöhen.

## Status von Datenschutzaufträgen überwachen {#monitor-status}

Um Datenschutzaufträge effektiv zu überwachen und ihren Status zu überprüfen, bietet Privacy Service drei Methoden. Die verfügbaren Methoden zur Überwachung von Effizienz und Produktivität sind nachfolgend aufgeführt. Jede Methode enthält Best-Practice-Richtlinien zur Verbesserung Ihres Erlebnisses, gefolgt von einem idealen Szenario-Beispiel, in dem alle Ansätze kombiniert werden.

### Echtzeit-Benachrichtigungen empfangen {#real-time-notifications}

**I/O-Ereignisse** bieten eine nahezu Echtzeit-Statusüberwachung durch Statusereignisse. Dies ist die effizienteste Methode, da sie die Implementierung von Abrufmechanismen und zusätzlichen API-Traffic vermeidet.

**Recommendations:**

- **Webhook-Einrichtung:** Richten Sie Webhooks ein, um Push-Benachrichtigungen zu erhalten, wenn Statusänderungen für gesendete Aufträge auftreten. Dies erleichtert die Echtzeitüberwachung.
- **Benachrichtigungen:** Verwenden Sie Benachrichtigungen sowohl auf Auftrags- als auch auf Produktebene, um den Fortschritt von Anforderungen zu überwachen.

Anweisungen zum Einrichten einer Ereignisregistrierung für Privacy Service-Benachrichtigungen und zum Interpretieren der Benachrichtigungs-Payloads finden Sie in der Dokumentation zu [Abonnieren von Privacy Service-Ereignissen](./privacy-events.md) .

### Abrufen aller Aufträge basierend auf Filtern {#retrieve-filtered-responses-for-all-jobs}

Um alle Daten Ihres Datenschutzauftrags auf der Basis eines angegebenen Filters abzurufen, führt **eine GET-Anfrage an den `/jobs` -Endpunkt** durch. Dieser API-Aufruf ist nützlich, um eine allgemeine Ansicht des aktuellen Auftragsstatus für große Mengen von Auftrags-IDs mit nur einer Anfrage bereitzustellen. Es fehlen keine detaillierten Produktantworten, aber sie können mit dem [`/jobs/{jobID}` -Endpunkt](#retrieve-detailed-responses-for-specific-jobs) gefunden werden.

Eine GET-Anfrage an den `/jobs` -Endpunkt eignet sich am besten zum Erfassen oder Vergleichen der Statusdaten einer großen Menge von Auftrags-IDs, ist jedoch **nicht** für reguläre Abruffaktivitäten vorgesehen.

**Recommendations:**

- **Abfrageparameter:** Verwenden Sie bestimmte Filter, um Ihre Ergebnisse einzuschränken, z. B. Datenbereiche, Regelungstypen und Status (Verarbeitung, Abschluss usw.).

Über die Privacy Service-Benutzeroberfläche können Sie eine Liste aller aktuellen Datenschutzaufträge in Ihrem Unternehmen anzeigen. Informationen zum Filtern der Auftragsanfrageliste finden Sie in der Dokumentation zur Benutzeroberfläche unter [Verwalten von Datenschutzaufträgen](./ui/user-guide.md#job-requests) . Alternativ dazu finden Sie in der Dokumentation zur Verwendung des Endpunkts /job in der Privacy Service-API](./api/privacy-jobs.md).[

Die Dokumentation zur Privacy Service-API enthält Details zu [den verfügbaren Abfrageparametern-Filtern](https://developer.adobe.com/experience-platform-apis/references/privacy-service/#tag/Privacy-jobs/operation/listPrivacyJobs).

### Abrufen detaillierter Antworten für einen einzelnen Auftrag {#retrieve-detailed-responses-for-specific-jobs}

Um detaillierte Antworten für einen einzelnen Auftrag abzurufen, führen **eine GET-Anfrage an den Endpunkt /jobs/{jobID}** durch. Diese Methode ist für eine tiefergehende Informationserfassung wie produktspezifische Antworten und Erfolgsmeldungen vorgesehen. Ein Aufruf an diesen Endpunkt stellt die beste Möglichkeit dar, zu sehen, welche Produkte reagiert haben und welche noch ausstehen. Er ist jedoch für die regelmäßige Abruffaktivität **nicht** vorgesehen.

Weitere Informationen zum [Überprüfen des Status eines bestimmten Auftrags](./api/privacy-jobs.md#check-status) finden Sie in der Dokumentation zum `/jobs/{JOB_ID}` -Endpunkt .

### Ideal-Szenario-Beispiel {#ideal-scenario}

Verwenden Sie einen Webhook, damit das System Datensätze automatisch aktualisieren und Berichte oder Warnhinweise bereitstellen kann, wenn Gruppen der IDs aus einer Anforderung abgeschlossen sind. Wenn Aufträge noch ausstehen, ruft das System diese Auftragsstatus mit einer GET-Anfrage an den Privacy Service-API-Endpunkt `/jobs` ab und stellt eine allgemeine Listenaktualisierung bereit.

Wenn ein bestimmter Auftrag noch aussteht oder einen Fehler zurückgegeben hat, können Sie die detaillierte Antwort mit einer GET-Anfrage an den `/job/{jobId}` -Endpunkt abrufen.

## Auf Anfragedaten zugreifen {#access-request-data}

Wenn Informationen zum Datensubjekt angefordert werden, gibt jeder Dienst Daten in einem Format zurück, das mit der Art und Weise übereinstimmt, in der sie diese Daten speichern und verwenden. Sobald alle Dienste die Anfrage abgeschlossen haben, wird in den Auftragsdetails eine .ZIP-Archivdatei-URL bereitgestellt, damit diese Daten heruntergeladen werden können. Informationen zum Herunterladen von Datenschutzauftragsergebnissen ](https://experienceleague.adobe.com/docs/experience-platform/privacy/troubleshooting-guide.html?lang=en#how-do-i-download-the-results-of-my-completed-privacy-jobs%3F) finden Sie im Handbuch zur Fehlerbehebung .[

Im Folgenden finden Sie wichtige Hinweise zur Verwaltung des Datenarchivs:

- Alle Archivdateien werden nach 30 Tagen von Experience Platform-Servern gelöscht. Kundendaten, die älter als 30 Tage sind, können nicht abgefragt werden.
- Die Struktur der Archivdatei enthält Ordner für jedes in der Anfrage enthaltene Produkt und die darin enthaltenen Datendateien. Archivdateien oder -ordner können leer sein, wenn für die angegebene ID keine Daten gefunden wurden.
- Auf die Daten für zuvor erstellte Aufträge kann erst 30 Tage nach dem Abschlussdatum zugegriffen werden. Danach werden die Daten aus dem System entfernt und es muss eine neue Anfrage gestellt werden.

**Recommendations:**

- **Protect-Datenarchive:** Sowohl die URL- als auch die ZIP-Datei sollten geschützt sein, da sie möglicherweise personenbezogene Daten (PII) für die betroffene Person enthalten.

## Technische Aspekte {#technical-considerations}

Beim Abschließen von Privacy Service-Anforderungen müssen einige technische Aspekte beachtet werden:

- **Datenaufbewahrungszeitraum:** Der maximale Rückblickzeitraum beträgt 60 Tage für jede Auftrags-Gruppe und die maximale Zeitspanne für eine Abfrage beträgt 30 Tage (vom/bis Datum).
- **Gateway timeout:** Achten Sie darauf, dass Ihre Anfrage vom Gateway gelöscht werden kann, wenn sie 60 Sekunden überschreitet.
- **Umgang mit Fehlern:** Überprüfen Sie die Fehlermeldungen gründlich und übermitteln Sie gegebenenfalls Anfragen erneut. Privacy Service verarbeitet Aufträge nach einem Fehler nicht automatisch neu.
- **Grundlegendes zu HTTP 429-Fehlern:** Machen Sie sich mit HTTP 429-Fehlermeldungen und den erforderlichen Schritten zur Problembehebung vertraut. HTTP 429-Fehler sind das Ergebnis von &quot;Zu viele Anfragen&quot;. Weitere Informationen zur Behebung des Problems finden Sie im Abschnitt [Allgemeine Fehlermeldungen](./troubleshooting-guide.md#common-error-messages) des Handbuch zur Fehlerbehebung .

## Nächste Schritte

Durch die Lektüre dieses Dokuments verfügen Sie nun über die erforderlichen Kenntnisse und Verfahren für eine effiziente und wirksame Nutzung des Privacy Service. Als Nächstes finden Sie im [Handbuch zur Fehlerbehebung](./troubleshooting-guide.md) Antworten auf häufig gestellte Fragen zu Privacy Service und Informationen zu häufig aufgetretenen Fehlern in der API.
