---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Anzeigen effektiver Richtlinien
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 69%

---


# Anzeigen effektiver Richtlinien

To view effective policies for the current user, make a POST request to the `/acl/effective-policies` endpoint in the [!DNL Access Control] API. Die Berechtigungen und Ressourcentypen, die Sie abrufen möchten, müssen in der Anfrage-Payload in Form eines Arrays angegeben werden. Dies wird im folgenden Beispiel-API-Aufruf demonstriert.

**API-Format**

```http
POST /acl/effective-policies
```

**Anfrage**

The following requests retrieves information about the &quot;[!UICONTROL Manage Datasets]&quot; permission and access to the &quot;[!UICONTROL schemas]&quot; resource type for the current user.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/acl/effective-policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    "/permissions/manage-datasets",
    "/resource-types/schemas"
  ]'
```

>[!NOTE]
>
>Eine vollständige Liste der Berechtigungen und Ressourcentypen, die im Payload-Array bereitgestellt werden können, finden Sie im Anhang im Abschnitt [zu den akzeptierten Berechtigungen und Ressourcentypen](#accepted-permissions-and-resource-types).

**Antwort**

Eine erfolgreiche Antwort gibt Informationen über die in der Anfrage angegebenen Berechtigungen und Ressourcentypen zurück. Die Antwort enthält die aktiven Berechtigungen, die der aktuelle Benutzer für die in der Anfrage angegebenen Ressourcentypen hat. Wenn eine in der Anfrage-Payload enthaltene Berechtigung für den aktuellen Benutzer aktiv sind, gibt die API die Berechtigung mit einem Asterisk (`*`) zurück, um anzuzeigen, dass die Berechtigung aktiv ist. In der Anfrage angegebene Berechtigungen, die für den Benutzer nicht aktiv sind, werden in der Antwort-Payload weggelassen.

```json
{
    "policies": {
        "/resource-types/schemas": [
            "read",
            "write",
            "delete"
        ],
        "/permissions/manage-datasets": [
            "*"
        ]
    }
}
```

## Nächste Schritte

This document covered how to make calls to the [!DNL Access Control] API to return information on active permissions and related policies for resource types. For more information about access control for [!DNL Experience Platform], see the [access control overview](../home.md).

## Anhang

This section provides supplemental information for using the [!DNL Access Control] API.

### Akzeptierte Berechtigungen und Ressourcentypen

Im Folgenden finden Sie eine Liste der Berechtigungen und Ressourcentypen, die Sie in die Payload einer POST-Anfrage an den `/acl/active-permissions`-Endpunkt aufnehmen können.

**Berechtigungen**

```plaintext
"permissions/activate-destinations"
"permissions/export-audience-for-segments"
"permissions/manage-datasets"
"permissions/manage-destinations"
"permissions/manage-identity-namespaces"
"permissions/manage-profiles"
"permissions/manage-sandboxes"
"permissions/manage-schemas"
"permissions/reset-sandboxes"
"permissions/view-datasets"
"permissions/view-destinations"
"permissions/view-identity-namespaces"
"permissions/view-monitoring-dashboard"
"permissions/view-profiles"
"permissions/view-sandboxes"
"permissions/view-schemas"
```

**Ressourcentypen**

```plaintext
"resource-types/classes"
"resource-types/connections"
"resource-types/data-types"
"resource-types/dataset-data"
"resource-types/datasets"
"resource-types/destinations"
"resource-types/dule-labels"
"resource-types/identity-descriptors"
"resource-types/identity-namespaces"
"resource-types/mixins"
"resource-types/monitoring"
"resource-types/profile-configs
"resource-types/profile-datasets"
"resource-types/profiles"
"resource-types/relationship-descriptors"
"resource-types/reset-sandboxes"
"resource-types/sandboxes"
"resource-types/schemas"
"resource-types/segment-jobs"
"resource-types/segments"
```
