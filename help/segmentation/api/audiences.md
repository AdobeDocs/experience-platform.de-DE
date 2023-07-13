---
title: Zielgruppen-API-Endpunkt
description: Verwenden Sie den Zielgruppen-Endpunkt in der Adobe Experience Platform Segmentation Service-API, um Zielgruppen für Ihr Unternehmen programmgesteuert zu erstellen, zu verwalten und zu aktualisieren.
exl-id: cb1a46e5-3294-4db2-ad46-c5e45f48df15
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '2124'
ht-degree: 8%

---

# Zielgruppen-Endpunkt

Eine Zielgruppe ist eine Sammlung von Personen, die ähnliche Verhaltensweisen und/oder Merkmale aufweisen. Diese Personensammlungen können entweder mit Adobe Experience Platform oder aus externen Quellen erstellt werden. Sie können die `/audiences` -Endpunkt in der Segmentation-API, mit dem Sie Zielgruppen programmgesteuert abrufen, erstellen, aktualisieren und löschen können.

## Erste Schritte

Die in diesem Handbuch verwendeten API-Endpunkte sind Teil der [!DNL Adobe Experience Platform Segmentation Service]-. Bevor Sie fortfahren, lesen Sie bitte die [Erste Schritte](./getting-started.md) für wichtige Informationen, die Sie benötigen, um die API erfolgreich aufrufen zu können, einschließlich erforderlicher Kopfzeilen und Informationen zum Lesen von Beispiel-API-Aufrufen.

## Abrufen einer Zielgruppenliste {#list}

Sie können eine Liste aller Zielgruppen für Ihr Unternehmen abrufen, indem Sie eine GET-Anfrage an die `/audiences` -Endpunkt.

**API-Format**

Der `/audiences`-Endpunkt unterstützt verschiedene Abfrageparameter, mit denen Sie Ihre Ergebnisse filtern können. Diese Parameter sind zwar optional, doch wird ihre Verwendung dringend empfohlen, um bei der Auflistung von Ressourcen den teuren Verwaltungsaufwand zu reduzieren. Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für Ihre Organisation verfügbaren Zielgruppen abgerufen. Es können mehrere Parameter eingeschlossen werden, die durch kaufmännische Und-Zeichen (`&`) voneinander getrennt werden.

```http
GET /audiences
GET /audiences?{QUERY_PARAMETERS}
```

Beim Abrufen einer Zielgruppenliste können die folgenden Abfrageparameter verwendet werden:

| Abfrageparameter | Beschreibung | Beispiel |
| --------------- | ----------- | ------- |
| `start` | Gibt den Startversatz für die zurückgegebenen Zielgruppen an. | `start=5` |
| `limit` | Gibt die maximale Anzahl von Zielgruppen an, die pro Seite zurückgegeben werden. | `limit=10` |
| `sort` | Gibt die Reihenfolge an, nach der die Ergebnisse sortiert werden sollen. Dies wird im Format `attributeName:[desc/asc]`. | `sort=updateTime:desc` |
| `property` | Ein Filter, mit dem Sie Zielgruppen angeben können, die **just** mit dem Wert eines Attributs übereinstimmen. Dies wird im Format `property=` | `property=audienceId==test-audience-id` |
| `name` | Ein Filter, mit dem Sie Zielgruppen angeben können, deren Namen **contain** den bereitgestellten Wert. Bei diesem Wert wird nicht zwischen Groß- und Kleinschreibung unterschieden. | `name=Sample` |
| `description` | Ein Filter, mit dem Sie Zielgruppen angeben können, deren Beschreibungen **contain** den bereitgestellten Wert. Bei diesem Wert wird nicht zwischen Groß- und Kleinschreibung unterschieden. | `description=Test Description` |

**Anfrage**

Mit der folgenden Anfrage werden die letzten beiden Zielgruppen abgerufen, die in Ihrer Organisation erstellt wurden.

++ + Eine Beispielanfrage zum Abrufen einer Liste von Zielgruppen.

