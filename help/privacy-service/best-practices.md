---
title: Best Practices für den Privacy Service
description: Erfahren Sie, wie Sie die Verarbeitungszeit und die Kosten reduzieren können, die Ihrem Unternehmen beim Ausfüllen von Datenschutzanfragen entstehen, indem Sie diese optimalen Nutzungsrichtlinien befolgen.
exl-id: 1333d6c6-5ca0-41c1-9f9e-aa2a5a8b8a9c
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '1234'
ht-degree: 0%

---

# Best Practices für den Privacy Service

Verwenden Sie Privacy Service, um die Einhaltung von Datenschutzbestimmungen zu automatisieren, wenn Kunden auf ihre personenbezogenen Daten in Ihren Datenspeichern zugreifen oder diese löschen möchten. Um diesen sich verändernden Geschäftsanforderungen gerecht zu werden, bietet Privacy Service eine RESTful-API und eine Benutzeroberfläche, um in allen Adobe Experience Cloud-Programmen Zugriffs- und Löschanfragen für Kundendaten zu senden.

In diesem Handbuch werden die Best Practices für die effiziente Verarbeitung von Datenschutzanfragen und die Optimierung der Ausführungszeiten bei der Verwaltung von Kundendatenanfragen beschrieben.

## Erste Schritte {#getting-started}

