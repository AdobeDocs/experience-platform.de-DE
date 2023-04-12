---
keywords: Experience Platform; Startseite; beliebte Themen; Sandbox-Entwicklerhandbuch
solution: Experience Platform
title: Erste Schritte mit der Sandbox-API
description: Mit der Sandbox-API können Entwickler Sandboxes in Adobe Experience Platform programmgesteuert verwalten. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
exl-id: 1ae27f30-2f89-4bfa-887d-a5def17b5cbc
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 85%

---

# Erste Schritte mit der Sandbox-API

Sandboxes in Adobe Experience Platform stellen isolierte Entwicklungsumgebungen bereit, mit denen Sie Funktionen testen, Experimente ausführen und benutzerdefinierte Konfigurationen vornehmen können, ohne Ihre Produktionsumgebung zu beeinträchtigen.

In diesem Entwicklerhandbuch finden Sie Anweisungen dazu, wie Sie die Sandbox-API zur Verwaltung von Sandboxes in Experience Platform verwenden können. Außerdem finden Sie Beispiele für API-Aufrufe zur Ausführung verschiedener Vorgänge.

## Voraussetzungen

Um Sandboxes für Ihre Organisation verwalten zu können, benötigen Sie Sandbox-Administratorberechtigungen. Benutzer ohne Zugriffsberechtigungen können nur die [verfügbarer Sandbox-Endpunkt](./available.md) , um aktive Sandboxes für den aktuellen Benutzer aufzulisten. Weiterführende Informationen zum Zuweisen von Sandbox-Berechtigungen für Experience Platform finden Sie unter [Zugriffskontrolle – Übersicht](../../access-control/home.md).

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung in Experience Platform.

### Sammeln von Werten für erforderliche Kopfzeilen

Für diese Anleitung müssen Sie das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abgeschlossen haben, damit Sie Platform-APIs erfolgreich aufrufen können. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Zusätzlich zu den Authentifizierungskopfzeilen benötigen alle Anfragen eine Kopfzeile, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* x-sandbox-name: `{SANDBOX_NAME}`

Für alle Anfragen mit einer Payload (POST, PUT, PATCH) wird eine zusätzliche Kopfzeile benötigt:

* Content-Type: application/json

## Nächste Schritte

Nachdem Sie die erforderlichen Anmeldedaten gesammelt haben, können Sie nun das restliche Entwicklerhandbuch lesen. Jeder Abschnitt enthält wichtige Informationen zu ihren Endpunkten und veranschaulicht Beispiel-API-Aufrufe zur Durchführung von CRUD-Vorgängen. Zu jedem Aufruf gehören das allgemeine API-Format, eine Beispielanfrage mit erforderlichen Kopfzeilen und ordnungsgemäß formatierten Payloads sowie eine Beispielantwort eines erfolgreichen Aufrufs.
