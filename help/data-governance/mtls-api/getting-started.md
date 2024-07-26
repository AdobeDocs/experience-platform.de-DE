---
title: Erste Schritte mit der MTLS-Dienst-API
description: Dieses Dokument enthält zusätzliche Informationen, die Sie benötigen, um erfolgreich mit der MTLS-API arbeiten zu können.
role: Developer
source-git-commit: f0b9d414d7b08015478c132de6910629d86c9cf9
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 42%

---

# Erste Schritte mit der MTLS-Service-API {#getting-started}

Mit der MTLS Service API können Sie die von Adobe ausgestellten öffentlichen Zertifikate sicher abrufen und überprüfen.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um erfolgreich mit der MTLS-Service-API arbeiten zu können.

## Lesen von Beispiel-API-Aufrufen

Die Dokumentation zur MTLS-Service-API enthält einen Beispiel-API-Aufruf, der die Formatierung Ihrer Anfragen demonstriert. Dazu gehören der Pfad, die erforderlichen Kopfzeilen und die ordnungsgemäß formatierte Anfrage-Payload. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

## Erforderliche Kopfzeilen

Außerdem setzt die API-Dokumentation voraus, dass Sie das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abgeschlossen haben, um Platform-Endpunkte erfolgreich aufrufen zu können. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

## Nächste Schritte

Um Aufrufe mit der MTLS-Dienst-API durchzuführen, wählen Sie die Endpunktleitfäden entweder mithilfe der linken Navigation oder in der [Übersicht über das Entwicklerhandbuch](./overview.md) aus