```shell
curl -X GET https: //platform.adobe.io/data/core/ups/audiences?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit einer Liste von Zielgruppen zurück, die in Ihrem Unternehmen als JSON erstellt wurden.

++ + Eine Beispielantwort mit den beiden zuletzt erstellten Zielgruppen, die zu Ihrem Unternehmen gehören

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "People who ordered in the last 30 days",
            "description": "Last 30 days",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"US\""
            },
            "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "isSystem": false,
            "creationTime": 1650374572000,
            "updateEpoch": 1650374573,
            "updateTime": 1650374573000,
            "createEpoch": 1650374572,
            "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
            "dependents": [],
            "definedOn": [
                {
                    "meta: resourceType": "unions",
                    "meta: containerId": "tenant",
                    "$ref": "https: //ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "dependencies": [],
            "type": "SegmentDefinition",
            "originName": "REAL_TIME_CUSTOMER_PROFILE",
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycleState": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        },
        {
            "id": "32a83b5d-a118-4bd6-b3cb-3aee2f4c30a1",
            "audienceId": "test-external-audience-id",
            "name": "externalSegment1",
            "namespace": "aam",
            "imsOrgId": "{ORG_ID}",
            "sandbox":{
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "isSystem": false,
            "description": "Last 30 days",
            "type": "ExternalSegment",
            "originName": "CUSTOM_UPLOAD",
            "lifecycleState": "published",
            "createdBy": "{CREATED_BY_ID}",
            "datasetId": "6254cf3c97f8e31b639fb14d",
            "labels":[
                "core/C1"
            ],
            "linkedAudienceRef": {
                "flowId": "4685ea90-d2b6-11ec-9d64-0242ac120002"
            },
            "creationTime": 1642745034000000,
            "updateEpoch": 1649926314,
            "updateTime": 1649926314000,
            "createEpoch": 1642745034
        }
    ],
    "_page":{
      "totalCount": 111,
      "pageSize": 2,
      "next": "1"
   },
   "_links":{
      "next":{
         "href":"@/audiences?start=1&limit=2&totalCount=111"
      }
   }
}
```

| Eigenschaft | Zielgruppentyp | Beschreibung |
| -------- | ------------- | ----------- | 
| `id` | Beide | Eine systemgenerierte schreibgeschützte Kennung für die Zielgruppe. |
| `audienceId` | Beide | Wenn es sich bei der Audience um eine Platform-generierte Audience handelt, ist dies derselbe Wert wie der `id`. Wenn die Audience extern generiert wird, wird dieser Wert vom Client bereitgestellt. |
| `schema` | Beide | Das Experience-Datenmodell (XDM)-Schema der Zielgruppe. |
| `imsOrgId` | Beide | Die ID der Organisation, zu der die Zielgruppe gehört. |
| `sandbox` | Beide | Informationen zur Sandbox, zu der die Zielgruppe gehört. Weitere Informationen zu Sandboxes finden Sie im [Sandbox-Übersicht](../../sandboxes/home.md). |
| `name` | Beide | Der Name der Zielgruppe. |
| `description` | Beide | Eine Beschreibung der Zielgruppe. |
| `expression` | Plattformgenerierte | Der PQL-Ausdruck (Profile Query Language) der Audience. Weitere Informationen zu PQL-Ausdrücken finden Sie im [Handbuch zu PQL-Ausdrücken](../pql/overview.md). |
| `mergePolicyId` | Plattformgenerierte | Die Kennung der Zusammenführungsrichtlinie, mit der die Zielgruppe verknüpft ist. Weitere Informationen zu Zusammenführungsrichtlinien finden Sie im [Handbuch zu Zusammenführungsrichtlinien](../../profile/api/merge-policies.md). |
| `evaluationInfo` | Plattformgenerierte | Zeigt an, wie die Zielgruppe bewertet wird. Mögliche Auswertungsmethoden sind Batch, synchron (Streaming) oder kontinuierlich (Edge). Weitere Informationen zu den Bewertungsmethoden finden Sie im [Segmentierungsübersicht](../home.md) |
| `dependents` | Beide | Ein Array von Zielgruppen-IDs, die von der aktuellen Zielgruppe abhängen. Dies wird verwendet, wenn Sie eine Zielgruppe erstellen, die ein Segment eines Segments ist. |
| `dependencies` | Beide | Ein Array von Zielgruppen-IDs, von denen die Zielgruppe abhängig ist. Dies wird verwendet, wenn Sie eine Zielgruppe erstellen, die ein Segment eines Segments ist. |
| `type` | Beide | Ein systemgeneriertes Feld, das anzeigt, ob die Zielgruppe Platform-generiert ist oder eine extern generierte Zielgruppe ist. Mögliche Werte sind `SegmentDefinition` und `ExternalSegment`. A `SegmentDefinition` bezieht sich auf eine Zielgruppe, die in Platform generiert wurde, während eine `ExternalSegment` bezieht sich auf eine Zielgruppe, die nicht in Platform generiert wurde. |
| `originName` | Beide | Ein Feld, das auf den Namen der Herkunft der Zielgruppe verweist. Für plattformgenerierte Zielgruppen wird dieser Wert `REAL_TIME_CUSTOMER_PROFILE`. Für in Audience Orchestration generierte Zielgruppen lautet dieser Wert `AUDIENCE_ORCHESTRATION`. Für in Adobe Audience Manager generierte Zielgruppen wird dieser Wert `AUDIENCE_MANAGER`. Für andere extern generierte Zielgruppen wird dieser Wert `CUSTOM_UPLOAD`. |
| `createdBy` | Beide | Die ID des Benutzers, der die Zielgruppe erstellt hat. |
| `labels` | Beide | Datennutzung auf Objektebene und attributbasierte Zugriffssteuerungsbeschriftungen, die für die Zielgruppe relevant sind. |
| `namespace` | Beide | Der Namespace, zu dem die Zielgruppe gehört. Mögliche Werte sind `AAM`, `AAMSegments`, `AAMTraits`und `AEPSegments`. |
| `linkedAudienceRef` | Beide | Ein Objekt, das IDs für andere Zielgruppen-bezogene Systeme enthält. |

