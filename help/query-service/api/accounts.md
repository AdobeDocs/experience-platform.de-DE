---
keywords: Experience Platform; Startseite; beliebte Themen; Query Service; API-Handbuch; Query Service; Query Service-Konten; Konten;
solution: Experience Platform
title: Konto-API-Endpunkt
description: Sie können ein Query Service-Konto für beständig erstellen.
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 5%

---

# Konten-Endpunkt

In Adobe Experience Platform Query Service werden Konten verwendet, um nicht ablaufende Anmeldeinformationen zu erstellen, die Sie mit externen SQL-Clients verwenden können. Sie können die `/accounts` -Endpunkt in der Query Service-API, mit dem Sie programmatisch Ihre Query Service-Integrationskonten erstellen, abrufen, bearbeiten und löschen können (auch als technisches Konto bezeichnet).

## Erste Schritte

Die in diesem Handbuch verwendeten Endpunkte sind Teil der Query Service-API. Bevor Sie fortfahren, lesen Sie bitte die [Erste Schritte](./getting-started.md) für wichtige Informationen, die Sie benötigen, um die API erfolgreich aufrufen zu können, einschließlich erforderlicher Kopfzeilen und Informationen zum Lesen von Beispiel-API-Aufrufen.

## Konto erstellen

Sie können ein Integrationskonto für Query Service erstellen, indem Sie eine POST-Anfrage an die `/accounts` -Endpunkt.

**API-Format**

```http
POST /accounts
```

**Anfrage**

Mit der folgenden Anfrage wird ein neues Query Service-Integrationskonto für Ihre IMS-Organisation erstellt.

