---
keywords: Experience Platform;Home;beliebte Themen;Adobe Experience Platform;API-Handbuch;Plattform-API-Handbuch;Einführung in die Plattform;Entwicklerhandbuch
solution: Experience Platform
title: Erste Schritte mit Adobe Experience Platform APIs
topic: API-Handbuch
description: Adobe Experience Platform stellt API-Dienste bereit, die eng miteinander verbunden sind. Dieses Handbuch enthält Informationen zu den verfügbaren Diensten, erforderlichen Kopfzeilen für CRUD-Vorgänge, Fehlermeldungen, Postman-Sammlungen und Beispiel-API-Aufrufen.
translation-type: tm+mt
source-git-commit: 85d2ae5ccf1b27baaafe839f1d3f00d588abe4fc
workflow-type: tm+mt
source-wordcount: '1427'
ht-degree: 25%

---


# Erste Schritte mit Adobe Experience Platform APIs

Adobe Experience Platform wird unter der Philosophie &quot;API first&quot;entwickelt. Mithilfe von Plattform-APIs können Sie grundlegende CRUD-Vorgänge (Erstellen, Lesen, Aktualisieren, Löschen) programmgesteuert für Daten durchführen, z. B. die Konfiguration berechneter Attribute, den Zugriff auf Daten/Entitäten, den Export von Daten, das Löschen nicht benötigter Daten oder Stapel usw.

Die APIs für jeden Experience Platform-Dienst verwenden alle denselben Satz von Authentifizierungs-Headern und verwenden ähnliche Syntaxen für ihre CRUD-Vorgänge. In der folgenden Anleitung werden die erforderlichen Schritte für die ersten Schritte mit Plattform-APIs beschrieben.

## Authentifizierung und Kopfzeilen

Damit Sie erfolgreich Aufrufe an Plattform-Endpunkte vornehmen können, müssen Sie das [Authentifizierungstutorial](https://www.adobe.com/go/platform-api-authentication-en) abschließen. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

### Sandbox-Kopfzeile

Alle Ressourcen in Experience Platform sind auf bestimmte virtuelle Sandboxes beschränkt. Für Anfragen an Platform-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- `x-sandbox-name: {SANDBOX_NAME}`

Weitere Informationen zu Sandboxes in Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../sandboxes/home.md).

### Content-Type-Kopfzeile

