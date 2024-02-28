---
keywords: Experience Platform;Startseite;beliebte Themen;Zugangssteuerung;API;Erste Schritte
solution: Experience Platform
title: Handbuch der Zugangssteuerungs-APIs
description: Mit der Zugangssteuerung in Adobe Experience Platform können Sie Rollen und Berechtigungen für verschiedene Funktionen der Plattform mithilfe von Adobe Admin Console verwalten. Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die Schema Registry-API erfolgreich aufrufen zu können.
role: Developer
exl-id: 6fd956fb-ade4-48d3-843f-4c9a605945c9
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 97%

---

# [!DNL Access Control]-API-Handbuch

[!DNL Access control] für [!DNL Experience Platform] wird über [Adobe Admin Console](https://adminconsole.adobe.com) verwaltet. Diese Funktion nutzt Produktprofile in Admin Console, um Anwender mit Berechtigungen und Sandboxes zu verknüpfen. Weiterführende Informationen dazu finden Sie unter [Zugangssteuerung – Übersicht](../home.md).

Dieses Entwicklerhandbuch enthält Informationen zum Formatieren Ihrer Anfragen an die [[!DNL Access Control API]](https://www.adobe.io/experience-platform-apis/references/access-control/) und behandelt die folgenden Vorgänge:

- [Berechtigungsnamen und Ressourcentypen auflisten](./permissions-and-resource-types.md)
- [Gültige Zugriffsrichtlinien für den aktuellen Benutzer anzeigen](./effective-policies.md)

## Erste Schritte

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die [!DNL Access Control]-API erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an [!DNL Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

- Content-Type: application/json

## Nächste Schritte

Nachdem Sie die erforderlichen Anmeldedaten gesammelt haben, können Sie nun das restliche Entwicklerhandbuch lesen. Jeder Abschnitt enthält wichtige Informationen zu ihren Endpunkten und veranschaulicht Beispiel-API-Aufrufe zur Durchführung von CRUD-Vorgängen. Zu jedem Aufruf gehören das allgemeine API-Format, eine Beispielanfrage mit erforderlichen Kopfzeilen und ordnungsgemäß formatierten Payloads sowie eine Beispielantwort eines erfolgreichen Aufrufs.
