---
keywords: Experience Platform;Home;beliebte Themen
solution: Experience Platform
title: API-Endpunkt für Zustimmung
topic-legacy: developer guide
description: Erfahren Sie, wie Sie mit der Privacy Service-API Anfragen zur Kundenzustimmung für Experience Cloud-Anwendungen verwalten.
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
source-git-commit: e226990fc84926587308077b32b128bfe334e812
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 5%

---

# Zustimmungsendpunkt

Bestimmte Vorschriften erfordern eine ausdrückliche Zustimmung des Kunden, bevor seine personenbezogenen Daten erfasst werden können. Mit dem Endpunkt `/consent` in der API [!DNL Privacy Service] können Sie Anfragen zur Kundenzustimmung verarbeiten und in Ihren Datenschutz-Workflow integrieren.

Bevor Sie dieses Handbuch verwenden, finden Sie im Abschnitt [Erste Schritte](./getting-started.md) Informationen zu den erforderlichen Authentifizierungskopfzeilen, die im folgenden Beispiel-API-Aufruf vorgestellt werden.

## Verarbeiten einer Kundenzustimmungsanfrage

Einverständnisanfragen werden verarbeitet, indem eine POST-Anfrage an den Endpunkt `/consent` gesendet wird.

**API-Format**

```http
POST /consent
```

**Anfrage**

Mit der folgenden Anfrage wird ein neuer Zustimmungsauftrag für die Benutzer-IDs erstellt, die im Array `entities` bereitgestellt werden.

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
| `optOutOfSale` | Gibt bei Festlegung auf &quot;true&quot;an, dass die unter `entities` angegebenen Benutzer den Verkauf oder die Weitergabe ihrer personenbezogenen Daten deaktivieren möchten. |
| `entities` | Ein Array von Objekten, die die Benutzer angeben, für die die Genehmigungsanfrage gilt. Jedes Objekt enthält ein `namespace` und ein Array von `values`, um einzelne Benutzer mit diesem Namespace abzugleichen. |
| `nameSpace` | Jedes Objekt im Array `entities` muss einen der [standardmäßigen Identitäts-Namespaces](./appendix.md#standard-namespaces) enthalten, die von der Privacy Service-API erkannt werden. |
| `values` | Ein Array von Werten für jeden Benutzer, das dem bereitgestellten `nameSpace` entspricht. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Weitere Informationen dazu, wie Sie bestimmen, welche Identitätswerte von Kunden an [!DNL Privacy Service] gesendet werden, finden Sie im Handbuch zu [Bereitstellen von Identitätsdaten](../identity-data.md).

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 202 (Akzeptiert) ohne Payload zurück und gibt an, dass die Anfrage von [!DNL Privacy Service] akzeptiert wurde und derzeit verarbeitet wird.