```shell
curl -X POST https://platform.adobe.io/data/foundation/queryauth/accounts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
{
    "accountName": "sampleName",
    "assignedToUser": "sample@example.com",
    "credential": "samplecredential",
    "description": "Sample description"
}'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `accountName` | **Erforderlich** Der Name des Query Service-Integrationskontos. |
| `assignedToUser` | **Erforderlich** Die Adobe ID, für die das Query Service-Integrationskonto erstellt wird. |
| `credential` | *(Optional)* Die Berechtigung, die für die Integration von Query Service verwendet wird. Wenn kein Wert angegeben wird, generiert das System automatisch eine Berechtigung für Sie. |
| `description` | *(Optional)* Eine Beschreibung für das Query Service-Integrationskonto. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zum neu erstellten Query Service-Integrationskonto zurück. Sie können diese Kontodetails verwenden, um Query Service mit externen Clients zu verbinden.

```json
{
    "technicalAccountName": "2428A037-D963-47C2-A14D-CD816EFB0AA3@TECHACCT.ADOBE.COM",
    "technicalAccountId": "E09A0DFB5FDB25D90A494012",
    "credential": "samplecredential"
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `technicalAccountName` | Der Name Ihres Query Service-Integrationskontos. |
| `technicalAccountId` | Die ID Ihres Query Service-Integrationskontos. Dies wird zusammen mit dem `credential`, stellt Ihr Passwort für Ihr Konto zusammen. |
| `credential` | Die Berechtigung Ihres Query Service-Integrationskontos. Dies wird zusammen mit dem `technicalAccountId`, stellt Ihr Passwort für Ihr Konto zusammen. |

## Konto aktualisieren

Sie können Ihr Integrationskonto für Query Service aktualisieren, indem Sie eine PUT-Anfrage an die `/accounts` -Endpunkt.

**API-Format**

```http
POST /accounts/{ACCOUNT_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{ACCOUNT_ID}` | Die ID des Query Service-Integrationskontos, das Sie aktualisieren möchten. |

**Anfrage**

```shell
curl -X PUT https://platform.adobe.io/data/foundation/queryauth/accounts/E09A0DFB5FDB25D90A494012 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
     "accountName": "Updated account name",
     "assignedToUser": "sampleuser2@adobe.com",
     "credential": "UpdatedCredential",
     "description": "Updated description"
 }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `accountName` | *(Optional)* Der aktualisierte Name für das Query Service-Integrationskonto. |
| `assignedToUser` | *(Optional)* Die aktualisierte Adobe ID, mit der das Query Service-Integrationskonto verknüpft ist. |
| `credential` | *(Optional)* Die aktualisierte Berechtigung für Ihr Query Service-Konto. |
| `description` | *(Optional)* Die aktualisierte Beschreibung für das Query Service-Integrationskonto. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Informationen zu Ihrem neu aktualisierten Query Service-Integrationskonto zurück.

```json
{
    "accountName": "Updated account name",
    "assignedToUser": "sampleuser2@adobe.com",
    "created": "2021-06-16T16:44:42.073Z",
    "createdBy": "3BF132EF5BC636C10A49400B@AdobeID",
    "credential": "UpdatedCredential",
    "description": "Updated description",
    "lastUpdated": "2021-08-03T23:47:46.588Z",
    "lastUpdatedBy": "3BF132EF5BC636C10A49400B@AdobeID",
    "technicalAccountName": "2428A037-D963-47C2-A14D-CD816EFB0AA3@TECHACCT.ADOBE.COM",
    "technicalAccountId": "E09A0DFB5FDB25D90A494012"
}
```

## Alle Konten auflisten

Sie können eine Liste aller Query Service-Integrationskonten abrufen, indem Sie eine GET-Anfrage an die `/accounts` -Endpunkt.

**API-Format**

```http
GET /accounts
```

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/foundation/queryauth/accounts \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit einer Liste aller Query Service-Integrationskonten zurück.

```json
{
    "accounts": [
        {
            "lastUpdated": "2021-06-16T18:07:49.581Z",
            "accountName": "Use for XQL testing of account creation",
            "description": "Local test",
            "assignedToUser": "platform-ui-automation@adobe.com",
            "technicalAccountName": "ADC7EB19-63B4-4B9F-A192-EBE3CD0C034E@TECHACCT.ADOBE.COM",
            "technicalAccountId": "38645A7360CA3DF30A49400F",
            "lastUpdatedBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "createdBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "created": "2021-06-16T18:07:49.581Z",
            "active": true
        },
        {
            "lastUpdated": "2021-06-16T16:44:42.073Z",
            "accountName": "Use for XQL testing of account creation",
            "description": " ",
            "assignedToUser": "platform-ui-automation@adobe.com",
            "technicalAccountName": "66E91FDD-4733-45E2-A312-D87580CFA55D@TECHACCT.ADOBE.COM",
            "technicalAccountId": "392202E060CA2A770A49420A",
            "lastUpdatedBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "createdBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "created": "2021-06-16T16:44:42.073Z",
            "active": true
        }
    ],
    "_page": {
        "count": 2,
        "next": "2021-06-16T16:44:42.073Z",
        "orderby": "-created",
        "property": "active==true",
        "start": "2021-06-16T18:07:49.581Z"
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/queryauth/accounts?orderby=-created&property=active==true&start=2021-06-16T16:44:42.073Z"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/queryauth/accounts?orderby=-created&property=active==true&start=2021-06-16T18:07:49.581Z&isPrevLink=true"
        }
    },
    "version": 1
}
```

## Konto löschen

Sie können Ihr Integrationskonto für Query Service löschen, indem Sie eine DELETE-Anfrage an die `/accounts` -Endpunkt.

**API-Format**

```http
DELETE /accounts/{ACCOUNT_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{ACCOUNT_ID}` | Die ID des Query Service-Integrationskontos, das Sie löschen möchten. |

**Anfrage**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/queryauth/accounts/E09A0DFB5FDB25D90A494012 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit einer Meldung zurück, dass das Konto erfolgreich gelöscht wurde.

```json
{
    "result": "Success"
}
```
