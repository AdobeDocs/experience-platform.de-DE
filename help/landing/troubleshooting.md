---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Häufig gestellte Fragen zur Adobe Experience Platform und Handbuch zur Fehlerbehebung
topic: getting started
translation-type: tm+mt
source-git-commit: 2e5668a8b1d5fb831188fbd4e453b9f4aa7474df
workflow-type: tm+mt
source-wordcount: '1959'
ht-degree: 3%

---


# [!DNL Platform] FAQ und Handbuch zur Fehlerbehebung

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zur Adobe Experience Platform sowie eine allgemeine Anleitung zur Fehlerbehebung für häufige Fehler, die in einer beliebigen [!DNL Experience Platform] API auftreten können. Hinweise zur Fehlerbehebung bei einzelnen [!DNL Platform] Diensten finden Sie im [Fehlerbehebungsordner](#service-troubleshooting-directory) unten.

## FAQs {#faq}

Im Folgenden finden Sie eine Liste von Antworten auf häufig gestellte Fragen zur Adobe Experience Platform.

## Was sind [!DNL Experience Platform] APIs? {#what-are-experience-platform-apis}

[!DNL Experience Platform] Angebot mehrerer RESTful-APIs, die HTTP-Anforderungen für den Zugriff auf [!DNL Platform] Ressourcen verwenden. Diese Dienst-APIs stellen jeweils mehrere Endpunkte offen und ermöglichen Ihnen die Ausführung von Vorgängen zur Liste (GET), Suche (GET), Bearbeitung (PUT und/oder PATCH) und zum Löschen (DELETE) von Ressourcen. Weitere Informationen zu bestimmten Endpunkten und Vorgängen, die für jeden Dienst verfügbar sind, finden Sie in der [API-Referenzdokumentation](https://www.adobe.io/apis/experienceplatform/home/api-reference.html) zu Adobe I/O.

## Wie formatiere ich eine API-Anforderung? {#how-do-i-format-an-api-request}

Die Anforderungsformate hängen von der verwendeten [!DNL Platform] API ab. Die beste Methode, um zu erfahren, wie Sie Ihre API-Aufrufe strukturieren, besteht darin, die in der Dokumentation für den jeweiligen [!DNL Platform] Dienst, den Sie verwenden, angegebenen Beispiele zu verwenden.

### Lesen von Beispiel-API-Aufrufen

Die Dokumentation für [!DNL Experience Platform] zeigt Beispiel-API-Aufrufe auf zwei verschiedene Arten an. Zunächst wird der Aufruf im **API-Format** angezeigt, wobei nur die Operation (GET, POST, PUT, PATCH, DELETE) und der verwendete Endpunkt (z. B. `/global/classes`) angezeigt werden. Einige Vorlagen zeigen auch den Speicherort von Variablen an, um zu veranschaulichen, wie ein Aufruf formuliert werden sollte, z. B. `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

Die Aufrufe werden dann als cURL-Befehle in einer **Anforderung** angezeigt, die die erforderlichen Kopfzeilen und den vollständigen &quot;Basispfad&quot;enthält, der für eine erfolgreiche Interaktion mit der API erforderlich ist. Der Basispfad sollte allen Endpunkten vorangestellt werden. Der oben genannte `/global/classes` Endpunkt wird beispielsweise `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`geändert. Das API-Format/Anforderungsmuster wird in der gesamten Dokumentation angezeigt. Es wird erwartet, dass Sie den vollständigen Pfad verwenden, der in der Beispielanforderung angezeigt wird, wenn Sie Ihre eigenen Platform-APIs aufrufen.

### Beispiel-API-Anforderung

Im Folgenden finden Sie eine API-Beispielanforderung, die das Format zeigt, auf das Sie in der Dokumentation stoßen werden.

**API-Format**

Das API-Format zeigt den Vorgang (GET) und den verwendeten Endpunkt an. Variablen werden durch geschweifte Klammern angegeben (in diesem Fall `{CONTAINER_ID}`).

```http
GET /{CONTAINER_ID}/classes
```

**Anfrage**

In dieser Beispielanforderung werden die Variablen aus dem API-Format den tatsächlichen Werten im Anforderungspfad zugewiesen. Es werden auch alle erforderlichen Kopfzeilen angezeigt, entweder als Beispiel-Kopfzeilenwerte oder Variablen, in die vertrauliche Informationen (wie Sicherheits-Token und Zugriffs-IDs) einbezogen werden sollen.

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

Die Antwort zeigt, was Sie nach einem erfolgreichen Aufruf der API erwarten würden, basierend auf der gesendeten Anforderung. Gelegentlich wird die Antwort für Leerzeichen abgeschnitten, d. h., Sie sehen möglicherweise weitere Informationen oder zusätzliche Informationen zu den im Beispiel angezeigten Informationen.

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

Weitere Informationen zu bestimmten Endpunkten in Platform-APIs, einschließlich erforderlicher Kopfzeilen und Anforderungsgremien, finden Sie in der [API-Referenzdokumentation](https://www.adobe.io/apis/experienceplatform/home/api-reference.html).

## Was ist meine IMS-Einrichtung? {#what-is-my-ims-organization}

Eine IMS-Organisation ist eine Adobe-Vertretung eines Kunden. Alle lizenzierten Adobe-Lösungen sind in diese Kundenorganisation integriert. Wenn eine IMS-Organisation berechtigt ist, kann sie Entwicklern Zugriff zuweisen [!DNL Experience Platform]. Die IMS-Organisations-ID (`x-gw-ims-org-id`) stellt die Organisation dar, für die ein API-Aufruf ausgeführt werden soll, und ist daher in allen API-Anforderungen als Header erforderlich. Diese ID kann über die [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui)gefunden werden: Navigieren Sie auf der Registerkarte **Integrationen** zum Abschnitt **Übersicht** für eine bestimmte Integration, um die ID unter **Clientberechtigungen** zu finden. Eine schrittweise Anleitung zur Authentifizierung [!DNL Platform]finden Sie im [Authentifizierungslehrgang](../tutorials/authentication.md).

## Wo finde ich meinen API-Schlüssel? {#where-can-i-find-my-api-key}

In allen API-Anforderungen ist ein API-Schlüssel als Header erforderlich. Sie finden sie über die [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). Navigieren Sie in der Konsole auf der Registerkarte &quot; **Integrationen** &quot;zum Abschnitt &quot; **Übersicht** &quot;für eine bestimmte Integration und finden Sie den Schlüssel unter &quot; **Clientberechtigungen**&quot;. Eine schrittweise Anleitung zum Authentifizieren finden Sie [!DNL Platform]im [Authentifizierungstraining](../tutorials/authentication.md).

## Wie bekomme ich ein Zugriffstoken? {#how-do-i-get-an-access-token}

Zugriffstoken sind im Autorisierungs-Header aller API-Aufrufe erforderlich. Sie können mit einem `curl` Befehl generiert werden, vorausgesetzt, Sie haben Zugriff auf eine Integration für eine IMS-Organisation. Zugriffstoken sind nur 24 Stunden gültig. Danach muss ein neues Token generiert werden, um die API weiter verwenden zu können. Weitere Informationen zum Generieren von Zugriffstoken finden Sie im [Authentifizierungstraining](../tutorials/authentication.md).

## Wie verwende ich Abfragen-Parameter? {#how-do-i-user-query-parameters}

Einige [!DNL Platform] API-Endpunkte akzeptieren Abfragen-Parameter, um bestimmte Informationen zu suchen und die in der Antwort zurückgegebenen Ergebnisse zu filtern. An die Anforderungspfade mit einem Fragezeichen (`?`) werden Abfragen-Parameter angehängt, gefolgt von einem oder mehreren Abfragen-Parametern unter Verwendung des Formats `paramName=paramValue`. Wenn Sie mehrere Parameter in einem einzelnen Aufruf kombinieren, müssen Sie ein kaufmännisches Und (`&`) verwenden, um einzelne Parameter zu trennen. Das folgende Beispiel zeigt, wie eine Anforderung, die mehrere Abfragen verwendet, in der Dokumentation dargestellt wird.

Beispiele für häufig verwendete Parameter für die Abfrage:

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Detaillierte Informationen darüber, welche Abfragen für einen bestimmten Dienst oder Endpunkt verfügbar sind, finden Sie in der dienstspezifischen Dokumentation.

## Wie gebe ich ein JSON-Feld an, das in einer PATCH-Anforderung aktualisiert werden soll? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

Viele PATCH-Vorgänge in [!DNL Platform] APIs verwenden [JSON-Zeiger](https://tools.ietf.org/html/rfc6901) -Zeichenfolgen, um anzugeben, welche JSON-Eigenschaften aktualisiert werden sollen. Diese werden normalerweise in Anforderungs-Nutzlasten im [JSON Patch](https://tools.ietf.org/html/rfc6902) -Format enthalten. Detaillierte Informationen zur erforderlichen Syntax für diese Technologien finden Sie im Handbuch [zu den](api-fundamentals.md) API-Grundlagen.

## Kann ich Postman verwenden, um [!DNL Platform] APIs anzurufen? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.getpostman.com/) ist ein nützliches Werkzeug zur Visualisierung von Aufrufen an RESTful-APIs. Dieser [Mittlere Beitrag](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) beschreibt, wie Sie Postman so einrichten können, dass eine Authentifizierung automatisch durchgeführt wird und damit [!DNL Experience Platform] APIs verwendet werden.

## Wozu dienen die Systemanforderungen [!DNL Platform]? {#what-are-the-system-requirements-for-platform}

Je nachdem, ob Sie die Benutzeroberfläche oder API verwenden, gelten die folgenden Systemanforderungen:

**Für UI-basierte Vorgänge:**
- Ein moderner, standardmäßiger Webbrowser. Obwohl die neueste Version von empfohlen [!DNL Chrome] wird, werden auch aktuelle und frühere Hauptversionen von [!DNL Firefox], [!DNL Internet Explorer]und Safari unterstützt.
   - Bei jeder Veröffentlichung einer neuen Hauptversion werden [!DNL Platform] Beginn, die die neueste Version unterstützen, nicht unterstützt, während die Unterstützung für die dritte Version eingestellt wird.
- In allen Browsern müssen Cookies und JavaScript aktiviert sein.

**Für API- und Entwicklerinteraktionen:**
- Eine Entwicklungs-Umgebung, die für REST-, Streaming- und WebHook-Integrationen entwickelt werden soll.

## Fehler und Fehlerbehebung {#errors-and-troubleshooting}

Im Folgenden finden Sie eine Liste von Fehlern, die bei der Verwendung eines [!DNL Experience Platform] Dienstes auftreten können. Hinweise zur Fehlerbehebung bei einzelnen [!DNL Platform] Diensten finden Sie im [Fehlerbehebungsordner](#service-troubleshooting-directory) unten.

## API-Statuscodes {#api-status-codes}

Die folgenden Statuscodes können auf jeder [!DNL Experience Platform] API gefunden werden. Jede hat eine Vielzahl von Ursachen, daher sind die Erklärungen in diesem Abschnitt allgemeiner Natur. Weitere Informationen zu bestimmten Fehlern in einzelnen [!DNL Platform] Diensten finden Sie im [Service Troubleshooting Verzeichnis](#service-troubleshooting-directory) unten.

| Statuscode | Beschreibung | Mögliche Ursachen |
--- | --- | ---
| 400 | Ungültige Anforderung | Die Anforderung wurde falsch erstellt, fehlen wichtige Informationen und/oder enthielten eine falsche Syntax. |
| 401 | Authentifizierung fehlgeschlagen | Die Anforderung hat keine Authentifizierungsprüfung bestanden. Ihr Zugriffstoken fehlt oder ist ungültig. Weitere Informationen finden Sie im Abschnitt [OAuth-Token-Fehler](#oauth-token-is-missing) . |
| 403 | Verboten | Die Ressource wurde gefunden, Sie haben jedoch nicht die richtigen Anmeldeinformationen, um sie Ansicht. |
| 404 | Nicht gefunden | Die angeforderte Ressource konnte nicht auf dem Server gefunden werden. Die Ressource wurde möglicherweise gelöscht oder der angeforderte Pfad wurde falsch eingegeben. |
| 500 | Interner Server-Fehler | Dies ist ein serverseitiger Fehler. Wenn Sie viele gleichzeitige Aufrufe durchführen, erreichen Sie möglicherweise das API-Limit und müssen Ihre Ergebnisse filtern. (Weitere Informationen zum [!DNL Catalog Service] Filtern von Daten [finden Sie im Unterleitfaden zum](../catalog/api/filter-data.md) API-Entwickler.) Warten Sie kurz, bevor Sie Ihre Anforderung erneut ausprobieren, und wenden Sie sich an Ihren Administrator, wenn das Problem weiterhin besteht. |

## Anforderungskopfzeilenfehler {#request-header-errors}

Alle API-Aufrufe in [!DNL Platform] erfordern bestimmte Anforderungsheader. Informationen dazu, welche Header für einzelne Dienste erforderlich sind, finden Sie in der [API-Referenzdokumentation](https://www.adobe.io/apis/experienceplatform/home/api-reference.html). Die Werte für die erforderlichen Authentifizierungsheader finden Sie im [Authentifizierungslehrgang](../tutorials/authentication.md). Wenn einer dieser Header beim Durchführen eines API-Aufrufs fehlt oder ungültig ist, können die folgenden Fehler auftreten.

### OAuth-Token fehlt {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

Diese Fehlermeldung wird angezeigt, wenn eine `Authorization` Kopfzeile in einer API-Anforderung fehlt. Stellen Sie sicher, dass der Autorisierungs-Header in einem gültigen Zugriffstoken enthalten ist, bevor Sie es erneut versuchen.

### OAuth-Token ist nicht gültig

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

Diese Fehlermeldung wird angezeigt, wenn das angegebene Zugriffstoken in der `Authorization` Kopfzeile ungültig ist. Vergewissern Sie sich, dass das Token korrekt eingegeben wurde, oder [generieren Sie ein neues Token](../tutorials/authentication.md) in der Adobe-E/A-Konsole.

### API-Schlüssel erforderlich

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

Diese Fehlermeldung wird angezeigt, wenn in einer API-Anforderung ein API-Schlüsselheader (`x-api-key`) fehlt. Stellen Sie sicher, dass die Kopfzeile mit einem gültigen API-Schlüssel enthalten ist, bevor Sie es erneut versuchen.

### API-Schlüssel ist ungültig

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

Diese Fehlermeldung wird angezeigt, wenn der Wert der bereitgestellten API-Schlüsselüberschrift (`x-api-key`) ungültig ist. Vergewissern Sie sich, dass Sie den Schlüssel korrekt eingegeben haben, bevor Sie ihn erneut versuchen. Wenn Sie Ihren API-Schlüssel nicht kennen, finden Sie ihn in der [Adobe-E/A-Konsole](https://console.adobe.io): Navigieren Sie auf der Registerkarte **Integrationen** zum Abschnitt **Übersicht** für eine bestimmte Integration, um den API-Schlüssel unter **Clientanmeldeinformationen** zu suchen.


### Fehlende Kopfzeile

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

Diese Fehlermeldung wird angezeigt, wenn eine IMS-Organisations-Kopfzeile (`x-gw-ims-org-id`) in einer API-Anforderung fehlt. Stellen Sie sicher, dass der Header mit der ID Ihres IMS-Unternehmens enthalten ist, bevor Sie es erneut versuchen.

### Profil ist nicht gültig

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

Diese Fehlermeldung wird angezeigt, wenn der Benutzer oder die Adobe-E/A-Integration (durch das [Zugriffstoken](#how-do-i-get-an-access-token) im `Authorization` Header identifiziert) nicht berechtigt ist, Aufrufe an [!DNL Experience Platform] APIs für das im `x-gw-ims-org-id` Header bereitgestellte IMS-Org durchzuführen. Stellen Sie sicher, dass Sie die richtige ID für Ihr IMS-Unternehmen in der Kopfzeile angegeben haben, bevor Sie es erneut versuchen. Wenn Sie Ihre Organisations-ID nicht kennen, finden Sie sie in der [Adobe I/O-Konsole](https://console.adobe.io): Navigieren Sie auf der Registerkarte **Integrationen** zum Abschnitt **Übersicht** für eine bestimmte Integration, um die ID unter **Clientberechtigungen** zu suchen.

### Gültiger Inhaltstyp nicht angegeben

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

Diese Fehlermeldung wird angezeigt, wenn eine POST-, PUT- oder PATCH-Anforderung einen ungültigen oder fehlenden `Content-Type` Header enthält. Stellen Sie sicher, dass der Header in der Anforderung enthalten ist und dass der Wert `application/json`des Headers angegeben ist.


## Ordner zur Fehlerbehebung beim Dienst {#service-troubleshooting-directory}

Im Folgenden finden Sie eine Liste der Anleitungen zur Fehlerbehebung und der API-Referenzdokumentation für [!DNL Experience Platform] APIs. Jeder Leitfaden zur Fehlerbehebung enthält Antworten auf häufig gestellte Fragen und Lösungen zu Problemen, die für einzelne [!DNL Platform] Dienste spezifisch sind. Die API-Referenz-Dokumente bieten eine umfassende Anleitung zu allen verfügbaren Endpunkten für jeden Dienst und zeigen Beispielanforderungsgremien, Antworten und Fehlercodes an, die Sie möglicherweise erhalten.

| Service | API-Referenz | Fehlerbehebung |
--- | --- | ---
| Zugriffssteuerung | [Zugriffskontrolle-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml) | [Handbuch zur Fehlerbehebung bei Zugriffskontrollen](../access-control/troubleshooting-guide.md) |
| Katalog | [Katalogdienst-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) |  |
| Datenauffüllung (Batch) | [Dateneinführungs-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [Handbuch zur Fehlerbehebung bei der Stapelverarbeitung](../ingestion/batch-ingestion/troubleshooting.md) |
| Dateneinbettung (Streaming) | [Dateneinführungs-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [Handbuch zur Fehlerbehebung bei der Streaming-Erfassung](../ingestion/streaming-ingestion/troubleshooting.md) |
| Data Science-Arbeitsbereich | [Sensei Machine Learning API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [Data Science Workspace - Anleitung zur Fehlerbehebung](../data-science-workspace/troubleshooting-guide.md) |
| Datenverwendung - Kennzeichnung und Durchsetzung (DULE) | [API des DULE Policy Service](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) |  |
| Erlebnisdatenmodell (XDM) | [Schema Registry API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) | [XDM-System - FAQs und Handbuch zur Fehlerbehebung](../xdm/troubleshooting-guide.md) |
| Identitätsdienst | [Identitätsdienst-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml) | [Handbuch zur Fehlerbehebung beim Identitätsdienst](../identity-service/troubleshooting-guide.md) |
| Abfrage | [Abfrage Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml) | [Handbuch zur Fehlerbehebung beim Abfrage Service](../query-service/troubleshooting-guide.md) |
| Echtzeit-Kundenprofil | [Echtzeit-Client-Profil-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml) |  |
| Sandboxes | [Sandbox-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) | [Handbuch zur Fehlerbehebung bei Sandboxen](../sandboxes/troubleshooting-guide.md) |
| Segmentierung | [Segmentierungs-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml) |