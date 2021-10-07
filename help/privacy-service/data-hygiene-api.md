---
title: Data Hygiene API (Alpha)
description: Erfahren Sie, wie Sie die gespeicherten personenbezogenen Daten Ihrer Kunden in Adobe Experience Platform programmatisch korrigieren oder löschen können.
hide: true
hidefromtoc: true
source-git-commit: dd8978566730975f0bde36f3af490cd33362b3ba
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 19%

---

# Data Hygiene API (Alpha)

>[!IMPORTANT]
>
>Die Data Hygiene API befindet sich derzeit in der Alpha-Phase und Ihr Unternehmen hat möglicherweise noch keinen Zugriff darauf. Die in diesem Dokument beschriebene Funktionalität kann sich ändern.

Mit der Data Hygiene API können Sie die in Adobe Experience Platform gespeicherten personenbezogenen Daten Ihrer Kunden programmatisch korrigieren oder löschen. Im Gegensatz zur Privacy Service-API müssen diese Vorgänge nicht mit gesetzlichen Datenschutzbestimmungen in Verbindung gebracht werden und können ausschließlich dazu verwendet werden, Ihre Daten sauber und präzise zu halten.

## Erste Schritte

In diesem Abschnitt erhalten Sie eine Einführung in die wichtigsten Konzepte, die Sie kennen müssen, bevor Sie Aufrufe an die Data Hygiene-API durchführen.

### Sammeln von Werten für erforderliche Kopfzeilen

Um die Data Hygiene-API aufrufen zu können, müssen Sie zunächst Ihre Authentifizierungsdaten erfassen. Hierbei handelt es sich um dieselben Anmeldeinformationen, die für den Zugriff auf die Privacy Service-API verwendet werden. Folgen Sie dem Leitfaden [Erste Schritte](./api/getting-started.md) für die Privacy Service-API, um Werte für die einzelnen Header für die Data Hygiene-API zu generieren, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

* `Content-Type: application/json`

### Lesen von Beispiel-API-Aufrufen

Dieses Dokument enthält einen Beispiel-API-Aufruf, der die Formatierung Ihrer Anfragen demonstriert. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt [So lesen Sie Beispiel-API-Aufrufe](../landing/api-guide.md#sample-api) im Erste-Schritte-Handbuch für Experience Platform-APIs.

## Löschauftrag erstellen

Sie können einen Löschauftrag erstellen, indem Sie eine POST-Anfrage stellen.

**API-Format**

```http
POST /jobs
```

**Anfrage**

Die Anfrage-Payload ist ähnlich wie eine [Löschanfrage in der Privacy Service-API](./api/privacy-jobs.md#access-delete) strukturiert. Sie enthält ein `users`-Array, dessen Objekte die Benutzer darstellen, deren Daten gelöscht werden sollen.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "companyContexts": [
          {
            "namespace": "imsOrgID",
            "value": "{IMS_ORG}"
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
| `companyContexts` | Ein Array mit Authentifizierungsinformationen für Ihr Unternehmen. Sie muss ein einzelnes Objekt mit den folgenden Eigenschaften enthalten: <ul><li>`namespace`: Muss auf  `imsOrgID`gesetzt werden.</li><li>`value`: Ihre IMS-Organisationskennung. Dies ist derselbe Wert, der in der `x-gw-ims-org-id` -Kopfzeile angegeben wird.</li></ul> |
| `users` | Ein Array, das eine Sammlung von mindestens einem Benutzer enthält, dessen Informationen Sie löschen möchten. Jedes Benutzerobjekt enthält die folgenden Informationen: <ul><li>`key`: Ein Identifikator für einen Benutzer, der verwendet wird, um die separaten Auftrags-Identifikatoren in den Antwortdaten zu qualifizieren. Es empfiehlt sich, eine eindeutige, leicht identifizierbare Zeichenfolge für diesen Wert zu wählen, damit später darauf verwiesen oder nachgeschlagen werden kann.</li><li>`action`: Ein Array, das die gewünschten Aktionen zur Übernahme der Benutzerdaten auflistet. Muss einen einzelnen Zeichenfolgenwert enthalten: `delete`.</li><li>`userIDs`: Eine Sammlung von Identitäten für den Benutzer. Die Anzahl der Identitäten, die ein einzelner Benutzer haben kann, ist auf neun begrenzt. Jede Identität enthält die folgenden Eigenschaften: <ul><li>`namespace`: Das mit der ID verknüpfte  [Identitäts-](../identity-service/namespaces.md) Namespace. Dabei kann es sich um einen [Standard-Namespace](./api/appendix.md#standard-namespaces) handeln, der von Platform erkannt wird, oder um einen von Ihrem Unternehmen definierten benutzerdefinierten Namespace. Der Typ des verwendeten Namespace muss in der Eigenschaft `type` angegeben werden.</li><li>`value`: Der Identitätswert.</li><li>`type`: Muss auf gesetzt werden,  `standard` wenn Sie einen global erkannten Namespace verwenden oder  `custom` wenn Sie einen von Ihrem Unternehmen definierten Namespace verwenden.</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details der erstellten Aufträge zurück.

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
