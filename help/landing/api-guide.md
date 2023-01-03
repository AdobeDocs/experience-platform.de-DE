---
keywords: Experience Platform; Startseite; beliebte Themen; Adobe Experience Platform; API-Handbuch; Plattform-API-Handbuch; Einführung in die Plattform; Entwicklerhandbuch
solution: Experience Platform
title: Erste Schritte mit Adobe Experience Platform-APIs
topic-legacy: api guide
description: Adobe Experience Platform bietet API-Dienste, die eng miteinander verbunden sind. Dieses Handbuch enthält Informationen zu den verfügbaren Diensten, erforderlichen Kopfzeilen für CRUD-Vorgänge, Fehlermeldungen, Postman-Sammlungen und Beispiel-API-Aufrufen.
exl-id: a362bcb4-a908-43a8-abd3-0e1d21cb9117
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 30%

---

# Erste Schritte mit Adobe Experience Platform-APIs

Adobe Experience Platform wird unter der Philosophie &quot;API first&quot;entwickelt. Mit Platform-APIs können Sie programmatisch grundlegende CRUD-Vorgänge (Erstellen, Lesen, Aktualisieren, Löschen) für Daten durchführen, z. B. die Konfiguration berechneter Attribute, den Zugriff auf Daten/Entitäten, den Export von Daten, das Löschen nicht benötigter Daten oder Batches und mehr.

Die APIs für jeden Experience Platform-Dienst verwenden alle denselben Satz von Authentifizierungskopfzeilen und verwenden ähnliche Syntaxen für ihre CRUD-Vorgänge. Im folgenden Handbuch werden die erforderlichen Schritte für die ersten Schritte mit Platform-APIs beschrieben.

## Authentifizierung und Kopfzeilen

Um Platform-Endpunkte erfolgreich aufrufen zu können, müssen Sie die [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de). Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

### Sandbox-Kopfzeile

Alle Ressourcen in Experience Platform sind auf bestimmte virtuelle Sandboxes beschränkt. Für Anfragen an Platform-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- `x-sandbox-name: {SANDBOX_NAME}`

Weitere Informationen zu Sandboxes in Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../sandboxes/home.md).

### Content-Type-Kopfzeile

