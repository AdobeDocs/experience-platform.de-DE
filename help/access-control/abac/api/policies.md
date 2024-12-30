---
keywords: Experience Platform;Startseite;beliebte Themen;api;attributbasierte Zugriffssteuerung;attributbasierte Zugriffssteuerung
solution: Experience Platform
title: API-Endpunkt für Zugriffssteuerungsrichtlinien
description: Mit dem Endpunkt /policies in der attributbasierten Zugriffssteuerungs-API können Sie Richtlinien in Adobe Experience Platform programmgesteuert verwalten.
role: Developer
exl-id: 07690f43-fdd9-4254-9324-84e6bd226743
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1433'
ht-degree: 10%

---

# Endpunkt für Zugriffssteuerungsrichtlinien

>[!NOTE]
>
>Wenn ein Benutzer-Token übergeben wird, muss der Benutzer des Tokens über eine „org admin“-Rolle für die angeforderte Organisation verfügen.

Zugriffssteuerungsrichtlinien sind Anweisungen, die Attribute zusammenführen, um zulässige und unzulässige Aktionen festzulegen. Diese Richtlinien können entweder lokal oder global sein und andere Richtlinien überschreiben. Der `/policies`-Endpunkt in der attributbasierten Zugriffssteuerungs-API ermöglicht Ihnen die programmgesteuerte Verwaltung von Richtlinien, einschließlich Informationen zu den für sie geltenden Regeln und zu ihren jeweiligen Betreffbedingungen.

>[!IMPORTANT]
>
>Dieser Endpunkt ist nicht mit dem `/policies`-Endpunkt in der [Policy Service API](../../../data-governance/api/policies.md) zu verwechseln, der zur Verwaltung von Datennutzungsrichtlinien verwendet wird.

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil der attributbasierten Zugriffssteuerungs-API. Bevor Sie fortfahren, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den erforderlichen Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

## Abrufen einer Liste von Richtlinien {#list}

Stellen Sie eine GET-Anfrage an den `/policies`-Endpunkt, um alle in Ihrem Unternehmen vorhandenen Richtlinien aufzulisten.

**API-Format**

```http
GET /policies
```

**Anfrage**

Mit der folgenden Anfrage wird eine Liste der vorhandenen Richtlinien abgerufen.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste vorhandener Richtlinien zurück.

