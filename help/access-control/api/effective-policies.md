---
keywords: Experience Platform;Home;beliebte Themen;Effektive Richtlinien;Zugriffssteuerungs-API
solution: Experience Platform
title: API-Endpunkt für effektive Richtlinien
description: Erfahren Sie, wie Sie effektive Zugriffsrichtlinien mithilfe der Access Control-API für Adobe Experience Platform anzeigen können.
exl-id: 555d73db-115d-4f4c-8bd2-b91477799591
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 80%

---

# Endpunkt für effektive Richtlinien

Um effektive Zugriffssteuerungsrichtlinien für den aktuellen Benutzer anzuzeigen, stellen Sie eine POST-Anfrage an die `/acl/effective-policies` -Endpunkt im [!DNL Access Control] API. Die Berechtigungen und Ressourcentypen, die Sie abrufen möchten, müssen in der Anfrage-Payload in Form eines Arrays angegeben werden. Dies wird im folgenden Beispiel-API-Aufruf demonstriert.

**API-Format**

```http
POST /acl/effective-policies
```

**Anfrage**

Mit den folgenden Anfragen werden Informationen zur Zugriffsberechtigung [!UICONTROL Datensätze verwalten] und zum Zugriff auf den Ressourcentyp [!UICONTROL Schemas] für den aktuellen Benutzer abgerufen.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/acl/effective-policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

In diesem Dokument wurde beschrieben, wie Sie Aufrufe an die [!DNL Access Control] API zum Zurückgeben von Informationen zu aktiven Berechtigungen und zugehörigen Zugriffsrichtlinien für Ressourcentypen. Weitere Informationen zur Zugriffssteuerung für [!DNL Experience Platform] finden Sie in [Zugriffssteuerung – Übersicht](../home.md).

## Anhang

Dieser Abschnitt enthält zusätzliche Informationen zur Verwendung der [!DNL Access Control]-API.

### Akzeptierte Berechtigungen und Ressourcentypen

Im Folgenden finden Sie eine Liste der Berechtigungen und Ressourcentypen, die Sie in die Payload einer POST-Anfrage an den `/acl/active-permissions`-Endpunkt aufnehmen können.

**Berechtigungen**

```plaintext
permissions/activate-destinations
permissions/evaluate-segments
permissions/execute-decisioning-activities
permissions/export-audience-for-segment
permissions/manage-datasets
permissions/manage-decisioning-activities
permissions/manage-decisioning-options
permissions/manage-destinations
permissions/manage-dsw
permissions/manage-dule-labels
permissions/manage-dule-policies
permissions/manage-identity-namespaces
permissions/manage-privacy-workflows
permissions/manage-profile-configs
permissions/manage-profiles
permissions/manage-queries
permissions/manage-schemas
permissions/manage-segments
permissions/manage-sources
permissions/reset-sandboxes
permissions/view-datasets
permissions/view-destinations
permissions/view-dule-labels
permissions/view-dule-policies
permissions/view-identity-namespaces
permissions/view-monitoring-dashboard
permissions/view-privacy-workflows
permissions/view-profile-configs
permissions/view-profiles
permissions/view-sandboxes
permissions/view-schemas
permissions/view-segments
permissions/view-sources
```

**Ressourcentypen**

```plaintext
resource-types/activation-associations
resource-types/activations
resource-types/activities
resource-types/analytics-source
resource-types/audience-manager-source
resource-types/bizible-source
resource-types/connection
resource-types/customer-attributes-source
resource-types/data-science-workspace
resource-types/dataset-preview
resource-types/datasets
resource-types/dule-label
resource-types/dule-policy
resource-types/enterprise-source
resource-types/identity-descriptor
resource-types/identity-namespaces
resource-types/launch-source
resource-types/marketing-action
resource-types/marketo-source
resource-types/monitoring
resource-types/offers
resource-types/placements
resource-types/privacy-consent
resource-types/privacy-content-delivery
resource-types/privacy-job
resource-types/profile-configs
resource-types/profile-datasets
resource-types/profiles
resource-types/query
resource-types/relationship-descriptor
resource-types/sandboxes
resource-types/schemas
resource-types/segment-jobs
resource-types/segments
resource-types/streaming-source
```
