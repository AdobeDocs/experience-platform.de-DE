---
keywords: Experience Platform;Home;beliebte Themen
solution: Experience Platform
title: Zustimmungs-API-Endpunkt
topic-legacy: developer guide
description: Erfahren Sie, wie Sie mit der Privacy Service-API Kundenanfragen für Experience Cloud-Anwendungen verwalten.
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
source-git-commit: 82dea48c732b3ddea957511c22f90bbd032ed9b7
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 5%

---

# Zustimmungs-Endpunkt

Bestimmte Bestimmungen bedürfen der ausdrücklichen Zustimmung des Kunden, bevor seine persönlichen Daten erhoben werden können. Die `/consent` Endpunkt im [!DNL Privacy Service] API ermöglicht es Ihnen, Anfragen zur Kundengenehmigung zu verarbeiten und in Ihren Datenschutz-Workflow zu integrieren.

Bevor Sie dieses Handbuch verwenden, beachten Sie bitte die [Erste Schritte](./getting-started.md) Anleitung für Informationen zu den erforderlichen Authentifizierungskopfzeilen, die im Beispiel-API-Aufruf unten aufgeführt sind.

## Anfrage auf Kundenzustimmung verarbeiten

Zustimmungsanforderungen werden verarbeitet, indem Sie eine POST anfordern an die `/consent` Endpunkt.

**API-Format**

```http
POST /consent
```

**Anfrage**

Mit der folgenden Anforderung wird ein neuer Bestätigungsauftrag für die Benutzer-IDs erstellt, die in der `entities` Array.

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
| `optOutOfSale` | Wenn auf &quot;true&quot;eingestellt, bedeutet dies, dass die unter `entities` Sie möchten den Verkauf oder die Weitergabe ihrer personenbezogenen Daten ablehnen. |
| `entities` | Ein Array von Objekten, die die Benutzer angeben, für die die Genehmigungsanfrage gilt. Jedes Objekt enthält `namespace` und ein Array von `values` , um einzelne Benutzer mit diesem Namensraum abzustimmen. |
| `nameSpace` | Jedes Objekt in `entities` Array muss einen der folgenden enthalten: [Standard-Identitäts-Namensraum](./appendix.md#standard-namespaces) von der Privacy Service-API erkannt. |
| `values` | Ein Array von Werten für jeden Benutzer, das der angegebenen entspricht `nameSpace`. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Weitere Informationen dazu, wie Sie bestimmen, an welche Kundenidentitätswerte gesendet werden sollen [!DNL Privacy Service], siehe Leitfaden [Identitätsdaten bereitstellen](../identity-data.md).

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 202 (Akzeptiert) ohne Nutzlast zurück, was darauf hinweist, dass die Anforderung von [!DNL Privacy Service] und wird verarbeitet.
