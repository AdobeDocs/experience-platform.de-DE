---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: API-Endpunkt für Zustimmung
description: Erfahren Sie, wie Sie mit der Privacy Service-API Anfragen zur Kundenzustimmung für Experience Cloud-Anwendungen verwalten.
role: Developer
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 4%

---

# Zustimmungsendpunkt

Bestimmte Vorschriften erfordern eine ausdrückliche Zustimmung des Kunden, bevor seine personenbezogenen Daten erfasst werden können. Mit dem Endpunkt `/consent` in der API [!DNL Privacy Service] können Sie Anfragen zur Kundenzustimmung verarbeiten und in Ihren Datenschutz-Workflow integrieren.

Bevor Sie dieses Handbuch verwenden, finden Sie im Leitfaden [Erste Schritte](./getting-started.md) Informationen zu den erforderlichen Authentifizierungskopfzeilen, die im folgenden Beispiel-API-Aufruf vorgestellt werden.

## Verarbeiten einer Kundenzustimmungsanfrage

Zustimmungsanfragen werden verarbeitet, indem eine POST-Anfrage an den `/consent` -Endpunkt gesendet wird.

**API-Format**

```http
POST /consent
```

**Anfrage**

Mit der folgenden Anfrage wird ein neuer Zustimmungsauftrag für die Benutzer-IDs erstellt, die im Array `entities` angegeben sind.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/consent \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `optOutOfSale` | Gibt bei der Festlegung auf &quot;true&quot;an, dass die unter `entities` angegebenen Benutzer den Verkauf oder die Weitergabe ihrer personenbezogenen Daten deaktivieren möchten. |
| `entities` | Ein Array von Objekten, die die Benutzer angeben, für die die Genehmigungsanfrage gilt. Jedes Objekt enthält ein `namespace` und ein Array von `values`, um einzelne Benutzer mit diesem Namespace abzugleichen. |
| `nameSpace` | Jedes Objekt im `entities` -Array muss einen der von der Privacy Service-API erkannten [standardmäßigen Identitäts-Namespaces](./appendix.md#standard-namespaces) enthalten. |
| `values` | Ein Array von Werten für jeden Benutzer, das dem bereitgestellten `nameSpace` entspricht. |

{style="table-layout:auto"}

>[!NOTE]
>
>Weitere Informationen dazu, wie Sie bestimmen, welche Identitätswerte von Kunden an [!DNL Privacy Service] gesendet werden, finden Sie im Handbuch zu [Identitätsdaten bereitstellen](../identity-data.md) .

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 202 (Akzeptiert) ohne Payload zurück und gibt an, dass die Anfrage von [!DNL Privacy Service] akzeptiert wurde und derzeit verarbeitet wird.
