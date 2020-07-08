---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Entwicklerhandbuch für Abfrage Service
topic: query templates
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 1%

---


# Entwicklerhandbuch für Abfrage Service

Dieses Entwicklerhandbuch enthält Anweisungen zum Ausführen verschiedener Vorgänge in der Adobe Experience Platform Abfrage Service API.

## Erste Schritte

Dieser Leitfaden erfordert ein Verständnis der verschiedenen Adobe Experience Platformen, die mit der Verwendung des Abfrage-Dienstes verbunden sind.

- [Abfrage-Dienst](../home.md): Ermöglicht die Abfrage von Datensätzen und die Erfassung der resultierenden Abfragen als neue Datensätze in der Experience Platform.
- [Erlebnis-Datenmodell (XDM)-System](../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
- [Sandboxen](../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxen, die eine Instanz einer Platform in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um den Abfrage Service mit der API erfolgreich nutzen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in dieser Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt [zum Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung bei Experience Platformen.

### Werte für erforderliche Kopfzeilen sammeln

Um Experience Platformen-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungslehrgang](../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungtutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Platform API-Aufrufen bereit, wie unten dargestellt:

- Genehmigung: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in der Experience Platform werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Platform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zum Arbeiten mit Sandboxen in der Experience Platform finden Sie in der Übersicht über [Sandboxen](../../sandboxes/home.md).

## Beispiel-API-Aufrufe

Nachdem Sie wissen, welche Header verwendet werden sollen, können Sie mit dem Aufrufen der Abfrage Service API beginnen. In den folgenden Dokumenten werden die verschiedenen API-Aufrufe erläutert, die Sie mit der Abfrage Service API durchführen können. Zu jedem Beispielaufruf gehören das allgemeine API-Format, eine Beispielanforderung mit den erforderlichen Kopfzeilen und eine Beispielantwort.

- [Abfragen](queries.md)
- [Verbindungsparameter](connection-parameters.md)
- [Geplante Abfragen](scheduled-queries.md)
- [Wird für geplante Abfragen ausgeführt](runs-scheduled-queries.md)
- [Abfrage-Vorlagen](query-templates.md)

## Nächste Schritte

Nachdem Sie mit der API für den Abfrage-Dienst Aufrufe durchgeführt haben, können Sie Ihre eigenen nicht interaktiven Abfragen erstellen. Weitere Informationen zum Erstellen von Abfragen finden Sie im [SQL-Referenzhandbuch](../sql/overview.md).