---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handbuch für Sandbox-API-Entwickler
topic: developer guide
translation-type: tm+mt
source-git-commit: b4741cdfd065bbaed7f2feeafe8619191e4b8f6c
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---


# Handbuch für Sandbox-API-Entwickler

Sandboxen in Adobe Experience Platform bieten isolierte Umgebung zur Entwicklung, mit denen Sie Funktionen testen, Experimente ausführen und benutzerdefinierte Konfigurationen vornehmen können, ohne die Umgebung Ihrer Produktion zu beeinträchtigen.

In diesem Entwicklerhandbuch finden Sie Anweisungen, wie Sie Sandbox-API zur Verwaltung von Sandboxen in Experience Platform verwenden können. Außerdem finden Sie Beispiele für API-Aufrufe zur Durchführung verschiedener Vorgänge.

## Erste Schritte mit der Sandbox-API

Zum Verwalten von Sandboxen für Ihre IMS-Organisation benötigen Sie Sandbox-Administratorrechte. Benutzer ohne Zugriffsberechtigungen können den Endpunkt nur für die [Auflistung aktiver Sandboxen für den aktuellen Benutzer](./list-active-sandboxes.md)verwenden. Weitere Informationen zum Zuweisen von Sandbox-Berechtigungen für Experience Platform finden Sie im Überblick über die [Zugriffskontrolle](../../access-control/home.md) .

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt [zum Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Werte für erforderliche Kopfzeilen sammeln

Für dieses Handbuch müssen Sie das [Authentifizierungstraining](../../tutorials/authentication.md) abgeschlossen haben, um Platform-APIs erfolgreich aufrufen zu können. Das Abschließen des Authentifizierungstreutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

* Genehmigung: Träger `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Zusätzlich zu den Authentifizierungs-Headern benötigen alle Anforderungen einen Header, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

* x-sandbox-name: `{SANDBOX_NAME}`

Für alle Anforderungen mit einer Payload (POST, PUT und PATCH) ist ein zusätzlicher Header erforderlich:

* Content-Type: application/json

## Nächste Schritte

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie jetzt den Rest des Entwicklerhandbuchs lesen. Jeder Abschnitt enthält wichtige Informationen zu ihren Endpunkten und zeigt Beispiel-API-Aufrufe für CRUD-Vorgänge. Zu jedem Aufruf gehören das allgemeine **API-Format**, eine **Musteranforderung** mit erforderlichen Kopfzeilen und ordnungsgemäß formatierten Nutzdaten sowie eine Beispielantwort **** für einen erfolgreichen Aufruf.