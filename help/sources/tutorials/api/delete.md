---
keywords: Experience Platform;Startseite;beliebte Themen;Flussdienst;Konten löschen;löschen;API
solution: Experience Platform
title: Konto mithilfe der Flow Service-API löschen
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie ein Konto mithilfe der Flow Service-API löschen.
exl-id: 3d07ab7d-c012-472e-8db4-b19e3936dcba
source-git-commit: 609f7a5de51840fe657ca72df99c90da56c8f466
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 14%

---

# Konto mithilfe der Flow Service-API löschen

Sie können Quellenkonten löschen, die Fehler enthalten oder mit der Funktion [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Anweisungen zum Löschen eines Kontos mithilfe der API finden Sie im folgenden Tutorial .

## Erste Schritte

Für dieses Tutorial benötigen Sie eine gültige Verbindungs-ID. Wenn Sie keine gültige Verbindungs-ID haben, wählen Sie den gewünschten Connector aus der [Quellen - Übersicht](../../home.md) und führen Sie die Schritte aus, die vor dem Versuch dieses Tutorials beschrieben wurden.

Für dieses Tutorial benötigen Sie außerdem ein Verständnis der folgenden Komponenten von Adobe Experience Platform:

* [Quellen](../../home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten zu strukturieren, zu beschriften und zu erweitern, indem Sie [!DNL Platform] Dienste.
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

## Verwenden von Platform-APIs

Informationen zum erfolgreichen Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../landing/api-guide.md).

## Konto löschen

>[!TIP]
>
>Bevor Sie das Quellkonto löschen, müssen Sie zunächst alle vorhandenen Datenflüsse löschen, die mit dem Quellkonto verknüpft sind. Informationen zum Löschen vorhandener Datenflüsse finden Sie im Tutorial unter [Löschen von Datenflüssen für Quellen](./delete-dataflows.md).

Um ein Konto zu löschen, stellen Sie eine DELETE-Anfrage an die [!DNL Flow Service] API bei der Bereitstellung der grundlegenden Verbindungs-ID, die dem Konto entspricht, das Sie löschen möchten.

**API-Format**

```http
DELETE /connections/{BASE_CONNECTION_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Die Basisverbindungs-ID des Quellkontos, das Sie löschen möchten. |

**Anfrage**

```shell
curl -X DELETE \
  'https://platform-int.adobe.io/data/foundation/flowservice/connections/dd3631cd-d0ea-4fea-b631-cdd0ea6fea21' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) und leeren Text zurück.

Sie können den Löschvorgang bestätigen, indem Sie eine Nachschlageanfrage (GET) für die Verbindung ausführen.

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich die [!DNL Flow Service] API zum Löschen vorhandener Konten.

Anweisungen zum Ausführen dieser Vorgänge mithilfe der Benutzeroberfläche finden Sie im Tutorial zu [Löschen von Konten in der Benutzeroberfläche](../../tutorials/ui/delete-accounts.md).
