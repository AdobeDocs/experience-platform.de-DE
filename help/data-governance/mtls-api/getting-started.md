---
title: Erste Schritte mit der MTLS-Service-API
description: Dieses Dokument enthält zusätzliche Informationen, die Sie für eine erfolgreiche Arbeit mit der MTLS-API benötigen.
role: Developer
exl-id: db5978cf-fe47-4b76-86ba-c8ea1ee6b12f
source-git-commit: d9e9275db1989df22b13b4f000dde645f40d5744
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 42%

---

# Erste Schritte mit der MTLS-Service-API {#getting-started}

Mit der MTLS-Service-API können Sie die von Adobe ausgestellten öffentlichen Zertifikate sicher abrufen und überprüfen.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mit der MTLS-Service-API erfolgreich arbeiten zu können.

## Lesen von Beispiel-API-Aufrufen

In der Dokumentation zur MTLS-Service-API wird anhand eines Beispiel-API-Aufrufs die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören der Pfad, die erforderlichen Kopfzeilen und die ordnungsgemäß formatierte Anfrage-Payload. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

## Erforderliche Kopfzeilen

Außerdem setzt die API-Dokumentation voraus, dass Sie das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abgeschlossen haben, um Platform-Endpunkte erfolgreich aufrufen zu können. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

## Nächste Schritte

Um Aufrufe mit der MTLS-Service-API durchzuführen, wählen Sie die Endpunkthandbücher entweder über die linke Navigation oder innerhalb der [Übersicht über das Entwicklerhandbuch](./overview.md)
