---
keywords: Experience Platform;Startseite;beliebte Themen;Abfrage-Service;API-Handbuch;Abfrage-Service;Abfrage-Service-Konten;Konten;
solution: Experience Platform
title: API-Endpunkt für Konten
description: Sie können ein Abfrage-Service-Konto für persistente erstellen.
role: Developer
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 5%

---

# Konten-Endpunkt

Im Abfrage-Service von Adobe Experience Platform werden Konten verwendet, um nicht ablaufende Anmeldeinformationen zu erstellen, die Sie mit externen SQL-Clients verwenden können. Sie können den `/accounts`-Endpunkt in der Abfrage-Service-API verwenden, mit dem Sie programmgesteuert Ihre Query Service-Integrationskonten (auch als technisches Konto bezeichnet) erstellen, abrufen, bearbeiten und löschen können.

## Erste Schritte

Die in diesem Handbuch verwendeten Endpunkte sind Teil der Abfrage-Service-API. Bevor Sie fortfahren, lesen Sie den Abschnitt [Erste Schritte](./getting-started.md). Dort erhalten Sie wichtige Informationen darüber, wie Sie die API aufrufen und die erforderlichen Kopfzeilen sowie Beispiele für API-Aufrufe lesen können.

## Konto erstellen

Sie können ein Query Service-Integrationskonto erstellen, indem Sie eine POST-Anfrage an den `/accounts`-Endpunkt senden.

**API-Format**

```http
POST /accounts
```

**Anfrage**

Mit der folgenden Anfrage wird ein neues Query Service-Integrationskonto für Ihr Unternehmen erstellt.

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
| `credential` | *(Optional)* Die Berechtigung, die für die Integration des Abfrage-Service verwendet wird. Wenn nicht anders angegeben, generiert das System automatisch eine Berechtigung für Sie. |
| `description` | *(Optional)* Eine Beschreibung für das Integrationskonto des Abfrage-Service. |

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit Details zu Ihrem neu erstellten Query Service-Integrationskonto zurückgegeben. Sie können diese Kontodetails verwenden, um den Abfrage-Service mit externen Clients zu verbinden.

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
| `technicalAccountId` | Die ID Ihres Query Service-Integrationskontos. Zusammen mit dem `credential` bildet dies Ihr Passwort für Ihr Konto. |
| `credential` | Die Anmeldedaten für Ihr Query Service-Integrationskonto. Zusammen mit dem `technicalAccountId` bildet dies Ihr Passwort für Ihr Konto. |

## Aktualisieren eines Kontos

Sie können Ihr Query Service-Integrationskonto aktualisieren, indem Sie eine PUT-Anfrage an den `/accounts`-Endpunkt senden.

**API-Format**

```http
POST /accounts/{ACCOUNT_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{ACCOUNT_ID}` | Die ID des Abfrage-Service-Integrationskontos, das Sie aktualisieren möchten. |

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
| `credential` | *(Optional)* Die aktualisierte Berechtigung für Ihr Abfrage-Service-Konto. |
| `description` | *(Optional)* Die aktualisierte Beschreibung für das Integrationskonto des Abfrage-Services. |

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit Informationen zu Ihrem neu aktualisierten Query Service-Integrationskonto zurückgegeben.

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

Sie können eine Liste aller Query Service-Integrationskonten abrufen, indem Sie eine GET-Anfrage an den `/accounts`-Endpunkt senden.

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

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit einer Liste aller Query Service-Integrationskonten zurückgegeben.

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

## Löschen eines Kontos

Sie können Ihr Query Service-Integrationskonto löschen, indem Sie eine DELETE-Anfrage an den `/accounts`-Endpunkt senden.

**API-Format**

```http
DELETE /accounts/{ACCOUNT_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{ACCOUNT_ID}` | Die ID des Abfrage-Service-Integrationskontos, das Sie löschen möchten. |

**Anfrage**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/queryauth/accounts/E09A0DFB5FDB25D90A494012 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit einer Meldung zurückgegeben, die besagt, dass das Konto erfolgreich gelöscht wurde.

```json
{
    "result": "Success"
}
```
