---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Effektive Ansicht
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 1%

---


# Effektive Ansicht

Um effektive Richtlinien für den aktuellen Benutzer Ansicht, erstellen Sie eine POST-Anforderung an den `/acl/effective-policies` Endpunkt in der Zugriffskontrollen-API. Die Berechtigungen und Ressourcentypen, die Sie abrufen möchten, müssen in der Anforderungs-Nutzlast in Form eines Arrays bereitgestellt werden. Dies wird im Beispiel-API-Aufruf unten gezeigt.

**API-Format**

```http
POST /acl/effective-policies
```

**Anfrage**

Die folgenden Anforderungen rufen Informationen über die Berechtigung &quot;Datasets verwalten&quot;und den Zugriff auf den Ressourcentyp &quot;Schema&quot;für den aktuellen Benutzer ab.

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
>Eine vollständige Liste der Berechtigungen und Ressourcentypen, die im Payload-Array bereitgestellt werden können, finden Sie im Anhang zu [zulässigen Berechtigungen und Ressourcentypen](#accepted-permissions-and-resource-types).

**Antwort**

Eine erfolgreiche Antwort gibt Informationen zu den Berechtigungen und Ressourcentypen zurück, die in der Anforderung bereitgestellt werden. Die Antwort umfasst die aktiven Berechtigungen, die dem aktuellen Benutzer für die in der Anforderung angegebenen Ressourcentypen zugewiesen sind. Wenn in der Anforderungsnutzlast enthaltene Berechtigungen für den aktuellen Benutzer aktiv sind, gibt die API die Berechtigung mit einem Sternchen (`*`) zurück, um anzugeben, dass die Berechtigung aktiv ist. In der Anforderung bereitgestellte Berechtigungen, die für den Benutzer nicht aktiv sind, werden in der Antwortnutzlast weggelassen.

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

In diesem Dokument wurde beschrieben, wie Sie die Zugriffskontrollen-API aufrufen, um Informationen über aktive Berechtigungen und zugehörige Richtlinien für Ressourcentypen zurückzugeben. Weitere Informationen zur Zugriffskontrolle der Experience Platform finden Sie in der Übersicht über die [Zugriffskontrolle](../home.md).

## Anhang

Dieser Abschnitt enthält zusätzliche Informationen zur Verwendung der Zugriffskontrollen-API.

### Akzeptierte Berechtigungen und Ressourcentypen

Im Folgenden finden Sie eine Liste von Berechtigungen und Ressourcentypen, die Sie in die Nutzlast einer POST-Anforderung an den `/acl/active-permissions` Endpunkt einbeziehen können.

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
