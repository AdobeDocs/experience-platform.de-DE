---
title: Endpunkt des öffentlichen Zertifikats
description: Erfahren Sie, wie Sie Ihre öffentlichen Zertifikate mit dem Endpunkt /public-certificate der MTLS-Service-API abrufen.
role: Developer
exl-id: 8369c783-e595-476f-9546-801cf4f10f71
source-git-commit: 754044621cdaf1445f809bceaa3e865261eb16f0
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 3%

---

# Endpunkt des öffentlichen Zertifikats

In diesem Handbuch wird erläutert, wie Sie mit dem öffentlichen Zertifikatendpunkt öffentliche Zertifikate für die Adobe-Programme Ihres Unternehmens sicher abrufen können. Er enthält einen Beispiel-API-Aufruf und detaillierte Anweisungen, die Entwicklern bei der Authentifizierung und Überprüfung des Datenaustauschs helfen.

## Erste Schritte

Bevor Sie fortfahren, lesen Sie den Abschnitt [Erste Schritte](./getting-started.md). Dort erhalten Sie wichtige Informationen darüber, wie Sie die API aufrufen und die erforderlichen Kopfzeilen sowie Beispiele für API-Aufrufe lesen können.

## API-Pfade {#paths}

Im Folgenden finden Sie die wesentlichen API-Pfade, die Sie für die Verwendung der mTLS-Service-API benötigen. Dazu gehören die Platform-Gateway-URL, der Basispfad für die API und ein Beispiel für einen vollständigen Pfad zum Abrufen eines öffentlichen Zertifikats.

- PLATFORM-Gateway-URL: `https://platform.adobe.io/`
- Basispfad für diese API: `/data/core/mtls`
- Beispiel für einen vollständigen Pfad: `https://platform.adobe.io/data/core/mtls/v1/certificate/public-certificate`

## Abrufen Ihrer öffentlichen Zertifikate {#list}

Sie können die öffentlichen Zertifikate für alle Adobe-Programme Ihres Unternehmens abrufen, indem Sie eine GET-Anfrage an den `/v1/certificate/public-certificate`-Endpunkt stellen.

**API-Format**

```http
GET /v1/certificate/public-certificate
```

Die folgenden optionalen Abfrageparameter können beim Abrufen Ihrer öffentlichen Zertifikate verwendet werden.

| Abfrageparameter | Beschreibung | Beispiel |
| --------------- | ----------- | ------- |
| `page` | Gibt an, auf welcher Seite die Ergebnisse Ihrer Anfrage beginnen sollen. | `page=5` |
| `limit` | Die maximale Anzahl öffentlicher Zertifikate, die pro Seite abgerufen werden sollen. | `limit=20` |

{style="table-layout:auto"}

**Anfrage**

Eine Beispielanfrage zum Zurückgeben der mit Ihrer Organisation verknüpften öffentlichen Zertifikate finden Sie unten im ausblendbaren Abschnitt.

+++Beispielanfrage

```shell
curl -X GET https://platform.adobe.io/data/core/mtls/v1/certificate/public-certificate
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' 
```

+++

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 zurückgegeben und die öffentlichen Zertifikate für Ihre Organisation aufgelistet.

+++Beispiel für eine erfolgreiche Antwort

```json
{
   "results":[
      {
         "certCommonName":"Adobe Experience Platform",
         "publicCertificate":"-----BEGIN CERTIFICATE-----\nMIIDQTCCAimgAwIBAgITBmyfACAfma......KJY5u89CjAwj\n-----END CERTIFICATE-----",
         "expiryDate":"2024-07-17T21:27:57.434Z"
      }
   ],
   "total":0,
   "count":0,
   "_links":{
      "next":{
         "href":"string",
         "templated":true
      },
      "prev":{
         "href":"string",
         "templated":true
      },
      "page":{
         "href":"string",
         "templated":true
      }
   }
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `certCommonName` | Der allgemeine Name (CN) des Zertifikats, der normalerweise den Namen oder die Identität des Servers oder der Entität darstellt, für die das Zertifikat ausgestellt wird. |
| `publicCertificate` | Das eigentliche öffentliche Zertifikat in einem Zeichenfolgenformat, das zum Authentifizieren und Verschlüsseln der Kommunikation verwendet wird. |
| `expiryDate` | Datum und Uhrzeit des Ablaufs des öffentlichen Zertifikats, formatiert in ISO 8601 (UTC). |

{style="table-layout:auto"}

+++

## Nächste Schritte

Nach dem Lesen dieses Handbuchs wissen Sie jetzt, wie Sie Ihre öffentlichen Zertifikate mit der Adobe Experience Platform-API abrufen können. Weitere Informationen zur Verwaltung von Kundendaten, um die Einhaltung von Vorschriften und organisatorischen Richtlinien sicherzustellen, finden Sie unter [Data Governance - Übersicht](../home.md).

<!-- To test this API call, navigate to the [MTLS API reference page]() to interact with the Experience Platform API endpoints. -->

<!-- Add link after developer page is live -->
