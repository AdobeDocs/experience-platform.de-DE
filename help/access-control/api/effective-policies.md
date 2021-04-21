---
keywords: Experience Platform;Home;beliebte Themen;Effektive Richtlinien;Zugriffskontrolle API
solution: Experience Platform
title: API-Endpunkt für effektive Richtlinien
topic-legacy: developer guide
description: Mit der Zugriffskontrolle in Adobe Experience Platform können Sie Rollen und Berechtigungen für verschiedene Plattformfunktionen mithilfe des Adobe Admin Console verwalten. Dieses Dokument dient als Leitfaden für die Ansicht effektiver Richtlinien mithilfe der Zugriffskontrolle-API für Adobe Experience Platform.
exl-id: 555d73db-115d-4f4c-8bd2-b91477799591
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 55%

---

# Endpunkt für effektive Richtlinien

Um effektive Richtlinien für den aktuellen Benutzer Ansicht, stellen Sie eine POST-Anforderung an den `/acl/effective-policies`-Endpunkt in der [!DNL Access Control]-API ein. Die Berechtigungen und Ressourcentypen, die Sie abrufen möchten, müssen in der Anfrage-Payload in Form eines Arrays angegeben werden. Dies wird im folgenden Beispiel-API-Aufruf demonstriert.

**API-Format**

```http
POST /acl/effective-policies
```

**Anfrage**

Die folgenden Anforderungen rufen Informationen zur Berechtigung &quot;[!UICONTROL Datenbestände verwalten]&quot;und zum Zugriff auf den Ressourcentyp &quot;[!UICONTROL Schema]&quot;für den aktuellen Benutzer ab.

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

In diesem Dokument wurde beschrieben, wie Sie Aufrufe an die [!DNL Access Control]-API durchführen, um Informationen über aktive Berechtigungen und zugehörige Richtlinien für Ressourcentypen zurückzugeben. Weitere Informationen zur Zugriffskontrolle für [!DNL Experience Platform] finden Sie unter [Übersicht über die Zugriffskontrolle](../home.md).

## Anhang

Dieser Abschnitt enthält zusätzliche Informationen zur Verwendung der API [!DNL Access Control].

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