Dieses Handbuch setzt Grundkenntnisse des [Privacy Service ](./home.md) und dessen Verwaltung von Zugriffs- und Löschanfragen von betroffenen Personen (Kunden) in allen Adobe Experience Cloud-Programmen voraus. Es wird außerdem empfohlen, das Handbuch unter [Erstellen einer Datenschutzanfrage in der Benutzeroberfläche“ oder &quot;](./ui/user-guide.md#create-a-new-privacy-job-request)&quot; [API“ ](./api/overview.md) lesen und zu verstehen, wie diese Vorgänge programmgesteuert ausgeführt werden.

## Voraussetzungen {#prerequisites}

Der Zugriff auf den Adobe Experience Platform Privacy Service wird über granulare rollenbasierte Berechtigungen in Adobe Admin Console gesteuert. Sie benötigen die entsprechenden Berechtigungen in einem Produktprofil, um bestimmte Funktionen in der Privacy Service-Benutzeroberfläche und -API verwenden zu können. Wenden Sie sich an Ihren Systemadministrator, wenn Sie zusätzliche Berechtigungen benötigen.

Administratoren können das Handbuch unter [Verwalten von Berechtigungen für Privacy Service ](./permissions.md) für weitere Informationen lesen.

## Richtlinien zur Erstellung von Datenschutzaufträgen {#creation-guidelines}

Um die Verarbeitung Ihrer Anfragen zu optimieren und die Antwortzeiten zu verbessern, sollten Sie beim Erstellen von Datenschutzaufträgen die folgenden Richtlinien beachten. Dies gilt sowohl für die API- als auch für die UI-Methode.

1. **Maximieren Sie die Anzahl der betroffenen Personen pro Anfrage:** Schließen Sie so viele betroffene Personen wie möglich, bis zu 1.000, pro Anfrage ein.
2. **Gruppen-IDs für mehr Effizienz:** Gruppieren Sie in jeder Anfrage mehrere IDs für eine einzelne betroffene Person (bis zu neun). Die **IDs können von verschiedenen Adobe-Services in derselben Anfrage stammen**.
3. **Kombinieren von Zugriffs- und Löschvorgängen** Schließen Sie sowohl Zugriffs- als auch Löschvorgangstypen in eine einzige Anfrage ein, falls die betroffene Person dies benötigt.
4. **Nur erforderliche Produkte einbeziehen:** Nur Produkte einschließen, die erforderlich oder lizenziert sind. Zusätzliche Produkte können die Verarbeitungszeit verlängern und die Kosten erhöhen.

## Überwachen des Status von Datenschutzaufträgen {#monitor-status}

Um Datenschutzaufträge effektiv zu überwachen und ihren Status zu überprüfen, bietet Privacy Service drei Methoden. Die verfügbaren Methoden werden im Folgenden in der Reihenfolge der Überwachung von Effizienz und Produktivität aufgeführt. Jede Methode enthält Richtlinien zu Best Practices, um Ihr Erlebnis zu verbessern, gefolgt von einem idealen Szenario-Beispiel, das alle Ansätze kombiniert.

### Echtzeit-Benachrichtigungen empfangen {#real-time-notifications}

**I/O Events** bieten nahezu in Echtzeit Statusüberwachung über Statusereignisse. Dies ist die effizienteste Methode, da sie die Implementierung von Abrufmechanismen vermeidet und zusätzlichen API-Traffic verursacht.

**Recommendations:**

- **Webhook-Einrichtung:** Richten Sie Webhooks ein, um Push-Benachrichtigungen zu erhalten, wenn Statusänderungen für gesendete Aufträge auftreten. Dies hilft bei der Echtzeitüberwachung.
- **Benachrichtigungen:** Verwenden Sie Benachrichtigungen sowohl auf Auftrags- als auch auf Produktebene, um den Fortschritt der Anfragen zu überwachen.

Privacy Service Anleitungen zum Einrichten einer Ereignisregistrierung für [-Benachrichtigungen und zur Interpretation ](./privacy-events.md) Benachrichtigungs-Payloads finden Sie in der Dokumentation unter Abonnieren von Privacy Service-&quot;.

### Alle Aufträge basierend auf Filtern abrufen {#retrieve-filtered-responses-for-all-jobs}

Um alle Ihre Datenschutzauftragsdaten basierend auf angegebenen Filtern abzurufen, **führen Sie eine GET-Anfrage an den `/jobs`-Endpunkt aus**. Dieser API-Aufruf ist nützlich, um bei einer großen Anzahl von Auftrags-IDs mit nur einer einzigen Anfrage einen Überblick über den aktuellen Auftragsstatus zu erhalten. Es fehlen detaillierte Produktantworten, sie können jedoch mithilfe des [`/jobs/{jobID}`-Endpunkts gefunden werden](#retrieve-detailed-responses-for-specific-jobs).

Eine GET-Anfrage an den `/jobs`-Endpunkt dient am besten zum Erfassen oder Vergleichen der Statusdaten eines großen Satzes von Auftrags-IDs, ist jedoch **nicht** für Aktivitäten vom Typ „Reguläre Abfrage“ vorgesehen.

**Recommendations:**

- **Abfrageparameter:** Verwenden Sie spezifische Filter, um Ihre Ergebnisse einzugrenzen, z. B.: Datenbereiche, Regulierungstypen und Status (Verarbeitung, Abgeschlossen usw.).

Sie können eine Liste aller aktuellen Datenschutzaufträge in Ihrer Organisation über die Privacy Service-Benutzeroberfläche anzeigen. Informationen [ Filtern der Vorgangsanfrageliste finden Sie unter „Verwalten von Datenschutzaufträgen ](./ui/user-guide.md#job-requests) der Benutzeroberfläche“. Alternativ finden Sie weitere Informationen in der Dokumentation [Verwendung des /job-Endpunkts in der Privacy Service-API](./api/privacy-jobs.md).

Die Dokumentation zur Privacy Service-API enthält Details zu [den verfügbaren Abfrageparameterfiltern](https://developer.adobe.com/experience-platform-apis/references/privacy-service/#tag/Privacy-jobs/operation/listPrivacyJobs).

### Abrufen detaillierter Antworten für einen einzelnen Auftrag {#retrieve-detailed-responses-for-specific-jobs}

Um detaillierte Antworten für einen einzelnen Auftrag abzurufen, führen **eine GET-Anfrage an den Endpunkt /jobs/{jobID} durch**. Diese Methode dient zur umfassenderen Erfassung von Informationen, z. B. produktspezifische Antworten und Erfolgsmeldungen. Ein Aufruf dieses Endpunkts ist die beste Möglichkeit, um festzustellen, welche Produkte geantwortet haben und welche noch ausstehen, obwohl dies **nicht** für eine regelmäßige Abfrageaktivität vorgesehen ist.

Weitere Informationen finden Sie in der `/jobs/{JOB_ID}`-Endpunktdokumentation zum [Überprüfen des Status eines bestimmten Auftrags](./api/privacy-jobs.md#check-status).

### Beispiel für ein ideales Szenario {#ideal-scenario}

Verwenden Sie einen Webhook, damit das System automatisch Datensätze aktualisieren und Berichte oder Warnhinweise bereitstellen kann, wenn Gruppen von IDs aus einer Anfrage abgeschlossen sind. Wenn Aufträge noch ausstehen, ruft das System diese Auftragsstatus mit einer GET-Anfrage an den Privacy Service-API-`/jobs`-Endpunkt ab und bietet eine allgemeine Aktualisierung der Liste.

Wenn ein bestimmter Auftrag noch aussteht oder einen Fehler zurückgegeben hat, können Sie die detaillierte Antwort mit einer GET-Anfrage an den `/job/{jobId}`-Endpunkt abrufen.

## Zugriff auf Anfragedaten {#access-request-data}

Wenn Informationen über betroffene Personen angefordert werden, gibt jeder Service Daten in einem Format zurück, das der Art und Weise entspricht, in der sie diese Daten speichern und verwenden. Sobald alle Services die Anfrage abgeschlossen haben, wird in den Auftragsdetails eine ZIP-Archivdatei-URL angegeben, damit diese Daten heruntergeladen werden können. Informationen zum Herunterladen der Ergebnisse des Datenschutzauftrags finden [ im Handbuch zur Fehlerbehebung ](https://experienceleague.adobe.com/docs/experience-platform/privacy/troubleshooting-guide.html?lang=en#how-do-i-download-the-results-of-my-completed-privacy-jobs%3F).

Im Folgenden finden Sie wichtige Hinweise zur Verwaltung des Datenarchivs:

- Alle Archivdateien werden nach 30 Tagen von Experience Platform-Servern gelöscht. Sie können keine Kundendaten abfragen, die älter als 30 Tage sind.
- Die Struktur der Archivdatei enthält Ordner für jedes Produkt, das in der Anfrage enthalten ist, und die darin enthaltenen Datendateien. Archivdateien oder -ordner sind möglicherweise leer, wenn für die angegebene ID keine Daten gefunden wurden.
- Die Daten für zuvor erstellte Aufträge sind nur 30 Tage nach dem Abschlussdatum verfügbar. Danach werden die Daten aus dem System entfernt und es muss eine neue Anfrage gestellt werden.

**Recommendations:**

- **Protect-Datenarchiv:** Sowohl die URL- als auch die ZIP-Datei sollten geschützt werden, da sie personenbezogene Daten (PII) für die betroffene Person enthalten können.

## Technische Überlegungen {#technical-considerations}

Beim Ausfüllen von Privacy Service-Anfragen sind bestimmte technische Aspekte zu beachten:

- **Datenaufbewahrungszeitraum:** Der maximale Lookback-Zeitraum beträgt 60 Tage für jede Gruppe von Aufträgen und die maximale Zeitspanne für eine Abfrage beträgt 30 Tage (vom/bis-Datum).
- **Gateway-Zeitüberschreitung:** Sie sich vor, dass Ihre Anfrage aus dem Gateway gelöscht werden kann, wenn sie 60 Sekunden überschreitet.
- **Fehlerbehandlung:** Prüfen Sie Fehlermeldungen sorgfältig und senden Sie Anfragen ggf. erneut. Privacy Service verarbeitet Aufträge nach einem Fehler nicht automatisch neu.
- **Grundlegendes zu HTTP 429-Fehlern:** Machen Sie sich mit HTTP 429-Fehlermeldungen und den erforderlichen Schritten zur Behebung von Problemen vertraut. HTTP 429-Fehler sind das Ergebnis von „Zu viele Anfragen“. Weitere Informationen [ Beheben des Problems finden ](./troubleshooting-guide.md#common-error-messages) im Abschnitt „Häufige Fehlermeldungen“ des Handbuchs zur Fehlerbehebung .

## Nächste Schritte

Durch die Lektüre dieses Dokuments verfügen Sie nun über die erforderlichen Kenntnisse und Verfahren, um den Privacy Service effizient und effektiv nutzen zu können. Als Nächstes finden Sie [ Handbuch zur Fehlerbehebung ](./troubleshooting-guide.md) Antworten auf häufig gestellte Fragen zu Privacy Services und Informationen zu häufig aufgetretenen Fehlern in der API.
