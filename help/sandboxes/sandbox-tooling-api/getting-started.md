---
title: Erste Schritte mit der Sandbox Tooling API
description: Verwenden Sie die Sandbox-Tool-API, um Artefakte zu untersuchen und einen Schnappschuss von Sandbox-Konfigurationen zwischen Sandboxes zu exportieren und zu importieren. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
source-git-commit: bad6ad17a5f41e50b27ce44a6d52a79e2066c82f
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 70%

---

# Erste Schritte mit der Sandbox-Tool-API {#getting-started}

Dieses Entwicklerhandbuch enthält Schritte, die Sie bei der Verwendung der Sandbox-Tool-API zur Verwaltung von Paketen und Tools in Adobe Experience Platform unterstützen, sowie Beispiel-API-Aufrufe zur Durchführung verschiedener Vorgänge.

## Lesen von Beispiel-API-Aufrufen {#api-calls}

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Beispiel-JSON-Daten, die an die API-Antwort zurückgegeben werden, werden ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](/help/landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung in Experience Platform.

## Sammeln von Werten für erforderliche Kopfzeilen {#headers}

Für diese Anleitung müssen Sie das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abgeschlossen haben, damit Sie Platform-APIs erfolgreich aufrufen können. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Zusätzlich zu den Authentifizierungskopfzeilen benötigen alle Anfragen eine Kopfzeile, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* `x-sandbox-name: {SANDBOX_NAME}`

Für alle Anfragen mit einer Payload (POST, PUT, PATCH) wird eine zusätzliche Kopfzeile benötigt:

* `Content-Type: application/json`

## Nächste Schritte {#next-steps}

Nachdem Sie die erforderlichen Anmeldedaten gesammelt haben, können Sie nun das restliche Entwicklerhandbuch lesen. Jeder Abschnitt enthält wichtige Informationen zu ihren Endpunkten und veranschaulicht Beispiel-API-Aufrufe zur Durchführung von CRUD-Vorgängen. Zu jedem Aufruf gehören das allgemeine API-Format, eine Beispielanfrage mit erforderlichen Kopfzeilen und ordnungsgemäß formatierten Payloads sowie eine Beispielantwort eines erfolgreichen Aufrufs.

In den folgenden API-Tutorials erfahren Sie, wie Sie Aufrufe an die Sandbox-Tool-API starten:

* [Pakete-Endpunkt](./packages.md)
* [Tools-Endpunkt](./tools.md)
