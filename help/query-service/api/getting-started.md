---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Entwicklerhandbuch für Query Service
topic: query templates
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 23%

---


# [!DNL Query Service] Entwicklerhandbuch

Dieses Entwicklerhandbuch enthält Anweisungen zum Ausführen verschiedener Vorgänge in der Adobe Experience Platformen- [!DNL Query Service] API.

## Erste Schritte

This guide requires a working understanding of the various Adobe Experience Platform services involved with using [!DNL Query Service].

- [!DNL Query Service](../home.md): Ermöglicht die Abfrage von Datensätzen und die Erfassung der resultierenden Abfragen als neue Datensätze in [!DNL Experience Platform].
- [!DNL Experience Data Model (XDM) System](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Experience Platform] organisiert werden.
- [!DNL Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

The following sections provide additional information that you will need to know in order to successfully use [!DNL Query Service] using the API.

### Lesehilfe für Beispiel-API-Aufrufe

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dabei wird auf Pfade ebenso eingegangen wie auf die erforderlichen Kopfzeilen und die für Anfrage-Payloads zu verwendende Formatierung. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. For information on the conventions used in this documentation for sample API calls, see the section on [how to read example API calls](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in the [!DNL Experience Platform] troubleshooting guide.

### Werte der zu verwendenden Kopfzeilen

In order to make calls to [!DNL Experience Platform] APIs, you must first complete the [authentication tutorial](../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Platform] API calls, as shown below:

- Autorisierung: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox in which the operation will take place:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on working with sandboxes in [!DNL Experience Platform], see the [sandboxes overview documentation](../../sandboxes/home.md).

## Beispiel-API-Aufrufe

Now that you understand what headers to use, you are ready to begin making calls to the [!DNL Query Service] API. The following documents walk through the various API calls you can make using the [!DNL Query Service] API. Jeder Beispielaufruf enthält das allgemeine API-Format, eine Beispielanfrage mit den erforderlichen Kopfzeilen und eine Beispielantwort.

- [Abfragen](queries.md)
- [Verbindungsparameter](connection-parameters.md)
- [Geplante Abfragen](scheduled-queries.md)
- [Ausführungen für geplante Abfragen](runs-scheduled-queries.md)
- [Abfragevorlagen](query-templates.md)

## Nächste Schritte

Nachdem Sie nun gelernt haben, wie Sie mit der [!DNL Query Service] API Aufrufe durchführen, können Sie Ihre eigenen nicht interaktiven Abfragen erstellen. Weitere Informationen zum Erstellen von Abfragen finden Sie im [SQL-Referenzhandbuch](../sql/overview.md).