+++

## Erstellen einer neuen Zielgruppe {#create}

Sie können eine neue Zielgruppe erstellen, indem Sie eine POST-Anfrage an die `/audiences` -Endpunkt.

**API-Format**

```http
POST /audiences
```

**Anfrage**

>[!BEGINTABS]

>[!TAB Platform-generierte Zielgruppe]

+++ Beispielanfrage zum Erstellen einer Platform-generierten Zielgruppe

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "ups",
        "description": "Last 30 days",
        "type": "SegmentDefinition",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "workAddress.country = \"US\""
        },
        "schema": {
            "name": "_xdm.context.profile"
        },
        "labels": [
          "core/C1"
        ],
        "ttlInDays": 60
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- | 
| `name` | Der Name der Zielgruppe. |
| `description` | Eine Beschreibung der Zielgruppe. |
| `type` | Ein Feld, das anzeigt, ob die Zielgruppe Platform-generiert oder eine extern generierte Zielgruppe ist. Mögliche Werte sind `SegmentDefinition` und `ExternalSegment`. A `SegmentDefinition` bezieht sich auf eine Zielgruppe, die in Platform generiert wurde, während eine `ExternalSegment` bezieht sich auf eine Zielgruppe, die nicht in Platform generiert wurde. |
| `expression` | Der PQL-Ausdruck (Profile Query Language) der Audience. Weitere Informationen zu PQL-Ausdrücken finden Sie im [Handbuch zu PQL-Ausdrücken](../pql/overview.md). |
| `schema` | Das Experience-Datenmodell (XDM)-Schema der Zielgruppe. |
| `labels` | Datennutzung auf Objektebene und attributbasierte Zugriffssteuerungsbeschriftungen, die für die Zielgruppe relevant sind. |
| `ttlInDays` | Stellt den Datenablaufwert für die Zielgruppe in Tagen dar. |

+++

>[!TAB Extern generierte Zielgruppe]

