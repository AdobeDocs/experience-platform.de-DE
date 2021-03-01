---
keywords: Experience Platform;Home;beliebte Themen;API-Fehlercodes;API-Fehlercode;Fehlercode-API;Fehlercodes-API;API-Anforderungsfehler;API-Fehlerbehebung;API-Fehler
solution: Experience Platform
title: Häufig gestellte Fragen zu Adobe Experience Platform und Handbuch zur Fehlerbehebung
description: Hier finden Sie Antworten auf häufig gestellte Fragen und eine Anleitung zur Fehlerbehebung bei häufigen Fehlern in Experience Platform.
landing-page-description: Hier finden Sie Antworten auf häufig gestellte Fragen und eine Anleitung zur Fehlerbehebung bei häufigen Fehlern in Experience Platform.
topic: Erste Schritte
type: Dokumentation
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '1997'
ht-degree: 73%

---


# [!DNL Platform] FAQ und Handbuch zur Fehlerbehebung

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Adobe Experience Platform sowie eine allgemeine Anleitung zur Fehlerbehebung für häufige Fehler, die in einer [!DNL Experience Platform]-API auftreten können. Hinweise zur Fehlerbehebung bei einzelnen [!DNL Platform]-Diensten finden Sie im Ordner [Dienstfehlerbehebung](#service-troubleshooting-directory) unten.

## FAQs {#faq}

Im Folgenden finden Sie eine Liste von Antworten auf häufig gestellte Fragen zu Adobe Experience Platform.

## Was sind [!DNL Experience Platform]-APIs? {#what-are-experience-platform-apis}

[!DNL Experience Platform] Angebote mehrerer RESTful-APIs, die HTTP-Anforderungen für den Zugriff auf  [!DNL Platform] Ressourcen verwenden. Diese Dienst-APIs machen jeweils verschiedene Endpunkte verfügbar und ermöglichen Ihnen das Auflisten (GET), Nachschlagen (GET), Bearbeiten (PUT und/oder PATCH) und Löschen (DELETE) von Ressourcen. Weiterführende Informationen zu einzelnen Endpunkten und Vorgängen, die bei den jeweiligen Diensten verfügbar sind, finden Sie in der [API-Referenzdokumentation](http://www.adobe.com/go/platform-api-reference-en) in Adobe I/O.

## Wie kann ich eine API-Anfrage formatieren? {#how-do-i-format-an-api-request}

Die Anforderungsformate variieren je nach verwendeter API. [!DNL Platform] Die beste Möglichkeit, Ihre API-Aufrufe zu strukturieren, besteht darin, die in der Dokumentation für den jeweiligen [!DNL Platform]-Dienst angegebenen Beispiele zu verwenden.

### Lesen von Beispiel-API-Aufrufen

Die Dokumentation für [!DNL Experience Platform] zeigt Beispiel-API-Aufrufe auf zwei verschiedene Arten an. Zunächst wird der Aufruf im **API-Format** dargestellt, wobei es sich um eine Vorlagendarstellung handelt, die nur den Vorgang (GET, POST, PUT, PATCH, DELETE) und den verwendeten Endpunkt (z. B. `/global/classes`) zeigt. Manche Vorlagen zeigen auch die Stelle von Variablen an, um zu veranschaulichen, wie ein Aufruf formuliert werden sollte, z. B. `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

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

Weiterführende Informationen zu einzelnen Endpunkten in Platform-APIs, einschließlich erforderlicher Kopfzeilen und Anfragetexte, finden Sie in der [API-Referenzdokumentation](http://www.adobe.com/go/platform-api-reference-en).

## Was ist meine IMS-Organisation? {#what-is-my-ims-organization}

Eine IMS-Organisation ist eine Adobe-Darstellung eines Kunden. Alle lizenzierten Adobe-Lösungen sind in diese Kundenorganisation integriert. Wenn eine IMS-Organisation über die Berechtigung [!DNL Experience Platform] verfügt, kann sie Entwicklern Zugriff zuweisen. Die IMS-Organisations-ID (`x-gw-ims-org-id`) stellt die Organisation dar, für die ein API-Aufruf ausgeführt werden soll, und ist daher in allen API-Anfragen als Kopfzeile obligatorisch. Diese ID kann über die [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui_de) gefunden werden: Navigieren Sie auf der Registerkarte **Integrationen** zum Abschnitt **Übersicht**, um die ID unter **Clientanmeldeinformationen** zu finden. Eine schrittweise Anleitung zum Authentifizieren in [!DNL Platform] finden Sie im [Authentifizierungstutorial](https://www.adobe.com/go/platform-api-authentication-en).

## Wo finde ich meinen API-Schlüssel? {#where-can-i-find-my-api-key}

In allen API-Anfragen ist ein API-Schlüssel als Kopfzeile erforderlich. Sie finden sie über die [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). Navigieren Sie in der Konsole auf der Registerkarte **Integrationen** zum Abschnitt **Übersicht** einer bestimmten Integration; Sie finden den Schlüssel dann unter **Client-Anmeldedaten**. Eine schrittweise Anleitung zum Authentifizieren für [!DNL Platform] finden Sie im [Authentifizierungstutorial](https://www.adobe.com/go/platform-api-authentication-en).

## Woher bekomme ich ein Zugriffstoken? {#how-do-i-get-an-access-token}

Zugriffstoken sind in der Autorisierungskopfzeile aller API-Aufrufe erforderlich. Sie können mit einem `curl`-Befehl generiert werden, vorausgesetzt, Sie haben Zugriff auf eine Integration für eine IMS-Organisation. Zugriffstoken sind nur 24 Stunden lang gültig. Danach muss ein neues Token generiert werden, wenn Sie die API weiter verwenden möchten. Weiterführende Informationen zum Generieren von Zugriffstoken finden Sie im [Authentifizierungs-Tutorial](https://www.adobe.com/go/platform-api-authentication-en).

## Wie verwende ich Abfrageparameter? {#how-do-i-user-query-parameters}

Einige [!DNL Platform]-API-Endpunkte akzeptieren Abfragen-Parameter, um bestimmte Informationen zu suchen und die in der Antwort zurückgegebenen Ergebnisse zu filtern. Abfrageparameter werden mit einem Fragezeichen (`?`) an Anfragepfade angehängt, gefolgt von einem oder mehreren Abfrageparametern im Format `paramName=paramValue`. Wenn Sie mehrere Parameter in einem einzelnen Aufruf nutzen möchten, müssen Sie ein kaufmännisches Und-Zeichen (`&`) verwenden, um einzelne Parameter voneinander zu trennen. Das folgende Beispiel zeigt, wie eine Anfrage, bei der mehrere Abfrageparameter zum Einsatz kommen, in der Dokumentation dargestellt wird.

Beispiele für häufig verwendete Abfrageparameter sind:

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Detaillierte Informationen dazu, welche Abfragen bei einem bestimmten Dienst oder Endpunkt verfügbar sind, finden Sie in der dienstspezifischen Dokumentation.

## Wie gebe ich ein JSON-Feld an, das in einer PATCH-Anfrage aktualisiert werden soll? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

Viele PATCH-Vorgänge in [!DNL Platform]-APIs verwenden [JSON-Zeiger](https://tools.ietf.org/html/rfc6901)-Zeichenfolgen, um die zu aktualisierenden JSON-Eigenschaften anzugeben. Diese werden normalerweise im [JSON Patch](https://tools.ietf.org/html/rfc6902)-Format in Anfrage-Payloads eingebunden. Weiterführende Informationen zur für diese Technologien erforderlichen Syntax finden Sie im [API-Grundlagenhandbuch](api-fundamentals.md).

## Kann ich Postman verwenden, um Aufrufe an [!DNL Platform]-APIs zu tätigen? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.postman.com/) ist ein hilfreiches Tool zur Visualisierung von Aufrufen an RESTful-APIs. Dieser [Mittlerer Beitrag](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) beschreibt, wie Sie Postman so einrichten können, dass eine Authentifizierung automatisch durchgeführt wird und [!DNL Experience Platform]-APIs verwendet werden.

## Welche Systemanforderungen gelten für [!DNL Platform]? {#what-are-the-system-requirements-for-platform}

Je nachdem, ob Sie die Benutzeroberfläche oder API verwenden, gelten die folgenden Systemanforderungen:

**Für UI-basierte Vorgänge:**
- Ein moderner, standardmäßiger Webbrowser. Während die neueste Version von [!DNL Chrome] empfohlen wird, werden auch aktuelle und frühere Hauptversionen von [!DNL Firefox], [!DNL Internet Explorer] und Safari unterstützt.
   - Bei jeder Veröffentlichung einer neuen Hauptversion werden [!DNL Platform]-Beginn, die die neueste Version unterstützen, entfernt, während die Unterstützung für die dritte neueste Version eingestellt wird.
- Bei allen Browsern müssen Cookies und JavaScript aktiviert sein.

**Für Interaktionen mit APIs und Entwicklern:**
- Eine Entwicklungsumgebung für die Entwicklung von REST-, Streaming- und Webhook-Integrationen.

## Fehler und Fehlerbehebung {#errors-and-troubleshooting}

Im Folgenden finden Sie eine Liste von Fehlern, die bei der Verwendung eines [!DNL Experience Platform]-Dienstes auftreten können. Hinweise zur Fehlerbehebung bei einzelnen [!DNL Platform]-Diensten finden Sie im Ordner [Dienstfehlerbehebung](#service-troubleshooting-directory) unten.

## API-Status-Codes {#api-status-codes}

Die folgenden Statuscodes können bei jeder [!DNL Experience Platform]-API gefunden werden. Jeder Code kann verschiedene Ursachen haben; daher sind die Erklärungen in diesem Abschnitt allgemein gehalten. Weitere Informationen zu bestimmten Fehlern in einzelnen [!DNL Platform]-Diensten finden Sie im Ordner [Dienstfehlerbehebung](#service-troubleshooting-directory) unten.

| Status-Code | Beschreibung | Mögliche Ursachen |
--- | --- | ---
| 400 | Ungültige Anfrage | Die Anfrage wurde falsch erstellt, es fehlen wichtige Informationen und/oder die Syntax ist falsch. |
| 401 | Authentifizierung fehlgeschlagen | Die Anfrage hat eine Authentifizierungsprüfung nicht bestanden. Ihr Zugriffstoken fehlt oder ist ungültig. Weiterführende Informationen finden Sie im Abschnitt [OAuth-Token-Fehler](#oauth-token-is-missing). |
| 403 | Verboten | Die Ressource wurde zwar gefunden, Sie verfügen jedoch über nicht die richtigen Berechtigungen zur Anzeige. |
| 404 | Nicht gefunden | Die angeforderte Ressource konnte auf dem Server nicht gefunden werden. Die Ressource wurde möglicherweise gelöscht oder der angefragte Pfad wurde falsch eingegeben. |
| 500 | Interner Server-Fehler | Dies ist ein Server-seitiger Fehler. Wenn Sie viele simultane Aufrufe ausführen, erreichen Sie möglicherweise das API-Limit und müssen Ihre Ergebnisse filtern. (Weitere Informationen finden Sie im Unterhandbuch zum API-Entwicklerhandbuch zu [Filterdaten](../catalog/api/filter-data.md).) [!DNL Catalog Service] Warten Sie kurz, bevor Sie Ihre Anfrage erneut testen, und wenden Sie sich an Ihren Administrator, wenn das Problem fortbesteht. |

## Fehler in der Anfragekopfzeile {#request-header-errors}

Alle API-Aufrufe in [!DNL Platform] erfordern bestimmte Anforderungsheader. Informationen dazu, welche Kopfzeilen für einzelne Dienste benötigt werden, finden Sie in der [API-Referenzdokumentation](http://www.adobe.com/go/platform-api-reference-en). Die Werte für die erforderlichen Authentifizierungskopfzeilen finden Sie im [Authentifizierungs-Tutorial](https://www.adobe.com/go/platform-api-authentication-en). Wenn eine dieser Kopfzeilen beim Ausführen eines API-Aufrufs fehlt oder ungültig ist, können die folgenden Fehler auftreten.

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

Diese Fehlermeldung wird angezeigt, wenn das in der `Authorization`-Kopfzeile angegebene Zugriffstoken ungültig ist. Vergewissern Sie sich, dass Sie das Token richtig eingegeben haben, oder [generieren Sie ein neues Token](https://www.adobe.com/go/platform-api-authentication-en) in der Adobe I/O-Konsole.

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

Diese Fehlermeldung wird angezeigt, wenn der Benutzer oder die Adobe I/O-Integration (gekennzeichnet durch das [Zugriffstoken](#how-do-i-get-an-access-token) in der `Authorization`-Kopfzeile) nicht berechtigt ist, Aufrufe an [!DNL Experience Platform]-APIs für das IMS-Org durchzuführen, das in der `x-gw-ims-org-id`-Kopfzeile bereitgestellt wird. Stellen Sie sicher, dass Sie in der Kopfzeile die richtige Kennung für Ihre IMS-Organisation eingegeben haben, bevor Sie es erneut versuchen. Wenn Sie die Kennung Ihrer Organisation nicht kennen, können Sie sie in der [Adobe I/O-Konsole](https://console.adobe.io) finden: Navigieren Sie auf der Registerkarte **Integrationen** zum Abschnitt **Übersicht** einer bestimmten Integration, um die Kennung unter **Client-Anmeldedaten** anzuzeigen.

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

Im Folgenden finden Sie eine Liste der Anleitungen zur Fehlerbehebung und der API-Referenzdokumentation für [!DNL Experience Platform]-APIs. Jedes Handbuch zur Fehlerbehebung enthält Antworten auf häufig gestellte Fragen und Lösungen zu Problemen, die für einzelne [!DNL Platform]-Dienste spezifisch sind. API-Referenzdokumente bieten für jeden Dienst eine komplette Anleitung zu allen verfügbaren Endpunkten und umfassen Beispielanfragetexte, Antworten sowie Fehler-Codes, die Sie möglicherweise erhalten.

| Dienst | API-Referenz | Fehlerbehebung |
| --- | --- | --- |
| Zugriffskontrolle | [Access Control-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml) | [Handbuch zur Fehlerbehebung bei der Zugriffskontrolle](../access-control/troubleshooting-guide.md) |
| Datenerfassung in Adobe Experience Platform | [[!DNL Data Ingestion API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [Fehlerbehebung bei der Batchverarbeitung ](../ingestion/batch-ingestion/troubleshooting.md)<br><br>[Handbuch Streaming-Erfassung - Fehlerbehebung](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform Data Science Workspace | [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [[!DNL Data Science Workspace] Handbuch zur Fehlerbehebung](../data-science-workspace/troubleshooting-guide.md) |
| Adobe Experience Platform Data Governance | [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) |  |
| Adobe Experience Platform Identity Service | [[!DNL Identity Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml) | [[!DNL Identity Service] Handbuch zur Fehlerbehebung](../identity-service/troubleshooting-guide.md) |
| Query Service von Adobe Experience Platform | [[!DNL Query Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml) | [[!DNL Query Service] Handbuch zur Fehlerbehebung](../query-service/troubleshooting-guide.md) |
| Adobe Experience Platform-Segmentierung | [[!DNL Segmentation API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) | [[!DNL XDM System] FAQ und Handbuch zur Fehlerbehebung](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] und [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) |  |
| [!DNL Real-time Customer Profile] | [[!DNL Real-time Customer Profile API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml) | [[!DNL Profile] Handbuch zur Fehlerbehebung](../profile/troubleshooting.md) |
| Sandboxes | [Sandbox-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) | [Handbuch zur Fehlerbehebung bei Sandboxes](../sandboxes/troubleshooting-guide.md) |

