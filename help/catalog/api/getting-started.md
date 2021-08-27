---
keywords: Experience Platform; Startseite; beliebte Themen; Katalogdienst; Katalog; Katalogdienst; Katalog
solution: Experience Platform
title: Handbuch zur Catalog Service API
topic-legacy: developer guide
description: Mit der Catalog Service-API können Entwickler Datensatzmetadaten in Adobe Experience Platform verwalten. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
exl-id: 812fcdae-ed0e-4f2b-84d7-26f2f79e71b9
source-git-commit: 5160bc8057a7f71e6b0f7f2d594ba414bae9d8f6
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 63%

---

# [!DNL Catalog Service]-API-Handbuch

[!DNL Catalog Service] ist ein Aufzeichnungssystem für Speicherort und Herkunft von Daten in Adobe Experience Platform. [!DNL Catalog] dient als Metadatenspeicher oder „Katalog“, in dem Sie Informationen über Ihre Daten in finden können, ohne auf die Daten selbst zugreifen zu müssen.[!DNL Experience Platform] Weitere Informationen finden Sie in der [[!DNL Catalog] Übersicht über ](../home.md).

In diesem Entwicklerhandbuch finden Sie Anweisungen, wie Sie mit der Verwendung der [!DNL Catalog]-API beginnen können. Dann bietet das Handbuch Beispiel-API-Aufrufe für die Ausführung wichtiger Vorgänge mithilfe von [!DNL Catalog].

## Voraussetzungen

[!DNL Catalog] verfolgt Metadaten für verschiedene Arten von Ressourcen und Vorgängen in  [!DNL Experience Platform]. Dieses Entwicklerhandbuch setzt ein Verständnis der verschiedenen [!DNL Experience Platform]-Dienste voraus, die mit der Erstellung und Verwaltung dieser Ressourcen verbunden sind:

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Platform] Kundenerlebnisdaten organisiert.
* [Batch-Erfassung](../../ingestion/batch-ingestion/overview.md)[!DNL Experience Platform]: So erfasst und speichert Daten aus Datendateien wie CSV und Parquet.
* [Streaming-Erfassung](../../ingestion/streaming-ingestion/overview.md): So  [!DNL Experience Platform] erfasst und speichert Daten von Client- und Server-seitigen Geräten in Echtzeit.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die [!DNL Catalog Service]-API erfolgreich aufrufen zu können.

## Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

## Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de#platform-apis) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an [!DNL Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

* Content-Type: application/json

## Best Practices für API-Aufrufe von [!DNL Catalog]

Bei der Ausführung von GET-Anfragen an die API [!DNL Catalog] empfiehlt es sich, Abfrageparameter in Ihre Anfragen einzubeziehen, um nur die benötigten Objekte und Eigenschaften zurückzugeben. Ungefilterte Anfragen können dazu führen, dass Antwort-Payloads größer als 3 GB sind, was die Gesamtleistung verringern kann.

Außerdem können Sie bestimmte Objekte durch Einfügen ihrer Kennung in den Anfragepfad anzeigen oder Abfrageparameter wie `properties` und `limit` zum Filtern von Antworten verwenden. Filter können als Kopfzeilen und Abfrageparameter übergeben werden, wobei Abfrageparameter bei der Übergabe Vorrang erhalten. Weiterführende Informationen finden Sie im Dokument zum [Filtern von Catalog-Daten](filter-data.md).

Da einige Abfragen die API stark belasten können, wurden globale Beschränkungen für [!DNL Catalog]-Abfragen implementiert, um Best Practices weiter zu unterstützen.

## Nächste Schritte

In diesem Dokument wurden die erforderlichen Kenntnisse zum Aufrufen der [!DNL Catalog]-API behandelt. Sie können nun mit den Beispielaufrufen in diesem Entwicklerhandbuch fortfahren und den entsprechenden Anweisungen folgen.

Die meisten Beispiele in diesem Handbuch verwenden den Endpunkt `/dataSets`, die Prinzipien können jedoch auf andere Endpunkte innerhalb von [!DNL Catalog] angewendet werden (z. B. `/batches` und `/accounts`). Eine vollständige Liste aller bei einzelnen Endpunkten verfügbaren Aufrufe und Vorgänge finden Sie in der [Referenz zur Catalog Service-API](https://www.adobe.io/experience-platform-apis/references/catalog/).

Einen schrittweisen Workflow, der zeigt, wie die [!DNL Catalog]-API an der Datenerfassung beteiligt ist, finden Sie im Tutorial zum Erstellen eines Datensatzes](../datasets/create.md).[
