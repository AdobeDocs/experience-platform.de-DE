---
title: Öffentlicher Zertifikatsendpunkt
description: Erfahren Sie, wie Sie Ihre öffentlichen Zertifikate mithilfe des Endpunkts /public-certificate der MTLS Service-API abrufen.
role: Developer
exl-id: 8369c783-e595-476f-9546-801cf4f10f71
source-git-commit: 754044621cdaf1445f809bceaa3e865261eb16f0
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 3%

---

# Endpunkt für öffentliches Zertifikat

In diesem Handbuch wird erläutert, wie Sie mit dem öffentlichen Zertifikatendpunkt öffentliche Zertifikate für die Adobe-Anwendungen Ihres Unternehmens sicher abrufen können. Es enthält einen Beispiel-API-Aufruf und detaillierte Anweisungen, die Entwickler bei der Authentifizierung und Überprüfung des Datenaustauschs unterstützen.

## Erste Schritte

Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](./getting-started.md) , um wichtige Informationen zu erhalten, die Sie benötigen, um die API erfolgreich aufrufen zu können, einschließlich erforderlicher Kopfzeilen und Anweisungen zum Lesen von Beispiel-API-Aufrufen.

## API-Pfade {#paths}

Die folgenden Informationen sind die wichtigsten API-Pfade, die Sie für die Verwendung der mTLS-Dienst-API benötigen. Dazu gehören die Plattform-Gateway-URL, der Basispfad für die API und ein Beispiel für einen vollständigen Pfad zum Abrufen eines öffentlichen Zertifikats.

- PLATFORM Gateway URL: `https://platform.adobe.io/`
- Basispfad für diese API: `/data/core/mtls`
- Beispiel eines vollständigen Pfads: `https://platform.adobe.io/data/core/mtls/v1/certificate/public-certificate`

## Abrufen öffentlicher Zertifikate {#list}

Sie können die öffentlichen Zertifikate für alle Adobe-Anwendungen Ihres Unternehmens abrufen, indem Sie eine GET-Anfrage an den Endpunkt `/v1/certificate/public-certificate` senden.

**API-Format**

```http
GET /v1/certificate/public-certificate
```

Beim Abrufen Ihrer öffentlichen Zertifikate können die folgenden optionalen Abfrageparameter verwendet werden.

| Abfrageparameter | Beschreibung | Beispiel |
| --------------- | ----------- | ------- |
| `page` | Gibt an, von welcher Seite die Ergebnisse Ihrer Anfrage beginnen. | `page=5` |
| `limit` | Die maximale Anzahl öffentlicher Zertifikate, die pro Seite abgerufen werden sollen. | `limit=20` |

{style="table-layout:auto"}

**Anfrage**

Eine Beispielanfrage zum Zurückgeben der öffentlichen Zertifikate, die mit Ihrer Organisation verknüpft sind, finden Sie im unten stehenden ausblendbaren Abschnitt.

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

Eine erfolgreiche Antwort gibt den HTTP-Status 200 zurück und listet die öffentlichen Zertifikate für Ihr Unternehmen auf.

++ + Eine erfolgreiche Beispielantwort

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
| `certCommonName` | Der gebräuchliche Name (CN) des Zertifikats, der normalerweise den Namen oder die Identität des Servers oder der Entität darstellt, für den bzw. die das Zertifikat ausgestellt wird. |
| `publicCertificate` | Das tatsächliche öffentliche Zertifikat in einem Zeichenfolgenformat, das zum Authentifizieren und Verschlüsseln von Kommunikation verwendet wird. |
| `expiryDate` | Datum und Uhrzeit des Ablaufs des öffentlichen Zertifikats, formatiert in ISO 8601 (UTC). |

{style="table-layout:auto"}

+++

## Nächste Schritte

Nach dem Lesen dieses Handbuchs erfahren Sie jetzt, wie Sie Ihre öffentlichen Zertifikate mithilfe der Adobe Experience Platform-API abrufen können. Weitere Informationen zum Verwalten von Kundendaten zur Einhaltung von Vorschriften und Unternehmensrichtlinien finden Sie in der [Übersicht über Data Governance](../home.md).

<!-- To test this API call, navigate to the [MTLS API reference page]() to interact with the Experience Platform API endpoints. -->

<!-- Add link after developer page is live -->
