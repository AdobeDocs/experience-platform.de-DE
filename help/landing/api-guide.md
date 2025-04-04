---
keywords: Experience Platform;Startseite;beliebte Themen;Adobe Experience Platform;API-Handbuch;Platform-API-Handbuch;Einführung in Platform;Entwicklerhandbuch
solution: Experience Platform
title: Erste Schritte mit Adobe Experience Platform-APIs
description: Adobe Experience Platform bietet API-Services an, die eng miteinander verknüpft sind. Dieses Handbuch enthält Informationen zu den verfügbaren Services, erforderliche Kopfzeilen für CRUD-Vorgänge, Fehlermeldungen, Postman-Sammlungen und Beispiel-API-Aufrufe.
role: Developer
feature: API
exl-id: a362bcb4-a908-43a8-abd3-0e1d21cb9117
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 21%

---

# Erste Schritte mit Adobe Experience Platform-APIs

Adobe Experience Platform wird im Rahmen einer „API First“-Philosophie entwickelt. Mithilfe von Experience Platform-APIs können Sie programmgesteuert grundlegende CRUD-Vorgänge (Erstellen, Lesen, Aktualisieren, Löschen) für Daten durchführen, z. B. die Konfiguration berechneter Attribute, den Zugriff auf Daten/Entitäten, den Export von Daten, das Löschen nicht benötigter Daten oder Batches und mehr.

Die APIs für jeden Experience Platform-Service verwenden alle denselben Satz an Authentifizierungs-Headern und verwenden ähnliche Syntaxen für ihre CRUD-Vorgänge. Im folgenden Handbuch werden die erforderlichen Schritte für die ersten Schritte mit Experience Platform-APIs beschrieben.

## Authentifizierung und Header

Um Experience Platform-Endpunkte erfolgreich aufzurufen, müssen Sie das (Authentifizierungs[Tutorial) ](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de). Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

### Sandbox-Kopfzeile

Alle Ressourcen in Experience Platform sind auf bestimmte virtuelle Sandboxes beschränkt. Anfragen an Experience Platform-APIs erfordern eine Kopfzeile, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- `x-sandbox-name: {SANDBOX_NAME}`

Weitere Informationen zu Sandboxes in Experience Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../sandboxes/home.md).

### Inhaltstyp-Kopfzeile

