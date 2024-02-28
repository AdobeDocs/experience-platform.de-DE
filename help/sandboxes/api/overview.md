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

Die [!DNL Sandbox] Die API bietet mehrere Endpunkte, mit denen Sie programmatisch alle Sandboxes verwalten können, die Ihnen in Ihrem Unternehmen zur Verfügung stehen. Diese Endpunkte werden nachfolgend beschrieben. Weitere Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie in den einzelnen Endpunkthandbüchern sowie in den [Ersten Schritten](./getting-started.md).

Um alle verfügbaren Endpunkte und CRUD-Vorgänge anzuzeigen, besuchen Sie die [[!DNL Sandbox] API-Referenz](https://www.adobe.io/experience-platform-apis/references/sandbox).

## Verfügbare Sandboxes

Mit dem verfügbaren Sandbox-Endpunkt können Sie eine Liste aller für den aktuellen Benutzer verfügbaren Sandboxes anzeigen, einschließlich Informationen zu Name, Titel, Status, Typ und Region der einzelnen Sandboxes. Der verfügbare Sandbox-Endpunkt im [!DNL Sandbox] Der Zugriff auf die API ist für alle Benutzer möglich, auch für Benutzer ohne Sandbox Administration-Zugriffsberechtigungen. Siehe [Handbuch zum verfügbaren Sandbox-Endpunkt](./available.md) , um zu erfahren, wie Sie verfügbare Sandboxes in der API anzeigen können.

## Sandbox-Verwaltung

Eine Sandbox ist eine virtuelle Partition innerhalb einer einzigen Instanz von Adobe Experience Platform, die eine nahtlose Integration in den Entwicklungsprozess Ihrer Programme für digitale Erlebnisse ermöglicht. Sie können Produktions- und Entwicklungs-Sandboxes mit dem `/sandboxes` -Endpunkt. Informationen zur Verwendung dieses Endpunkts finden Sie unter [Sandbox-Endpunkthandbuch](./sandboxes.md).

## Sandbox-Typen

Derzeit werden auf dem Experience Platform Produktions- und Entwicklungs-Sandboxes unterstützt. Mit einer standardmäßigen Platform-Lizenz erhalten Sie insgesamt fünf Sandboxes, die Sie als Produktion oder Entwicklung klassifizieren können. Sie können Zusatzpakete von jeweils zehn Sandboxes bis zu einem Maximum von insgesamt 75 Sandboxes hinzufügen. Siehe [Endpunkthandbuch zu Sandbox-Typen](./types.md) , um zu erfahren, wie Sie unterstützte Sandbox-Typen für Ihre Organisation in der API anzeigen können.

## Nächste Schritte

So starten Sie Aufrufe mit dem [!DNL Sandbox] API, lesen Sie die [Erste Schritte](./getting-started.md) Wählen Sie dann eine der Endpunktleitfäden aus, um zu erfahren, wie Sie bestimmte Endpunkte verwenden.