Alle Anfragen mit einer Payload im Anfragetext (wie POST-, PUT- und PATCH-Aufrufe) müssen eine `Content-Type`-Kopfzeile enthalten. Akzeptierte Werte sind für jeden API-Endpunkt spezifisch. Wenn eine bestimmte `Content-Type` -Wert für einen Endpunkt erforderlich ist, wird sein Wert in den Beispiel-API-Anfragen angezeigt, die von der [API-Handbücher für einzelne Platform-Dienste](#api-guides).

## Grundlagen der Experience Platform-API

Adobe Experience Platform-APIs setzen verschiedene zugrunde liegende Technologien und Syntaxen ein, die für eine effektive Verwaltung von Platform-Ressourcen wichtig sind.

Weitere Informationen zu den zugrunde liegenden API-Technologien, die von Platform verwendet werden, einschließlich Beispiel-JSON-Schemaobjekten, finden Sie unter [Grundlagen der Experience Platform-API](api-fundamentals.md) Handbuch.

## Postman-Sammlungen für Experience Platform-APIs

Postman ist eine Kooperationsplattform für die API-Entwicklung, mit der Sie Umgebungen mit vordefinierten Variablen einrichten, API-Sammlungen freigeben, CRUD-Anforderungen optimieren und vieles mehr. Die meisten Platform-API-Dienste verfügen über Postman-Sammlungen, die beim Ausführen von API-Aufrufen verwendet werden können.

Weitere Informationen zu Postman, einschließlich der Einrichtung einer Umgebung, einer Liste der verfügbaren Sammlungen und des Imports von Sammlungen, finden Sie unter [Dokumentation zu Platform Postman](postman.md).

## Lesen von Beispiel-API-Aufrufen {#sample-api}

Anfrageformate variieren je nach der verwendeten Platform-API. Am einfachsten erfahren Sie, wie Sie API-Aufrufe strukturieren können, indem Sie sich die in der Dokumentation die für einzelne Platform-Dienste angegebenen Beispiele ansehen.

Die Dokumentation für [!DNL Experience Platform] zeigt Beispiel-API-Aufrufe auf zwei verschiedene Arten. Zunächst wird der Aufruf im **API-Format** dargestellt, wobei es sich um eine Vorlagendarstellung handelt, die nur den Vorgang (GET, POST, PUT, PATCH, DELETE) und den verwendeten Endpunkt (z. B. `/global/classes`) zeigt. Manche Vorlagen zeigen auch die Stelle von Variablen an, um zu veranschaulichen, wie ein Aufruf formuliert werden sollte, z. B. `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

Die Aufrufe werden dann als cURL-Befehle in einer **Anfrage** angezeigt, die die erforderlichen Kopfzeilen und den vollständigen „Basispfad“ enthält, die für eine erfolgreiche Interaktion mit der API erforderlich sind. Der Basispfad sollte allen Endpunkten vorangestellt werden. Der oben genannte Endpunkt `/global/classes` beispielsweise ändert sich in `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. Sie sehen das API-Format/Anforderungsmuster in der gesamten Dokumentation und sollten den vollständigen Pfad verwenden, der in der Beispielanfrage angezeigt wird, wenn Sie eigene Aufrufe an Platform-APIs durchführen.

### Beispiel-API-Anfrage

Im Folgenden finden Sie eine Beispiel-API-Anfrage, die das Format veranschaulicht, mit dem Sie es in der Dokumentation zu tun haben werden.

**API-Format**

Das API-Format gibt Auskunft über den Vorgang (GET) und den verwendeten Endpunkt. Variablen werden durch geschweifte Klammern gekennzeichnet (in diesem Fall `{CONTAINER_ID}`).

```http
GET /{CONTAINER_ID}/classes
```

**Anfrage**

In dieser Beispielanfrage werden den Variablen aus dem API-Format tatsächliche Werte im Anfragepfad zugewiesen. Darüber hinaus werden alle erforderlichen Kopfzeilen entweder als Beispiel-Kopfzeilenwerte oder Variablen angezeigt, in die vertrauliche Informationen (wie Sicherheits-Token und Zugriffs-IDs) einbezogen werden sollen.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Die [Handbuch zur Fehlerbehebung bei Platform](troubleshooting.md#errors-and-troubleshooting) enthält eine Liste von Fehlern, die bei der Verwendung von Experience Platform-Diensten auftreten können.

Informationen zur Fehlerbehebung bei einzelnen Platform-Diensten finden Sie in den [Verzeichnis zur Fehlerbehebung bei Diensten](troubleshooting.md#service-troubleshooting-directory).

Weitere Informationen zu bestimmten Endpunkten in Platform-APIs, einschließlich erforderlicher Kopfzeilen und Anfragetexte, finden Sie im Abschnitt [Handbuch zur Platform-API](#api-guides).

## Handbuch zur Platform-API {#api-guides}

| API-Handbuch | Beschreibung |
| --- | --- |
| [[!DNL Access Control] API-Handbuch](.././access-control/api/getting-started.md) | Die [!DNL Access Control] API-Endpunkt kann aktuelle Richtlinien abrufen, die für einen Benutzer für bestimmte Ressourcen in einer angegebenen Sandbox gelten. Alle anderen Zugriffssteuerungsfunktionen werden über die [Adobe Admin Console](https://adminconsole.adobe.com/). |
| [Handbuch zur Batch-Aufnahme-API](.././ingestion/batch-ingestion/api-overview.md) | Die Adobe Experience Platform [!DNL Data Ingestion] Mit der API können Sie Daten als Batch-Dateien in Platform erfassen. Daten, die erfasst werden, können Profildaten aus einer reduzierten Datei in einem CRM-System (z. B. eine Parquet-Datei) oder Daten sein, die einem bekannten Schema in der Schema Registry (XDM) entsprechen. |
| [[!DNL Catalog Service] API-Handbuch](.././catalog/api/getting-started.md) | Die [!DNL Catalog Service] Mit der API können Entwickler Datensatzmetadaten in Adobe Experience Platform verwalten. Dazu gehören Datenspeicherorte, Verarbeitungsphasen, während der Verarbeitung aufgetretene Fehler und Datenberichte. |
| [[!DNL Data Access] API-Handbuch](.././data-access/api.md) | Die [!DNL Data Access] Mit der API können Entwickler Informationen zu erfassten Datensätzen in Experience Platform abrufen. Dazu gehören der Zugriff auf und das Herunterladen von Datensatzdateien, das Abrufen von Kopfzeileninformationen, das Auflisten fehlgeschlagener und erfolgreicher Batches sowie das Herunterladen von CSV-/Parquet-Vorschaudateien. |
| [[!DNL Dataset Service] API-Handbuch](.././data-governance/labels/dataset-api.md) | Mit der Datensatz-Service-API können Sie Nutzungsbezeichnungen für Datensätze anwenden und bearbeiten. Sie gehört zu den Datenkatalogfunktionen von Adobe Experience Platform, ist jedoch von der Katalog-Service-API getrennt, die Datensatz-Metadaten verwaltet. |
| [[!DNL Identity Service] API-Handbuch](.././identity-service/api/getting-started.md) | Die [!DNL Identity Service] Mit der API können Entwickler die geräteübergreifende, kanalübergreifende und nahe Echtzeit-Kundenidentifizierung mithilfe von Identitätsdiagrammen in Adobe Experience Platform verwalten. |
| [[!DNL Observability Insights] API-Handbuch](.././observability/api/overview.md) | [!DNL Observability Insights] ist eine RESTful-API, mit der Entwickler wichtige Beobachtbarkeitsmetriken in Adobe Experience Platform verfügbar machen können. Diese Metriken liefern Einblicke in Statistiken zur Platform-Nutzung, Systemdiagnosen für Platform-Dienste, historische Trends und Leistungsindikatoren für verschiedene Platform-Funktionen. |
| [[!DNL Policy Service] API-Handbuch](.././data-governance/api/overview.md) <br> (Data Governance) | Die [!DNL Policy Service] Mit der API können Sie Datennutzungsbezeichnungen und -richtlinien erstellen und verwalten, um zu bestimmen, welche Marketing-Aktionen für Daten mit bestimmten Datennutzungsbezeichnungen durchgeführt werden können. Informationen zum Anwenden von Bezeichnungen auf Datensätze und Felder finden Sie im Abschnitt [[!DNL Dataset Service] API](.././data-governance/labels/dataset-api.md) Handbuch |
| [[!DNL Privacy Service] API-Handbuch](.././privacy-service/api/getting-started.md) | Die [!DNL Privacy Service] Mit der API können Entwickler Kundenanfragen erstellen und verwalten, um in allen Experience Cloud-Applikationen auf ihre personenbezogenen Daten zuzugreifen oder diese zu löschen. Dies geschieht in Übereinstimmung mit den gesetzlichen Datenschutzbestimmungen. |
| [[!DNL Query Service] API-Handbuch](.././query-service/api/getting-started.md) | Die [!DNL Query Service] Mit der API können Entwickler ihre Adobe Experience Platform-Daten mithilfe von Standard-SQL abfragen. |
| [[!DNL Real-Time Customer Profile] API-Handbuch](.././profile/api/overview.md) | Die Echtzeit-Kundenprofil-API ermöglicht es Entwicklern, Profildaten zu untersuchen und damit zu arbeiten, einschließlich Anzeigen von Profilen, Erstellen und Aktualisieren von Zusammenführungsrichtlinien, Exportieren oder Sampling von Profildaten und Löschen von Profildaten, die nicht mehr benötigt werden oder fehlerhaft hinzugefügt wurden. |
| [Handbuch zur Sandbox-API](.././sandboxes/api/getting-started.md) | Mit der Sandbox-API können Entwickler isolierte virtuelle Sandbox-Umgebungen in Adobe Experience Platform programmgesteuert verwalten. |
| [[!DNL Schema Registry] API-Handbuch](.././xdm/api/overview.md) <br> (XDM) | Die [!DNL Schema Registry] Mit der API können Entwickler alle Schemas und zugehörigen Experience-Datenmodell (XDM)-Ressourcen in Adobe Experience Platform programmgesteuert verwalten. |
| [[!DNL Segmentation Service] API-Handbuch](.././segmentation/api/overview.md) | Die [!DNL Segmentation Service] Mit der API können Entwickler Segmentierungsvorgänge in Adobe Experience Platform programmgesteuert verwalten. Dazu gehört das Erstellen von Segmenten und das Generieren von Zielgruppen aus Ihren Echtzeit-Kundenprofildaten. |
| [[!DNL Sensei Machine Learning] API-Handbuch](.././data-science-workspace/api/getting-started.md) <br> (Data Science Workspace) | Die [!DNL Sensei Machine Learning] Die API bietet Datenwissenschaftlern einen Mechanismus zum Organisieren und Verwalten von ML-Diensten (Machine Learning), angefangen beim Onboarding von Algorithmen, Experimentieren und der Bereitstellung von Diensten. |

Weitere Informationen zu bestimmten Endpunkten und Vorgängen, die für jeden Dienst verfügbar sind, finden Sie im Abschnitt [API-Referenzdokumentation](https://www.adobe.com/go/platform-api-reference-en) auf Adobe I/O.

## Nächste Schritte

In diesem Dokument wurden die erforderlichen Kopfzeilen und verfügbaren Handbücher vorgestellt und ein Beispiel für einen API-Aufruf bereitgestellt. Nachdem Sie nun über die erforderlichen Kopfzeilenwerte verfügen, um API-Aufrufe in Adobe Experience Platform durchzuführen, wählen Sie einen API-Endpunkt aus, den Sie über [Tabelle mit Handbüchern für Platform-API](#api-guides).

Antworten auf häufig gestellte Fragen finden Sie im Abschnitt [Handbuch zur Fehlerbehebung bei Platform](troubleshooting.md).

Informationen zum Einrichten einer Postman-Umgebung und Erkunden der verfügbaren Postman-Sammlungen finden Sie im Abschnitt [Handbuch zu Platform Postman](postman.md).
