---
keywords: Experience Platform;Home;beliebte Themen;Abfrage-Dienst;Abfrage-Dienst;Abfrage
solution: Experience Platform
title: Handbuch zur Abfrage Service API
topic-legacy: query templates
description: Die Abfrage Service API ermöglicht es Entwicklern, ihre Adobe Experience Platform-Daten mithilfe von SQL-Standard Abfrage. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
exl-id: 2f4a156b-5623-419a-a9b2-72310f755708
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 31%

---

# [!DNL Query Service] API-Handbuch

Dieses Entwicklerhandbuch enthält Schritte zum Ausführen verschiedener Vorgänge in der Adobe Experience Platform [!DNL Query Service]-API.

## Erste Schritte

Dieses Handbuch erfordert ein Verständnis der verschiedenen Adobe Experience Platform-Dienste, die mit [!DNL Query Service] arbeiten.

- [[!DNL Query Service]](../home.md): Ermöglicht die Abfrage von Datensätzen und die Erfassung der resultierenden Abfragen als neue Datensätze in  [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
- [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne  [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um [!DNL Query Service] erfolgreich mit der API verwenden zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den in dieser Dokumentation verwendeten Konventionen für Beispiel-API-Aufrufe finden Sie im Abschnitt [Anleitung zum Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch [!DNL Experience Platform] zur Fehlerbehebung.

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Experience Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://www.adobe.com/go/platform-api-authentication-en) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform] werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an [!DNL Platform]-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang stattfinden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zum Arbeiten mit Sandboxes in [!DNL Experience Platform] finden Sie in der [Übersicht über Sandboxen](../../sandboxes/home.md).

## Beispiel-API-Aufrufe

Nachdem Sie wissen, welche Header verwendet werden sollen, können Sie mit dem Aufrufen der [!DNL Query Service]-API beginnen. Die folgenden Dokumente gehen durch die verschiedenen API-Aufrufe, die Sie mit der API [!DNL Query Service] durchführen können. Jeder Beispielaufruf enthält das allgemeine API-Format, eine Beispielanfrage mit den erforderlichen Kopfzeilen und eine Beispielantwort.

- [Abfragen](queries.md)
- [Verbindungsparameter](connection-parameters.md)
- [Geplante Abfragen](scheduled-queries.md)
- [Ausführungen für geplante Abfragen](runs-scheduled-queries.md)
- [Abfragevorlagen](query-templates.md)

## Nächste Schritte

Nachdem Sie nun gelernt haben, wie Sie mit der [!DNL Query Service]-API Aufrufe durchführen, können Sie Ihre eigenen nicht interaktiven Abfragen erstellen. Weitere Informationen zum Erstellen von Abfragen finden Sie im [SQL-Referenzhandbuch](../sql/overview.md).
