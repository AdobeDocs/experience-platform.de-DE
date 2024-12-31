---
keywords: Experience Platform;Startseite;beliebte Themen;Sandbox-Entwicklerhandbuch
solution: Experience Platform
title: Sandbox-API-Handbuch
description: Sandboxes in Adobe Experience Platform stellen isolierte Entwicklungsumgebungen bereit, mit denen Sie Funktionen testen, Experimente ausführen und benutzerdefinierte Konfigurationen vornehmen können, ohne Ihre Produktionsumgebung zu beeinträchtigen.
role: Developer
exl-id: c77e96dc-d138-4126-bbb0-b67beb0a02d6
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 24%

---

# [!DNL Sandbox]-API-Handbuch

Die [!DNL Sandbox]-API bietet mehrere Endpunkte, mit denen Sie alle Sandboxes, die Ihnen in Ihrer Organisation zur Verfügung stehen, programmgesteuert verwalten können. Diese Endpunkte werden nachfolgend beschrieben. Weitere Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie in den einzelnen Endpunkthandbüchern sowie in den [Ersten Schritten](./getting-started.md).

Um alle verfügbaren Endpunkte und CRUD-Vorgänge anzuzeigen, besuchen Sie die [[!DNL Sandbox] API-Referenz](https://www.adobe.io/experience-platform-apis/references/sandbox).

## Verfügbare Sandboxes

Mit dem Endpunkt Verfügbare Sandboxes können Sie eine Liste aller für den aktuellen Benutzer verfügbaren Sandboxes anzeigen, einschließlich Informationen über Namen, Titel, Status, Typ und Region jeder Sandbox. Auf den verfügbaren Sandbox-Endpunkt in der [!DNL Sandbox]-API können alle Benutzer zugreifen, auch diejenigen ohne Zugriffsberechtigungen für die Sandbox-Administration. Informationen [ Anzeigen verfügbarer Sandboxes in der API finden ](./available.md) im Handbuch zum verfügbaren Sandbox-Endpunkt .

## Sandbox-Verwaltung

Eine Sandbox ist eine virtuelle Partition innerhalb einer einzigen Instanz von Adobe Experience Platform, die eine nahtlose Integration in den Entwicklungsprozess Ihrer Programme für digitale Erlebnisse ermöglicht. Mit dem Endpunkt `/sandboxes` können Sie Produktions- und Entwicklungs-Sandboxes erstellen, anzeigen, bearbeiten, zurücksetzen und löschen. Informationen zur Verwendung dieses Endpunkts finden Sie im [Sandbox-Endpunkthandbuch](./sandboxes.md).

## Sandbox-Typen

Derzeit werden Produktions- und Entwicklungs-Sandboxes als Sandbox-Typen auf Experience Platform unterstützt. Mit einer Standardlizenz für Platform erhalten Sie insgesamt fünf Sandboxes, die Sie als Produktion oder Entwicklung klassifizieren können. Sie können Zusatzpakete von jeweils zehn Sandboxes bis zu einem Maximum von insgesamt 75 Sandboxes hinzufügen. Informationen [ Anzeigen unterstützter Sandbox-Typen für Ihre Organisation in der API finden ](./types.md) im Handbuch zum Sandbox--Typ .

## Nächste Schritte

Um mit Aufrufen mit der [!DNL Sandbox]-API zu beginnen, lesen Sie [Erste Schritte](./getting-started.md) und wählen Sie dann eines der Endpunkthandbücher aus, um zu erfahren, wie bestimmte Endpunkte verwendet werden.