Alle Anfragen mit einer Payload im Anfragetext (wie POST-, PUT- und PATCH-Aufrufe) müssen eine `Content-Type`-Kopfzeile enthalten. Akzeptierte Werte sind für jeden API-Endpunkt spezifisch. Wenn ein bestimmter `Content-Type`-Wert für einen Endpunkt benötigt wird, wird sein Wert in den Beispiel-API-Anforderungen angezeigt, die von den [API-Handbüchern für einzelne Plattformdienste](#api-guides) bereitgestellt werden.

## Grundlagen der Experience Platform-API

Adobe Experience Platform-APIs setzen verschiedene zugrunde liegende Technologien und Syntaxen ein, die für eine effiziente Verwaltung der Plattformressourcen wichtig sind.

Weitere Informationen zu den zugrunde liegenden API-Technologien, einschließlich JSON-Schema-Beispielobjekten, finden Sie im Handbuch [Experience Platform API-Grundlagen](api-fundamentals.md).

## Postman-Sammlungen für Experience Platform-APIs

Postman ist eine Kooperationsplattform für die API-Entwicklung, mit der Sie Umgebung mit voreingestellten Variablen einrichten, API-Sammlungen freigeben, CRUD-Anforderungen optimieren und mehr. Die meisten Plattform-API-Dienste verfügen über Postman-Sammlungen, mit denen API-Aufrufe durchgeführt werden können.

Weitere Informationen zu Postman, einschließlich der Einrichtung einer Umgebung, einer Liste verfügbarer Sammlungen und dem Importieren von Sammlungen, finden Sie in der [Platform Postman-Dokumentation](postman.md).

## Lesen von Beispiel-API-Aufrufen {#sample-api}

Anfrageformate variieren je nach der verwendeten Platform-API. Am einfachsten erfahren Sie, wie Sie API-Aufrufe strukturieren können, indem Sie sich die in der Dokumentation die für einzelne Platform-Dienste angegebenen Beispiele ansehen.

Die Dokumentation für [!DNL Experience Platform] zeigt Beispiel-API-Aufrufe auf zwei verschiedene Arten an. Zunächst wird der Aufruf im **API-Format** dargestellt, wobei es sich um eine Vorlagendarstellung handelt, die nur den Vorgang (GET, POST, PUT, PATCH, DELETE) und den verwendeten Endpunkt (z. B. `/global/classes`) zeigt. Manche Vorlagen zeigen auch die Stelle von Variablen an, um zu veranschaulichen, wie ein Aufruf formuliert werden sollte, z. B. `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

Die Aufrufe werden dann als cURL-Befehle in einer **Anfrage** angezeigt, die die erforderlichen Kopfzeilen und den vollständigen „Basispfad“ enthält, die für eine erfolgreiche Interaktion mit der API erforderlich sind. Der Basispfad sollte allen Endpunkten vorangestellt werden. Der oben genannte Endpunkt `/global/classes` beispielsweise ändert sich in `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. Sie sehen das API-Format/Anforderungsmuster in der gesamten Dokumentation und müssen den vollständigen Pfad verwenden, der in der Beispielanforderung angezeigt wird, wenn Sie Ihre eigenen Aufrufe an Plattform-APIs durchführen.

### Beispiel-API-Anfrage

Im Folgenden finden Sie eine Beispiel-API-Anfrage, die das Format veranschaulicht, mit dem Sie es in der Dokumentation zu tun haben werden.

**API-Format**

Das API-Format gibt Auskunft über den Vorgang (GET) und den verwendeten Endpunkt. Variablen werden durch geschweifte Klammern gekennzeichnet (in diesem Fall `{CONTAINER_ID}`).

```http
GET /{CONTAINER_ID}/classes
```

**Anfrage**

In dieser Beispielanfrage werden den Variablen aus dem API-Format tatsächliche Werte im Anfragepfad zugewiesen. Darüber hinaus werden alle erforderlichen Header entweder als Beispiel-Header-Werte oder als Variablen angezeigt, in die vertrauliche Informationen (wie Sicherheits-Token und Zugriffs-IDs) einbezogen werden sollten.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Die Antwort zeigt, was Sie nach einem erfolgreichen Aufruf an die API erwarten würden, je nach gesendeter Anfrage. Zum Teil ist die Antwort aus Platzgründen abgeschnitten, d. h. Sie können möglicherweise mehr Informationen oder zusätzliche Informationen zu den im Beispiel dargestellten Informationen sehen.

```json
{
    "results": [
        {
            "title": "XDM ExperienceEvent",
            "$id": "https://ns.adobe.com/xdm/context/experienceevent",
            "meta:altId": "_xdm.context.experienceevent",
            "version": "1"
        },
        {
            "title": "XDM Individual Profile",
            "$id": "https://ns.adobe.com/xdm/context/profile",
            "meta:altId": "_xdm.context.profile",
            "version": "1"
        }
    ],
    "_links": {}
}
```

## Fehlermeldungen

Das Handbuch [Plattformfehlerbehebung](troubleshooting.md#errors-and-troubleshooting) enthält eine Liste von Fehlern, die bei der Verwendung eines Experience Platform-Dienstes auftreten können.

Hinweise zur Fehlerbehebung bei einzelnen Plattformdiensten finden Sie im Ordner [Dienstfehlerbehebung](troubleshooting.md#service-troubleshooting-directory).

Weitere Informationen zu bestimmten Endpunkten in Plattform-APIs, einschließlich der erforderlichen Kopfzeilen und Anforderungskörper, finden Sie in den [Plattform-API-Handbüchern](#api-guides).

## API-Handbücher für Plattformen {#api-guides}

| API-Handbuch | Beschreibung |
| --- | --- |
| [[!DNL Access Control] API-Handbuch](.././access-control/api/getting-started.md) | Der API-Endpunkt [!DNL Access Control] kann aktuelle Richtlinien abrufen, die für einen Benutzer bei bestimmten Ressourcen in einer angegebenen Sandbox gültig sind. Alle anderen Funktionen der Zugriffskontrolle werden über das [Adobe Admin Console](https://adminconsole.adobe.com/) bereitgestellt. |
| [Handbuch zur Batchaufnahme-API](.././ingestion/batch-ingestion/api-overview.md) | Mit der API Adobe Experience Platform [!DNL Data Ingestion] können Sie Daten als Batch-Dateien in Plattform erfassen. Daten, die erfasst werden, können die Profil-Daten aus einer einfachen Datei in einem CRM-System (z. B. einer Parquet-Datei) oder Daten sein, die einem bekannten Schema in der Schema Registry (XDM) entsprechen. |
| [[!DNL Catalog Service] API-Handbuch](.././catalog/api/getting-started.md) | Die [!DNL Catalog Service]-API ermöglicht Entwicklern die Verwaltung von DataSet-Metadaten in Adobe Experience Platform. Dazu gehören Datenspeicherorte, Verarbeitungsstufen, während der Verarbeitung aufgetretene Fehler und Datenberichte. |
| [[!DNL Data Access] API-Handbuch](.././data-access/api.md) | Die [!DNL Data Access]-API ermöglicht es Entwicklern, Informationen zu erfassten Datensätzen innerhalb der Experience Platform abzurufen. Dazu gehören der Zugriff auf und das Herunterladen von Datensatzdateien, das Abrufen von Header-Informationen, das Auflisten fehlgeschlagener und erfolgreicher Stapel und das Herunterladen von CSV-/Parquet-Vorschauen. |
| [[!DNL Dataset Service] API-Handbuch](.././data-governance/labels/dataset-api.md) | Mit der DataSet-Dienst-API können Sie Nutzungsbezeichnungen für Datensätze anwenden und bearbeiten. Es gehört zu den Funktionen des Adobe Experience Platform-Datenkatalogs, ist jedoch von der Katalogdienst-API getrennt, die die Metadaten des Datensatzes verwaltet. |
| [[!DNL Flow Service] API-Handbuch](.././sources/tutorials/api/create-dataset-base-connection.md) <br>  (Quellen und Ziele) | Die [!DNL Flow Service]-API wird zur Erfassung und Zentralisierung Ihrer Daten aus verschiedenen Quellen verwendet und dient zur Erstellung und Aktivierung von Daten an verschiedene Ziele in Adobe Experience Platform. Der Dienst stellt eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können. |
| [[!DNL Identity Service] API-Handbuch](.././identity-service/api/getting-started.md) | Die [!DNL Identity Service]-API ermöglicht es Entwicklern, geräteübergreifende, geräteübergreifende Kanal- und Echtzeitidentifizierung Ihrer Kunden mithilfe von Identitätsdiagrammen in Adobe Experience Platform zu verwalten. |
| [[!DNL Observability Insights] API-Handbuch](.././observability/api/overview.md) | [!DNL Observability Insights] ist eine RESTful-API, mit der Entwickler wichtige Kennzeichnungsmetriken in Adobe Experience Platform verfügbar machen können. Diese Metriken liefern Einblicke in Statistiken zur Platform-Nutzung, Systemdiagnosen für Platform-Dienste, historische Trends und Leistungsindikatoren für verschiedene Platform-Funktionen. |
| [[!DNL Policy Service] API-Handbuch](.././data-governance/api/overview.md) <br>  (Datenverwaltung) | Mit der API [!DNL Policy Service] können Sie Datenverwendungsbeschriftungen und -richtlinien erstellen und verwalten, um festzustellen, welche Marketingaktionen für Daten mit bestimmten Datenverwendungsbeschriftungen durchgeführt werden können. Informationen zum Anwenden von Bezeichnungen auf Datensätze und Felder finden Sie im Handbuch [[!DNL Dataset Service] API](.././data-governance/labels/dataset-api.md) |
| [[!DNL Privacy Service] API-Handbuch](.././privacy-service/api/getting-started.md) | Die [!DNL Privacy Service]-API ermöglicht es Entwicklern, Kundenanfragen zu erstellen und zu verwalten, um ihre personenbezogenen Daten in allen Experience Cloud-Anwendungen abzurufen oder zu löschen. Dabei gelten die gesetzlichen Datenschutzbestimmungen. |
| [[!DNL Query Service] API-Handbuch](.././query-service/api/getting-started.md) | Die [!DNL Query Service]-API ermöglicht Entwicklern die Abfrage ihrer Adobe Experience Platform-Daten mit Standard-SQL. |
| [[!DNL Real-time Customer Profile] API-Handbuch](.././profile/api/overview.md) | Die Echtzeit-Client-Profil-API ermöglicht es Entwicklern, Profil-Daten zu untersuchen und mit ihnen zu arbeiten, einschließlich Anzeigen von Profilen, Erstellen und Aktualisieren von Zusammenführungsrichtlinien, Exportieren oder Sampling-Profil-Daten und Löschen von Profil-Daten, die nicht mehr benötigt werden oder fehlerhaft hinzugefügt wurden. |
| [Handbuch zur Sandbox-API](.././sandboxes/api/getting-started.md) | Die Sandbox-API ermöglicht es Entwicklern, isolierte Virtual Sandbox-Umgebung in Adobe Experience Platform programmgesteuert zu verwalten. |
| [[!DNL Schema Registry] API-Handbuch](.././xdm/api/overview.md) <br>  (XDM) | Die [!DNL Schema Registry]-API ermöglicht es Entwicklern, alle Schema und zugehörigen XDM-Ressourcen (Experience Data Model) innerhalb von Adobe Experience Platform programmatisch zu verwalten. |
| [[!DNL Segmentation Service] API-Handbuch](.././segmentation/api/overview.md) | Die [!DNL Segmentation Service]-API ermöglicht es Entwicklern, Segmentierungsvorgänge in Adobe Experience Platform programmgesteuert zu verwalten. Dazu gehören das Erstellen von Segmenten und das Generieren von Audiencen aus Ihren Echtzeit-Daten zum Profil von Kunden. |
| [[!DNL Sensei Machine Learning] API-Handbuch](.././data-science-workspace/api/getting-started.md) <br>  (Data Science Workspace) | Die [!DNL Sensei Machine Learning]-API bietet Datenwissenschaftlern einen Mechanismus zum Organisieren und Verwalten von XML-Diensten (maschinelles Lernen), von der Algorithmusüberwachung über Experimentierung bis zur Dienstbereitstellung. |

Weitere Informationen zu spezifischen Endpunkten und Vorgängen, die für jeden Dienst verfügbar sind, finden Sie in der [API-Referenzdokumentation](http://www.adobe.com/go/platform-api-reference-en) zur Adobe I/O.

## Nächste Schritte

In diesem Dokument wurden die erforderlichen Kopfzeilen und verfügbaren Handbücher vorgestellt und ein API-Beispielaufruf bereitgestellt. Nachdem Sie die erforderlichen Header-Werte für API-Aufrufe unter Adobe Experience Platform verwendet haben, wählen Sie in der Tabelle [Plattform-API-Leitfäden](#api-guides) einen API-Endpunkt aus, den Sie untersuchen möchten.

Antworten auf häufig gestellte Fragen finden Sie im Handbuch [Plattformfehlerbehebung](troubleshooting.md).

Um eine Postman-Umgebung einzurichten und die verfügbaren Postman-Sammlungen zu erkunden, lesen Sie das [Platform Postman Guide](postman.md).

