---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Häufig gestellte Fragen zu Adobe Experience Platform und Handbuch zur Fehlerbehebung
topic: getting started
translation-type: tm+mt
source-git-commit: 635f8cf8173cc7db2032f2181848b0ce1e9095cc
workflow-type: tm+mt
source-wordcount: '1962'
ht-degree: 77%

---


# [!DNL Platform] FAQ und Handbuch zur Fehlerbehebung

This document provides answers to frequently asked questions about Adobe Experience Platform, as well as a high-level troubleshooting guide for common errors that may be encountered in any [!DNL Experience Platform] API. For troubleshooting guides on individual [!DNL Platform] services, see the [service troubleshooting directory](#service-troubleshooting-directory) below.

## FAQs {#faq}

Im Folgenden finden Sie eine Liste von Antworten auf häufig gestellte Fragen zu Adobe Experience Platform.

## Was sind [!DNL Experience Platform] APIs? {#what-are-experience-platform-apis}

[!DNL Experience Platform] Angebot mehrerer RESTful-APIs, die HTTP-Anforderungen für den Zugriff auf [!DNL Platform] Ressourcen verwenden. Diese Dienst-APIs machen jeweils verschiedene Endpunkte verfügbar und ermöglichen Ihnen das Auflisten (GET), Nachschlagen (GET), Bearbeiten (PUT und/oder PATCH) und Löschen (DELETE) von Ressourcen. Weiterführende Informationen zu einzelnen Endpunkten und Vorgängen, die bei den jeweiligen Diensten verfügbar sind, finden Sie in der [API-Referenzdokumentation](https://www.adobe.io/apis/experienceplatform/home/api-reference.html) in Adobe I/O.

## Wie kann ich eine API-Anfrage formatieren? {#how-do-i-format-an-api-request}

Request formats vary depending on the [!DNL Platform] API being used. The best way to learn how to structure your API calls is by following along with the examples provided in the documentation for the particular [!DNL Platform] service you are using.

### Lesen von Beispiel-API-Aufrufen

The documentation for [!DNL Experience Platform] shows example API calls in two different ways. Zunächst wird der Aufruf im **API-Format** dargestellt, wobei es sich um eine Vorlagendarstellung handelt, die nur den Vorgang (GET, POST, PUT, PATCH, DELETE) und den verwendeten Endpunkt (z. B. `/global/classes`) zeigt. Manche Vorlagen zeigen auch die Stelle von Variablen an, um zu veranschaulichen, wie ein Aufruf formuliert werden sollte, z. B. `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

Die Aufrufe werden dann als cURL-Befehle in einer **Anfrage** angezeigt, die die erforderlichen Kopfzeilen und den vollständigen „Basispfad“ enthält, die für eine erfolgreiche Interaktion mit der API erforderlich sind. Der Basispfad sollte allen Endpunkten vorangestellt werden. Der oben genannte Endpunkt `/global/classes` beispielsweise ändert sich in `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. Sie werden das API-Format/Anfragemuster in der Dokumentation immer wieder sehen. Es wird erwartet, dass Sie den vollständigen Pfad verwenden, der in der Beispielanfrage dargestellt ist, wenn Sie eigene Aufrufe an Platform-APIs ausführen.

### Beispiel-API-Anfrage

Im Folgenden finden Sie eine Beispiel-API-Anfrage, die das Format veranschaulicht, mit dem Sie es in der Dokumentation zu tun haben werden.

**API-Format**

Das API-Format gibt Auskunft über den Vorgang (GET) und den verwendeten Endpunkt. Variablen werden durch geschweifte Klammern gekennzeichnet (in diesem Fall `{CONTAINER_ID}`).

```http
GET /{CONTAINER_ID}/classes
```

**Anfrage**

In dieser Beispielanfrage werden den Variablen aus dem API-Format tatsächliche Werte im Anfragepfad zugewiesen. Außerdem werden alle erforderlichen Kopfzeilen angezeigt, entweder als beispielhafte Kopfzeilenwerte oder als Variablen, in die vertrauliche Daten (wie Sicherheits-Token und Zugriffskennungen) einbezogen werden sollen.

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

Weiterführende Informationen zu einzelnen Endpunkten in Platform-APIs, einschließlich erforderlicher Kopfzeilen und Anfragetexte, finden Sie in der [API-Referenzdokumentation](https://www.adobe.io/apis/experienceplatform/home/api-reference.html).

## Was ist meine IMS-Organisation? {#what-is-my-ims-organization}

Eine IMS-Organisation ist eine Adobe-Darstellung eines Kunden. Alle lizenzierten Adobe-Lösungen sind in diese Kundenorganisation integriert. When an IMS organization is entitled to [!DNL Experience Platform], it can assign access to developers. Die IMS-Organisations-ID (`x-gw-ims-org-id`) stellt die Organisation dar, für die ein API-Aufruf ausgeführt werden soll, und ist daher in allen API-Anfragen als Kopfzeile obligatorisch. This ID can be found through the [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui): in the **Integrations** tab, navigate to the **Overview** section for any particular integration to find the ID under **Client Credentials**. For a step-by-step walkthrough of how to authenticate into [!DNL Platform], see the [authentication tutorial](../tutorials/authentication.md).

## Wo finde ich meinen API-Schlüssel? {#where-can-i-find-my-api-key}

In allen API-Anfragen ist ein API-Schlüssel als Kopfzeile erforderlich. It can be found through the [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). Navigieren Sie in der Konsole auf der Registerkarte **Integrationen** zum Abschnitt **Übersicht** einer bestimmten Integration; Sie finden den Schlüssel dann unter **Client-Anmeldedaten**. For a step-by-step walkthrough of how to authenticate to [!DNL Platform], see the [authentication tutorial](../tutorials/authentication.md).

## Woher bekomme ich ein Zugriffstoken? {#how-do-i-get-an-access-token}

Zugriffstoken sind in der Autorisierungskopfzeile aller API-Aufrufe erforderlich. Sie können mit einem `curl`-Befehl generiert werden, vorausgesetzt, Sie haben Zugriff auf eine Integration für eine IMS-Organisation. Zugriffstoken sind nur 24 Stunden lang gültig. Danach muss ein neues Token generiert werden, wenn Sie die API weiter verwenden möchten. Weiterführende Informationen zum Generieren von Zugriffstoken finden Sie im [Authentifizierungs-Tutorial](../tutorials/authentication.md).

## Wie verwende ich Abfrageparameter? {#how-do-i-user-query-parameters}

Some [!DNL Platform] API endpoints accept query parameters to locate specific information and filter the results returned in the response. Abfrageparameter werden mit einem Fragezeichen (`?`) an Anfragepfade angehängt, gefolgt von einem oder mehreren Abfrageparametern im Format `paramName=paramValue`. Wenn Sie mehrere Parameter in einem einzelnen Aufruf nutzen möchten, müssen Sie ein kaufmännisches Und-Zeichen (`&`) verwenden, um einzelne Parameter voneinander zu trennen. Das folgende Beispiel zeigt, wie eine Anfrage, bei der mehrere Abfrageparameter zum Einsatz kommen, in der Dokumentation dargestellt wird.

Beispiele für häufig verwendete Abfrageparameter sind:

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Detaillierte Informationen dazu, welche Abfragen bei einem bestimmten Dienst oder Endpunkt verfügbar sind, finden Sie in der dienstspezifischen Dokumentation.

## Wie gebe ich ein JSON-Feld an, das in einer PATCH-Anfrage aktualisiert werden soll? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

Many PATCH operations in [!DNL Platform] APIs use [JSON Pointer](https://tools.ietf.org/html/rfc6901) strings to indicate JSON properties to update. Diese werden normalerweise im [JSON Patch](https://tools.ietf.org/html/rfc6902)-Format in Anfrage-Payloads eingebunden. Weiterführende Informationen zur für diese Technologien erforderlichen Syntax finden Sie im [API-Grundlagenhandbuch](api-fundamentals.md).

## Can I use Postman to make calls to [!DNL Platform] APIs? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.getpostman.com/) ist ein hilfreiches Tool zur Visualisierung von Aufrufen an RESTful-APIs. This [Medium post](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) describes how you can set up Postman to automatically perform authentication and use it to consume [!DNL Experience Platform] APIs.

## Welche Systemanforderungen gelten für [!DNL Platform]? {#what-are-the-system-requirements-for-platform}

Je nachdem, ob Sie die Benutzeroberfläche oder API verwenden, gelten die folgenden Systemanforderungen:

**Für UI-basierte Vorgänge:**
- Ein moderner, standardmäßiger Webbrowser. While the latest version of [!DNL Chrome] is recommended, current and previous major releases of [!DNL Firefox], [!DNL Internet Explorer], and Safari are also supported.
   - Each time a new major version is released, [!DNL Platform] starts supporting the most recent version while support for the third most recent version is dropped.
- Bei allen Browsern müssen Cookies und JavaScript aktiviert sein.

**Für Interaktionen mit APIs und Entwicklern:**
- Eine Entwicklungsumgebung für die Entwicklung von REST-, Streaming- und Webhook-Integrationen.

## Fehler und Fehlerbehebung {#errors-and-troubleshooting}

The following is a list of errors that you may encounter when using any [!DNL Experience Platform] service. For troubleshooting guides on individual [!DNL Platform] services, see the [service troubleshooting directory](#service-troubleshooting-directory) below.

## API-Status-Codes {#api-status-codes}

The following status codes may be encountered on any [!DNL Experience Platform] API. Jeder Code kann verschiedene Ursachen haben; daher sind die Erklärungen in diesem Abschnitt allgemein gehalten. For more details regarding specific errors in individual [!DNL Platform] services, please see the [service troubleshooting directory](#service-troubleshooting-directory) below.

| Status-Code | Beschreibung | Mögliche Ursachen |
--- | --- | ---
| 400 | Ungültige Anfrage | Die Anfrage wurde falsch erstellt, es fehlen wichtige Informationen und/oder die Syntax ist falsch. |
| 401 | Authentifizierung fehlgeschlagen | Die Anfrage hat eine Authentifizierungsprüfung nicht bestanden. Ihr Zugriffstoken fehlt oder ist ungültig. Weiterführende Informationen finden Sie im Abschnitt [OAuth-Token-Fehler](#oauth-token-is-missing). |
| 403 | Verboten | Die Ressource wurde zwar gefunden, Sie verfügen jedoch über nicht die richtigen Berechtigungen zur Anzeige. |
| 404 | Nicht gefunden | Die angeforderte Ressource konnte auf dem Server nicht gefunden werden. Die Ressource wurde möglicherweise gelöscht oder der angefragte Pfad wurde falsch eingegeben. |
| 500 | Interner Server-Fehler | Dies ist ein Server-seitiger Fehler. Wenn Sie viele simultane Aufrufe ausführen, erreichen Sie möglicherweise das API-Limit und müssen Ihre Ergebnisse filtern. (See the [!DNL Catalog Service] API developer guide sub-guide on [filtering data](../catalog/api/filter-data.md) to learn more.) Warten Sie kurz, bevor Sie Ihre Anfrage erneut testen, und wenden Sie sich an Ihren Administrator, wenn das Problem fortbesteht. |

## Fehler in der Anfragekopfzeile {#request-header-errors}

All API calls in [!DNL Platform] require specific request headers. Informationen dazu, welche Kopfzeilen für einzelne Dienste benötigt werden, finden Sie in der [API-Referenzdokumentation](https://www.adobe.io/apis/experienceplatform/home/api-reference.html). Die Werte für die erforderlichen Authentifizierungskopfzeilen finden Sie im [Authentifizierungs-Tutorial](../tutorials/authentication.md). Wenn eine dieser Kopfzeilen beim Ausführen eines API-Aufrufs fehlt oder ungültig ist, können die folgenden Fehler auftreten.

### OAuth-Token fehlt {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

Diese Fehlermeldung wird angezeigt, wenn in einer API-Anfrage eine `Authorization`-Kopfzeile fehlt. Stellen Sie sicher, dass die Autorisierungskopfzeile ein gültiges Zugriffstoken beinhaltet, bevor Sie es erneut versuchen.

### OAuth-Token ist ungültig

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

Diese Fehlermeldung wird angezeigt, wenn das in der `Authorization`-Kopfzeile angegebene Zugriffstoken ungültig ist. Vergewissern Sie sich, dass Sie das Token richtig eingegeben haben, oder [generieren Sie ein neues Token](../tutorials/authentication.md) in der Adobe I/O-Konsole.

### API-Schlüssel erforderlich

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

Diese Fehlermeldung wird angezeigt, wenn in einer API-Anfrage eine Kopfzeile für den API-Schlüssel (`x-api-key`) fehlt. Stellen Sie sicher, dass die Kopfzeile einen gültigen API-Schlüssel enthält, bevor Sie es erneut versuchen.

### API-Schlüssel ist ungültig

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

Diese Fehlermeldung wird angezeigt, wenn der Wert der bereitgestellten API-Schlüsselkopfzeile (`x-api-key`) ungültig ist. Vergewissern Sie sich, dass Sie den Schlüssel richtig eingegeben haben, bevor Sie es erneut versuchen. Wenn Sie Ihren API-Schlüssel nicht kennen, können Sie ihn in der [Adobe I/O-Konsole](https://console.adobe.io) finden: Navigieren Sie auf der Registerkarte **Integrationen** zum Abschnitt **Übersicht** einer bestimmten Integration, um den API-Schlüssel unter **Client-Anmeldedaten** anzuzeigen.


### Fehlende Kopfzeile

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

Diese Fehlermeldung wird angezeigt, wenn in einer API-Anfrage eine Kopfzeile für die IMS-Organisation (`x-gw-ims-org-id`) fehlt. Stellen Sie sicher, dass die Kopfzeile die Kennung Ihrer IMS-Organisation enthält, bevor Sie es erneut versuchen.

### Profil ist ungültig

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

This error message displays when the user or Adobe I/O integration (identified by the [access token](#how-do-i-get-an-access-token) in the `Authorization` header) is not entitled to make calls to [!DNL Experience Platform] APIs for the IMS Org provided in the `x-gw-ims-org-id` header. Stellen Sie sicher, dass Sie in der Kopfzeile die richtige Kennung für Ihre IMS-Organisation eingegeben haben, bevor Sie es erneut versuchen. Wenn Sie die Kennung Ihrer Organisation nicht kennen, können Sie sie in der [Adobe I/O-Konsole](https://console.adobe.io) finden: Navigieren Sie auf der Registerkarte **Integrationen** zum Abschnitt **Übersicht** einer bestimmten Integration, um die Kennung unter **Client-Anmeldedaten** anzuzeigen.

### Kein gültiger Inhaltstyp angegeben

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

Diese Fehlermeldung wird angezeigt, wenn eine POST-, PUT- oder PATCH-Anfrage eine ungültige oder fehlende `Content-Type`-Kopfzeile aufweist. Stellen Sie sicher, dass die Kopfzeile in der Anfrage enthalten ist und ihr Wert `application/json` lautet.


## Verzeichnis zur Fehlerbehebung bei Diensten {#service-troubleshooting-directory}

The following is a list of troubleshooting guides and API reference documentation for [!DNL Experience Platform] APIs. Each troubleshooting guide provides answers to frequently asked questions and solutions to problems that are specific to individual [!DNL Platform] services. API-Referenzdokumente bieten für jeden Dienst eine komplette Anleitung zu allen verfügbaren Endpunkten und umfassen Beispielanfragetexte, Antworten sowie Fehler-Codes, die Sie möglicherweise erhalten.

| Dienst | API-Referenz | Fehlerbehebung |
--- | --- | ---
| Access Control | [Access Control-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml) | [Handbuch zur Fehlerbehebung bei Access Control](../access-control/troubleshooting-guide.md) |
| Catalog | [Catalog Service-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) |  |
| Data Ingestion (Batch) | [Data Ingestion-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [Handbuch zur Fehlerbehebung bei der Batch-Erfassung](../ingestion/batch-ingestion/troubleshooting.md) |
| Data Ingestion (Streaming) | [Data Ingestion-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [Handbuch zur Fehlerbehebung bei der Streaming-Erfassung](../ingestion/streaming-ingestion/troubleshooting.md) |
| Data Science Workspace | [Sensei Machine Learning-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [Data Science Workspace – Handbuch zur Fehlerbehebung](../data-science-workspace/troubleshooting-guide.md) |
| Data Usage Labeling and Enforcement (DULE) | [DULE Policy Service-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) |  |
| Experience-Datenmodell (XDM) | [Schemaregistrierungs-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) | [XDM-System – FAQs und Handbuch zur Fehlerbehebung](../xdm/troubleshooting-guide.md) |
| Identity Service | [Identity Service-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml) | [Handbuch zur Fehlerbehebung bei Identity Service](../identity-service/troubleshooting-guide.md) |
| Query Service | [Query Service-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml) | [Handbuch zur Fehlerbehebung bei Query Service](../query-service/troubleshooting-guide.md) |
| Echtzeit-Kundenprofil | [Echtzeit-Kundenprofil-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml) | [Handbuch zur Fehlerbehebung bei Profilen](../profile/troubleshooting.md) |
| Sandboxes | [Sandbox-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) | [Handbuch zur Fehlerbehebung bei Sandboxes](../sandboxes/troubleshooting-guide.md) |
| Segmentierung | [Segmentierungs-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml) |