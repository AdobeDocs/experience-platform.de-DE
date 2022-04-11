---
keywords: Experience Platform;Startseite;beliebte Themen;Flow Service;Konten löschen;löschen;API
solution: Experience Platform
title: Löschen eines Kontos mithilfe der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie ein Konto mithilfe der Flow Service-API löschen können.
exl-id: 3d07ab7d-c012-472e-8db4-b19e3936dcba
source-git-commit: 95f455bd03b7baefe0133a9818c9d048f36f9d38
workflow-type: ht
source-wordcount: '339'
ht-degree: 100%

---

# Löschen eines Kontos mithilfe der Flow Service-API

Mit der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) können Sie Quellkonten löschen, die Fehler enthalten oder nicht mehr aktuell sind.

Anweisungen zum Löschen eines Kontos mithilfe der API finden Sie im folgenden Tutorial.

## Erste Schritte

Für dieses Tutorial benötigen Sie eine gültige Verbindungs-ID. Wenn Sie keine gültige Verbindungs-ID haben, wählen Sie den gewünschten Connector aus der [Quellenübersicht](../../home.md) und führen Sie die angegebenen Schritte vor Beginn des Tutorials aus.

Dieses Tutorial setzt außerdem ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Platform-APIs

Informationen zum Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../landing/api-guide.md).

## Löschen eines Kontos

>[!TIP]
>
>Bevor Sie das Quellkonto löschen, müssen Sie zunächst alle damit verbundenen Datenflüsse löschen. Informationen zum Löschen vorhandener Datenflüsse finden Sie im Tutorial [Löschen von Datenflüssen für Quellen](./delete-dataflows.md).

Um ein Konto zu löschen, stellen Sie eine DELETE-Anfrage an die API [!DNL Flow Service] - unter Angabe der ID der Basisverbindung, die dem zu löschenden Konto entspricht.

**API-Format**

```http
DELETE /connections/{BASE_CONNECTION_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Die ID der Basisverbindungs des Quellkontos, das Sie löschen möchten. |

**Anfrage**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd3631cd-d0ea-4fea-b631-cdd0ea6fea21' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) und leeren Text zurück.

Sie können den Löschvorgang bestätigen, indem Sie eine Suchanfrage (GET) an die Verbindung stellen.

## Nächste Schritte

In diesem Tutorial haben Sie die [!DNL Flow Service]-API zum Löschen vorhandener Konten verwendet.

Anweisungen zum Ausführen dieser Abläufe mithilfe der Benutzeroberfläche finden Sie im Tutorial [Löschen von Konten in der Benutzeroberfläche](../../tutorials/ui/delete-accounts.md).
