---
keywords: Experience Platform;Home;beliebte Themen;Query Service;Query Service;Abfrage
solution: Experience Platform
title: API-Anleitung für Query Service
topic-legacy: query templates
description: Mit der Query Service-API können Entwickler ihre Adobe Experience Platform-Daten mit Standard-SQL abfragen. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
exl-id: 2f4a156b-5623-419a-a9b2-72310f755708
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 46%

---

# [!DNL Query Service]-API-Handbuch

Dieses Entwicklerhandbuch enthält Schritte zum Ausführen verschiedener Vorgänge in der Adobe Experience Platform-API [!DNL Query Service].

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der verschiedenen Adobe Experience Platform-Dienste voraus, die mit der Verwendung von [!DNL Query Service] verbunden sind.

- [[!DNL Query Service]](../home.md): Bietet die Möglichkeit, Datensätze abzufragen und die resultierenden Abfragen als neue Datensätze in  [!DNL Experience Platform]zu erfassen.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
- [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um [!DNL Query Service] erfolgreich mit der API verwenden zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in dieser Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt [So lesen Sie Beispiel-API-Aufrufe](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung [!DNL Experience Platform].

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Experience Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de#platform-apis) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Für alle Anfragen an [!DNL Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zum Arbeiten mit Sandboxes in [!DNL Experience Platform] finden Sie in der [Sandboxes - Übersichtsdokumentation für Sandboxes](../../sandboxes/home.md).

## Beispiel-API-Aufrufe

Nachdem Sie nun wissen, welche Header verwendet werden sollen, können Sie mit Aufrufen an die [!DNL Query Service]-API beginnen. Die folgenden Dokumente führen Sie durch die verschiedenen API-Aufrufe, die Sie mit der [!DNL Query Service]-API ausführen können. Jeder Beispielaufruf enthält das allgemeine API-Format, eine Beispielanfrage mit den erforderlichen Kopfzeilen und eine Beispielantwort.

- [Abfragen](queries.md)
- [Verbindungsparameter](connection-parameters.md)
- [Geplante Abfragen](scheduled-queries.md)
- [Ausführungen für geplante Abfragen](runs-scheduled-queries.md)
- [Abfragevorlagen](query-templates.md)

## Nächste Schritte

Nachdem Sie nun gelernt haben, wie Sie Aufrufe mit der [!DNL Query Service]-API tätigen, können Sie Ihre eigenen nicht-interaktiven Abfragen erstellen. Weitere Informationen zum Erstellen von Abfragen finden Sie im [SQL-Referenzhandbuch](../sql/overview.md).
