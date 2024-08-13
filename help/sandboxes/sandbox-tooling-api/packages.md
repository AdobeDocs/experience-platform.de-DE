---
title: Sandbox Tooling Packages API Endpoint
description: Mit dem Endpunkt /packages in der Sandbox Tooling API können Sie Pakete in Adobe Experience Platform programmgesteuert verwalten.
exl-id: 46efee26-d897-4941-baf4-d5ca0b8311f0
source-git-commit: f81e15ccfd89e2d0cb450f596743341264187f52
workflow-type: tm+mt
source-wordcount: '1621'
ht-degree: 10%

---

# Pakete-Endpunkt

Mit Sandbox-Tools können Sie verschiedene Artefakte auswählen (auch als Objekte bezeichnet) und sie in ein Paket exportieren. Ein Paket kann aus einem einzelnen Artefakt oder mehreren Artefakten bestehen (z. B. Datensätzen oder Schemas). Alle Artefakte, die in einem Paket enthalten sind, müssen aus derselben Sandbox stammen.

Mit dem Endpunkt `/packages` in der Sandbox-Tool-API können Sie Pakete in Ihrer Organisation programmgesteuert verwalten, einschließlich der Veröffentlichung eines Pakets und des Imports eines Pakets in eine Sandbox.

## Package erstellen {#create}

Sie können ein Multiartifact-Paket erstellen, indem Sie eine POST-Anfrage an den `/packages` -Endpunkt senden und dabei Werte für den Paketnamen und den Pakettyp angeben.

**API-Format**

```http
POST /packages/
```

**Anfrage**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "name": "acme",
      "description": "Acme Business Group",
      "packageType": "PARTIAL",    
      "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
      },
      "expiry": "2023-05-20T20:05:10Z",
      "artifacts": [
        {
          "id": "27115daa-c92b-4f17-a077-d65ffeb0c525",
          "type": "PROFILE_SEGMENT",
          "title": "Acme Profile Segment"
        }      
      ]
  }'
```

| Eigenschaft | Beschreibung | Typ | Erforderlich |
| --- | --- | --- | --- |
| `name` | Der Name Ihres Pakets. | Zeichenfolge | Ja |
| `description` | Eine Beschreibung, die weitere Informationen zu Ihrem Paket enthält. | Zeichenfolge | Nein |
| `packageType` | Der Pakettyp ist **PARTIAL** , um anzugeben, dass Sie bestimmte Artefakte in ein Paket einschließen. | String | JA |
| `sourceSandbox` | Die Quell-Sandbox des Pakets. | Zeichenfolge | Nein |
| `expiry` | Der Zeitstempel, der das Ablaufdatum für das Paket definiert. Der Standardwert beträgt 90 Tage ab dem Erstellungsdatum. Das Feld für das Ablaufdatum der Antwort ist Epoch-UTC-Zeit. | Zeichenfolge (UTC-Zeitstempelformat) | Nein |
| `artifacts` | Eine Liste von Artefakten, die in das Paket exportiert werden sollen. Der `artifacts` -Wert sollte **null** oder **leer** sein, wenn der `packageType` den Wert `FULL` aufweist. | Array | Nein |

**Antwort**

Eine erfolgreiche Antwort gibt Ihr neu erstelltes Paket zurück. Die Antwort enthält die entsprechende Paket-ID sowie Informationen zu Status, Ablauf und Liste der Artefakte.

```json
{
    "id": "209f886b00444eac9bb5836fe32e7681",
    "version": 0,
    "createdDate": 1684475012105,
    "modifiedDate": 1684475012105,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "requestId": "devxa54a6b56d04f46119d9e3cc006fcc1cb",
    "userId": "platform_exim",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",     
    "sourceSandbox": {
        "name": "cjm-mr",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },     
    "packageType": "PARTIAL",
    "expiry": 1684613110000,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

## Aktualisieren eines Pakets {#update}

Sie können ein Paket aktualisieren, indem Sie eine PUT-Anfrage an den Endpunkt `/packages` senden.

### Hinzufügen von Artefakten zu einem Paket {#add-artifacts}

Um Artefakte zu einem Paket hinzuzufügen, müssen Sie `id` angeben und **ADD** für die `action` einschließen.

**API-Format**

```http
PUT /packages/
```

**Anfrage**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "id": "6fa50baedd344a278129a87e68cc9dc7",
      "action": "ADD",
      "expiry": "2023-05-20T20:05:10Z", 
      "artifacts": [
        {
         "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29@1647559351683",
         "type": "JOURNEY"
        }      
      ]
  }'
