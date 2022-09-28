---
keywords: Experience Platform;Home;beliebte Themen;Query Service;Query Service;Abfrage
solution: Experience Platform
title: API-Anleitung für Query Service
topic-legacy: query templates
description: Mit der Query Service-API können Entwickler ihre Adobe Experience Platform-Daten mit Standard-SQL abfragen. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
exl-id: 2f4a156b-5623-419a-a9b2-72310f755708
source-git-commit: 62463e1542d4306c5c769e5690b566a3c30c59cd
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 45%

---

# [!DNL Query Service]-API-Handbuch

Dieses Entwicklerhandbuch enthält Schritte zum Ausführen verschiedener Vorgänge in Adobe Experience Platform [!DNL Query Service] API.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der verschiedenen Adobe Experience Platform-Dienste voraus, die mit der Verwendung von [!DNL Query Service].

- [[!DNL Query Service]](../home.md): Bietet die Möglichkeit, Datensätze abzufragen und die resultierenden Abfragen als neue Datensätze in [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Experience Platform] organisiert werden.
- [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um erfolgreich verwenden zu können [!DNL Query Service] die API verwenden.

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in dieser Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zu [So lesen Sie Beispiel-API-Aufrufe](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im [!DNL Experience Platform] Handbuch zur Fehlerbehebung.

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Experience Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Alle Anfragen an [!DNL Platform] APIs erfordern eine Kopfzeile, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zum Arbeiten mit Sandboxes finden Sie unter [!DNL Experience Platform], siehe [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

## Beispiel-API-Aufrufe

Nachdem Sie nun wissen, welche Header verwendet werden sollen, können Sie mit den Aufrufen an die [!DNL Query Service] API. In den folgenden Dokumenten werden die verschiedenen API-Aufrufe erläutert, die Sie mithilfe der [!DNL Query Service] API. Jeder Beispielaufruf enthält das allgemeine API-Format, eine Beispielanfrage mit den erforderlichen Kopfzeilen und eine Beispielantwort.

- [Abfragen](queries.md)
- [Verbindungsparameter](connection-parameters.md)
- [Geplante Abfragen](scheduled-queries.md)
- [Ausführungen für geplante Abfragen](runs-scheduled-queries.md)
- [Abfragevorlagen](query-templates.md)
- [Warnhinweis-Abonnements](./alert-subscriptions.md)

## Nächste Schritte

Nachdem Sie nun gelernt haben, wie Sie Aufrufe mit dem [!DNL Query Service] API können Sie Ihre eigenen nicht interaktiven Abfragen erstellen. Weitere Informationen zum Erstellen von Abfragen finden Sie im Abschnitt [SQL-Referenzhandbuch](../sql/overview.md).