Alle Anfragen mit einer Payload im Anfragetext (wie POST-, PUT- und PATCH-Aufrufe) müssen eine `Content-Type`-Kopfzeile enthalten. Akzeptierte Werte sind für jeden API-Endpunkt spezifisch. Wenn ein bestimmter `Content-Type` für einen Endpunkt benötigt wird, wird sein Wert in den Beispiel-API-Anfragen angezeigt, die von den [API-Handbüchern für einzelne Experience Platform-Services) ](#api-guides) werden.

## Experience Platform API-Grundlagen

Adobe Experience Platform-APIs verwenden verschiedene zugrunde liegende Technologien und Syntaxen, die für das effektive Verwalten von Experience Platform-Ressourcen wichtig sind.

Weitere Informationen zu den zugrunde liegenden API-Technologien, die Experience Platform verwendet, einschließlich Beispiel-JSON-Schemaobjekten, finden Sie im Handbuch [Grundlagen der Experience Platform-API](api-fundamentals.md).

## Postman-Sammlungen für Experience Platform-APIs

Postman ist eine Kollaborationsplattform für die API-Entwicklung, mit der Sie Umgebungen mit voreingestellten Variablen einrichten, API-Sammlungen freigeben, CRUD-Anfragen optimieren und vieles mehr. Die meisten Experience Platform-API-Services verfügen über Postman-Sammlungen, die Sie bei API-Aufrufen unterstützen können.

Weitere Informationen zu Postman, einschließlich der Einrichtung einer Umgebung, einer Liste der verfügbaren Sammlungen und des Imports von Sammlungen, finden Sie in der [Dokumentation zu Experience Platform Postman](postman.md).

## Lesen von Beispiel-API-Aufrufen {#sample-api}

Anfrageformate variieren je nach der verwendeten Experience Platform-API. Am einfachsten erfahren Sie, wie Sie API-Aufrufe strukturieren können, indem Sie sich die in der Dokumentation für einzelne Experience Platform-Services angegebenen Beispiele ansehen.

Die Dokumentation für [!DNL Experience Platform] zeigt Beispiel-API-Aufrufe auf zwei verschiedene Arten. Zunächst wird der Aufruf im **API-Format** dargestellt, wobei es sich um eine Vorlagendarstellung handelt, die nur den Vorgang (GET, POST, PUT, PATCH, DELETE) und den verwendeten Endpunkt (z. B. `/global/classes`) zeigt. Manche Vorlagen zeigen auch die Stelle von Variablen an, um zu veranschaulichen, wie ein Aufruf formuliert werden sollte, z. B. `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

Die Aufrufe werden dann als cURL-Befehle in einer **Anfrage** angezeigt, die die erforderlichen Kopfzeilen und den vollständigen „Basispfad“ enthält, die für eine erfolgreiche Interaktion mit der API erforderlich sind. Der Basispfad sollte allen Endpunkten vorangestellt werden. Der oben genannte Endpunkt `/global/classes` beispielsweise ändert sich in `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. In der gesamten Dokumentation wird das API-Format-/Anfragemuster angezeigt. Es wird erwartet, dass Sie den vollständigen Pfad verwenden, der in der Beispielanfrage angezeigt wird, wenn Sie Ihre eigenen Aufrufe an Experience Platform-APIs durchführen.

### Beispiel-API-Anfrage

Im Folgenden finden Sie eine Beispiel-API-Anfrage, die das Format veranschaulicht, mit dem Sie es in der Dokumentation zu tun haben werden.

**API-Format**

Das API-Format gibt Auskunft über den Vorgang (GET) und den verwendeten Endpunkt. Variablen werden durch geschweifte Klammern gekennzeichnet (in diesem Fall `{CONTAINER_ID}`).

```http
GET /{CONTAINER_ID}/classes
```

**Anfrage**

In dieser Beispielanfrage werden den Variablen aus dem API-Format tatsächliche Werte im Anfragepfad zugewiesen. Darüber hinaus werden alle erforderlichen Kopfzeilen entweder als Beispiel-Kopfzeilenwerte oder als Variablen angezeigt, in denen sensible Informationen (wie Sicherheits-Token und Zugriffs-IDs) enthalten sein sollten.

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

Das [Handbuch zur Fehlerbehebung bei Experience Platform](troubleshooting.md#errors-and-troubleshooting) enthält eine Liste von Fehlern, auf die Sie bei der Verwendung von Experience Platform-Services stoßen können.

Hinweise zur Fehlerbehebung bei einzelnen Experience Platform-Services finden Sie unter [Verzeichnis zur Fehlerbehebung bei Services](troubleshooting.md#service-troubleshooting-directory).

Weitere Informationen zu bestimmten Endpunkten in Experience Platform-APIs, einschließlich erforderlicher Kopfzeilen und Anfragetexte, finden Sie in den [Experience Platform-API-Handbüchern](#api-guides).

## Experience Platform-API-Handbücher {#api-guides}

| API-Handbuch | Beschreibung |
| --- | --- |
| [[!DNL Access Control] API-Handbuch](.././access-control/api/getting-started.md) | Der [!DNL Access Control]-API-Endpunkt kann aktuelle Richtlinien abrufen, die für einen Benutzer in Bezug auf bestimmte Ressourcen innerhalb einer angegebenen Sandbox gelten. Alle anderen Zugriffssteuerungsfunktionen werden über die [Adobe Admin Console](https://adminconsole.adobe.com/) bereitgestellt. |
| [Handbuch zur Batch-Aufnahme-API](.././ingestion/batch-ingestion/api-overview.md) | Mit der Adobe Experience Platform [!DNL Data Ingestion]-API können Sie Daten als Batch-Dateien in Experience Platform aufnehmen. Bei den aufgenommenen Daten kann es sich um Profildaten aus einer flachen Datei in einem CRM-System (z. B. einer Parquet-Datei) oder um Daten handeln, die einem bekannten Schema in der Schemaregistrierung (XDM) entsprechen. |
| [[!DNL Catalog Service] API-Handbuch](.././catalog/api/getting-started.md) | Mit der [!DNL Catalog Service]-API können Entwicklerinnen und Entwickler Datensatz-Metadaten in Adobe Experience Platform verwalten. Dazu gehören Datenspeicherorte, Verarbeitungsstadien, bei der Verarbeitung aufgetretene Fehler und Datenberichte. |
| [[!DNL Data Access] API-Handbuch](.././data-access/api.md) | Mit der [!DNL Data Access]-API können Entwicklerinnen und Entwickler Informationen zu aufgenommenen Datensätzen in Experience Platform abrufen. Dazu gehören der Zugriff auf und das Herunterladen von Datensatzdateien, das Abrufen von Kopfzeileninformationen, das Auflisten fehlgeschlagener und erfolgreicher Batches und das Herunterladen von CSV-/Parquet-Vorschaudateien. |
| [[!DNL Dataset Service] API-Handbuch](.././data-governance/labels/dataset-api.md) | Mit der Datensatz-Service-API können Sie Nutzungsbezeichnungen für Datensätze anwenden und bearbeiten. Sie gehört zu den Datenkatalogfunktionen von Adobe Experience Platform, ist jedoch von der Katalog-Service-API getrennt, die Datensatz-Metadaten verwaltet. |
| [[!DNL Data Hygiene API guide]](../hygiene/api/overview.md) | Mit der [!DNL Data Hygiene]-API können Sie die in Adobe Experience Platform gespeicherten personenbezogenen Daten Ihrer Kunden programmgesteuert korrigieren oder löschen sowie Ablaufdaten für Datensätze planen. |
| [[!DNL Edge Network Server] API-Handbuch](../server-api/overview.md) | Die [!DNL Edge Network Server API] kann für eine Vielzahl von Datenerfassungs-, Personalisierungs-, Werbe- und Marketing-Anwendungsfällen verwendet werden. Die [!DNL Server API] kann auf Servern, [!DNL IoT], Set-Top-Boxen und einer Vielzahl anderer Geräte verwendet werden. |
| [[!DNL Identity Service] API-Handbuch](.././identity-service/api/getting-started.md) | Mit der [!DNL Identity Service]-API können Entwicklerinnen und Entwickler die geräte- und kanalübergreifende, nahezu in Echtzeit ausgeführte Identifizierung Ihrer Kundinnen und Kunden mithilfe von Identitätsdiagrammen in Adobe Experience Platform verwalten. |
| [[!DNL MTLS Service API guide]](../data-governance/mtls-api/overview.md) | Mit der [!DNL MTLS Service]-API können Sie öffentliche Zertifikate, die von Adobe für Ihr Unternehmen ausgestellt wurden, sicher abrufen. |
| [[!DNL Observability Insights] API-Handbuch](.././observability/api/overview.md) | [!DNL Observability Insights] ist eine RESTful-API, mit der Entwickelnde Schlüsselmetriken zur Beobachtung in Adobe Experience Platform bereitstellen können. Diese Metriken liefern Einblicke in Statistiken zur Nutzung von Experience Platform, Systemdiagnosen für Experience Platform-Services, historische Trends und Leistungsindikatoren für verschiedene Experience Platform-Funktionen. |
| [[!DNL Policy Service] API-Handbuch](.././data-governance/api/overview.md) <br> (Data Governance) | Mit der [!DNL Policy Service]-API können Sie Datennutzungskennzeichnungen und -richtlinien erstellen und verwalten, um festzulegen, welche Marketing-Aktionen für Daten durchgeführt werden können, die bestimmte Datennutzungskennzeichnungen enthalten. Informationen zum Anwenden von Kennzeichnungen auf Datensätze und Felder finden Sie im [[!DNL Dataset Service] API](.././data-governance/labels/dataset-api.md)Handbuch |
| [[!DNL Privacy Service] API-Handbuch](.././privacy-service/api/getting-started.md) | Mit der [!DNL Privacy Service]-API können Entwickler Kundenanfragen erstellen und verwalten, um in allen Experience Cloud-Anwendungen unter Einhaltung gesetzlicher Datenschutzbestimmungen auf ihre personenbezogenen Daten zuzugreifen oder sie zu löschen. |
| [[!DNL Query Service] API-Handbuch](.././query-service/api/getting-started.md) | Mit der [!DNL Query Service]-API können Entwickler ihre Adobe Experience Platform-Daten mit Standard-SQL abfragen. |
| [[!DNL Real-Time Customer Profile] API-Handbuch](.././profile/api/overview.md) | Mit der Echtzeit-Kundenprofil-API können Entwickler Profildaten untersuchen und mit ihnen arbeiten, einschließlich der Anzeige von Profilen, der Erstellung und Aktualisierung von Zusammenführungsrichtlinien, des Exports oder Samplings von Profildaten und des Löschens von Profildaten, die nicht mehr erforderlich sind oder irrtümlich hinzugefügt wurden. |
| [Sandbox-API-Handbuch](.././sandboxes/api/getting-started.md) | Mit der Sandbox-API können Entwickler isolierte virtuelle Sandbox-Umgebungen in Adobe Experience Platform programmgesteuert verwalten. |
| [[!DNL Schema Registry] API-Handbuch](.././xdm/api/overview.md) <br> (XDM) | Mit der [!DNL Schema Registry]-API können Entwicklerinnen und Entwickler alle Schemas und zugehörigen Experience-Datenmodell (XDM)-Ressourcen in Adobe Experience Platform programmgesteuert verwalten. |
| [[!DNL Segmentation Service] API-Handbuch](.././segmentation/api/overview.md) | Mit der [!DNL Segmentation Service]-API können Entwicklerinnen und Entwickler Segmentierungsvorgänge in Adobe Experience Platform programmgesteuert verwalten. Dazu gehört das Erstellen von Segmenten und das Generieren von Zielgruppen aus Ihren Echtzeit-Kundenprofildaten. |
| [[!DNL Sensei Machine Learning] API-Handbuch](.././data-science-workspace/api/getting-started.md) <br> (Data Science Workspace) | Die [!DNL Sensei Machine Learning]-API bietet Datenwissenschaftlern einen Mechanismus zum Organisieren und Verwalten von ML-Services (maschinelles Lernen), von der Einführung von Algorithmen über Experimente bis hin zur Bereitstellung von Services. |

Weitere Informationen zu bestimmten Endpunkten und Vorgängen, die für jeden Service verfügbar sind, finden Sie in der [API-Referenzdokumentation](https://www.adobe.com/go/platform-api-reference-en) auf Adobe I/O.

## Nächste Schritte

In diesem Dokument wurden die erforderlichen Kopfzeilen und verfügbaren Handbücher vorgestellt und ein Beispiel für einen API-Aufruf bereitgestellt. Nachdem Sie nun über die erforderlichen Kopfzeilenwerte verfügen, die für API-Aufrufe auf Adobe Experience Platform erforderlich sind, wählen Sie einen zu untersuchenden API-Endpunkt aus der Tabelle [Experience Platform-API-Handbücher](#api-guides).

Antworten auf häufig gestellte Fragen finden Sie im [Handbuch zur Fehlerbehebung bei Experience Platform](troubleshooting.md).

Informationen zum Einrichten einer Postman-Umgebung und zum Untersuchen der verfügbaren Postman-Sammlungen finden Sie im [Handbuch zu Experience Platform Postman](postman.md).
