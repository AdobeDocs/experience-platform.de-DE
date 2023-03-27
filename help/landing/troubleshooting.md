---
keywords: Experience Platform;Startseite;beliebte Themen;API-Fehler-Codes;API-Fehler-Code;Fehler-Code API;Fehler-Codes API;API-Anfragefehler;API-Fehlerbehebung;API-Fehler
solution: Experience Platform
title: Häufig gestellte Fragen zu Adobe Experience Platform und Handbuch zur Fehlerbehebung
description: Hier finden Sie Antworten auf häufig gestellte Fragen und eine Anleitung zur Fehlerbehebung bei häufigen Fehlern in Experience Platform.
landing-page-description: Hier finden Sie Antworten auf häufig gestellte Fragen und eine Anleitung zur Fehlerbehebung bei häufigen Fehlern in Experience Platform.
short-description: Find answers to frequently asked questions and a guide for troubleshooting common errors in Experience Platform.
type: Documentation
exl-id: 3e6d29aa-2138-421b-8bee-82b632962c01
source-git-commit: 76ef5638316a89aee1c6fb33370af943228b75e1
workflow-type: tm+mt
source-wordcount: '1861'
ht-degree: 99%

---

# [!DNL Platform] – Häufig gestellte Fragen und Handbuch zur Fehlerbehebung

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Adobe Experience Platform sowie eine allgemeine Anleitung zur Behebung gängiger Fehler, die in [!DNL Experience Platform]-APIs auftreten können. Hinweise zur Fehlerbehebung bei einzelnen [!DNL Platform]-Services finden Sie unten im [Verzeichnis zur Fehlerbehebung bei Services](#service-troubleshooting-directory).

## Häufig gestellte Fragen {#faq}

Im Folgenden finden Sie eine Liste von Antworten auf häufig gestellte Fragen zu Adobe Experience Platform.

## Was sind [!DNL Experience Platform]-APIs? {#what-are-experience-platform-apis}

[!DNL Experience Platform] bietet verschiedene RESTful-APIs, die HTTP-Anfragen für den Zugriff auf [!DNL Platform]-Ressourcen verwenden. Diese Dienst-APIs machen jeweils verschiedene Endpunkte verfügbar und ermöglichen Ihnen das Auflisten (GET), Nachschlagen (GET), Bearbeiten (PUT und/oder PATCH) und Löschen (DELETE) von Ressourcen. Weiterführende Informationen zu einzelnen Endpunkten und Vorgängen, die bei den jeweiligen Diensten verfügbar sind, finden Sie in der [API-Referenzdokumentation](https://www.adobe.com/go/platform-api-reference-en) in Adobe I/O.

## Wie kann ich eine API-Anfrage formatieren? {#how-do-i-format-an-api-request}

Anfrageformate variieren je nach der verwendeten [!DNL Platform]-API. Am einfachsten erfahren Sie, wie Sie API-Aufrufe strukturieren können, indem Sie sich die in der Dokumentation für einzelne [!DNL Platform]-Services angegebenen Beispiele ansehen.

Weiterführende Informationen zum Erstellen von API-Anfragen finden Sie in den Ersten Schritten für die Platform-API im Abschnitt zum [Lesen beispielhafter API-Aufrufe](./api-guide.md#sample-api).

## Was ist meine IMS-Organisation? {#what-is-my-ims-organization}

Eine IMS-Organisation ist eine Adobe-Darstellung eines Kunden. Alle lizenzierten Adobe-Lösungen sind in diese Kundenorganisation integriert. Wenn eine IMS-Organisation über die Berechtigung [!DNL Experience Platform] verfügt, kann sie Entwicklern Zugriff zuweisen. Die IMS-Organisations-ID (`x-gw-ims-org-id`) stellt die Organisation dar, für die ein API-Aufruf ausgeführt werden soll, und ist daher in allen API-Anfragen als Kopfzeile obligatorisch. Diese ID können Sie unter Verwendung der [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) suchen: Navigieren Sie auf der Registerkarte **Integrationen** zum Abschnitt **Übersicht** einer bestimmten Integration, um unter **Client-Anmeldedaten** die ID anzuzeigen. Eine schrittweise Anleitung zum Authentifizieren bei [!DNL Platform] finden Sie im [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de).

## Wo finde ich meinen API-Schlüssel? {#where-can-i-find-my-api-key}

In allen API-Anfragen ist ein API-Schlüssel als Kopfzeile erforderlich. Sie können ihn über die [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) finden. Navigieren Sie in der Konsole auf der Registerkarte **Integrationen** zum Abschnitt **Übersicht** einer bestimmten Integration; Sie finden den Schlüssel dann unter **Client-Anmeldedaten**. Eine schrittweise Anleitung zum Authentifizieren bei [!DNL Platform] finden Sie im [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de).

## Woher bekomme ich ein Zugriffs-Token? {#how-do-i-get-an-access-token}

Zugriffstoken sind in der Autorisierungskopfzeile aller API-Aufrufe erforderlich. Sie können mit einem `curl`-Befehl generiert werden, vorausgesetzt, Sie haben Zugriff auf eine Integration für eine IMS-Organisation. Zugriffstoken sind nur 24 Stunden lang gültig. Danach muss ein neues Token generiert werden, wenn Sie die API weiter verwenden möchten. Weiterführende Informationen zum Generieren von Zugriffstoken finden Sie im [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de).

## Wie verwende ich Abfrageparameter? {#how-do-i-user-query-parameters}

Einige [!DNL Platform]-API-Endpunkte akzeptieren Abfrageparameter, damit Sie nach bestimmten Informationen suchen und die in der Antwort zurückgegebenen Ergebnisse filtern können. Abfrageparameter werden mit einem Fragezeichen (`?`) an Anfragepfade angehängt, gefolgt von einem oder mehreren Abfrageparametern im Format `paramName=paramValue`. Wenn Sie mehrere Parameter in einem einzelnen Aufruf nutzen möchten, müssen Sie ein kaufmännisches Und-Zeichen (`&`) verwenden, um einzelne Parameter voneinander zu trennen. Das folgende Beispiel zeigt, wie eine Anfrage, bei der mehrere Abfrageparameter zum Einsatz kommen, in der Dokumentation dargestellt wird.

Beispiele für häufig verwendete Abfrageparameter sind:

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Detaillierte Informationen dazu, welche Abfragen bei einem bestimmten Service oder Endpunkt verfügbar sind, finden Sie in der dienstspezifischen Dokumentation.

## Wie gebe ich ein JSON-Feld an, das in einer PATCH-Anfrage aktualisiert werden soll? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

Viele PATCH-Vorgänge in [!DNL Platform]-APIs verwenden [JSON-Zeiger](https://tools.ietf.org/html/rfc6901)-Zeichenfolgen, um anzugeben, welche JSON-Eigenschaften aktualisiert werden sollen. Diese werden normalerweise im [JSON Patch](https://tools.ietf.org/html/rfc6902)-Format in Anfrage-Payloads eingebunden. Weiterführende Informationen zur für diese Technologien erforderlichen Syntax finden Sie im [API-Grundlagenhandbuch](api-fundamentals.md).

## Kann ich Postman nutzen, um Aufrufe an [!DNL Platform]-APIs auszuführen? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.postman.com/) ist ein hilfreiches Tool zur Visualisierung von Aufrufen an RESTful-APIs. Das Dokument [Erste Schritte mit der Platform-API](api-guide.md) enthält ein Video und Anweisungen zum Importieren von Postman-Sammlungen. Darüber hinaus wird eine Liste mit Postman-Sammlungen für jeden Service bereitgestellt.

## Welche Systemanforderungen gelten für [!DNL Platform]? {#what-are-the-system-requirements-for-platform}

Je nachdem, ob Sie die Benutzeroberfläche oder API verwenden, gelten die folgenden Systemanforderungen:

**Für UI-basierte Vorgänge:**
- Ein moderner, standardmäßiger Webbrowser. Zwar wird die neueste Version von [!DNL Chrome] empfohlen, doch werden auch aktuelle und frühere Hauptversionen von [!DNL Firefox], [!DNL Internet Explorer] und Safari unterstützt.
   - Bei jeder Veröffentlichung einer neuen Hauptversion beginnt [!DNL Platform] mit der Unterstützung der neuesten Version, während die Unterstützung für die drittneueste Version eingestellt wird.
- Bei allen Browsern müssen Cookies und JavaScript aktiviert sein.

**Für Interaktionen mit APIs und Entwicklern:**
- Eine Entwicklungsumgebung für die Entwicklung von REST-, Streaming- und Webhook-Integrationen.

## Fehler und Fehlerbehebung {#errors-and-troubleshooting}

Im Folgenden finden Sie eine Liste mit Fehlern, die bei der Verwendung von [!DNL Experience Platform]-Services auftreten können. Hinweise zur Fehlerbehebung bei einzelnen [!DNL Platform]-Services finden Sie unten im [Verzeichnis zur Fehlerbehebung bei Services](#service-troubleshooting-directory).

## API-Status-Codes {#api-status-codes}

Die folgenden Status-Codes können bei jeder [!DNL Experience Platform]-API auftreten. Jeder Code kann verschiedene Ursachen haben; daher sind die Erklärungen in diesem Abschnitt allgemein gehalten. Weiterführende Details zu bestimmten Fehlern in einzelnen [!DNL Platform]-Services finden Sie unten im [Verzeichnis zur Fehlerbehebung bei Services](#service-troubleshooting-directory).

| Status-Code | Beschreibung | Mögliche Ursachen |
|--- | --- | ---|
| 400 | Ungültige Anfrage | Die Anfrage wurde falsch erstellt, es fehlen wichtige Informationen und/oder die Syntax ist falsch. |
| 401 | Authentifizierung fehlgeschlagen | Die Anfrage hat eine Authentifizierungsprüfung nicht bestanden. Ihr Zugriffstoken fehlt oder ist ungültig. Weiterführende Informationen finden Sie im Abschnitt [OAuth-Token-Fehler](#oauth-token-is-missing). |
| 403 | Verboten | Die Ressource wurde zwar gefunden, Sie verfügen jedoch über nicht die richtigen Berechtigungen zur Anzeige. |
| 404 | Nicht gefunden | Die angeforderte Ressource konnte auf dem Server nicht gefunden werden. Die Ressource wurde möglicherweise gelöscht oder der angefragte Pfad wurde falsch eingegeben. |
| 500 | Interner Server-Fehler | Dies ist ein Server-seitiger Fehler. Wenn Sie viele simultane Aufrufe ausführen, erreichen Sie möglicherweise das API-Limit und müssen Ihre Ergebnisse filtern. (Weitere Informationen zum [Filtern von Daten](../catalog/api/filter-data.md) finden Sie im Entwicklerhandbuch für die [!DNL Catalog Service]-API.) Warten Sie kurz, bevor Sie Ihre Anfrage erneut testen, und wenden Sie sich an Ihren Administrator, wenn das Problem fortbesteht. |

## Fehler in der Anfragekopfzeile {#request-header-errors}

Für alle [!DNL Platform]-Aufrufe in sind spezifische Anfragekopfzeilen erforderlich. Informationen dazu, welche Kopfzeilen für einzelne Dienste benötigt werden, finden Sie in der [API-Referenzdokumentation](https://www.adobe.com/go/platform-api-reference-en). Die Werte für die erforderlichen Authentifizierungskopfzeilen finden Sie im [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de). Wenn eine dieser Kopfzeilen beim Ausführen eines API-Aufrufs fehlt oder ungültig ist, können die folgenden Fehler auftreten.

### OAuth-Token fehlt {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

Diese Fehlermeldung wird angezeigt, wenn in einer API-Anfrage eine `Authorization`-Kopfzeile fehlt. Stellen Sie sicher, dass die Autorisierungskopfzeile ein gültiges Zugriffstoken beinhaltet, bevor Sie es erneut versuchen.

### OAuth-Token ist ungültig {#oauth-token-is-not-valid}

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

Diese Fehlermeldung wird angezeigt, wenn das in der `Authorization`-Kopfzeile angegebene Zugriffstoken ungültig ist. Vergewissern Sie sich, dass Sie das Token richtig eingegeben haben, oder [generieren Sie ein neues Token](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) in der Adobe I/O-Konsole.

### API-Schlüssel erforderlich {#api-key-is-required}

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

Diese Fehlermeldung wird angezeigt, wenn in einer API-Anfrage eine Kopfzeile für den API-Schlüssel (`x-api-key`) fehlt. Stellen Sie sicher, dass die Kopfzeile einen gültigen API-Schlüssel enthält, bevor Sie es erneut versuchen.

### API-Schlüssel ist ungültig {#api-key-is-invalid}

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

Diese Fehlermeldung wird angezeigt, wenn der Wert der bereitgestellten API-Schlüsselkopfzeile (`x-api-key`) ungültig ist. Vergewissern Sie sich, dass Sie den Schlüssel richtig eingegeben haben, bevor Sie es erneut versuchen. Wenn Sie Ihren API-Schlüssel nicht kennen, können Sie ihn in der [Adobe I/O-Konsole](https://console.adobe.io) finden: Navigieren Sie auf der Registerkarte **Integrationen** zum Abschnitt **Übersicht** einer bestimmten Integration, um den API-Schlüssel unter **Client-Anmeldedaten** anzuzeigen.

### Fehlende Kopfzeile {#missing-header}

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

Diese Fehlermeldung wird angezeigt, wenn in einer API-Anfrage eine Kopfzeile für die IMS-Organisation (`x-gw-ims-org-id`) fehlt. Stellen Sie sicher, dass die Kopfzeile die Kennung Ihrer IMS-Organisation enthält, bevor Sie es erneut versuchen.

### Profil ist ungültig {#profile-is-not-valid}

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

Diese Fehlermeldung wird angezeigt, wenn die Benutzerin oder der Benutzer oder die Adobe I/O-Integration (identifiziert durch das [Zugriffstoken](#how-do-i-get-an-access-token) in der `Authorization`-Kopfzeile) nicht dazu berechtigt ist, für die in der `x-gw-ims-org-id`-Kopfzeile angegebene IMS-Organisation Aufrufe an [!DNL Experience Platform]-APIs auszuführen. Stellen Sie sicher, dass Sie in der Kopfzeile die richtige Kennung für Ihre IMS-Organisation eingegeben haben, bevor Sie es erneut versuchen. Wenn Sie die Kennung Ihrer Organisation nicht kennen, können Sie sie in der [Adobe I/O-Konsole](https://console.adobe.io) finden: Navigieren Sie auf der Registerkarte **Integrationen** zum Abschnitt **Übersicht** einer bestimmten Integration, um die Kennung unter **Client-Anmeldedaten** anzuzeigen.

### eTag-Fehler bei Aktualisierung {#refresh-etag-error}

```json
{
"errorMessage":"Supplied version=[\\\\\\\"a200a2a3-0000-0200-0000-123178f90000\\\\\\\"] does not match the current version on entity=[\\\\\\\"a200cdb2-0000-0200-0000-456179940000\\\\\\\"]"
}
```

Sie erhalten möglicherweise einen eTag-Fehler, wenn eine Änderung an einer Quell- oder Zielentität wie Fluss, Verbindung, Quell-Connector oder Zielverbindung durch einen anderen API-Aufrufer vorgenommen wurde. Aufgrund der unterschiedlichen Versionen wird dann die Änderung, die Sie vornehmen möchten, nicht auf die neueste Version der Entität angewendet.

Um dies zu beheben, müssen Sie die Entität erneut abrufen, sicherstellen, dass Ihre Änderungen mit der neuen Version der Entität kompatibel sind, dann das neue eTag in der `If-Match`-Kopfzeile platzieren und schließlich den API-Aufruf ausführen.

### Kein gültiger Inhaltstyp angegeben {#valid-content-type-not-specified}

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

Diese Fehlermeldung wird angezeigt, wenn eine POST-, PUT- oder PATCH-Anfrage eine ungültige oder fehlende `Content-Type`-Kopfzeile aufweist. Stellen Sie sicher, dass die Kopfzeile in der Anfrage enthalten ist und ihr Wert `application/json` lautet.

### Benutzerregion fehlt {#user-region-is-missing}

```json
{
    "error_code": "403027",
    "message": "User region is missing"
}
```

Diese Fehlermeldung wird in einem der beiden folgenden Fälle angezeigt:
- Wenn eine falsche oder falsch formatierte Kopfzeile der IMS-Organisation (`x-gw-ims-org-id`) in einer API-Anfrage übergeben wird. Stellen Sie sicher, dass die richtige Kennung Ihrer IMS-Organisation vorhanden ist, bevor Sie es erneut versuchen.
- Wenn Ihr Konto (wie durch die angegebenen Authentifizierungs-Anmeldeinformationen dargestellt) nicht mit einem Produktprofil für Experience Platform verknüpft ist. Befolgen Sie im Tutorial zur Platform-API-Authentifizierung die Schritte zum [Generieren von Anmeldeinformationen für den Zugriff](./api-authentication.md#authentication-for-each-session), um Platform zu Ihrem Konto hinzuzufügen und Ihre Authentifizierungs-Anmeldeinformationen entsprechend zu aktualisieren.

## Verzeichnis zur Fehlerbehebung bei Diensten {#service-troubleshooting-directory}

Im Folgenden finden Sie eine Liste mit Handbüchern zur Fehlerbehebung und API-Referenzdokumenten für [!DNL Experience Platform]-APIs. Jedes Handbuch zur Fehlerbehebung beinhaltet Antworten auf häufig gestellte Fragen und Lösungen für Probleme, die bei einzelnen [!DNL Platform]-Services auftreten können. API-Referenzdokumente bieten für jeden Service eine komplette Anleitung zu allen verfügbaren Endpunkten und umfassen Beispielanfragetexte, Antworten sowie Fehler-Codes, die Sie möglicherweise erhalten.

| Service | API-Referenz | Fehlerbehebung |
| --- | --- | --- |
| Zugangssteuerung | [Zugangssteuerungs-API](https://www.adobe.io/experience-platform-apis/references/access-control/) | [Handbuch zur Fehlerbehebung bei der Zugriffskontrolle](../access-control/troubleshooting-guide.md) |
| Datenerfassung in Adobe Experience Platform | [[!DNL Batch Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) | [Handbuch zur Fehlerbehebung bei der Batch-Erfassung](../ingestion/batch-ingestion/troubleshooting.md) |
| Datenerfassung in Adobe Experience Platform | [[!DNL Streaming Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/) | [Handbuch zur Fehlerbehebung bei der Streaming-Erfassung](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform-Datenwissenschafts-Arbeitsbereich | [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [[!DNL Data Science Workspace] Handbuch zur Fehlerbehebung](../data-science-workspace/troubleshooting-guide.md) |
| Data Governance in Adobe Experience Platform | [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) |  |
| Adobe Experience Platform Identity Service | [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service) | [[!DNL Identity Service] Handbuch zur Fehlerbehebung](../identity-service/troubleshooting-guide.md) |
| Query Service von Adobe Experience Platform | [[!DNL Query Service API]](https://www.adobe.io/experience-platform-apis/references/query-service/) | [[!DNL Query Service] Handbuch zur Fehlerbehebung](../query-service/troubleshooting-guide.md) |
| Adobe Experience Platform-Segmentierung | [[!DNL Segmentation API]](https://www.adobe.io/experience-platform-apis/references/segmentation/) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/) | [[!DNL XDM System] Häufig gestellte Fragen und Handbuch zur Fehlerbehebung](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] und [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/) |  |
| [!DNL Real-Time Customer Profile] | [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en) | [[!DNL Profile] Handbuch zur Fehlerbehebung](../profile/troubleshooting.md) |
| Sandboxes | [Sandbox-API](https://www.adobe.io/experience-platform-apis/references/sandbox) | [Handbuch zur Fehlerbehebung bei Sandboxes](../sandboxes/troubleshooting-guide.md) |
