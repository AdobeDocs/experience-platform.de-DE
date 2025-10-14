---
title: Wiederholen fehlgeschlagener Datenflussdurchgänge
description: Erfahren Sie, wie Sie fehlgeschlagene Datenflussausführungen mithilfe der Flow Service-API erneut versuchen können.
exl-id: b9abc737-9a57-47e6-98ab-6d6c44f38d17
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 11%

---

# Wiederholen fehlgeschlagener Datenfluss-Ausführungen

>[!IMPORTANT]
>
>Unterstützung für die Wiederholung fehlgeschlagener Datenflussausführungen ist für Batch-Quellen verfügbar. Sie können nur fehlgeschlagene Datenflussausführungen wiederholen.

In diesem Tutorial werden Schritte zum Wiederholen fehlgeschlagener Datenflussausführungen mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne [!DNL Experience Platform] in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

### Verwenden von Experience Platform-APIs

Informationen zum erfolgreichen Aufrufen von Experience Platform-APIs finden Sie im Handbuch unter [&#x200B; mit Experience Platform-APIs](../../../landing/api-guide.md).

## Wiederholen einer fehlgeschlagenen Datenflussausführung

Um einen fehlgeschlagenen Datenfluss erneut auszuführen, stellen Sie eine POST-Anfrage an den `/runs`-Endpunkt, wobei Sie die Ausführungs-ID Ihres Datenflusses und den `re-trigger` als Teil Ihrer Abfrageparameter angeben.

**API-Format**

```http
POST /runs/{RUN_ID}/action?op=re-trigger
```

| Parameter | Beschreibung |
| --- | --- |
| `{RUN_ID}` | Die Ausführungs-ID, die der Datenflussausführung entspricht, die Sie erneut versuchen möchten. |
| `op` | Ein Vorgang, der die auszuführende Aktion bestimmt. Um eine fehlgeschlagene Datenflussausführung erneut auszuführen, müssen Sie `re-trigger` als Vorgang angeben. |

**Anfrage**

>[!NOTE]
>
>Sie können den `re-trigger`-Vorgang auch verwenden, um erfolgreiche Datenflussausführungen erneut auszuführen, da der erfolgreiche Datenflussdurchgang keine Datensätze aufgenommen hat.

Mit der folgenden Anfrage wird die Datenflussausführung für die Ausführungs-ID `4fb0418e-1804-45d6-8d56-dd51f05c0baf` wiederholt.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs/4fb0418e-1804-45d6-8d56-dd51f05c0baf/action?op=re-trigger' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine neu erstellte Flussausführungs-ID und die entsprechende eTag-Version zurück.

```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "etag": "\"1100c53e-0000-0200-0000-627138980000\""
}
```