```json
{
  {
      "id": "7019068e-a3a0-48ce-b56b-008109470592",
      "imsOrgId": "{IMS_ORG}",
      "createdBy": "{CREATED_BY}",
      "createdAt": 1652892767559,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1652895736367,
      "name": "schema-field",
      "description": "schema-field",
      "status": "inactive",
      "subjectCondition": null,
      "rules": [
          {
              "effect": "Deny",
              "resource": "/orgs/{IMS_ORG}/sandboxes/xql/schemas/*/schema-fields/*",
              "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
              "actions": [
                  "com.adobe.action.read",
                  "com.adobe.action.write",
                  "com.adobe.action.view"
              ]
          },
          {
              "effect": "Permit",
              "resource": "/orgs/{IMS_ORG}/sandboxes/*/schemas/*/schema-fields/*",
              "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
              "actions": [
                  "com.adobe.action.delete"
              ]
          },
          {
              "effect": "Deny",
              "resource": "/orgs/{IMS_ORG}/sandboxes/delete-sandbox-adfengine-test-8/segments/*",
              "condition": "{\"!\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}",
              "actions": [
                  "com.adobe.action.write"
              ]
          }
      ],
      "_etag": "\"0300593f-0000-0200-0000-62852ff80000\""
  },
  {
      "id": "13138ef6-c007-495d-837f-0a248867e219",
      "imsOrgId": "{IMS_ORG}",
      "createdBy": "{CREATED_BY}",
      "createdAt": 1652859368555,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1652890780206,
      "name": "Documentation-Copy",
      "description": "xyz",
      "status": "active",
      "subjectCondition": null,
      "rules": [
          {
              "effect": "Permit",
              "resource": "orgs/{IMS_ORG}/sandboxes/ro-sand/schemas/*/schema-fields/*",
              "condition": "{\"!\":[{\"or\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"and\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}]}]}",
              "actions": [
                  "com.adobe.action.read"
              ]
          },
          {
              "effect": "Deny",
              "resource": "orgs/{IMS_ORG}/sandboxes/*/segments/*",
              "condition": "{\"!\":[{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}]}",
              "actions": [
                  "com.adobe.action.read"
              ]
          }
      ],
      "_etag": "\"0300d43c-0000-0200-0000-62851c9c0000\""
  },
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `id` | Die ID, die einer Richtlinie entspricht. Diese Kennung wird automatisch generiert und kann zum Suchen, Aktualisieren und Löschen einer Richtlinie verwendet werden. |
| `imsOrgId` | Die Organisation, in der die abgefragte Richtlinie verfügbar ist. |
| `createdBy` | Die ID des Benutzers, der die Richtlinie erstellt hat. |
| `createdAt` | Der Zeitpunkt, zu dem die Richtlinie erstellt wurde. Die `createdAt`-Eigenschaft wird im Unix-Epochenzeitstempel angezeigt. |
| `modifiedBy` | Die ID des Benutzers, der die Richtlinie zuletzt aktualisiert hat. |
| `modifiedAt` | Der Zeitpunkt, zu dem die Richtlinie zuletzt aktualisiert wurde. Die `modifiedAt`-Eigenschaft wird im Unix-Epochenzeitstempel angezeigt. |
| `name` | Der Name der Richtlinie. |
| `description` | (Optional) Eine Eigenschaft, die hinzugefügt werden kann, um weitere Informationen zu einer bestimmten Richtlinie bereitzustellen. |
| `status` | Der aktuelle Status einer Richtlinie. Diese Eigenschaft definiert, ob eine Richtlinie derzeit `active` oder `inactive` ist. |
| `subjectCondition` | Die Bedingungen, die auf ein Subjekt angewendet werden. Ein Subjekt ist ein Benutzer mit bestimmten Attributen, der Zugriff auf eine Ressource anfordert, um eine Aktion durchzuführen. In diesem Fall sind `subjectCondition` abfragebasierte Bedingungen, die auf die Betreffattribute angewendet werden. |
| `rules` | Der Regelsatz, der eine Richtlinie definiert. Regeln definieren, welche Attributkombinationen zulässig sind, damit der Betreff erfolgreich eine Aktion auf der Ressource durchführen kann. |
| `rules.effect` | Der Effekt, der sich nach der Berücksichtigung von Werten für `action`, `condition` und `resource` ergibt. Mögliche Werte sind: `permit`, `deny` oder `indeterminate`. |
| `rules.resource` | Das Asset oder Objekt, auf das ein Subjekt zugreifen kann oder nicht.  Bei Ressourcen kann es sich um Dateien, Anwendungen, Server oder sogar APIs handeln. |
| `rules.condition` | Die auf eine Ressource angewendeten Bedingungen. Wenn eine Ressource beispielsweise ein Schema ist, können auf ein Schema bestimmte Kennzeichnungen angewendet werden, die dazu beitragen, ob eine Aktion gegen dieses Schema zulässig oder unzulässig ist. |
| `rules.action` | Die Aktion, die ein Subjekt für eine abgefragte Ressource ausführen darf. Mögliche Werte sind: `read`, `create`, `edit` und `delete`. |

## Richtliniendetails nach ID nachschlagen {#lookup}

Stellen Sie eine GET-Anfrage an den `/policies`-Endpunkt, während Sie im Anfragepfad eine Richtlinien-ID angeben, um Informationen über diese einzelne Richtlinie abzurufen.

**API-Format**

```http
GET /policies/{POLICY_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| {POLICY_ID} | Die ID der Richtlinie, die Sie abrufen möchten. |

**Anfrage**

Die folgende Anfrage ruft Informationen zu einer einzelnen Richtlinie ab.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/13138ef6-c007-495d-837f-0a248867e219 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Antwort**

Bei einer erfolgreichen Anfrage werden Informationen zur abgefragten Richtlinien-ID zurückgegeben.

```json
{
  "policies": [
    {
      "id": "7019068e-a3a0-48ce-b56b-008109470592",
      "imsOrgId": "5555467B5D8013E50A494220@AdobeOrg",
      "createdBy": "example@AdobeID",
      "createdAt": 1652892767559,
      "modifiedBy": "example@AdobeID",
      "modifiedAt": 1652895736367,
      "name": "schema-field",
      "description": "schema-field",
      "status": "inactive",
      "subjectCondition": null,
      "rules": [
        {
          "effect": "Deny",
          "resource": "/orgs/5555467B5D8013E50A494220@AdobeOrg/sandboxes/xql/schemas/*/schema-fields/*",
          "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
          "actions": [
            "com.adobe.action.read",
            "com.adobe.action.write",
            "com.adobe.action.view"
          ]
        },
        {
          "effect": "Permit",
          "resource": "/orgs/5555467B5D8013E50A494220@AdobeOrg/sandboxes/*/schemas/*/schema-fields/*",
          "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
          "actions": [
            "com.adobe.action.delete"
          ]
        },
        {
          "effect": "Deny",
          "resource": "/orgs/5555467B5D8013E50A494220@AdobeOrg/sandboxes/delete-sandbox-adfengine-test-8/segments/*",
          "condition": "{\"!\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}",
          "actions": [
            "com.adobe.action.write"
          ]
        }
      ],
      "etag": "\"0300593f-0000-0200-0000-62852ff80000\""
    }
  ]
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `id` | Die ID, die einer Richtlinie entspricht. Diese Kennung wird automatisch generiert und kann zum Suchen, Aktualisieren und Löschen einer Richtlinie verwendet werden. |
| `imsOrgId` | Die Organisation, in der die abgefragte Richtlinie verfügbar ist. |
| `createdBy` | Die ID des Benutzers, der die Richtlinie erstellt hat. |
| `createdAt` | Der Zeitpunkt, zu dem die Richtlinie erstellt wurde. Die `createdAt`-Eigenschaft wird im Unix-Epochenzeitstempel angezeigt. |
| `modifiedBy` | Die ID des Benutzers, der die Richtlinie zuletzt aktualisiert hat. |
| `modifiedAt` | Der Zeitpunkt, zu dem die Richtlinie zuletzt aktualisiert wurde. Die `modifiedAt`-Eigenschaft wird im Unix-Epochenzeitstempel angezeigt. |
| `name` | Der Name der Richtlinie. |
| `description` | (Optional) Eine Eigenschaft, die hinzugefügt werden kann, um weitere Informationen zu einer bestimmten Richtlinie bereitzustellen. |
| `status` | Der aktuelle Status einer Richtlinie. Diese Eigenschaft definiert, ob eine Richtlinie derzeit `active` oder `inactive` ist. |
| `subjectCondition` | Die Bedingungen, die auf ein Subjekt angewendet werden. Ein Subjekt ist ein Benutzer mit bestimmten Attributen, der Zugriff auf eine Ressource anfordert, um eine Aktion durchzuführen. In diesem Fall sind `subjectCondition` abfragebasierte Bedingungen, die auf die Betreffattribute angewendet werden. |
| `rules` | Der Regelsatz, der eine Richtlinie definiert. Regeln definieren, welche Attributkombinationen zulässig sind, damit der Betreff erfolgreich eine Aktion auf der Ressource durchführen kann. |
| `rules.effect` | Der Effekt, der sich nach der Berücksichtigung von Werten für `action`, `condition` und `resource` ergibt. Mögliche Werte sind: `permit`, `deny` oder `indeterminate`. |
| `rules.resource` | Das Asset oder Objekt, auf das ein Subjekt zugreifen kann oder nicht.  Bei Ressourcen kann es sich um Dateien, Anwendungen, Server oder sogar APIs handeln. |
| `rules.condition` | Die auf eine Ressource angewendeten Bedingungen. Wenn eine Ressource beispielsweise ein Schema ist, können auf ein Schema bestimmte Kennzeichnungen angewendet werden, die dazu beitragen, ob eine Aktion gegen dieses Schema zulässig oder unzulässig ist. |
| `rules.action` | Die Aktion, die ein Subjekt für eine abgefragte Ressource ausführen darf. Mögliche Werte sind: `read`, `create`, `edit` und `delete`. |


## Erstellen einer Richtlinie {#create}

Um eine neue Richtlinie zu erstellen, stellen Sie eine POST-Anfrage an den `/policies`-Endpunkt.

**API-Format**

```http
POST /policies
```

**Anfrage**

Die folgende Anfrage erstellt eine neue Richtlinie mit dem Namen `acme-integration-policy`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/administration/policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
      "name": "acme-integration-policy",
      "description": "Policy for ACME",
      "imsOrgId": "{IMS_ORG}",
      "rules": [
        {
          "effect": "Permit",
          "resource": "/orgs/{IMS_ORG}/sandboxes/*",
          "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
          "actions": [
            "com.adobe.action.read"
          ]
        }
      ]
    }'
```

| Parameter | Beschreibung |
| --- | --- |
| `name` | Der Name der Richtlinie. |
| `description` | (Optional) Eine Eigenschaft, die hinzugefügt werden kann, um weitere Informationen zu einer bestimmten Richtlinie bereitzustellen. |
| `imsOrgId` | Die Organisation, die die Richtlinie enthält. |
| `rules` | Der Regelsatz, der eine Richtlinie definiert. Regeln definieren, welche Attributkombinationen zulässig sind, damit der Betreff erfolgreich eine Aktion auf der Ressource durchführen kann. |
| `rules.effect` | Der Effekt, der sich nach der Berücksichtigung von Werten für `action`, `condition` und `resource` ergibt. Mögliche Werte sind: `permit`, `deny` oder `indeterminate`. |
| `rules.resource` | Das Asset oder Objekt, auf das ein Subjekt zugreifen kann oder nicht.  Bei Ressourcen kann es sich um Dateien, Anwendungen, Server oder sogar APIs handeln. |
| `rules.condition` | Die auf eine Ressource angewendeten Bedingungen. Wenn eine Ressource beispielsweise ein Schema ist, können auf ein Schema bestimmte Kennzeichnungen angewendet werden, die dazu beitragen, ob eine Aktion gegen dieses Schema zulässig oder unzulässig ist. |
| `rules.action` | Die Aktion, die ein Subjekt für eine abgefragte Ressource ausführen darf. Mögliche Werte sind: `read`, `create`, `edit` und `delete`. |

**Antwort**

Eine erfolgreiche Anfrage gibt die neu erstellte Richtlinie zurück, einschließlich der eindeutigen Richtlinien-ID und der zugehörigen Regeln.

```json
{
    "id": "c3863937-5d40-448d-a7be-416e538f955e",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "{CREATED_BY}",
    "createdAt": 1652988384458,
    "modifiedBy": "{MODIFIED_BY}",
    "modifiedAt": 1652988384458,
    "name": "acme-integration-policy",
    "description": "Policy for ACME",
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Permit",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "com.adobe.action.read"
            ]
        }
    ],
    "_etag": null
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `id` | Die ID, die einer Richtlinie entspricht. Diese Kennung wird automatisch generiert und kann zum Suchen, Aktualisieren und Löschen einer Richtlinie verwendet werden. |
| `name` | Der Name einer Richtlinie. |
| `rules` | Der Regelsatz, der eine Richtlinie definiert. Regeln definieren, welche Attributkombinationen zulässig sind, damit der Betreff erfolgreich eine Aktion auf der Ressource durchführen kann. |
| `rules.effect` | Der Effekt, der sich nach der Berücksichtigung von Werten für `action`, `condition` und `resource` ergibt. Mögliche Werte sind: `permit`, `deny` oder `indeterminate`. |
| `rules.resource` | Das Asset oder Objekt, auf das ein Subjekt zugreifen kann oder nicht.  Bei Ressourcen kann es sich um Dateien, Anwendungen, Server oder sogar APIs handeln. |
| `rules.condition` | Die auf eine Ressource angewendeten Bedingungen. Wenn eine Ressource beispielsweise ein Schema ist, können auf ein Schema bestimmte Kennzeichnungen angewendet werden, die dazu beitragen, ob eine Aktion gegen dieses Schema zulässig oder unzulässig ist. |
| `rules.action` | Die Aktion, die ein Subjekt für eine abgefragte Ressource ausführen darf. Mögliche Werte sind: `read`, `create`, `edit` und `delete`. |


## Aktualisieren einer Richtlinie nach Richtlinien-ID {#put}

Um die Regeln einer einzelnen Richtlinie zu aktualisieren, stellen Sie eine PUT-Anfrage an den `/policies`-Endpunkt, wobei Sie im Anfragepfad die ID der Richtlinie angeben, die Sie aktualisieren möchten.

**API-Format**

```http
PUT /policies/{POLICY_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| {POLICY_ID} | Die ID der Richtlinie, die Sie aktualisieren möchten. |

**Anfrage**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/8cf487d7-3642-4243-a8ea-213d72f694b9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
      "id": "8cf487d7-3642-4243-a8ea-213d72f694b9",
      "imsOrgId": "{IMS_ORG}",
      "name": "test-2",
      "rules": [
      {
        "effect": "Deny",
        "resource": "/orgs/{IMS_ORG}/sandboxes/*",
        "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
        "actions": [
          "com.adobe.action.read"
        ]
      }
    ]
  }'
```

**Antwort**

Eine erfolgreiche Antwort gibt die aktualisierte Richtlinie zurück.

```json
{
    "id": "8cf487d7-3642-4243-a8ea-213d72f694b9",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "{CREATED_BY}",
    "createdAt": 1652988866647,
    "modifiedBy": "{MODIFIED_BY}",
    "modifiedAt": 1652989297287,
    "name": "test-2",
    "description": null,
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Deny",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "com.adobe.action.read"
            ]
        }
    ],
    "_etag": null
}
```

## Richtlinieneigenschaften aktualisieren {#patch}

Um die Eigenschaften einer einzelnen Richtlinie zu aktualisieren, stellen Sie eine PATCH-Anfrage an den `/policies`-Endpunkt, wobei Sie im Anfragepfad die ID der Richtlinie angeben, die Sie aktualisieren möchten.

**API-Format**

```http
PATCH /policies/{POLICY_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| {POLICY_ID} | Die ID der Richtlinie, die Sie aktualisieren möchten. |

**Anfrage**

Die folgende Anfrage ersetzt den Wert `/description` in der Richtlinien-ID `c3863937-5d40-448d-a7be-416e538f955e`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/c3863937-5d40-448d-a7be-416e538f955e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "operations": [
      {
        "op": "replace",
        "path": "/description",
        "value": "Pre-set policy to be applied for ACME"
      }
    ]
  }'
