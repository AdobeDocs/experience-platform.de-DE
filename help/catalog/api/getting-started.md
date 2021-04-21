---
keywords: Experience Platform;Home;beliebte Themen;Katalogdienst;Katalog;Katalogdienst;Katalog
solution: Experience Platform
title: Handbuch zur API für Katalogdienst
topic-legacy: developer guide
description: Mit der Katalogdienst-API können Entwickler Datensatzmetadaten in Adobe Experience Platform verwalten. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
exl-id: 812fcdae-ed0e-4f2b-84d7-26f2f79e71b9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 55%

---

# [!DNL Catalog Service] API-Handbuch

[!DNL Catalog Service] ist ein Aufzeichnungssystem für Speicherort und Herkunft von Daten in Experience Platform. [!DNL Catalog] dient als Metadatenspeicher oder „Katalog“, in dem Sie Informationen über Ihre Daten in finden können, ohne auf die Daten selbst zugreifen zu müssen.[!DNL Experience Platform] Weitere Informationen finden Sie in der [[!DNL Catalog] Übersicht über ](../home.md).

In diesem Entwicklerhandbuch finden Sie Anweisungen, wie Sie mit der Verwendung der [!DNL Catalog]-API beginnen können. Dann bietet das Handbuch Beispiel-API-Aufrufe für die Ausführung wichtiger Vorgänge mithilfe von [!DNL Catalog].

## Voraussetzungen

[!DNL Catalog] verfolgt Metadaten für verschiedene Arten von Ressourcen und Vorgängen innerhalb von  [!DNL Experience Platform]. Dieses Entwicklerhandbuch erfordert ein Verständnis der verschiedenen [!DNL Experience Platform]-Dienste, die mit der Erstellung und Verwaltung dieser Ressourcen verbunden sind:

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Platform] Kundenerlebnisdaten organisiert.
* [Batch-Erfassung](../../ingestion/batch-ingestion/overview.md)[!DNL Experience Platform]: So erfasst und speichert Daten aus Datendateien wie CSV und Parquet.
* [Streaming-Erfassung](../../ingestion/streaming-ingestion/overview.md): So  [!DNL Experience Platform] werden Daten von Client- und serverseitigen Geräten in Echtzeit erfasst und gespeichert.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die [!DNL Catalog Service]-API erfolgreich aufrufen zu können.

## Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Fehlerbehebungshandbuch für [!DNL Experience Platform]

## Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://www.adobe.com/go/platform-api-authentication-en) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform] werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an [!DNL Platform]-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird in:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxen in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

* Content-Type: application/json

## Bewährte Verfahren für API-Aufrufe von [!DNL Catalog]

Beim Durchführen von GET an die API ist es am besten, Abfragen-Parameter in Ihre Anforderungen einzubeziehen, um nur die benötigten Objekte und Eigenschaften zurückzugeben. [!DNL Catalog] Ungefilterte Anfragen können dazu führen, dass Antwort-Payloads größer als 3 GB sind, was die Gesamtleistung verringern kann.

Außerdem können Sie bestimmte Objekte durch Einfügen ihrer Kennung in den Anfragepfad anzeigen oder Abfrageparameter wie `properties` und `limit` zum Filtern von Antworten verwenden. Filter können als Kopfzeilen und Abfrageparameter übergeben werden, wobei Abfrageparameter bei der Übergabe Vorrang erhalten. Weiterführende Informationen finden Sie im Dokument zum [Filtern von Catalog-Daten](filter-data.md).

Da einige Abfragen die API stark belasten können, wurden globale Beschränkungen für [!DNL Catalog]-Abfragen implementiert, um Best Practices weiter zu unterstützen.

## Nächste Schritte

Dieses Dokument deckte die erforderlichen Kenntnisse ab, um Aufrufe an die [!DNL Catalog]-API durchzuführen. Sie können nun mit den Beispielaufrufen in diesem Entwicklerhandbuch fortfahren und den entsprechenden Anweisungen folgen.

Die meisten Beispiele in diesem Handbuch verwenden den Endpunkt `/dataSets`, aber die Prinzipien können auf andere Endpunkte innerhalb von [!DNL Catalog] angewendet werden (z. B. `/batches` und `/accounts`). Eine vollständige Liste aller bei einzelnen Endpunkten verfügbaren Aufrufe und Vorgänge finden Sie in der [Referenz zur Catalog Service-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml).

Ein schrittweiser Arbeitsablauf, der zeigt, wie die [!DNL Catalog]-API mit der Datenerfassung verbunden ist, finden Sie im Lernprogramm [Erstellen eines Datensatzes](../datasets/create.md).
