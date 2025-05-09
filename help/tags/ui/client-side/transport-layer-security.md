---
title: Informationen zu Transport Layer Security (TLS)
description: Informationen darüber, welche TLS-Versionen und Chiffren verwendet werden
exl-id: 04948cd8-6cf0-4159-a9d3-3130b97af106
source-git-commit: 236c5a11f40490fc7ee536358fb146027fe64545
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 25%

---

# Informationen zu Transport Layer Security (TLS)

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine Übersicht der terminologischen Änderungen finden Sie im Dokument [Terminologieaktualisierungen](../../term-updates.md).

Transport Layer Security (TLS) ist ein kryptografisches Protokoll, das End-to-End-Sicherheit für Daten bietet, die zwischen Anwendungen über das Internet gesendet werden. Weitere Informationen zu TLS finden Sie in der Dokumentation [TLS-Grundlagen](https://www.internetsociety.org/deploy360/tls/basics/) .

Tags in Adobe Experience Platform sind ein Tag-Management-System, das dazu dient, Skripte auf Ihrer Website dynamisch zu laden. TLS sichert die Kommunikation zwischen dem Adobe-Host-`assets.adobedtm.com` und Ihrer Website, wenn diese Skripte geladen werden.

Es sind mehrere TLS-Versionen verfügbar, und sie unterstützt eine Reihe verschiedener Chiffren. Nicht alle Versionen und Chiffren sind die gleichen wie einige gelten als weniger oder sicherer als andere.

## Unterstützte TLS-Versionen und Chiffren

Die Adobe-Host-Option unterstützt derzeit die folgenden TLS-Versionen und -Chiffren:

```
PORT    STATE SERVICE
443/tcp open  https
| ssl-enum-ciphers:
|   TLSv1.2:
|     ciphers:
|       TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|       TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|     compressors:
|       NULL
|     cipher preference: server
|   TLSv1.3:
|     ciphers:
|       TLS_AKE_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|       TLS_AKE_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_AKE_WITH_CHACHA20_POLY1305_SHA256 (secp256r1) - A
|     cipher preference: client
|_  least strength: A
```

### Selbstständiges Hosting

Wenn Sie Ihre Bibliothek [selbst hosten](../publishing/hosts/self-hosting-libraries.md) werden die unterstützten TLS-Versionen von Ihrem eigenen Hosting-Service bestimmt.
