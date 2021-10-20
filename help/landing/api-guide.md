---
keywords: Experience Platform;Home;beliebte Themen;Adobe Experience Platform;API-Leitfaden;Plattform-API-Leitfaden;Einführung in die Plattform;Entwicklerleitfaden
solution: Experience Platform
title: Erste Schritte mit Adobe Experience Platform APIs
topic-legacy: api guide
description: Adobe Experience Platform bietet API-Dienste an, die eng miteinander verbunden sind. Dieses Handbuch enthält Informationen zu den verfügbaren Diensten, erforderlichen Kopfzeilen für CRUD-Operationen, Fehlermeldungen, Postman-Sammlungen und Beispiel-API-Aufrufen.
exl-id: a362bcb4-a908-43a8-abd3-0e1d21cb9117
source-git-commit: e62e4e3a12ad2a85de5b10c60fde3618cde84c4b
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 30%

---

# Erste Schritte mit Adobe Experience Platform APIs

Adobe Experience Platform wird unter der Philosophie &quot;API first&quot; entwickelt. Mithilfe von Plattform-APIs können Sie programmgesteuert grundlegende CRUD-Vorgänge (Erstellen, Lesen, Aktualisieren, Löschen) mit Daten durchführen, z. B. die Konfiguration berechneter Attribute, den Zugriff auf Daten/Entitäten, den Export von Daten, das Löschen nicht benötigter Daten oder Stapel und vieles mehr.

Die APIs für jeden Experience Platform-Dienst verwenden alle denselben Satz von Authentifizierungskopfzeilen und verwenden ähnliche Syntaxen für ihre CRUD-Operationen. Im folgenden Handbuch werden die notwendigen Schritte für die ersten Schritte mit Platform APIs beschrieben.

## Authentifizierung und Überschriften

Um erfolgreich Aufrufe von Plattformendpunkten durchführen zu können, müssen Sie [Authentifizierungslehrgang](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de#platform-apis). Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

### Sandbox-Kopfzeile

Alle Ressourcen in Experience Platform sind auf bestimmte virtuelle Sandboxes beschränkt. Für Anfragen an Platform-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- `x-sandbox-name: {SANDBOX_NAME}`

Weitere Informationen zu Sandboxes in Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../sandboxes/home.md).

### Inhaltstyp-Kopfzeile

