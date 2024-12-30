---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Einverständnis-API-Endpunkt
description: Erfahren Sie, wie Sie Einverständnisanfragen von Kunden für Experience Cloud-Anwendungen mithilfe der Privacy Service-API verwalten.
role: Developer
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 4%

---

# Einverständnis-Endpunkt

Bestimmte Vorschriften erfordern die ausdrückliche Zustimmung des Kunden, bevor seine personenbezogenen Daten erfasst werden können. Mit dem `/consent`-Endpunkt in der [!DNL Privacy Service]-API können Sie Einverständnisanfragen von Kunden verarbeiten und in Ihren Datenschutz-Workflow integrieren.

Bevor Sie dieses Handbuch verwenden, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) um Informationen zu den erforderlichen Authentifizierungskopfzeilen zu erhalten, die im folgenden Beispiel-API-Aufruf dargestellt werden.

## Verarbeiten einer Einverständnisanfrage eines Kunden

Einverständnisanfragen werden verarbeitet, indem eine POST-Anfrage an den `/consent`-Endpunkt gesendet wird.

**API-Format**

```http
POST /consent
```

**Anfrage**

Die folgende Anfrage erstellt einen neuen Einverständnisvorgang für die im `entities`-Array angegebenen Benutzer-IDs.

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
| `optOutOfSale` | Wenn auf „true“ gesetzt, bedeutet dies, dass die unter `entities` bereitgestellten Benutzer den Verkauf oder die Freigabe ihrer personenbezogenen Daten deaktivieren möchten. |
| `entities` | Ein Array von Objekten, die die Benutzer angeben, für die die Einverständnisanfrage gilt. Jedes -Objekt enthält ein -`namespace` und ein -Array von `values`, um die einzelnen Benutzer mit diesem Namespace abzugleichen. |
| `nameSpace` | Jedes Objekt im `entities`-Array muss einen der [Standard-Identity-Namespaces“ enthalten](./appendix.md#standard-namespaces) die von der Privacy Service-API erkannt werden. |
| `values` | Ein Array von Werten für jeden Benutzer, das der angegebenen `nameSpace` entspricht. |

{style="table-layout:auto"}

>[!NOTE]
>
>Weiterführende Informationen dazu, wie Sie bestimmen, welche Kundenidentitätswerte an [!DNL Privacy Service] gesendet werden sollen, finden Sie im Handbuch [Bereitstellen von Identitätsdaten](../identity-data.md).

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 202 (Akzeptiert) ohne Payload zurück und zeigt an, dass die Anfrage von [!DNL Privacy Service] akzeptiert wurde und verarbeitet wird.
