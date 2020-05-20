---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Entwicklerhandbuch für Zugriffskontrollen
topic: developer guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 1%

---


# Entwicklerhandbuch für Zugriffskontrollen

Access control for Experience Platform is administered through the [Adobe Admin Console](https://adminconsole.adobe.com). Diese Funktion nutzt die Profil der Produkte in der Admin-Konsole, die Benutzer mit Berechtigungen und Sandboxen verknüpfen. See the [access control overview](../home.md) for more information.

Dieses Entwicklerhandbuch enthält Informationen zum Formatieren Ihrer Anforderungen an die [Zugriffskontrollen-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml)und behandelt die folgenden Vorgänge:

- [Berechtigungsnamen und Ressourcentypen der Liste](./permissions-and-resource-types.md)
- [Ansicht effektiver Richtlinien für den aktuellen Benutzer](./effective-policies.md)

## Erste Schritte

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die Schema Registry API erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Werte für erforderliche Kopfzeilen sammeln

Um Aufrufe an Plattform-APIs durchzuführen, müssen Sie zunächst das [Authentifizierungstraining](../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungstreutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

- Genehmigung: Träger `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in Experience Platform werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Plattform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Weitere Informationen zu Sandboxes in Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Für alle Anforderungen mit einer Payload (POST, PUT, PATCH) ist ein zusätzlicher Header erforderlich:

- Content-Type: application/json

## Nächste Schritte

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie jetzt den Rest des Entwicklerhandbuchs lesen. Jeder Abschnitt enthält wichtige Informationen zu ihren Endpunkten und zeigt Beispiel-API-Aufrufe für CRUD-Vorgänge. Zu jedem Aufruf gehören das allgemeine **API-Format**, eine **Musteranforderung** mit erforderlichen Kopfzeilen und ordnungsgemäß formatierten Nutzdaten sowie eine Beispielantwort **** für einen erfolgreichen Aufruf.