```

| Eigenschaft | Beschreibung | Typ | Obligatorisch |
| --- | --- | --- | --- |
| `id` | Die ID des zu aktualisierenden Pakets. | Zeichenfolge | Ja |
| `action` | Um Artefakte zum Paket hinzuzufügen, sollte der Aktionswert **ADD** sein. Diese Aktion wird nur für die Pakettypen **PARTIAL** unterstützt. | Zeichenfolge | Ja |
| `artifacts` | Eine Liste von Artefakten, die dem Paket hinzugefügt werden sollen. Es gibt keine Änderung am Paket, wenn die Liste **null** oder **leer** ist. Artefakte werden dedupliziert, bevor sie zum Paket hinzugefügt werden. Eine vollständige Liste der unterstützten Artefakte finden Sie in der nachfolgenden Tabelle. | Array | Nein |
| `expiry` | Der Zeitstempel, der das Ablaufdatum für das Paket definiert. Der Standardwert beträgt 90 Tage ab dem Zeitpunkt, zu dem die PUT-API aufgerufen wird, wenn in der Payload kein Ablaufdatum angegeben ist. Das Feld für das Ablaufdatum der Antwort ist Epoch-UTC-Zeit. | Zeichenfolge (UTC-Zeitstempelformat) | Nein |

Die folgenden Artefakttypen werden derzeit unterstützt.

| Artefakt | Plattform | Objekt | Teilfluss | Vollständige Sandbox |
| --- | --- | --- | --- | --- |
| `JOURNEY` | Adobe Journey Optimizer | Journeys | Ja | Nein |
| `ID_NAMESPACE` | Kundendatenplattform | Identitäten | Ja | Ja |
| `REGISTRY_DATATYPE` | Kundendatenplattform | Datentyp | Ja | Ja |
| `REGISTRY_CLASS` | Kundendatenplattform | Klasse | Ja | Ja |
| `REGISTRY_MIXIN` | Kundendatenplattform | Feldergruppe | Ja | Ja |
| `REGISTRY_SCHEMA` | Kundendatenplattform | Schemata | Ja | Ja |
| `CATALOG_DATASET` | Kundendatenplattform | Datensätze | Ja | Ja |
| `DULE_CONSENT_POLICY` | Kundendatenplattform | Einverständnis und Governance-Richtlinien | Ja | Ja |
| `PROFILE_SEGMENT` | Kundendatenplattform | Zielgruppen | Ja | Ja |
| `FLOW` | Kundendatenplattform | Datenfluss der Quellen | Ja | Ja |

**Antwort**

Eine erfolgreiche Antwort gibt Ihr aktualisiertes Paket zurück. Die Antwort enthält die entsprechende Paket-ID sowie Informationen zu Status, Ablauf und Liste der Artefakte.

```json
{
    "id": "6fa50baedd344a278129a87e68cc9dc7",
    "version": 4,
    "createdDate": 1684235842000,
    "modifiedDate": 1684475861366,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",     
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },     
    "packageType": "PARTIAL",
    "expiry": 1692251861352,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29@1647559351683",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        },
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

### Löschen von Artefakten aus einem Paket {#delete-artifacts}

Um Artefakte aus einem Package zu löschen, müssen Sie `id` angeben und **DELETE** für die `action` einschließen.


**API-Format**

```http
PUT /packages/
```

