---
keywords: Experience Platform; Startseite; beliebte Themen; Sandbox-Entwicklerhandbuch
solution: Experience Platform
title: Sandbox-API-Anleitung
topic-legacy: developer guide
description: Sandboxes in Adobe Experience Platform stellen isolierte Entwicklungsumgebungen bereit, mit denen Sie Funktionen testen, Experimente ausführen und benutzerdefinierte Konfigurationen vornehmen können, ohne Ihre Produktionsumgebung zu beeinträchtigen.
source-git-commit: f5ce7b7f09c624c53065757bb8a9b09f989dce0a
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 26%

---

# [!DNL Sandbox]-API-Handbuch

Die [!DNL Sandbox]-API bietet mehrere Endpunkte, mit denen Sie alle Sandboxes, die Ihnen in Ihrer IMS-Organisation zur Verfügung stehen, programmgesteuert verwalten können. Diese Endpunkte werden nachfolgend beschrieben. Weitere Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie in den einzelnen Endpunkthandbüchern sowie in den [Ersten Schritten](./getting-started.md).

Um alle verfügbaren Endpunkte und CRUD-Vorgänge anzuzeigen, besuchen Sie die [[!DNL Sandbox] API-Referenz](https://www.adobe.io/experience-platform-apis/references/sandbox).

## Verfügbare Sandboxes

Mit dem verfügbaren Sandbox-Endpunkt können Sie eine Liste aller für den aktuellen Benutzer verfügbaren Sandboxes anzeigen, einschließlich Informationen zu Name, Titel, Status, Typ und Region der einzelnen Sandboxes. Der verfügbare Sandbox-Endpunkt in der API [!DNL Sandbox] kann von allen Benutzern aufgerufen werden, auch von solchen ohne Sandbox Administration-Zugriffsberechtigungen. Informationen zum Anzeigen der verfügbaren Sandboxes in der API finden Sie im [verfügbaren Sandbox-Endpunkthandbuch](./available.md) .

## Sandbox-Verwaltung

Eine Sandbox ist eine virtuelle Partition innerhalb einer einzigen Instanz von Adobe Experience Platform, die eine nahtlose Integration in den Entwicklungsprozess Ihrer Programme für digitale Erlebnisse ermöglicht. Mit dem Endpunkt `/sandboxes` können Sie Produktions- und Entwicklungs-Sandboxes erstellen, anzeigen, bearbeiten, zurücksetzen und löschen. Informationen zur Verwendung dieses Endpunkts finden Sie im [Sandboxes-Endpunkthandbuch](./sandboxes.md).

## Sandbox-Typen

Derzeit werden in Experience Platform Produktions- und Entwicklungs-Sandboxes unterstützt. Mit einer standardmäßigen Platform-Lizenz erhalten Sie insgesamt fünf Sandboxes, die Sie als Produktion oder Entwicklung klassifizieren können. Sie können weitere Packs mit 10 Sandboxes bis zu insgesamt maximal 75 Sandboxes lizenzieren. Informationen zum Anzeigen unterstützter Sandbox-Typen für Ihre Organisation in der API finden Sie im Endpunkthandbuch [Sandbox-Typen](./types.md) .

## Nächste Schritte

Um mit Aufrufen mit der [!DNL Sandbox]-API zu beginnen, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) und wählen Sie dann eins der Endpunkthandbücher aus, um zu erfahren, wie bestimmte Endpunkte verwendet werden.