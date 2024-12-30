---
title: Wiederholen fehlgeschlagener Datenflussdurchgänge
description: Erfahren Sie, wie Sie fehlgeschlagene Datenflussausführungen mithilfe der Flow Service-API erneut versuchen können.
exl-id: b9abc737-9a57-47e6-98ab-6d6c44f38d17
source-git-commit: d4dba26a151619a555a69287e182ff8398cca7b4
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 19%

---

# Wiederholen fehlgeschlagener Datenfluss-Ausführungen

>[!IMPORTANT]
>
>Unterstützung für die Wiederholung fehlgeschlagener Datenflussausführungen ist für Batch-Quellen verfügbar. Sie können nur fehlgeschlagene Datenflussausführungen wiederholen.

In diesem Tutorial werden Schritte zum Wiederholen fehlgeschlagener Datenflussausführungen mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Platform-APIs

Informationen darüber, wie Sie Platform-APIs erfolgreich aufrufen können, finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../landing/api-guide.md).

## Wiederholen einer fehlgeschlagenen Datenflussausführung

Um einen fehlgeschlagenen Datenfluss erneut auszuführen, stellen Sie eine POST-Anfrage an den `/runs`-Endpunkt und geben Sie dabei die Ausführungs-ID Ihres Datenflusses und den `re-trigger` als Teil Ihrer Abfrageparameter an.

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
