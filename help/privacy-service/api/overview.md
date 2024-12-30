---
title: Privacy Service-API-Handbuch
description: Erfahren Sie, wie Sie mit der Privacy Service-API Datenschutzaufträge für unterstützte Adobe Experience Cloud-Programme programmgesteuert verwalten können.
role: Developer
exl-id: 665466ac-2447-4a9d-a8cf-62092c09e431
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 15%

---

# [!DNL Privacy Service]-API-Handbuch

Die Privacy Service-API bietet mehrere Endpunkte, mit denen Sie Datenschutzaufträge für Ihr Unternehmen programmgesteuert verwalten können. Diese Endpunkte werden nachfolgend beschrieben. Weitere Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie in den einzelnen Endpunkthandbüchern sowie in den [Ersten Schritten](./getting-started.md).

>[!NOTE]
>
>In diesem Handbuch wird die Verwendung der [!DNL Privacy Service]-API beschrieben. Weitere Informationen zur Verwendung der Benutzeroberfläche finden Sie in der Übersicht über die Privacy Service-Benutzeroberfläche von [](../ui/overview.md).

Um alle verfügbaren Endpunkte und CRUD-Vorgänge anzuzeigen, besuchen Sie die [Privacy Service-API-Referenz](https://www.adobe.io/experience-platform-apis/references/privacy-service/).

## Datenschutzaufträge

Wenn der Privacy Service eine Anfrage zum Zugriff auf oder zur Löschung der personenbezogenen Daten einer betroffenen Person erhält, erstellt das System Datenschutzaufträge, um diese Anfrage zu erfüllen. Jeder Datenschutzauftrag enthält Identitätsinformationen zur betroffenen Person, Metadaten zum Adobe Experience Cloud-Produkt, für das der Auftrag gilt, und den Verarbeitungsstatus des Auftrags.

Mit dem `/jobs`-Endpunkt können Sie Datenschutzaufträge für Ihre Organisation erstellen und abrufen. Informationen zur Verwendung dieses Endpunkts finden Sie im [Handbuch zu Datenschutzvorgängen](./privacy-jobs.md).

## Einverständnis

Bestimmte Vorschriften erfordern die ausdrückliche Zustimmung des Kunden, bevor seine personenbezogenen Daten erfasst werden können. Mit dem `/consent`-Endpunkt können Sie Einverständnisanfragen von Kunden verarbeiten und in Ihren Datenschutz-Workflow integrieren. Weitere Informationen finden [ im ](./consent.md) zum Einverständnisendpunkt .

## Nächste Schritte

Um mit Aufrufen mit der Privacy Service-API zu beginnen, lesen Sie [Erste Schritte](./getting-started.md) und wählen Sie dann eines der Endpunkthandbücher aus, um zu erfahren, wie bestimmte Endpunkte verwendet werden.
