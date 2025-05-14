---
title: Endpunkt des öffentlichen Zertifikats
description: Erfahren Sie, wie Sie Ihre öffentlichen Zertifikate mit dem Endpunkt /public-certificate der MTLS-Service-API abrufen.
role: Developer
exl-id: 8369c783-e595-476f-9546-801cf4f10f71
source-git-commit: d74353e70e992150c031397009d0c8add3df5e7b
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 2%

---

# Endpunkt des öffentlichen Zertifikats

>[!NOTE]
>
>Adobe unterstützt nicht mehr das statische Herunterladen öffentlicher mTLS-Zertifikate. Verwenden Sie diese API, um gültige Zertifikate für Ihre Integrationen abzurufen. Um Service-Unterbrechungen zu vermeiden, ist jetzt ein automatisierter Abruf erforderlich.

In diesem Handbuch wird erläutert, wie Sie mit dem öffentlichen Zertifikatendpunkt öffentliche Zertifikate für die Adobe-Programme Ihres Unternehmens sicher abrufen können. Er enthält einen Beispiel-API-Aufruf und detaillierte Anweisungen, die Entwicklern bei der Authentifizierung und Überprüfung des Datenaustauschs helfen.

## Erste Schritte

Bevor Sie fortfahren, lesen Sie [Erste Schritte](./getting-started.md) um wichtige Details zu erforderlichen Kopfzeilen und zur Interpretation von Beispiel-API-Aufrufen zu erhalten.

## API-Pfade {#paths}

Im Folgenden finden Sie die wesentlichen API-Pfade, die Sie für die Verwendung der mTLS-Service-API benötigen. Dazu gehören die Platform-Gateway-URL, der Basispfad für die API und ein Beispiel für einen vollständigen Pfad zum Abrufen eines öffentlichen Zertifikats.

- PLATFORM-Gateway-URL: `https://platform.adobe.io/`
- Basispfad für diese API: `/data/core/mtls`
- Beispiel für einen vollständigen Pfad: `https://platform.adobe.io/data/core/mtls/v1/certificate/public-certificate`

## Abrufen Ihrer öffentlichen Zertifikate {#list}

Stellen Sie eine GET-Anfrage an den `/v1/certificate/public-certificate`-Endpunkt, um die öffentlichen Zertifikate für eines der Adobe-Programme Ihres Unternehmens abzurufen.

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

## Automatisierung des Zertifikatlebenszyklus {#certificate-lifecycle-automation}

Adobe automatisiert den Lebenszyklus öffentlicher mTLS-Zertifikate, um Kontinuität zu gewährleisten und Service-Unterbrechungen zu reduzieren.

- Zertifikate werden 60 Tage vor ihrem Ablauf erneut ausgestellt.
- Zertifikate werden 30 Tage vor ihrem Ablauf widerrufen.

>[!NOTE]
>
>Diese Zeitpläne werden im Laufe der Zeit in Übereinstimmung mit den [CA/B-Forum-Richtlinien](https://www.digicert.com/blog/tls-certificate-lifetimes-will-officially-reduce-to-47-days) verkürzt, die darauf abzielen, die Zertifikatlebensdauer auf maximal 47 Tage zu reduzieren.

Sie müssen Ihre Integrationen aktualisieren, um den automatisierten Abruf über die API zu unterstützen. Verlassen Sie sich nicht auf manuelle Zertifikat-Downloads oder statische Kopien, da diese zu abgelaufenen oder widerrufenen Zertifikaten führen können.

## Nächste Schritte

Nachdem Sie Ihre öffentlichen Zertifikate mit der API abgerufen haben, aktualisieren Sie Ihre Integrationen, damit dieser Endpunkt regelmäßig aufgerufen wird, bevor die Zertifikate ablaufen. Um diesen Aufruf interaktiv zu testen, besuchen Sie die [MTLS-API-Referenzseite](https://developer.adobe.com/experience-platform-apis/references/mtls-service/). Weitere Anleitungen zu zertifikatbasierten Integrationen finden Sie unter [Datenverschlüsselung in Adobe Experience Platform - Übersicht](../../landing/governance-privacy-security/encryption.md) oder [Data Governance - Übersicht](../home.md).