+++ Beispielanfrage zum Erstellen einer extern generierten Zielgruppe

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "audienceId":"test-external-audience-id",
        "name":"externalAudience",
        "namespace":"aam",
        "description":"Last 30 days",
        "type":"ExternalSegment",
        "originName":"CUSTOM_UPLOAD",
        "lifecycleState":"published",
        "datasetId":"6254cf3c97f8e31b639fb14d",
        "labels":[
            "core/C1"
        ],
        "linkedAudienceRef":{
            "flowId": "4685ea90-d2b6-11ec-9d64-0242ac120002"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- | 
| `audienceId` | Eine vom Benutzer bereitgestellte ID für die Zielgruppe. |
| `name` | Der Name der Zielgruppe. |
| `namespace` | Der Namespace für die Zielgruppe. |
| `description` | Eine Beschreibung der Zielgruppe. |
| `type` | Ein Feld, das anzeigt, ob die Zielgruppe Platform-generiert oder eine extern generierte Zielgruppe ist. Mögliche Werte sind `SegmentDefinition` und `ExternalSegment`. A `SegmentDefinition` bezieht sich auf eine Zielgruppe, die in Platform generiert wurde, während eine `ExternalSegment` bezieht sich auf eine Zielgruppe, die nicht in Platform generiert wurde. |
| `originName` | Der Name der Audience-Herkunft. Für extern generierte Zielgruppen lautet der Standardwert `CUSTOM_UPLOAD`. Andere unterstützte Werte sind `REAL_TIME_CUSTOMER_PROFILE`, `CUSTOM_UPLOAD`, `AUDIENCE_ORCHESTRATION`und `AUDIENCE_MATCH`. |
| `lifecycleState` | Ein optionales Feld, das den Anfangsstatus der Zielgruppe bestimmt, die Sie erstellen möchten. Zu den unterstützten Werten gehören `draft`, `published`und `inactive`. |
| `datasetId` | Die ID des Datensatzes, in dem die Daten, die die Zielgruppe enthalten, gefunden werden können. |
| `labels` | Datennutzung auf Objektebene und attributbasierte Zugriffssteuerungsbeschriftungen, die für die Zielgruppe relevant sind. |
| `audienceMeta` | Metadaten, die zur extern generierten Zielgruppe gehören. |
| `linkedAudienceRef` | Ein Objekt, das IDs für andere Zielgruppen-bezogene Systeme enthält. Dies kann Folgendes umfassen: <ul><li>`flowId`: Diese ID wird verwendet, um die Zielgruppe mit dem Datenfluss zu verbinden, der zum Einbringen der Zielgruppendaten verwendet wurde. Weitere Informationen zu den erforderlichen IDs finden Sie im Abschnitt [Erstellen eines Datenfluss-Handbuchs](../../sources/tutorials/api/collect/cloud-storage.md).</li><li>`aoWorkflowId`: Diese ID wird verwendet, um die Zielgruppe mit einer zugehörigen Audience Orchestration-Komposition zu verbinden.&lt;/li/> <li>`payloadFieldGroupRef`: Diese ID wird verwendet, um auf das XDM-Feldergruppen-Schema zu verweisen, das die Struktur der Zielgruppe beschreibt. Weitere Informationen zum Wert dieses Felds finden Sie im [Handbuch zum Endpunkt der XDM-Feldergruppe](../../xdm/api/field-groups.md).</li><li>`audienceFolderId`: Diese ID wird verwendet, um auf die Ordner-ID in Adobe Audience Manager für die Zielgruppe zu verweisen. Weitere Informationen zu dieser API finden Sie im Abschnitt [Handbuch zur Adobe Audience Manager API](https://bank.demdex.com/portal/swagger/index.html#/Segment%20Folder%20API).</ul> |

+++

>[!ENDTABS]

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Informationen zu Ihrer neu erstellten Zielgruppe zurück.

>[!BEGINTABS]

>[!TAB Platform-generierte Zielgruppe]

+++ Eine Beispielantwort beim Erstellen einer Platform-generierten Zielgruppe.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
     "schema": {
      "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem":false,     
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
    },
    "dataGovernancePolicy": {
      "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "originName": "REAL_TIME_CUSTOMER_PROFILE",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycleState": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

+++

>[!TAB Extern generierte Zielgruppe]

+++ Eine Beispielantwort beim Erstellen einer extern generierten Zielgruppe.

```json
{
   "id": "322f9f62-cd27-11ec-9d64-0242ac120002",
   "audienceId": "test-external-audience-id",
   "name": "externalAudience",
   "namespace": "aam",
   "imsOrgId": "{ORG_ID}",
   "sandbox":{
      "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
      "sandboxName": "prod",
      "type": "production",
      "default": true
   },
   "isSystem": false,
   "description": "Last 30 days",
   "type": "ExternalSegment",
   "originName": "CUSTOM_UPLOAD",
   "lifecycleState": "published",
   "createdBy": "{CREATED_BY_ID}",
   "datasetId": "6254cf3c97f8e31b639fb14d",
   "labels": [
      "core/C1"
   ],
   "linkedAudienceRef": {
      "flowId": "4685ea90-d2b6-11ec-9d64-0242ac120002"
   },
   "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
   "creationTime": 1650251290000,
   "updateEpoch": 1650251290,
   "updateTime": 1650251290000,
   "createEpoch": 1650251290
}
```

+++

## Bestimmte Zielgruppe nachschlagen {#get}

Sie können detaillierte Informationen zu einer bestimmten Zielgruppe nachschlagen, indem Sie eine GET-Anfrage an die `/audiences` -Endpunkt und geben Sie die Kennung der Zielgruppe an, die Sie im Anfragepfad abrufen möchten.

**API-Format**

```http
GET /audiences/{AUDIENCE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- | 
| `{AUDIENCE_ID}` | Die Kennung der Zielgruppe, die Sie abrufen möchten. Bitte beachten Sie, dass dies der `id` und **not** die `audienceId` -Feld. |

**Anfrage**

++ + Eine Beispielanfrage zum Abrufen einer Zielgruppe

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Informationen zur angegebenen Zielgruppe zurück. Die Antwort unterscheidet sich je nachdem, ob die Zielgruppe mit Adobe Experience Platform oder externen Quellen generiert wurde.

>[!BEGINTABS]

>[!TAB Platform-generierte Zielgruppe]

+++ Eine Beispielantwort beim Abrufen einer Platform-generierten Zielgruppe.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem": false,
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycleState": "active",
    "labels": [
        "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

+++

>[!TAB Extern generierte Zielgruppe]

+++ Eine Beispielantwort beim Abrufen einer extern generierten Zielgruppe.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "test-external-audience-id",
    "name": "externalAudience",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem": false,
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycleState": "active",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "labels": [
        "core/C1"
    ],
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

+++

>[!ENDTABS]

## Aktualisieren eines Felds in einer Audience {#update-field}

Sie können die Felder einer bestimmten Zielgruppe aktualisieren, indem Sie eine PATCH-Anfrage an die `/audiences` -Endpunkt und die Kennung der Zielgruppe angeben, die Sie im Anfragepfad aktualisieren möchten.

**API-Format**

```http
PATCH /audiences/{AUDIENCE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{AUDIENCE_ID}` | Die ID der Zielgruppe, die Sie aktualisieren möchten. Bitte beachten Sie, dass dies der `id` und **not** die `audienceId` -Feld. |

**Anfrage**

+++ Eine Beispielanfrage zum Aktualisieren eines Felds in einer Zielgruppe.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
     [
        {
            "op": "add",
            "path": "/expression",
            "value": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"CA\""
            }
        }
      ]'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `op` | Für die Aktualisierung von Zielgruppen ist dieser Wert immer `add`. |
| `path` | Der Pfad des Felds, das Sie aktualisieren möchten. |
| `value` | Der Wert, auf den das Feld aktualisiert werden soll. |

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Informationen zu Ihrer neu aktualisierten Zielgruppe zurück.

+++ Eine Beispielantwort beim Aktualisieren eines Felds in einer Zielgruppe.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"CA\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
    },
    "dataGovernancePolicy": {
      "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycleState": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

+++

## Audience aktualisieren {#put}

Sie können eine bestimmte Zielgruppe aktualisieren (überschreiben), indem Sie eine PUT-Anfrage an die `/audiences` -Endpunkt und die Kennung der Zielgruppe angeben, die Sie im Anfragepfad aktualisieren möchten.

**API-Format**

```http
PUT /audiences/{AUDIENCE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{AUDIENCE_ID}` | Die ID der Zielgruppe, die Sie aktualisieren möchten. Bitte beachten Sie, dass dies der `id` und **not** die `audienceId` -Feld. |

**Anfrage**

++ + Eine Beispielanfrage zum Aktualisieren einer gesamten Zielgruppe.

```shell
curl -X PUT https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "audienceId": "test-external-audience-id",
    "name": "New external audience",
    "namespace": "aam",
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycleState": "published",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "labels": [
        "core/C1"
    ]
}' 
```

| Eigenschaft | Beschreibung |
| -------- | ----------- | 
| `audienceId` | Die Kennung der Audience. Bei extern generierten Zielgruppen kann dieser Wert vom Benutzer angegeben werden. |
| `name` | Der Name der Zielgruppe. |
| `namespace` | Der Namespace für die Zielgruppe. |
| `description` | Eine Beschreibung der Zielgruppe. |
| `type` | Ein systemgeneriertes Feld, das anzeigt, ob die Zielgruppe Platform-generiert ist oder eine extern generierte Zielgruppe ist. Mögliche Werte sind `SegmentDefinition` und `ExternalSegment`. A `SegmentDefinition` bezieht sich auf eine Zielgruppe, die in Platform generiert wurde, während eine `ExternalSegment` bezieht sich auf eine Zielgruppe, die nicht in Platform generiert wurde. |
| `lifecycleState` | Der Status der Zielgruppe. Zu den möglichen Werten gehören `draft`, `published` und `inactive`. `draft` steht für den Zeitpunkt der Erstellung der Audience; `published` Zeitpunkt der Veröffentlichung der Zielgruppe und `inactive` wenn die Zielgruppe nicht mehr aktiv ist. |
| `datasetId` | Die ID des Datensatzes, in dem die Zielgruppendaten gefunden werden können. |
| `labels` | Datennutzung auf Objektebene und attributbasierte Zugriffssteuerungsbeschriftungen, die für die Zielgruppe relevant sind. |

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu Ihrer neu aktualisierten Zielgruppe zurück. Beachten Sie, dass die Details Ihrer Zielgruppe je nachdem, ob es sich um eine Platform-generierte Zielgruppe oder eine extern generierte Zielgruppe handelt, unterschiedlich sind.

++ + Eine Beispielantwort beim Aktualisieren einer gesamten Zielgruppe.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-external-audience-id",
    "name": "New external audience",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycleState": "published",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

+++

## Löschen einer Zielgruppe {#delete}

Sie können eine bestimmte Zielgruppe löschen, indem Sie eine DELETE-Anfrage an die `/audiences` -Endpunkt und die Kennung der Zielgruppe angeben, die Sie im Anfragepfad löschen möchten.

**API-Format**

```http
DELETE /audiences/{AUDIENCE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{AUDIENCE_ID}` | Die ID der Zielgruppe, die Sie löschen möchten. Bitte beachten Sie, dass dies der `id` und **not** die `audienceId` -Feld. |

**Anfrage**

+++ Beispielanfrage zum Löschen einer Zielgruppe.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab5 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 ohne Meldung zurück.

## Abrufen mehrerer Zielgruppen {#bulk-get}

Sie können mehrere Zielgruppen abrufen, indem Sie eine POST-Anfrage an die `/audiences/bulk-get` -Endpunkt und geben die IDs der Zielgruppen an, die Sie abrufen möchten.

**API-Format**

```http
POST /audiences/bulk-get
```

**Anfrage**

+++ Eine Beispielanfrage zum Abrufen mehrerer Zielgruppen.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences/bulk-get
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d ' {
    "ids": [
        {
            "id": "72c393ea-caed-441a-9eb6-5f66bb1bd6cd"
        },
        {
            "id": "QU9fLTEzOTgzNTE0MzY0NzY0NDg5NzkyOTkx_6ed34f6f-fe21-4a30-934f-6ffe21fa3075"
        }
    ]
 }
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 207 mit Informationen zu Ihren angeforderten Zielgruppen zurück.

+++ Eine Beispielantwort beim Abrufen mehrerer Zielgruppen.

```json
{
   "results":{
      "72c393ea-caed-441a-9eb6-5f66bb1bd6cd":{
         "id": "72c393ea-caed-441a-9eb6-5f66bb1bd6cd",
         "audienceId": "72c393ea-caed-441a-9eb6-5f66bb1bd6cd",
         "schema": {
            "name": "_xdm.context.profile"
         },
         "ttlInDays": 30,
         "imsOrgId": "{ORG_ID}",
         "sandbox": {
            "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
            "sandboxName": "prod",
            "type": "production",
            "default": true
         },
         "name": "Sample audience",
         "expression": {
            "type": "pql",
            "format": "pql/text",
            "value": "_id = \"abc\""         
        },
         "mergePolicyId": "87c94d51-239c-4391-932c-29c2412100e5",
         "evaluationInfo": {
            "batch": {
               "enabled": false
            },
            "continuous": {
               "enabled": true
            },
            "synchronous": {
               "enabled": false
            }
         },
         "ansibleUiEnabled": false,
         "dataGovernancePolicy": {
            "excludeOptOut": true
         },
         "creationTime": 1623889553000000,
         "updateEpoch": 1674646369,
         "updateTime": 1674646369000,
         "createEpoch": 1623889552,
         "_etag": "\"61030ec7-0000-0200-0000-63d113610000\"",
         "dependents": [],
         "definedOn": [
            {
               "meta:resourceType": "unions",
               "meta:containerId": "tenant",
               "$ref": "https://ns.adobe.com/xdm/context/profile__union"
            }
         ],
         "dependencies": [],
         "type": "SegmentDefinition",
         "state": "enabled",
         "overridePerformanceWarnings": false,
         "lastModifiedBy": "{CREATED_ID}",
         "lifecycleState": "published",
         "namespace": "AEPSegments",
         "isSystem": false,
         "saveSegmentMembership": true,
         "originName": "REAL_TIME_CUSTOMER_PROFILE"
      },
      "QU9fLTEzOTgzNTE0MzY0NzY0NDg5NzkyOTkx_6ed34f6f-fe21-4a30-934f-6ffe21fa3075":{
         "id": "QU9fLTEzOTgzNTE0MzY0NzY0NDg5NzkyOTkx_6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
         "name": "label test24764489707692",
         "namespace": "AO",
         "imsOrgId": "{ORG_ID}",
         "sandbox":{
            "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
            "sandboxName": "prod",
            "type": "production",
            "default": true
         },
         "type": "ExternalSegment",
         "lifecycleState": "published",
         "sourceId": "source-id",
         "createdBy": "{USER_ID}",
         "datasetId": "62bf31a105e9891b63525c92",
         "_etag": "\"3100da6d-0000-0200-0000-62bf31a10000\"",
         "creationTime": 1656697249000,
         "updateEpoch": 1656697249,
         "updateTime": 1656697249000,
         "createEpoch": 1656697249,
         "audienceId": "test-audience-id",
         "isSystem": false,
         "saveSegmentMembership": true,
         "linkedAudienceRef": {
            "aoWorkflowId": "62bf31858e87e34c8364befa"
         },
         "originName": "AUDIENCE_ORCHESTRATION"
      }
   }
}
```

+++

## Mehrere Zielgruppen aktualisieren {#bulk-patch}

Sie können das Profil aktualisieren und die Anzahl mehrerer Zielgruppen aufzeichnen, indem Sie eine POST-Anfrage an die `/audiences/bulk-patch-metric` -Endpunkt und geben die IDs der Zielgruppen an, die Sie aktualisieren möchten.

**API-Format**

```http
POST /audiences/bulk-patch-metric
```

**Anfrage**

+++ Eine Beispielanfrage zum Aktualisieren mehrerer Zielgruppen.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences/bulk-patch-metric
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d ' {
    "jobId": "12345",
    "jobType": "AO",
    "resources": [
        {
            "audienceId": "QUFNVHJhaXRzX2V4dGVybmFsU2VnbWVudC1hdWRpZW5jZS1pZA_6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
            "namespace": "AAMTraits",
            "operations": [
                {
                    "op": "add",
                    "path": "/metrics/data",
                    "value": {
                        "totalProfiles": 11037
                    }
                },
            ]
        },
        {
            "audienceId": "QUFNVHJhaXRzX2V4dGVybmFsU2VnbWVudC1hdWRpZW5jZS1pZA_6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
            "namespace": "AAMTraits",
            "operations": [
                {
                    "op": "add",
                    "path": "/metrics/data",
                    "value": {
                        "totalProfiles": 523
                    }
                }
            ]
        }
    ]
    }
```

<table>
<thead>
<tr>
<th>Parameter</th>
<th>Beschreibung</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>jobId</code></td>
<td>Die ID des Auftrags, der die Aktualisierung ausführt.</td>
</tr>
<tr>
<td><code>jobType</code></td>
<td>Der Auftragstyp, der die Aktualisierung ausführt. Dieser Wert kann entweder <code>export</code> oder <code>AO</code>.</td>
</tr>
<tr>
<td><code>audienceId</code></td>
<td>Die ID der Zielgruppen, die Sie aktualisieren möchten. Bitte beachten Sie, dass dies der <code>audienceId</code> Wert und <strong>not</strong> die <code>id</code> Wert der Zielgruppen.</td>
</tr>
<tr>
<td><code>namespace</code></td>
<td>Der Namespace für die Zielgruppe, die Sie aktualisieren möchten.</td>
</tr>
<tr>
<td><code>operations</code></td>
<td>Ein Objekt, das die zur Aktualisierung der Audience verwendeten Informationen enthält.</td>
</tr>
<tr>
<td><code>operations.op</code></td>
<td>Der für den Patch verwendete Vorgang. Beim Aktualisieren mehrerer Zielgruppen lautet dieser Wert <strong>always</strong> <code>add</code>.</td>
</tr>
<tr>
<td><code>operations.path</code></td>
<td>Der Pfad des zu aktualisierenden Felds. Derzeit werden nur zwei Pfade unterstützt: <code>/metrics/data</code> beim Aktualisieren der <strong>profile</strong> zählen und <code>/recordMetrics/data</code> beim Aktualisieren der <strong>record</strong> count.</td>
</tr>
<tr>
<td><code>operations.value</code></td>
<td>
Der -Wert des zu aktualisierenden Felds. Wenn Sie die Profilanzahl aktualisieren, sieht dieser Wert wie folgt aus: 
<pre>
{ "totalProfiles": 123456 }
</pre>
Wenn Sie die Datensatzanzahl aktualisieren, sieht dieser Wert wie folgt aus: 
<pre>
{ "recordCount": 123456 }
</pre>
</td>
</tr>
</tbody>
</table>

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 207 mit Details zu den aktualisierten Zielgruppen zurück.

+++ Eine Beispielantwort zum Aktualisieren mehrerer Zielgruppen.

```json
{
   "resources":[
      {
         "audienceId":"QUFNVHJhaXRzX2V4dGVybmFsU2VnbWVudC1hdWRpZW5jZS1pZA_6ed34f6f-fe21-4a30-934f-6ffe21fa3075",

         "namespace": "AAMTraits",
         "status":200
      },
      {
         "audienceId":"QUFNVHJhaXRzX2V4dGVybmFsU2VnbWVudC1vcmlnaW4tdGVzdDE_6ed34f6f-fe21-4a30-934f-6ffe21fa3075",

         "namespace": "AAMTraits",
         "status":200
      }
   ]
}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `status` | Der Status der aktualisierten Zielgruppe. Wenn der zurückgegebene Status 200 ist, wurde die Zielgruppe erfolgreich aktualisiert. Wenn die Audience nicht aktualisiert werden konnte, wird ein Fehler zurückgegeben, der erklärt, warum die Audience nicht aktualisiert wurde. |

+++

## Nächste Schritte

Nach dem Lesen dieses Handbuchs erfahren Sie jetzt mehr über das Erstellen, Verwalten und Löschen von Zielgruppen mithilfe der Adobe Experience Platform-API. Weitere Informationen zum Zielgruppen-Management mithilfe der Benutzeroberfläche finden Sie im Abschnitt [Handbuch zur Segmentierungsbenutzeroberfläche](../ui/overview.md).