```

| Funktionsweise | Beschreibung |
| --- | --- |
| `op` | Der Operationsaufruf, der verwendet wird, um die Aktion zu definieren, die zum Aktualisieren der Rolle erforderlich ist. Die Operationen umfassen `add`, `replace` und `remove`. |
| `path` | Der Pfad des zu aktualisierenden Parameters. |
| `value` | Der neue Wert, mit dem Sie Ihren Parameter aktualisieren möchten. |

**Antwort**

Eine erfolgreiche Antwort gibt die abgefragte Richtlinien-ID mit der aktualisierten Beschreibung zurück.

```json
{
    "id": "c3863937-5d40-448d-a7be-416e538f955e",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "acp_accessControlService",
    "createdAt": 1652988384458,
    "modifiedBy": "acp_accessControlService",
    "modifiedAt": 1652988384458,
    "name": "acme-integration-policy",
    "description": "Pre-set policy to be applied for ACME",
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Permit",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "com.adobe.action.read"
            ]
        }
    ],
    "_etag": null
}
```

## Löschen einer Richtlinie {#delete}

Um eine Richtlinie zu löschen, stellen Sie eine DELETE-Anfrage an den `/policies`-Endpunkt, wobei Sie die ID der Richtlinie angeben, die Sie löschen möchten.

**API-Format**

```http
DELETE /policies/{POLICY_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| {POLICY_ID} | Die ID der Richtlinie, die Sie löschen möchten. |

**Anfrage**

Die folgende Anfrage löscht die Richtlinie mit der ID `c3863937-5d40-448d-a7be-416e538f955e`.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/c3863937-5d40-448d-a7be-416e538f955e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) und leeren Text zurück.

Sie können den Löschvorgang bestätigen, indem Sie eine Suchanfrage (GET) an die Richtlinie stellen. Sie erhalten den HTTP-Status 404 (Nicht gefunden), da die Richtlinie aus der Administration entfernt wurde.
