---
title: Wiederholen fehlgeschlagener Datenfluss-Ausführungen
description: Erfahren Sie, wie Sie fehlgeschlagene Datenfluss-Ausführungen mithilfe der Flow Service-API erneut testen können.
exl-id: b9abc737-9a57-47e6-98ab-6d6c44f38d17
source-git-commit: d4dba26a151619a555a69287e182ff8398cca7b4
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 38%

---

# Wiederholen fehlgeschlagener Datenfluss-Ausführungen

>[!IMPORTANT]
>
>Unterstützung für das Wiederholen fehlgeschlagener Datenfluss-Ausführungen ist für Batch-Quellen verfügbar. Sie können nur fehlgeschlagene Datenfluss-Ausführungen wiederholen.

In diesem Tutorial werden die Schritte zum Wiederholen fehlgeschlagener Datenfluss-Ausführungen mit dem [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../home.md)[!DNL Platform]: Experience ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../sandboxes/home.md)[!DNL Platform]: Experience bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Platform-APIs

Informationen darüber, wie Sie Platform-APIs erfolgreich aufrufen können, finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../landing/api-guide.md).

## Fehler beim Ausführen eines Datenflusses wiederholen

Um einen fehlgeschlagenen Datenfluss erneut auszuführen, stellen Sie eine POST-Anfrage an die `/runs` -Endpunkt bei Angabe der Start-ID Ihres Datenflusses und der `re-trigger` -Operation als Teil Ihrer Abfrageparameter.

**API-Format**

```http
POST /runs/{RUN_ID}/action?op=re-trigger
```

| Parameter | Beschreibung |
| --- | --- |
| `{RUN_ID}` | Die Run-ID, die der Datenflug-Ausführung entspricht, die Sie erneut versuchen möchten. |
| `op` | Ein Vorgang, der die auszuführende Aktion bestimmt. Um einen fehlgeschlagenen Datenfluss erneut auszuführen, müssen Sie `re-trigger` als Ihren Vorgang. |

**Anfrage**

>[!NOTE]
>
>Sie können die `re-trigger` -Vorgang, um den erfolgreichen Datenfluss erneut auszuführen, da der erfolgreiche Datenfluss null aufgenommene Datensätze aufweist.

Die folgende Anfrage versucht erneut, den Datenfluss für die Ausführungs-ID auszuführen `4fb0418e-1804-45d6-8d56-dd51f05c0baf`.

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

Eine erfolgreiche Antwort gibt eine neu erstellte Flusslaufs-ID und die zugehörige eTag-Version zurück.

```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "etag": "\"1100c53e-0000-0200-0000-627138980000\""
}
```
