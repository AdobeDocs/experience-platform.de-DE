---
title: Zielgruppen-API-Endpunkt erstellen
description: Erfahren Sie, wie Sie die Metadaten für eine externe Zielgruppe mithilfe der API erstellen.
hide: true
hidefromtoc: true
exl-id: e841a5f6-f406-4e1d-9e8a-acb861ba6587
source-git-commit: a3b82eb1efaf257723208504c90210850a44b4a4
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 35%

---

# Zielgruppen-Endpunkt erstellen

Der Endpunkt POST-`/audiences` kann verwendet werden, um die Metadaten für eine externe Zielgruppe zu erstellen, wodurch die Zielgruppe im Zielgruppenportal sichtbar wird. Sie sollten diesen Endpunkt verwenden, wenn die Zielgruppenaufnahme in einem separaten Service verwaltet wird, z. B. in der Batch-Aufnahme.

## Erste Schritte

>[!IMPORTANT]
>
>Den Endpunkten in diesem Handbuch wird im Gegensatz zu `/core/ais` das Präfix `/core/ups` vorangestellt.

Um Experience Platform-APIs verwenden zu können, müssen Sie das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abgeschlossen haben. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Alle an [!DNL Experience Platform]-APIs gerichtete Anfragen müssen über eine Kopfzeile verfügen, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zum Arbeiten mit Sandboxes in [!DNL Experience Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

**API-Format**

>[!IMPORTANT]
>
>Sie **müssen** den `createAudienceMetaOnly=true` Abfrageparameter als Teil der Anfrage einbeziehen.

```http
POST /audiences?createAudienceMetaOnly=true
```

**Anfrage**

>[!IMPORTANT]
>
>Sie **müssen** den `Accept: application/vnd.adobe.external.audiences+json; version=2`-Header als Teil der API-Anfrage einbeziehen.

```shell
curl -X POST https://platform.adobe.io/data/core/ais/audiences?createAudienceMetaOnly=true \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'\
 -H 'Accept: application/vnd.adobe.external.audiences+json; version=2'
 -d '{
    "name": "Sample audience name",
    "description" "A sample description for the audience.",
    "namespace": "agora",
    "originName": "Agora_Collaboration"
 }'
```

| Eigenschaft | Typ | Beschreibung |
| -------- | ---- | ----------- |
| `name` | Zeichenfolge | Der Name für die Zielgruppe. |
| `description` | String | Eine optionale Beschreibung für die Zielgruppe. |
| `namespace` | String | Der Namespace für die Zielgruppe. |
| `originName` | String | Der Name der Herkunft der Zielgruppe. |

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit Informationen zur neu erstellten Zielgruppe zurückgegeben.

```json
{
    "name": "Sample audience name",
    "audienceId": "4a815904-f2f9-4237-82fb-55605bcc2ad7"
}
```

| Eigenschaft | Typ | Beschreibung |
| -------- | ---- | ----------- |
| `name` | Zeichenfolge | Der Name der erstellten Zielgruppe. |
| `audienceId` | String | Die ID der von Ihnen erstellten Zielgruppe. |