Alle Anfragen mit einer Payload im Anfragetext (wie POST-, PUT- und PATCH-Aufrufe) müssen eine `Content-Type`-Kopfzeile enthalten. Akzeptierte Werte sind für jeden API-Endpunkt spezifisch. Wenn eine bestimmte `Content-Type` Wert für einen Endpunkt erforderlich ist, wird der Wert in den Beispiel-API-Anforderungen angezeigt, die von der [API-Leitfäden für einzelne Plattformdienste](#api-guides).

## Grundlagen der Experience Platform-API

Adobe Experience Platform-APIs verwenden mehrere zugrunde liegende Technologien und Syntaxen, die für eine effiziente Verwaltung der Plattformressourcen wichtig sind.

Weitere Informationen zu den zugrunde liegenden API-Technologien, die von der Plattform verwendet werden, einschließlich JSON-Schema-Objekten, finden Sie unter [Experience Platform-API-Grundlagen](api-fundamentals.md) Leitfaden.

## Postman-Sammlungen für Experience Platform-APIs

Postman ist eine Kooperationsplattform für die API-Entwicklung, mit der Sie Umgebung mit vorgegebenen Variablen einrichten, API-Sammlungen freigeben, CRUD-Anforderungen optimieren und vieles mehr. Die meisten Platform API-Dienste verfügen über Postman-Sammlungen, die bei der Erstellung von API-Aufrufen verwendet werden können.

Weitere Informationen über Postman, wie Sie eine Umgebung einrichten, eine Liste der verfügbaren Sammlungen und das Importieren von Sammlungen, finden Sie unter [Platform Postman-Dokumentation](postman.md).

## Lesen von Beispiel-API-Aufrufen {#sample-api}

Anfrageformate variieren je nach der verwendeten Platform-API. Am einfachsten erfahren Sie, wie Sie API-Aufrufe strukturieren können, indem Sie sich die in der Dokumentation die für einzelne Platform-Dienste angegebenen Beispiele ansehen.

Die Dokumentation für [!DNL Experience Platform] zeigt Beispiel-API-Aufrufe auf zwei verschiedene Arten an. Zunächst wird der Aufruf im **API-Format** dargestellt, wobei es sich um eine Vorlagendarstellung handelt, die nur den Vorgang (GET, POST, PUT, PATCH, DELETE) und den verwendeten Endpunkt (z. B. `/global/classes`) zeigt. Manche Vorlagen zeigen auch die Stelle von Variablen an, um zu veranschaulichen, wie ein Aufruf formuliert werden sollte, z. B. `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

Die Aufrufe werden dann als cURL-Befehle in einer **Anfrage** angezeigt, die die erforderlichen Kopfzeilen und den vollständigen „Basispfad“ enthält, die für eine erfolgreiche Interaktion mit der API erforderlich sind. Der Basispfad sollte allen Endpunkten vorangestellt werden. Der oben genannte Endpunkt `/global/classes` beispielsweise ändert sich in `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. Das API-Format/Anforderungsmuster wird in der gesamten Dokumentation angezeigt und es wird erwartet, dass Sie den vollständigen Pfad verwenden, der in der Beispielanforderung angezeigt wird, wenn Sie Ihre eigenen Aufrufe an Platform APIs durchführen.

### Beispiel-API-Anfrage

Im Folgenden finden Sie eine Beispiel-API-Anfrage, die das Format veranschaulicht, mit dem Sie es in der Dokumentation zu tun haben werden.

**API-Format**

Das API-Format gibt Auskunft über den Vorgang (GET) und den verwendeten Endpunkt. Variablen werden durch geschweifte Klammern gekennzeichnet (in diesem Fall `{CONTAINER_ID}`).

```http
GET /{CONTAINER_ID}/classes
```

**Anfrage**

In dieser Beispielanfrage werden den Variablen aus dem API-Format tatsächliche Werte im Anfragepfad zugewiesen. Außerdem werden alle erforderlichen Kopfzeilen entweder als Beispiel-Kopfzeilenwerte oder als Variablen angezeigt, in die sensible Informationen (wie Sicherheits-Token und Zugriffs-IDs) aufgenommen werden sollen.

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

Die [Handbuch zur Fehlerbehebung für Plattformen](troubleshooting.md#errors-and-troubleshooting) stellt eine Liste von Fehlern bereit, auf die Sie bei der Verwendung eines beliebigen Experience Platform-Diensts stoßen können.

Informationen zur Fehlerbehebung bei einzelnen Plattformdiensten finden Sie in den [Verzeichnis zur Fehlerbehebung für Dienst](troubleshooting.md#service-troubleshooting-directory).

Weitere Informationen zu bestimmten Endpunkten in Plattform-APIs, einschließlich erforderlicher Kopfzeilen und Anforderungskörper, finden Sie im [API-Leitfäden](#api-guides).

## API-Leitfäden {#api-guides}

| API-Handbuch | Beschreibung |
| --- | --- |
| [[!DNL Access Control] API-Handbuch](.././access-control/api/getting-started.md) | Die [!DNL Access Control] API-Endpunkt kann aktuelle Richtlinien abrufen, die für einen Benutzer bei bestimmten Ressourcen in einer angegebenen Sandbox gelten. Alle anderen Funktionen der Zugriffskontrolle werden über [Adobe Admin Console](https://adminconsole.adobe.com/). |
| [Handbuch zur Batch-Erfassung-API](.././ingestion/batch-ingestion/api-overview.md) | Die Adobe Experience Platform [!DNL Data Ingestion] API ermöglicht das Erfassen von Daten in Platform als Batch-Dateien. Daten, die erfasst werden, können Profil-Daten aus einer einfachen Datei in einem CRM-System (z. B. einer Parquet-Datei) oder Daten sein, die einem bekannten Schema in der Schema-Registrierung (XDM) entsprechen. |
| [[!DNL Catalog Service] API-Handbuch](.././catalog/api/getting-started.md) | Die [!DNL Catalog Service] API ermöglicht Entwicklern die Verwaltung von DataSet-Metadaten in Adobe Experience Platform. Dazu gehören Datenpositionen, Verarbeitungsphasen, während der Verarbeitung aufgetretene Fehler und Datenberichte. |
| [[!DNL Data Access] API-Handbuch](.././data-access/api.md) | Die [!DNL Data Access] API ermöglicht es Entwicklern, Informationen über ingetierte Datensätze in der Experience Platform abzurufen. Dazu gehören der Zugriff auf und das Herunterladen von DataSet-Dateien, das Abrufen von Header-Informationen, das Auflisten fehlgeschlagener und erfolgreicher Stapel sowie das Herunterladen von Vorschau-CSV-/Parquet-Dateien. |
| [[!DNL Dataset Service] API-Handbuch](.././data-governance/labels/dataset-api.md) | Mit der Datensatz-Service-API können Sie Nutzungsbezeichnungen für Datensätze anwenden und bearbeiten. Sie gehört zu den Datenkatalogfunktionen von Adobe Experience Platform, ist jedoch von der Katalog-Service-API getrennt, die Datensatz-Metadaten verwaltet. |
| [[!DNL Identity Service] API-Handbuch](.././identity-service/api/getting-started.md) | Die [!DNL Identity Service] API ermöglicht Entwicklern die Verwaltung des geräteübergreifenden, geräteübergreifenden Kanals und der nahtlosen Echtzeit-Kundenidentifizierung mithilfe von Identitätsdiagrammen in Adobe Experience Platform. |
| [[!DNL Observability Insights] API-Handbuch](.././observability/api/overview.md) | [!DNL Observability Insights] ist eine RESTful-API, die es Entwicklern ermöglicht, wichtige Kennzahlen in Adobe Experience Platform anzuzeigen. Diese Metriken liefern Einblicke in Statistiken zur Platform-Nutzung, Systemdiagnosen für Platform-Dienste, historische Trends und Leistungsindikatoren für verschiedene Platform-Funktionen. |
| [[!DNL Policy Service] API-Handbuch](.././data-governance/api/overview.md) <br> (Datenverwaltung) | Die [!DNL Policy Service] API ermöglicht die Erstellung und Verwaltung von Bezeichnungen und Richtlinien zur Datenauslastung, um zu bestimmen, welche Marketingaktionen mit Daten durchgeführt werden können, die bestimmte Bezeichnungen zur Datenauslastung enthalten. Informationen zum Anwenden von Beschriftungen auf Datensätze und Felder finden Sie in der [[!DNL Dataset Service] API](.././data-governance/labels/dataset-api.md) Guide |
| [[!DNL Privacy Service] API-Handbuch](.././privacy-service/api/getting-started.md) | Die [!DNL Privacy Service] API ermöglicht es Entwicklern, Kundenanfragen zu erstellen und zu verwalten, um in Experience Cloud-Applikationen auf ihre personenbezogenen Daten zuzugreifen oder sie zu löschen, und zwar unter Einhaltung der gesetzlichen Datenschutzbestimmungen. |
| [[!DNL Query Service] API-Handbuch](.././query-service/api/getting-started.md) | Die [!DNL Query Service] API ermöglicht Entwicklern die Abfrage ihrer Adobe Experience Platform-Daten mithilfe von Standard-SQL. |
| [[!DNL Real-time Customer Profile] API-Handbuch](.././profile/api/overview.md) | Die Echtzeit-Customer-Profil-API ermöglicht es Entwicklern, Profil-Daten zu erforschen und mit ihnen zu arbeiten. Dazu gehören das Anzeigen von Profilen, das Erstellen und Aktualisieren von Zusammenführungsrichtlinien, das Exportieren oder Sammeln von Profil-Daten und das Löschen von Profil-Daten, die nicht mehr benötigt werden oder fehlerhaft hinzugefügt wurden. |
| [Sandbox-API-Handbuch](.././sandboxes/api/getting-started.md) | Die Sandbox-API ermöglicht es Entwicklern, isolierte Virtual Sandbox-Umgebung in Adobe Experience Platform programmgesteuert zu verwalten. |
| [[!DNL Schema Registry] API-Handbuch](.././xdm/api/overview.md) <br> (XDM) | Die [!DNL Schema Registry] API ermöglicht Entwicklern die programmgesteuerte Verwaltung aller Schema und zugehörigen XDM-Ressourcen (Experience Data Model) innerhalb von Adobe Experience Platform. |
| [[!DNL Segmentation Service] API-Handbuch](.././segmentation/api/overview.md) | Die [!DNL Segmentation Service] API ermöglicht es Entwicklern, Segmentierungsoperationen in Adobe Experience Platform programmgesteuert zu verwalten. Dazu gehören das Erstellen von Segmenten und das Generieren von Audiencen aus den Daten Ihres Echtzeit-Profils. |
| [[!DNL Sensei Machine Learning] API-Handbuch](.././data-science-workspace/api/getting-started.md) <br> (Data Science Workspace) | Die [!DNL Sensei Machine Learning] API bietet einen Mechanismus für Datenwissenschaftler, um maschinelles Lernen (ML) von Algorithmus-Onboarding-, Experimentierungs- und Service-Bereitstellungen zu organisieren und zu verwalten. |

Weitere Informationen zu bestimmten Endpunkten und verfügbaren Vorgängen für jeden Dienst finden Sie im [API-Referenzdokumentation](https://www.adobe.com/go/platform-api-reference-en) auf Adobe I/O.

## Nächste Schritte

In diesem Dokument wurden die erforderlichen Kopfzeilen und verfügbaren Leitfäden vorgestellt und ein API-Beispielaufruf bereitgestellt. Wählen Sie einen API-Endpunkt aus dem [Tabelle mit API-Hilfslinien](#api-guides).

Antworten auf häufig gestellte Fragen finden Sie im [Handbuch zur Fehlerbehebung für Plattformen](troubleshooting.md).

Weitere Informationen zum Einrichten einer Postman-Umgebung und zum Erforschen der verfügbaren Postman-Sammlungen finden Sie im [Plattform-Postleitfaden](postman.md).
