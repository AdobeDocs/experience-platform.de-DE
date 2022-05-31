---
keywords: Experience Platform; Startseite; beliebte Themen; Attributbasierte Zugriffssteuerung; attributbasierte Zugriffssteuerung
title: Erste Schritte mit der attributbasierten Zugriffssteuerung
description: Mit der attributbasierten Zugriffssteuerung können Sie Rollen und Richtlinien in Adobe Experience Platform programmgesteuert verwalten. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
exl-id: d1a66afa-dff4-49d7-b57c-527f05977155
source-git-commit: 567bfe089fd96cb08cb8ea7c90d065c804be9413
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 64%

---

# Erste Schritte mit der attributbasierten Zugriffskontrolle

>[!IMPORTANT]
>
>Die attribut-basierte Zugriffskontrolle ist derzeit in einer eingeschränkten Version für US-Kunden im Gesundheitswesen verfügbar. Diese Funktion steht allen Real-time Customer Data Platform-Kunden nach der vollständigen Veröffentlichung zur Verfügung.

Dieses Entwicklerhandbuch enthält Schritte, die Sie bei der Verwendung der attributbasierten Zugriffssteuerung unterstützen, um Rollen, Produkte, Berechtigungskategorien und Berechtigungssätze in Adobe Experience Platform zu verwalten. Außerdem enthält es Beispiel-API-Aufrufe für die Durchführung verschiedener Vorgänge.

## Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung in Experience Platform.

## Sammeln von Werten für erforderliche Kopfzeilen

Für diese Anleitung müssen Sie das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abgeschlossen haben, damit Sie Platform-APIs erfolgreich aufrufen können. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Zusätzlich zu den Authentifizierungskopfzeilen benötigen alle Anfragen eine Kopfzeile, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* `x-sandbox-name: {SANDBOX_NAME}`

Für alle Anfragen mit einer Payload (POST, PUT, PATCH) wird eine zusätzliche Kopfzeile benötigt:

* `Content-Type: application/json`

## Nächste Schritte

Nachdem Sie die erforderlichen Anmeldedaten gesammelt haben, können Sie nun das restliche Entwicklerhandbuch lesen. Jeder Abschnitt enthält wichtige Informationen zu ihren Endpunkten und veranschaulicht Beispiel-API-Aufrufe zur Durchführung von CRUD-Vorgängen. Zu jedem Aufruf gehören das allgemeine API-Format, eine Beispielanfrage mit erforderlichen Kopfzeilen und ordnungsgemäß formatierten Payloads sowie eine Beispielantwort eines erfolgreichen Aufrufs.

In den folgenden API-Tutorials erfahren Sie, wie Sie Aufrufe an die attributbasierte Zugriffssteuerungs-API starten:

* [Benutzerendpunkt](./roles.md)
* [Endpunkt &quot;Produkte&quot;](./products.md)