**Anfrage**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "id": "6fa50baedd344a278129a87e68cc9dc7",
      "action": "DELETE",
      "artifacts": [
        {
          "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29@1647559351683",
          "type": "JOURNEY"
        }      
      ]
  }'
```

| Eigenschaft | Beschreibung | Typ | Obligatorisch |
| --- | --- | --- | --- |
| `id` | Die ID des zu aktualisierenden Pakets. | Zeichenfolge | Ja |
| `action` | Um Artefakte aus einem Package zu löschen, sollte der Aktionswert **DELETE** sein. Diese Aktion wird nur für die Pakettypen **PARTIAL** unterstützt. | Zeichenfolge | Ja |
| `artifacts` | Eine Liste von Artefakten, die aus dem Paket gelöscht werden sollen. Es gibt keine Änderung am Paket, wenn die Liste **null** oder **leer** ist. | Array | Nein |

**Antwort**

Eine erfolgreiche Antwort gibt Ihr aktualisiertes Paket zurück. Die Antwort enthält die entsprechende Paket-ID sowie Informationen zu Status, Ablauf und Liste der Artefakte.

```json
{
    "id": "6fa50baedd344a278129a87e68cc9dc7",
    "version": 5,
    "createdDate": 1684235842000,
    "modifiedDate": 1684478830416,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",     
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },      
    "packageType": "PARTIAL",
    "expiry": 1692254830403,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

### Aktualisieren von Metadatenfeldern in einem Paket {#update-metadata}

>[!NOTE]
>
>Mit der Aktion **UPDATE** werden die Paketmetadatenfelder des Pakets aktualisiert und **kann** nicht zum Hinzufügen/Löschen von Artefakten zu einem Paket verwendet werden.

Um die Metadatenfelder in einem Paket zu aktualisieren, müssen Sie einen `id` angeben und **UPDATE** für den `action` einschließen.

**API-Format**

```http
PUT /packages/
```

**Anfrage**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "id": "6fa50baedd344a278129a87e68cc9dc7",
      "action": "UPDATE",
      "name": "acme",
      "description": "Acme Business Group",  
      "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
      }
  }'
