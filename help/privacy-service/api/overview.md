---
title: Privacy Service-API-Handbuch
description: Erfahren Sie, wie Sie mit der Privacy Service-API Datenschutzaufträge für unterstützte Adobe Experience Cloud-Anwendungen programmgesteuert verwalten.
source-git-commit: 196147e7691010707953561c110a3934fec8ba1b
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 21%

---

# [!DNL Privacy Service]-API-Handbuch

Die Privacy Service-API bietet mehrere Endpunkte, mit denen Sie Datenschutzaufträge für Ihr Unternehmen programmgesteuert verwalten können. Diese Endpunkte werden nachfolgend beschrieben. Weitere Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie in den einzelnen Endpunkthandbüchern sowie in den [Ersten Schritten](./getting-started.md).

>[!NOTE]
>
>Dieses Handbuch behandelt die Verwendung der [!DNL Privacy Service] API. Weitere Informationen zur Verwendung der Benutzeroberfläche finden Sie in der [Übersicht über die Privacy Service-Benutzeroberfläche](../ui/overview.md).

Um alle verfügbaren Endpunkte und CRUD-Vorgänge Ansicht, besuchen Sie die [Privacy Service-API-Verweis](https://www.adobe.io/experience-platform-apis/references/privacy-service/).

## Datenschutzaufträge

Wenn der Privacy Service eine Anfrage auf den Zugriff auf die personenbezogenen Daten eines Betreffenden oder deren Löschung erhält, erstellt das System Datenschutzaufträge, um diese Anforderung zu erfüllen. Jeder Auftrag zum Schutz der Privatsphäre enthält Identitätsdaten zur betroffenen Person, Metadaten zum Adobe Experience Cloud-Produkt, für das der Auftrag gilt, und den Verarbeitungsstatus des Auftrags.

Die `/jobs` endpoint ermöglicht das Erstellen und Abrufen von Datenschutzaufträgen für Ihr Unternehmen. Weitere Informationen zur Verwendung dieses Endpunkts finden Sie unter [Endpunkt für Datenschutzaufträge](./privacy-jobs.md).

## Einverständnis

Bestimmte Bestimmungen bedürfen der ausdrücklichen Zustimmung des Kunden, bevor seine persönlichen Daten erhoben werden können. Die `/consent` endpoint ermöglicht es Ihnen, Anfragen zur Kundengenehmigung zu verarbeiten und in Ihren Datenschutz-Workflow zu integrieren. Siehe [Endpunkt-Handbuch für Zustimmung](./consent.md) um mehr zu erfahren.

## Nächste Schritte

Lesen Sie die folgenden Informationen, um mit dem Aufrufen der Privacy Service-API zu beginnen: [Erste Schritte](./getting-started.md) wählen Sie dann eine der Endpunkt-Hilfslinien aus, um zu erfahren, wie bestimmte Endpunkte verwendet werden.
