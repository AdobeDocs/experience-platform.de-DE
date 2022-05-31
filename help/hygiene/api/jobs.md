---
title: Löschen von Verbraucherdatensätzen mithilfe der Data Hygiene API
description: Erfahren Sie, wie Sie die gespeicherten personenbezogenen Daten Ihrer Kunden in Adobe Experience Platform programmatisch korrigieren oder löschen können.
hide: true
hidefromtoc: true
source-git-commit: 9057d424d63217a3cef7ad2237a65700d9159323
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 92%

---

# Löschen von Verbraucherdatensätzen mithilfe der Data Hygiene API

Mit der Data Hygiene-API können Sie die in Adobe Experience Platform gespeicherten personenbezogenen Daten Ihrer Kunden programmatisch korrigieren oder löschen.

Sie können über den folgenden Stammpfad auf die API zugreifen: `https://platform.adobe.io/data/core/hygiene/`

## Erste Schritte

In diesem Abschnitt erhalten Sie eine Einführung in die wichtigsten Konzepte, die Sie kennen sollten, bevor Sie Aufrufe an die Data Hygiene-API durchführen.

### Sammeln von Werten für erforderliche Kopfzeilen

Um die Data Hygiene-API aufrufen zu können, müssen Sie zunächst Ihre Authentifizierungsdaten erfassen. Hierbei handelt es sich um dieselben Anmeldeinformationen wie die, die Sie für den Zugriff auf die Privacy Service-API verwenden. Siehe Abschnitt [API-Übersicht](./overview.md#getting-started) um Werte für die einzelnen Header zu generieren, die für die Data Hygiene-API erforderlich sind, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

* `Content-Type: application/json`

### Lesen von Beispiel-API-Aufrufen

In diesem Dokument wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/api-guide.md#sample-api) in den Ersten Schritten für Experience Platform-APIs.

## Erstellen eines Löschvorgangs

Sie können einen Löschvorgang erstellen, indem Sie eine POST-Anfrage ausführen.

**API-Format**

```http
POST /jobs
```

**Anfrage**

Die Anfrage-Payload ist ähnlich wie eine [Löschanfrage in der Privacy Service-API](../../privacy-service/api/privacy-jobs.md#access-delete) strukturiert. Sie enthält ein `users`-Array, dessen Objekte die Benutzer darstellen, deren Daten gelöscht werden sollen.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "companyContexts": [
          {
            "namespace": "imsOrgID",
            "value": "{ORG_ID}"
          }
        ],
        "users": [
          {
            "key": "John Doe",
            "action": [
              "delete"
            ],
            "userIDs": [
              {
                "namespace": "email",
                "value": "johnd@example.com",
                "type": "standard",
              },
              {
                "namespace": "ECID",
                "value": "9cbefef1-dd44-4411-87db-2d387bf882bc",
                "type": "standard"
              }
            ]
          },
          {
            "key": "Jane Doe",
            "action": [
              "delete"
            ],
            "userIDs": [
              {
                "namespace": "Loyalty ID",
                "value": "30583967185734",
                "type": "custom"
              }
            ]
          }
        ]
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `companyContexts` | Ein Array mit Authentifizierungsinformationen für Ihr Unternehmen. Sie muss ein einzelnes Objekt mit den folgenden Eigenschaften enthalten: <ul><li>`namespace`: Muss auf `imsOrgID` festgelegt werden.</li><li>`value`: Ihre IMS-Organisationskennung. Dies ist derselbe Wert, der in der `x-gw-ims-org-id`-Kopfzeile angegeben wird.</li></ul> |
| `users` | Ein Array mit einer Sammlung von mindestens einem Benutzer, dessen Informationen Sie löschen möchten. Jedes Benutzerobjekt enthält die folgenden Informationen: <ul><li>`key`: Ein Identifikator für einen Benutzer, der verwendet wird, um die separaten Auftrags-Identifikatoren in den Antwortdaten zu qualifizieren. Es gilt als Best Practice, eine eindeutige, leicht identifizierbare Zeichenfolge für diesen Wert zu wählen, damit später ein einfaches Verweisen auf oder Nachschlagen des Werts möglich ist.</li><li>`action`: Ein Array, das die gewünschten Aktionen zur Übernahme der Benutzerdaten auflistet. Muss einen einzelnen Zeichenfolgenwert enthalten: `delete`.</li><li>`userIDs`: Eine Sammlung von Identitäten für den Benutzer. Die Anzahl der Identitäten, die ein einzelner Benutzer haben kann, ist auf neun begrenzt. Jede Identität enthält die folgenden Eigenschaften: <ul><li>`namespace`: Der mit der ID verknüpfte [Identity-Namespace](../../identity-service/namespaces.md). Dabei kann es sich um einen [Standard-Namespace](../../privacy-service/api/appendix.md#standard-namespaces) handeln, der von Platform erkannt wird, oder um einen von Ihrem Unternehmen definierten benutzerdefinierten Namespace. Der Typ des verwendeten Namespace muss in der Eigenschaft `type` angegeben werden.</li><li>`value`: Der Identitätswert.</li><li>`type`: Muss auf `standard` gesetzt werden, wenn Sie einen global anerkannten Namespace verwenden, oder auf `custom`, wenn Sie einen von Ihrem Unternehmen definierten Namespace verwenden.</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Vorgänge zurück.

```json
{
  "requestId": "16318094870430026RX-334",
  "totalRecords": 2,
  "jobs": [
    {
      "jobId": "c9b5fd82-db14-4c27-8bec-64a06e1fbda4",
      "customer": {
        "user": {
          "key": "John Doe",
          "action": ["delete"],
          "userIDs": [
            {
              "namespace": "email",
              "value": "johnd@example.com",
              "type": "standard",
              "namespaceId": 6,
              "isDeletedClientSide": false
            },
            {
              "namespace": "ECID",
              "value": "9cbefef1-dd44-4411-87db-2d387bf882bc",
              "type": "standard",
              "namespaceId": 4,
              "isDeletedClientSide": false
            }
          ]
        }
      }
    },
    {
      "jobId": "8ddc8e73-cecc-4be3-ae44-cdba127f7c70",
      "customer": {
        "user": {
          "key": "Jane Doe",
          "action": ["delete"],
          "userIDs": [
            {
              "namespace": "Loyalty ID",
              "value": "30583967185734",
              "type": "custom",
              "isDeletedClientSide": false
            }
          ]
        }
      }
    }
  ]
}
```
