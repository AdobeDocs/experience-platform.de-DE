---
keywords: Experience Platform;Home;beliebte Themen;Query Service;Query Service;Abfrage
solution: Experience Platform
title: Handbuch zur Abfrage-Service-API
description: Mit der Abfrage-Service-API können Entwickler ihre Adobe Experience Platform-Daten mit Standard-SQL abfragen. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
exl-id: 2f4a156b-5623-419a-a9b2-72310f755708
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 100%

---

# [!DNL Query Service]-API-Handbuch

Dieses Entwicklerhandbuch enthält Schritte zum Ausführen verschiedener Vorgänge in der [!DNL Query Service]-API von Adobe Experience Platform.

## Erste Schritte

Dieses Handbuch setzt Grundkenntnisse der verschiedenen Adobe Experience Platform-Services voraus, die mit der Verwendung von [!DNL Query Service] zusammenhängen.

- [[!DNL Query Service]](../home.md): Bietet die Möglichkeit, Datensätze abzufragen und die resultierenden Abfragen als neue Datensätze in [!DNL Experience Platform] zu erfassen.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Experience Platform] organisiert werden.
- [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um [!DNL Query Service] mithilfe der API erfolgreich zu verwenden zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in dieser Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Fehlerbehebungshandbuch für [!DNL Experience Platform].

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Experience Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Alle an [!DNL Platform]-APIs gerichtete Anfragen müssen über eine Kopfzeile verfügen, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zum Arbeiten mit Sandboxes in [!DNL Experience Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

## Beispiel-API-Aufrufe

Nachdem Sie nun wissen, welche Kopfzeilen zu verwenden sind, können Sie damit beginnen, die [!DNL Query Service]-API aufzurufen. In den folgenden Dokumenten werden die verschiedenen API-Aufrufe beschrieben, die Sie mithilfe der [!DNL Query Service]-API ausführen können. Jeder Beispielaufruf enthält das allgemeine API-Format, eine Beispielanfrage mit den erforderlichen Kopfzeilen und eine Beispielantwort.

- [Abfragen](queries.md)
- [Verbindungsparameter](connection-parameters.md)
- [Geplante Abfragen](scheduled-queries.md)
- [Ausführungen für geplante Abfragen](runs-scheduled-queries.md)
- [Abfragevorlagen](query-templates.md)
- [Beschleunigte Abfragen](./accelerated-queries.md)
- [Abonnements von Warnhinweisen](./alert-subscriptions.md)

## Nächste Schritte

Nachdem Sie nun gelernt haben, wie Sie Aufrufe mit der [!DNL Query Service]-API formulieren, können Sie Ihre eigenen nicht interaktiven Abfragen erstellen. Weitere Informationen zum Erstellen von Abfragen finden Sie im [SQL-Referenzhandbuch](../sql/overview.md).
