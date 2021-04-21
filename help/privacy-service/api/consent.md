---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: API-Endpunkt für Zustimmung
topic-legacy: developer guide
description: Erfahren Sie, wie Sie mit der Privacy Service-API Anfragen zur Kundengenehmigung für Experience Cloud-Anwendungen verwalten.
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 2%

---

# Endpunkt der Zustimmung

Bestimmte Vorschriften erfordern eine ausdrückliche Zustimmung des Kunden, bevor seine persönlichen Daten gesammelt werden können. Mit dem `/consent`-Endpunkt in der [!DNL Privacy Service]-API können Sie Anfragen zur Kundengenehmigung bearbeiten und in Ihren Datenschutzarbeitsablauf integrieren.

Bevor Sie dieses Handbuch verwenden, lesen Sie bitte den Abschnitt [Erste Schritte](./getting-started.md), um Informationen zu den erforderlichen Authentifizierungskopfzeilen zu erhalten, die im Beispiel-API-Aufruf unten aufgeführt sind.

## Eine Anfrage zur Kundengenehmigung verarbeiten

Zustimmungsanforderungen werden verarbeitet, indem eine POST an den `/consent`-Endpunkt angefordert wird.

**API-Format**

```http
POST /consent
```

**Anfrage**

Mit der folgenden Anforderung wird ein neuer Genehmigungsauftrag für die Benutzer-IDs erstellt, die im Array `entities` bereitgestellt werden.

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
| `optOutOfSale` | Wenn &quot;true&quot;festgelegt ist, zeigt an, dass die unter `entities` bereitgestellten Benutzer den Verkauf oder die Weitergabe ihrer personenbezogenen Daten deaktivieren möchten. |
| `entities` | Ein Array von Objekten, die die Benutzer angeben, für die die Genehmigungsanfrage gilt. Jedes Objekt enthält ein `namespace`- und ein Array von `values`, um die einzelnen Benutzer mit diesem Namensraum abzugleichen. |
| `nameSpace` | Jedes Objekt im Array `entities` muss einen der [standardmäßigen Identitäts-Namensraum](./appendix.md#standard-namespaces) enthalten, die von der Privacy Service-API erkannt werden. |
| `values` | Ein Array von Werten für jeden Benutzer, das dem bereitgestellten `nameSpace` entspricht. |

>[!NOTE]
>
>Weitere Informationen dazu, wie Sie bestimmen, welche Werte zur Kundenidentität an [!DNL Privacy Service] gesendet werden sollen, finden Sie im Handbuch [Identitätsdaten](../identity-data.md) bereitstellen.

**Antwort**

Bei einer erfolgreichen Antwort wird HTTP-Status 202 (Akzeptiert) ohne Nutzlast zurückgegeben, was bedeutet, dass die Anforderung von [!DNL Privacy Service] akzeptiert wurde und verarbeitet wird.
