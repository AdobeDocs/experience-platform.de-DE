---
title: Best Practices für Privacy Service
description: Erfahren Sie, wie Sie die Verarbeitungszeit und die Kosten reduzieren, die Ihrem Unternehmen beim Ausführen von Datenschutzanfragen entstehen, indem Sie diese optimalen Nutzungsrichtlinien befolgen.
source-git-commit: c6507a39ba5ae5ca6aa2bf02cf8844a4592152ac
workflow-type: tm+mt
source-wordcount: '1234'
ht-degree: 0%

---

# Best Practices für Privacy Service

Verwenden Sie Privacy Service, um die Einhaltung von Datenschutzbestimmungen zu automatisieren, wenn Kunden auf ihre personenbezogenen Daten in Ihren Datenspeichern zugreifen oder diese löschen möchten. Um diese sich wandelnden geschäftlichen Anforderungen zu erfüllen, bietet Privacy Service eine RESTful-API und -Benutzeroberfläche, mit der Zugriffs- und Löschanfragen für Kundendaten in Adobe Experience Cloud-Anwendungen eingereicht werden können.

In diesem Handbuch werden Best Practices für die effiziente Verarbeitung von Datenschutzanfragen und die Optimierung der Reaktionszeiten bei der Verwaltung von Kundendatenanfragen beschrieben.

## Erste Schritte {#getting-started}

