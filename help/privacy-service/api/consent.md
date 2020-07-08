---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Zustimmung
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 1%

---


# Zustimmung

Bestimmte Vorschriften bedürfen der ausdrücklichen Zustimmung des Kunden, bevor seine personenbezogenen Daten gesammelt werden können. Der `/consent` Endpunkt in der Privacy Service-API ermöglicht es Ihnen, Anfragen zur Kundengenehmigung zu bearbeiten und sie in Ihren Datenschutzarbeitsablauf zu integrieren.

Bevor Sie dieses Handbuch verwenden, lesen Sie bitte den Abschnitt [Erste Schritte](./getting-started.md) , um Informationen zu den erforderlichen Authentifizierungskopfzeilen zu erhalten, die im Beispiel-API-Aufruf unten aufgeführt sind.

## Eine Anfrage zur Kundengenehmigung verarbeiten

Zustimmungsanforderungen werden verarbeitet, indem eine POST-Anforderung an den `/consent` Endpunkt gesendet wird.

**API-Format**

```http
POST /consent
```

**Anfrage**

Die folgende Anforderung erstellt einen neuen Genehmigungsauftrag für die Benutzer-IDs, die im `entities` Array bereitgestellt werden.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/consent \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
        "optOutOfSale": true,
        "entities": [
          {
            "nameSpace": "email",
            "values": [
              "dsmith@acme.com",
              "ajones@acme.com"
            ]
          },
          {
            "nameSpace": "ECID",
            "values": [
              "443636576799758681021090721276"
            ]
          }
        ]
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `optOutOfSale` | Wenn &quot;true&quot;festgelegt ist, gibt dies an, dass die unter dem `entities` Wunsch angegebenen Benutzer den Verkauf oder die Weitergabe ihrer personenbezogenen Daten deaktivieren möchten. |
| `entities` | Ein Array von Objekten, die die Benutzer angeben, für die die Genehmigungsanfrage gilt. Jedes Objekt enthält ein `namespace` und ein Array von `values` Benutzern, die mit diesem Namensraum übereinstimmen. |
| `nameSpace` | Jedes Objekt im `entities` Array muss einen der von der Privacy Service-API erkannten [Identitäts-Namensraum](./appendix.md#standard-namespaces) enthalten. |
| `values` | Ein Array von Werten für jeden Benutzer, das dem angegebenen Wert entspricht `nameSpace`. |

>[!NOTE]
>
>Weitere Informationen dazu, wie Sie bestimmen, welche Kundenidentitätswerte an Privacy Service gesendet werden sollen, finden Sie im Handbuch zur [Bereitstellung von Identitätsdaten](../identity-data.md).

**Antwort**

Bei einer erfolgreichen Antwort wird HTTP-Status 202 (Akzeptiert) ohne Nutzlast zurückgegeben, was bedeutet, dass die Anforderung von Privacy Service akzeptiert wurde und verarbeitet wird.