---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handbuch zum Entwickler von Datenschutzdiensten
description: Verwenden Sie die RESTful-API, um die personenbezogenen Daten Ihrer Betroffenen in allen Adobe Experience Cloud-Anwendungen zu verwalten
topic: developer guide
translation-type: tm+mt
source-git-commit: a1161630c8edae107b784f32ee20af225f9f8c46
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 2%

---


# Handbuch zum Entwickler von Datenschutzdiensten

Der Datenschutzdienst für Adobe Experience Platform bietet eine RESTful-API und eine Benutzeroberfläche, mit der Sie die persönlichen Daten Ihrer betroffenen Personen (Kunden) in allen Adobe Experience Cloud-Anwendungen verwalten (aufrufen und löschen) können. Der Datenschutzdienst bietet außerdem einen zentralen Prüfungs- und Protokollierungsmechanismus, mit dem Sie auf den Status und die Ergebnisse von Aufträgen zugreifen können, die Experience Cloud-Anwendungen betreffen.

In diesem Handbuch wird die Verwendung der Datenschutzdienst-API behandelt. Weitere Informationen zur Verwendung der Benutzeroberfläche finden Sie in der Übersicht über die Benutzeroberfläche des [Datenschutzdienstes](../ui/overview.md). Eine umfassende Liste aller verfügbaren Endpunkte in der Datenschutzdienst-API finden Sie in der [API-Referenz](https://www.adobe.io/apis/experiencecloud/gdpr/api-reference.html).

## Erste Schritte

Dieses Handbuch erfordert ein Verständnis der folgenden Funktionen der Erlebnisplattform:

* [Datenschutzdienst](../home.md): Bietet eine RESTful-API und eine Benutzeroberfläche, mit der Sie den Zugriff auf und das Löschen von Anforderungen Ihrer betroffenen Personen (Kunden) in allen Adobe Experience Cloud-Anwendungen verwalten können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die Datenschutzdienst-API erfolgreich aufzurufen.

### Lesen von Beispiel-API-Aufrufen

In diesem Lernprogramm finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md) im Handbuch zur Fehlerbehebung für Experience Platform.

### Werte für erforderliche Kopfzeilen sammeln

Um Aufrufe an Plattform-APIs durchzuführen, müssen Sie zunächst das [Authentifizierungstraining](../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungstreutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

* Genehmigung: Träger `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Für alle Anforderungen mit einer Payload (POST, PUT, PATCH) ist ein zusätzlicher Header erforderlich:

* Content-Type: application/json

## Nächste Schritte

Nachdem Sie wissen, welche Header Sie verwenden sollten, können Sie mit dem Aufrufen der Datenschutzdienst-API beginnen. Das Dokument zu [Datenschutzaufträgen](privacy-jobs.md) durchläuft die verschiedenen API-Aufrufe, die Sie mit der Datenschutzdienst-API durchführen können. Zu jedem Beispielaufruf gehören das allgemeine API-Format, eine Beispielanforderung mit den erforderlichen Kopfzeilen und eine Beispielantwort.