```

| Eigenschaft | Beschreibung | Typ | Obligatorisch |
| --- | --- | --- | --- |
| `id` | Die ID des zu aktualisierenden Pakets. | Zeichenfolge | Ja |
| `action` | Um die Metadatenfelder in einem Paket zu aktualisieren, sollte der Aktionswert **UPDATE** sein. Diese Aktion wird nur für die Pakettypen **PARTIAL** unterstützt. | Zeichenfolge | Ja |
| `name` | Der aktualisierte Name des Pakets. Doppelte Paketnamen sind nicht zulässig. | Array | Ja |
| `sourceSandbox` | Die Source-Sandbox sollte derselben Organisation angehören, die in der Kopfzeile der Anfrage angegeben ist. | Zeichenfolge | Ja |

**Antwort**

Eine erfolgreiche Antwort gibt Ihr aktualisiertes Paket zurück. Die Antwort enthält die entsprechende Paket-ID sowie Informationen zu Beschreibung, Status, Ablauf und Liste der Artefakte.

```json
{
    "id": "6fa50baedd344a278129a87e68cc9dc7",
    "version": 6,
    "createdDate": 1684235842000,
    "modifiedDate": 1684479094129,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",    
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "packageType": "PARTIAL",
    "expiry": 1692255094127,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

## Löschen eines Pakets {#delete}

Um ein DELETE zu löschen, senden Sie eine Paketanfrage an den Endpunkt `/packages` und geben Sie die Kennung des Pakets an, das Sie löschen möchten.

**API-Format**

```http
DELETE /packages/{PACKAGE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| {PACKAGE_ID} | Die Kennung des Pakets, das Sie löschen möchten. |

**Anfrage**

Mit der folgenden Anfrage wird das Paket mit der Kennung {PACKAGE_ID} gelöscht.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt einen Grund zurück, der anzeigt, dass die Paket-ID gelöscht wurde.

```json
{
    "reason": "Package d30e0424a37b46ada6a5cf37f47a86ff deleted"
}
```

## Publish a package {#publish}

Um den Import eines Packages in eine Sandbox zu ermöglichen, müssen Sie es veröffentlichen. Stellen Sie eine GET-Anfrage an den `/packages` -Endpunkt, während Sie die Kennung des Pakets angeben, das Sie veröffentlichen möchten.

**API-Format**

```http
GET /packages/{PACKAGE_ID}/export
```

| Parameter | Beschreibung |
| --- | --- |
| {PACKAGE_ID} | Die ID des Pakets, das Sie veröffentlichen möchten. |

**Anfrage**

Mit der folgenden Anfrage wird das Paket mit der ID {PACKAGE_ID} veröffentlicht.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}\export \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

| Eigenschaft | Beschreibung | Typ | Obligatorisch |
| --- | --- | --- | --- |
| `expiryPeriod` | Dieser vom Benutzer angegebene Zeitraum definiert das Ablaufdatum des Pakets (in Tagen) ab der Veröffentlichung des Pakets. Dieser Wert darf nicht negativ sein.<br> Wenn kein Wert angegeben ist, wird der Standardwert als 90 (Tage) ab dem Datum der Veröffentlichung berechnet. | Ganzzahl | Nein |

**Antwort**

Eine erfolgreiche Antwort gibt das veröffentlichte Paket zurück.

```json
{
    "name": "acme",
    "description": "Acme Business Group",
    "visibility": "TENANT",
    "sourceSandbox":
    {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "type": "PARTIAL",
    "correlationId": "48effe5e-1bef-4250-9c71-23b93ef5d285"
}
```

## Paket nachschlagen {#look-up-package}

Sie können nach einem einzelnen GET suchen, indem Sie eine Anfrage an den `/packages` -Endpunkt senden, der die entsprechende Paketkennung im Anfragepfad enthält.

**API-Format**

```http
GET /packages/{PACKAGE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| {PACKAGE_ID} | Die Kennung des Pakets, das Sie nachschlagen möchten. |

**Anfrage**

Die folgende Anfrage ruft Informationen für {PACKAGE_ID} ab.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt Details für die abgefragte Paket-ID zurück. Die Antwort enthält den Namen, die Beschreibung, das Veröffentlichungsdatum und das Ablaufdatum, die Quell-Sandbox des Pakets sowie eine Liste von Artefakten.

```json
{
    "id": "8f585fad94d042cd82dbcba594108a41",
    "version": 2,
    "createdDate": 1685597784000,
    "modifiedDate": 1685597810000,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
    "packageType": "PARTIAL",
    "expiry": 1693373810000,
    "publishDate": 1685597810000,
    "status": "PUBLISHED",
    "artifactsList": [
        {
            "id": "f4f57771-2bd2-469a-9c13-8d803eeb6515",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        },
        {
            "id": "7f4caca7-a477-400d-a41e-c4735f8e780d",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ],
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    }
}
```

## Auflisten von Packages {#list-packages}

Sie können alle Pakete in Ihrer Organisation auflisten, indem Sie eine GET-Anfrage an den Endpunkt `/packages` senden.

**API-Format**

```http
GET /packages/?{QUERY_PARAMS}
```

| Parameter | Beschreibung |
| --- | --- |
| {QUERY_PARAMS} | Optionale Abfrageparameter zum Filtern der Ergebnisse. Weitere Informationen finden Sie im Abschnitt zu [Abfrageparametern](./appendix.md) . |

**Anfrage**

Die folgende Anfrage ruft Informationen der Pakete basierend auf dem {QUERY_PARAMS} ab.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/?property=status==DRAFT,PUBLISHED&property=createdDate>=2023-05-11T18:29:59.999Z&property=createdDate<=2023-05-16T18:29:59.999Z&start=0&orderby=-createdDate&limit=20 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Bei einer erfolgreichen Antwort wird eine Liste von Paketen zurückgegeben, die zu Ihrer Organisation gehören, einschließlich Details wie Name, Status, Ablauf und Artefaktliste.

```json
{
    "totalElements": 109,
    "currentPage": 0,
    "totalPages": 6,
    "hasPreviousPage": false,
    "hasNextPage": true,
    "data": [
        {
            "id": "8f585fad94d042cd82dbcba594108a41",
            "version": 2,
            "createdDate": 1685597784000,
            "modifiedDate": 1685597810000,
            "createdBy": "{CREATED_BY}",
            "modifiedBy": "{MODIFIED_BY}",
            "tenantId": "c875b077162b40409c1327b16da99c1b",
            "name": "acme",
            "description": "Acme Business Group",
            "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
            "packageType": "PARTIAL",
            "expiry": 1693373810000,
            "publishDate": 1685597810000,
            "status": "PUBLISHED",
            "artifactsList": [
                {
                    "id": "f4f57771-2bd2-469a-9c13-8d803eeb6515",
                    "type": "JOURNEY",
                    "found": false,
                    "count": 0
                },
                {
                    "id": "7f4caca7-a477-400d-a41e-c4735f8e780d",
                    "type": "JOURNEY",
                    "found": false,
                    "count": 0
                }
            ],
            "sourceSandbox": {
                "name": "acme-sandbox",
                "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
            }
        },
        {
            "id": "0d7e427ce4cb4dc1b78e30ef61b125c1",
            "version": 2,
            "createdDate": 1685555213000,
            "modifiedDate": 1685555275000,
            "createdBy": "{CREATED_BY}",
            "modifiedBy": "{MODIFIED_BY}",
            "tenantId": "7d7d8bbe3c7c4a8ea701cc5e42c57aeb",
            "name": "acme",
            "description": "Acme Business Group",
            "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
            "packageType": "PARTIAL",
            "expiry": 1693331275000,
            "publishDate": 1685555275000,
            "status": "PUBLISHED",
            "artifactsList": [
                {
                    "id": "626a9669a9f5b818db270e95",
                    "type": "CATALOG_DATASET",
                    "found": false,
                    "count": 0
                }
            ],
            "sourceSandbox": {
                "name": "acme-sandbox",
                "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
            }
        }
    ]
}
```

## Package importieren {#import}

Dieser Endpunkt wird zum Abrufen der in Konflikt stehenden Objekte in der angegebenen Ziel-Sandbox verwendet. Konfliktobjekte stellen ähnliche Objekte dar, die bereits in der Ziel-Sandbox vorhanden sind.

**API-Format**

```http
GET /packages/{PACKAGE_ID}/import?targetSandbox=targetSandboxName
```

| Parameter | Beschreibung |
| --- | --- |
| {PACKAGE_ID} | Die Kennung des Pakets, das Sie nachschlagen möchten. |

**Anfrage**

Die folgende Anfrage importiert die {PACKAGE_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/import?targetSandbox=targetSandboxName \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

In der Antwort werden Konflikte zurückgegeben. Die Antwort zeigt das Originalpaket sowie das `alternatives` -Fragment als Array an, das nach Rang geordnet ist.

Antwort anzeigen+++

```json
[
    {
        "artifact": {
            "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
            "type": "REGISTRY_SCHEMA",
            "found": false,
            "count": 0,
            "messages": [
                {
                    "status": "FOUND",
                    "attempt": 1,
                    "message": "Found object with ID: https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c"
                }
            ]
        },
        "suggestionList": [
            {
                "id": "https://ns.adobe.com/cjmstage/schemas/176f33f6a8ff6542de1256f8dc01cce4be1b3a68fd5f5bc5",
                "type": "REGISTRY_SCHEMA",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - adhoc schema - 1618950408870_1686403052050"
            },
            {
                "id": "https://ns.adobe.com/cjmstage/schemas/1b37c3403e4e12c7aa46ea9dfe380a9f2b72d4da9db62b46",
                "type": "REGISTRY_SCHEMA",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - adhoc schema - 1618950408870_1686218766627"
            }
        ],
        "parentID": "745F37C35E4B776E0A49421B@AdobeOrg::prod::REGISTRY_SCHEMA::https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c"
    },
    {
        "artifact": {
            "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
            "type": "REGISTRY_CLASS",
            "found": false,
            "count": 0,
            "messages": [
                {
                    "status": "FOUND",
                    "attempt": 1,
                    "message": "Found object with ID: https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26"
                }
            ]
        },
        "suggestionList": [
            {
                "id": "https://ns.adobe.com/cjmstage/classes/1dd81d61cdaa89a89382d0a424db77494475bd1db3105feb",
                "type": "REGISTRY_CLASS",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - Adhoc class - 1618950408870_1686564843736"
            },
            {
                "id": "https://ns.adobe.com/cjmstage/classes/2511fb5396a630b2cd3d5d9e9b69d42ce66a4289db8ac917",
                "type": "REGISTRY_CLASS",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - Adhoc class - 1618950408870_1686408152916"
            }
        ],
        "parentID": "745F37C35E4B776E0A49421B@AdobeOrg::prod::REGISTRY_CLASS::https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26"
    },
    {
        "artifact": {
            "id": "4d4c874ec3344d64bf8b3160e60ac78b",
            "type": "MAPPING_SET",
            "found": false,
            "count": 0,
            "messages": [
                {
                    "status": "FOUND",
                    "attempt": 1,
                    "message": "Found object with ID: 4d4c874ec3344d64bf8b3160e60ac78b"
                }
            ]
        },
        "suggestionList": [
            {
                "id": "6b49c959d77c48e9904f7616fe2e7848",
                "type": "MAPPING_SET",
                "found": false,
                "count": 0,
                "title": ""
            },
            {
                "id": "7b363da9e6704afb9716f57193d5246f",
                "type": "MAPPING_SET",
                "found": false,
                "count": 0,
                "title": ""
            },
            {
                "id": "93ca0b4f437c4eaf9f1986408679e965",
                "type": "MAPPING_SET",
                "found": false,
                "count": 0,
                "title": ""
            }
        ],
        "parentID": "745F37C35E4B776E0A49421B@AdobeOrg::prod::MAPPING_SET::4d4c874ec3344d64bf8b3160e60ac78b"
    }
]
```

+++

## Importe übermitteln {#submit-import}

>[!NOTE]
>
>Mit der Konfliktbeilegung ist es inhärent, dass das alternative Artefakt bereits in der Ziel-Sandbox vorhanden ist.

Sie können einen Package-Import senden, sobald Sie Konflikte überprüft und Ersatzteile bereitgestellt haben, indem Sie eine POST-Anfrage an den Endpunkt `/packages` stellen. Das Ergebnis wird als Payload bereitgestellt, die den Importauftrag für die Ziel-Sandbox startet, wie in der Payload angegeben.

Die Nutzlast akzeptiert auch den vom Benutzer angegebenen Auftragsnamen und die Beschreibung für den Importauftrag. Wenn der vom Benutzer angegebene Name und die Beschreibung nicht verfügbar sind, werden der Paketname und die Beschreibung für den Auftragsnamen und die Beschreibung verwendet.

**API-Format**

```http
POST /packages/import
```

**Anfrage**

Die folgende Anfrage ruft die zu importierenden Pakete ab. Die Payload ist eine Zuordnung von Substitutionen, bei der, wenn ein Eintrag vorhanden ist, der Schlüssel der vom Paket bereitgestellte `artifactId` und die Alternative der Wert ist. Wenn die Zuordnung oder Payload **leer** ist, werden keine Ersetzungen durchgeführt.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages/import/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
       "id": "09484a599f5f4a5faa43986643964615",
       "name": "acme",
       "description": "Acme Business Group",
       "destinationSandbox": {
         "name": "cjm-mr",
         "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
     },
     "alternatives": {
       "https://ns.adobe.com/cjmstage/schemas/ac33bbd22eb4ad6656e1c7e12e9f520261fb39fd28a902a9": {
         "id": "https://ns.adobe.com/cjmstage/schemas/a3b935344685afad4e52c753161cf673ec23d4fb1b3e9ce",
         "type": "REGISTRY_SCHEMA"
       }
     }
  }'
```

| Eigenschaft | Beschreibung | Typ | Obligatorisch |
| --- | --- | --- | --- |
| `alternatives` | `alternatives` stellt die Zuordnung von Quell-Sandbox-Artefakten zu den vorhandenen Ziel-Sandbox-Artefakten dar. Da sie bereits vorhanden sind, verhindert der Importauftrag, dass diese Artefakte in der Ziel-Sandbox erstellt werden. | Zeichenfolge | Nein |

**Antwort**

```json
{
    "name": "acme",
    "description": "Acme Business Group",
    "visibility": "TENANT",
    "sourceSandbox":
    {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "destinationSandbox":
    {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "type": "PARTIAL",
    "correlationId": "48effe5e-1bef-4250-9c71-23b93ef5d285"
}
```

## Alle abhängigen Objekte auflisten {#dependent-objects}

Auflisten aller abhängigen Objekte für die exportierten Objekte in einem Package durch eine POST-Anfrage an den Endpunkt `/packages` bei Angabe der Paketkennung.

**API-Format**

```http
POST /packages/{PACKAGE_ID}/children
```

| Parameter | Beschreibung |
| --- | --- |
| {PACKAGE_ID} | Die Kennung des Pakets. |

**Anfrage**

Die folgende Anfrage listet alle abhängigen Objekte für den {PACKAGE_ID} auf.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/import?targetSandbox=targetSandboxName \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d'[
      {
        "id": "4d4c874ec3344d64bf8b3160e60ac78b",
        "type": "MAPPING_SET"
      },
      {
        "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
        "type": "REGISTRY_SCHEMA"
      },
      {
        "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
        "type": "REGISTRY_CLASS"
      }
  ]'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von untergeordneten Elementen für die Objekte zurück.

```json
[
    {
        "id": "4d4c874ec3344d64bf8b3160e60ac78b",
        "title": "4d4c874ec3344d64bf8b3160e60ac78b",
        "type": "MAPPING_SET",
        "children": [
            {
                "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
                "title": "Dean Dataset 1 - adhoc schema - 1618950408870",
                "type": "REGISTRY_SCHEMA"
            }
        ]
    },
    {
        "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
        "title": "Dean Dataset 1 - adhoc schema - 1618950408870",
        "type": "REGISTRY_SCHEMA",
        "children": [
            {
                "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
                "title": "Dean Dataset 1 - Adhoc class - 1618950408870",
                "type": "REGISTRY_CLASS"
            }
        ]
    },
    {
        "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
        "title": "Dean Dataset 1 - Adhoc class - 1618950408870",
        "type": "REGISTRY_CLASS",
        "children": []
    }
]
```

## Überprüfen rollenbasierter Berechtigungen zum Importieren aller Paketartefakte {#role-based-permissions}

Sie können überprüfen, ob Sie berechtigt sind, Paketartefakte zu importieren, indem Sie eine GET-Anfrage an den `/packages` -Endpunkt senden und dabei die Paketkennung und den Ziel-Sandbox-Namen angeben.

**API-Format**

```http
GET /packages/preflight/{packageId}?targetSandbox=<sandbox_name
```

| Parameter | Beschreibung |
| --- | --- |
| {PACKAGE_ID} | Die Kennung des Pakets, das Sie importieren möchten. |

**Anfrage**

Die folgende Anfrage überprüft Ihre Berechtigungen auf {PACKAGE_ID} und die Sandbox.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/preflight/{PACKAGE_ID}?targetSandbox=<sandbox_name> \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt Ressourcenberechtigungen für die Ziel-Sandbox zurück, einschließlich einer Liste der erforderlichen Berechtigungen, fehlender Berechtigungen, des Typs des Artefakts und einer Entscheidung, ob die Erstellung zulässig ist.

Antwort anzeigen+++

```json
{
  "packageID": "b7bda68eb1214c86824f1d7204616e51",
  "targetSandboxName": "acme-sandbox",
  "permissionResponse": [
    {
      "artifactID": "4aca57b6-8b83-450b-a460-e8a07ca79a44",
      "requiredPermissions": {
        "resources": [
          {
            "palmResourceType": "Sandbox",
            "resourcePermissions": [
              "view"
            ]
          },
          {
            "palmResourceType": "Schema",
            "resourcePermissions": [
              "read"
            ]
          },
          {
            "palmResourceType": "ProfileConfig",
            "resourcePermissions": [
              "read"
            ]
          },
          {
            "palmResourceType": "Segment",
            "resourcePermissions": [
              "read",
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Composition",
            "resourcePermissions": [
              "read",
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Query",
            "resourcePermissions": [
              "write"
            ]
          },
          {
            "palmResourceType": "SegmentDashboard",
            "resourcePermissions": [
              "read"
            ]
          }
        ]
      },
      "missingPermissions": {
        "resources": []
      },
      "artifactType": "PROFILE_SEGMENT",
      "creationAllowed": true
    },
    {
      "artifactID": "36bb82bc-a00d-4d6b-a598-227d43e027c1",
      "requiredPermissions": {
        "resources": [
          {
            "palmResourceType": "Sandbox",
            "resourcePermissions": [
              "view"
            ]
          },
          {
            "palmResourceType": "ProfileConfig",
            "resourcePermissions": [
              "read",
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Dataset",
            "resourcePermissions": [
              "read"
            ]
          }
        ]
      },
      "missingPermissions": {
        "resources": [
          {
            "palmResourceType": "ProfileConfig",
            "resourcePermissions": [
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Dataset",
            "resourcePermissions": [
              "read"
            ]
          }
        ]
      },
      "artifactType": "PROFILE_MERGE",
      "creationAllowed": false
    }
  ]
}
```

+++

## Listen von Export-/Importvorgängen {#list-jobs}

Sie können die aktuellen Export-/Importvorgänge auflisten, indem Sie eine GET-Anfrage an den `/packages` -Endpunkt senden.

**API-Format**

```http
GET /packages/jobs?{QUERY_PARAMS}
```

| Parameter | Beschreibung |
| --- | --- |
| {QUERY_PARAMS} | Optionale Abfrageparameter zum Filtern der Ergebnisse. Weitere Informationen finden Sie im Abschnitt zu [Abfrageparametern](./appendix.md) . |

**Anfrage**

Die folgende Anfrage listet alle erfolgreichen Importvorgänge auf.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/jobs?property=requestType==IMPORT&property=jobStatus==SUCCESS&orderby=createdDate&start=0&limit=5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt alle erfolgreichen Importaufträge zurück.

```json
{
    "totalElements": 42,
    "currentPage": 0,
    "totalPages": 9,
    "hasPreviousPage": false,
    "hasNextPage": true,
    "data": [
        {
            "id": "3c1b92cf47a246d7bfbe6fd507c5d543",
            "name": "acme",
            "updated": 1685973675401,
            "created": 1685973675401,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "ead59d21405f4184a94dd786a1bf040d",
            "name": "acme1",
            "updated": 1685986367198,
            "created": 1685986367198,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "85ddaa3c2f6c475088167cde7a9d4326",
            "name": "acme2",
            "updated": 1686147692568,
            "created": 1686147692568,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "c49a4fcb31954cbd828ece1da096c8f5",
            "name": "acme3",
            "updated": 1686148007586,
            "created": 1686148007586,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "a3669315baed4cf2af49bf9ce90b8158",
            "name": "acme4",
            "updated": 1686148651910,
            "created": 1686148651910,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        }
    ]
}
```
