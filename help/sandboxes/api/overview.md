---
keywords: Experience Platform;home;popular topics;sandbox developer guide
solution: Experience Platform
title: Sandbox-API-Anleitung
description: Sandboxes in Adobe Experience Platform stellen isolierte Entwicklungsumgebungen bereit, mit denen Sie Funktionen testen, Experimente ausführen und benutzerdefinierte Konfigurationen vornehmen können, ohne Ihre Produktionsumgebung zu beeinträchtigen.
role: Developer
exl-id: c77e96dc-d138-4126-bbb0-b67beb0a02d6
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 24%

---

# [!DNL Sandbox]-API-Handbuch

Die [!DNL Sandbox] -API bietet mehrere Endpunkte, mit denen Sie alle Sandboxes, die Ihnen in Ihrem Unternehmen zur Verfügung stehen, programmgesteuert verwalten können. Diese Endpunkte werden nachfolgend beschrieben. Weitere Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie in den einzelnen Endpunkthandbüchern sowie in den [Ersten Schritten](./getting-started.md).

Um alle verfügbaren Endpunkte und CRUD-Vorgänge anzuzeigen, besuchen Sie die [[!DNL Sandbox] API-Referenz](https://www.adobe.io/experience-platform-apis/references/sandbox).

## Verfügbare Sandboxes

Mit dem verfügbaren Sandbox-Endpunkt können Sie eine Liste aller für den aktuellen Benutzer verfügbaren Sandboxes anzeigen, einschließlich Informationen zu Name, Titel, Status, Typ und Region der einzelnen Sandboxes. Auf den verfügbaren Sandbox-Endpunkt in der [!DNL Sandbox]-API können alle Benutzer zugreifen, auch solche ohne Sandbox-Administrationszugriffsberechtigungen. Informationen zum Anzeigen verfügbarer Sandboxes in der API finden Sie im [verfügbaren Sandbox-Endpunkthandbuch](./available.md) .

## Sandbox-Verwaltung

Eine Sandbox ist eine virtuelle Partition innerhalb einer einzigen Instanz von Adobe Experience Platform, die eine nahtlose Integration in den Entwicklungsprozess Ihrer Programme für digitale Erlebnisse ermöglicht. Sie können Produktions- und Entwicklungs-Sandboxes mit dem `/sandboxes` -Endpunkt erstellen, anzeigen, bearbeiten, zurücksetzen und löschen. Informationen zur Verwendung dieses Endpunkts finden Sie im [Sandboxes-Endpunkthandbuch](./sandboxes.md).

## Sandbox-Typen

Derzeit werden auf dem Experience Platform Produktions- und Entwicklungs-Sandboxes unterstützt. Mit einer standardmäßigen Platform-Lizenz erhalten Sie insgesamt fünf Sandboxes, die Sie als Produktion oder Entwicklung klassifizieren können. Sie können Zusatzpakete von jeweils zehn Sandboxes bis zu einem Maximum von insgesamt 75 Sandboxes hinzufügen. Informationen zum Anzeigen unterstützter Sandbox-Typen für Ihre Organisation in der API finden Sie im [Endpunkthandbuch zu Sandbox-Typen](./types.md) .

## Nächste Schritte

Um Aufrufe mit der API [!DNL Sandbox] durchzuführen, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) und wählen Sie dann eine der Endpunkthandbücher aus, um zu erfahren, wie Sie bestimmte Endpunkte verwenden.