Dieses Handbuch setzt ein Verständnis der [Privacy Service](./home.md) und wie Sie damit Zugriffs- und Löschanfragen Ihrer Datensubjekte (Kunden) in allen Adobe Experience Cloud-Anwendungen verwalten können. Es wird auch empfohlen, das Handbuch zu lesen unter [Erstellen einer Datenschutzanfrage in der Benutzeroberfläche](./ui/user-guide.md#create-a-new-privacy-job-request) oder [die API](./api/overview.md)und verstehen, wie diese Vorgänge programmatisch ausgeführt werden.

## Voraussetzungen {#prerequisites}

Der Zugriff auf Adobe Experience Platform Privacy Service wird über granulare rollenbasierte Berechtigungen in Adobe Admin Console gesteuert. Sie benötigen die entsprechenden Berechtigungen in einem Produktprofil, um bestimmte Funktionen in der Privacy Service-Benutzeroberfläche und -API verwenden zu können. Wenden Sie sich an Ihren Systemadministrator, wenn Sie zusätzliche Berechtigungen benötigen.

Administratoren können das Handbuch unter [Berechtigungen für Privacy Service verwalten](./permissions.md) für weitere Informationen.

## Richtlinien zur Erstellung von Datenschutzaufträgen {#creation-guidelines}

Um die Anforderungsverarbeitung zu optimieren und die Antwortzeiten zu verbessern, beachten Sie beim Erstellen von Datenschutzaufträgen die folgenden Richtlinien. Dies gilt sowohl für die API- als auch für die UI-Methoden.

1. **Maximieren Sie die Datensubjekte pro Anforderung:** Binden Sie so viele Datensubjekte wie möglich ein, bis zu 1000 pro Anforderung.
2. **Gruppen-IDs für Effizienz:** Gruppieren Sie in jeder Anfrage mehrere IDs für ein einzelnes Datensubjekt (bis zu neun). Die **IDs können aus verschiedenen Adobe-Diensten in derselben Anfrage stammen**.
3. **Zugriff- und Löschvorgänge kombinieren:** Schließen Sie sowohl die Auftragstypen &quot;access&quot;als auch &quot;delete&quot;in eine Anfrage ein, falls dies vom Datensubjekt benötigt wird.
4. **Nur erforderliche Produkte einschließen:** Schließen Sie nur Produkte ein, die erforderlich oder lizenziert sind. Zusätzliche Produkte können die Verarbeitungszeit verkürzen und die Kosten erhöhen.

## Status von Datenschutzaufträgen überwachen {#monitor-status}

Um Datenschutzaufträge effektiv zu überwachen und ihren Status zu überprüfen, bietet Privacy Service drei Methoden. Die verfügbaren Methoden zur Überwachung von Effizienz und Produktivität sind nachfolgend aufgeführt. Jede Methode enthält Best-Practice-Richtlinien zur Verbesserung Ihres Erlebnisses, gefolgt von einem idealen Szenario-Beispiel, in dem alle Ansätze kombiniert werden.

### Echtzeit-Benachrichtigungen empfangen {#real-time-notifications}

**E/A-Ereignisse** bieten nahezu Echtzeit-Statusüberwachung durch Statusereignisse. Dies ist die effizienteste Methode, da sie die Implementierung von Abrufmechanismen und zusätzlichen API-Traffic vermeidet.

**Recommendations:**

- **Webhook-Einrichtung:** Richten Sie Webhooks ein, um Push-Benachrichtigungen zu erhalten, wenn sich der Status für gesendete Aufträge ändert. Dies erleichtert die Echtzeitüberwachung.
- **Benachrichtigungen:** Verwenden Sie Benachrichtigungen auf Auftrags- und Produktebene, um den Fortschritt von Anforderungen zu überwachen.

Siehe die Dokumentation unter [Abonnieren von Privacy Service-Ereignissen](./privacy-events.md) für Anweisungen zum Einrichten einer Ereignisregistrierung für Privacy Service-Benachrichtigungen und zum Interpretieren der Benachrichtigungs-Payloads.

### Abrufen aller Aufträge basierend auf Filtern {#retrieve-filtered-responses-for-all-jobs}

So rufen Sie alle Daten Ihres Datenschutzauftrags basierend auf angegebenen Filtern ab: **eine GET-Anfrage an die `/jobs` Endpunkt**. Dieser API-Aufruf ist nützlich, um eine allgemeine Ansicht des aktuellen Auftragsstatus für große Mengen von Auftrags-IDs mit nur einer Anfrage bereitzustellen. Es fehlen keine detaillierten Produktantworten, aber sie können mithilfe der [`/jobs/{jobID}` Endpunkt](#retrieve-detailed-responses-for-specific-jobs).

Eine GET-Anfrage an die `/jobs` Endpunkt eignet sich am besten zum Erfassen oder Vergleichen der Statusdaten eines großen Satzes von Auftrags-IDs, ist aber **not** für regelmäßige Abruffriken bestimmt.

**Recommendations:**

- **Abfrageparameter:** Verwenden Sie bestimmte Filter, um Ihre Ergebnisse einzuschränken, z. B. Datenbereiche, Regulierungstypen und Status (Verarbeitung, Abschluss usw.).

Über die Privacy Service-Benutzeroberfläche können Sie eine Liste aller aktuellen Datenschutzaufträge in Ihrem Unternehmen anzeigen. Siehe [Verwalten von Datenschutzaufträgen in der UI-Dokumentation](./ui/user-guide.md#job-requests) für Informationen zum Filtern der Auftragsanforderungsliste. Die Dokumentation finden Sie auch in der [Verwendung des Endpunkts /job in der Privacy Service-API](./api/privacy-jobs.md).

Die Dokumentation zur Privacy Service-API enthält Details zu [die verfügbaren Abfrageparameter-Filter](https://developer.adobe.com/experience-platform-apis/references/privacy-service/#tag/Privacy-jobs/operation/listPrivacyJobs).

### Abrufen detaillierter Antworten für einen einzelnen Auftrag {#retrieve-detailed-responses-for-specific-jobs}

So rufen Sie detaillierte Antworten für einen einzelnen Auftrag ab: **eine GET-Anfrage an die /jobs/ ausführen{jobID} Endpunkt**. Diese Methode ist für eine tiefergehende Informationserfassung wie produktspezifische Antworten und Erfolgsmeldungen vorgesehen. Ein Aufruf an diesen Endpunkt ist der beste Weg, um zu sehen, welche Produkte reagiert haben und welche noch ausstehen. **not** für die regelmäßige Abruffunktion bestimmt.

Siehe `/jobs/{JOB_ID}` Endpunktdokumentation für Details zu [Überprüfen des Status eines bestimmten Auftrags](./api/privacy-jobs.md#check-status).

### Ideal-Szenario-Beispiel {#ideal-scenario}

Verwenden Sie einen Webhook, damit das System Datensätze automatisch aktualisieren und Berichte oder Warnhinweise bereitstellen kann, wenn Gruppen der IDs aus einer Anforderung abgeschlossen sind. Wenn Aufträge noch nicht abgeschlossen sind, ruft das System diese Auftragsstatus mit einer GET-Anfrage an die Privacy Service-API ab `/jobs` -Endpunkt und bietet eine allgemeine Aktualisierung der Liste.

Wenn ein bestimmter Auftrag noch aussteht oder einen Fehler zurückgegeben hat, können Sie die detaillierte Antwort mit einer GET-Anfrage an die `/job/{jobId}` -Endpunkt.

## Auf Anfragedaten zugreifen {#access-request-data}

Wenn Informationen zum Datensubjekt angefordert werden, gibt jeder Dienst Daten in einem Format zurück, das mit der Art und Weise übereinstimmt, in der sie diese Daten speichern und verwenden. Sobald alle Dienste die Anfrage abgeschlossen haben, wird in den Auftragsdetails eine .ZIP-Archivdatei-URL bereitgestellt, damit diese Daten heruntergeladen werden können. Informationen zu [Herunterladen von Ergebnissen von Datenschutzaufträgen](https://experienceleague.adobe.com/docs/experience-platform/privacy/troubleshooting-guide.html?lang=en#how-do-i-download-the-results-of-my-completed-privacy-jobs%3F).

Im Folgenden finden Sie wichtige Hinweise zur Verwaltung des Datenarchivs:

- Alle Archivdateien werden nach 30 Tagen von Experience Platform-Servern gelöscht. Kundendaten, die älter als 30 Tage sind, können nicht abgefragt werden.
- Die Struktur der Archivdatei enthält Ordner für jedes in der Anfrage enthaltene Produkt und die darin enthaltenen Datendateien. Archivdateien oder -ordner können leer sein, wenn für die angegebene ID keine Daten gefunden wurden.
- Auf die Daten für zuvor erstellte Aufträge kann erst 30 Tage nach dem Abschlussdatum zugegriffen werden. Danach werden die Daten aus dem System entfernt und es muss eine neue Anfrage gestellt werden.

**Recommendations:**

- **Protect-Datenarchive:** Sowohl die URL- als auch die ZIP-Datei sollten geschützt werden, da sie personenbezogene Daten (PII) für die betroffene Person enthalten können.

## Technische Aspekte {#technical-considerations}

Beim Abschließen von Privacy Service-Anforderungen müssen einige technische Aspekte beachtet werden:

- **Datenaufbewahrungszeitraum:** Der maximale Rückblickzeitraum beträgt 60 Tage für jede Vorgangsgruppe und die maximale Zeitspanne für eine Abfrage beträgt 30 Tage (vom/bis Datum).
- **Gateway-Zeitüberschreitung:** Achten Sie darauf, dass Ihre Anfrage vom Gateway gelöscht werden kann, wenn sie 60 Sekunden überschreitet.
- **Fehlerbehandlung:** Überprüfen Sie die Fehlermeldungen gründlich und reichen Sie ggf. Anforderungen erneut ein. Privacy Service verarbeitet Aufträge nach einem Fehler nicht automatisch neu.
- **HTTP 429-Fehler verstehen:** Machen Sie sich mit HTTP 429-Fehlermeldungen und den erforderlichen Schritten zur Problembehebung vertraut. HTTP 429-Fehler sind das Ergebnis von &quot;Zu viele Anfragen&quot;. Siehe [Allgemeine Fehlermeldungen](./troubleshooting-guide.md#common-error-messages) im Handbuch zur Fehlerbehebung finden Sie weitere Informationen zur Behebung des Problems.

## Nächste Schritte

Durch die Lektüre dieses Dokuments verfügen Sie nun über die erforderlichen Kenntnisse und Verfahren für eine effiziente und wirksame Nutzung des Privacy Service. Lesen Sie als Nächstes den Abschnitt [Handbuch zur Fehlerbehebung](./troubleshooting-guide.md) für Antworten auf häufig gestellte Fragen zu Privacy Service und Informationen zu häufig aufgetretenen Fehlern in der API.
