---
title: Handbuch zur Privacy Service-API
description: Erfahren Sie, wie Sie mit der Privacy Service-API Datenschutzaufträge für unterstützte Adobe Experience Cloud-Anwendungen programmgesteuert verwalten können.
exl-id: 665466ac-2447-4a9d-a8cf-62092c09e431
source-git-commit: bda8d0ee1db4b58b4b856a23a8790cd7f76c0656
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 21%

---

# [!DNL Privacy Service]-API-Handbuch

Die Privacy Service-API bietet mehrere Endpunkte, mit denen Sie Datenschutzaufträge für Ihr Unternehmen programmgesteuert verwalten können. Diese Endpunkte werden nachfolgend beschrieben. Weitere Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie in den einzelnen Endpunkthandbüchern sowie in den [Ersten Schritten](./getting-started.md).

>[!NOTE]
>
>In diesem Handbuch wird die Verwendung der [!DNL Privacy Service] API. Weitere Informationen zur Verwendung der Benutzeroberfläche finden Sie in der [Übersicht über die Privacy Service-Benutzeroberfläche](../ui/overview.md).

Um alle verfügbaren Endpunkte und CRUD-Vorgänge anzuzeigen, besuchen Sie die [Privacy Service-API-Referenz](https://www.adobe.io/experience-platform-apis/references/privacy-service/).

## Datenschutzaufträge

Wenn Privacy Service eine Anfrage zum Zugriff auf oder Löschen der personenbezogenen Daten eines Betreffs erhalten, erstellt das System Datenschutzaufträge, um diese Anfrage zu erfüllen. Jeder Datenschutzauftrag enthält Identitätsdaten zum Datensubjekt, Metadaten zum Adobe Experience Cloud-Produkt, für das der Auftrag gilt, und den Verarbeitungsstatus des Auftrags.

Die `/jobs` Mit dem -Endpunkt können Sie Datenschutzaufträge für Ihre Organisation erstellen und abrufen. Informationen zur Verwendung dieses Endpunkts finden Sie unter [Endleitfaden für Datenschutzaufträge](./privacy-jobs.md).

## Einverständnis

Bestimmte Vorschriften erfordern eine ausdrückliche Zustimmung des Kunden, bevor seine personenbezogenen Daten erfasst werden können. Die `/consent` Mit dem Endpunkt können Sie Anfragen zur Kundenzustimmung verarbeiten und in Ihren Datenschutz-Workflow integrieren. Siehe [Einverständnisendpunkt-Handbuch](./consent.md) , um mehr zu erfahren.

## Nächste Schritte

Um mit der Privacy Service-API Aufrufe zu tätigen, lesen Sie den Abschnitt [Erste Schritte](./getting-started.md) Wählen Sie dann eine der Endpunktleitfäden aus, um zu erfahren, wie Sie bestimmte Endpunkte verwenden.
