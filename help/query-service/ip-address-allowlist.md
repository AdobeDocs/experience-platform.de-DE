---
keywords: IP-Adresse, IP-Bereich, Zulassungsliste, Zulassungsliste, Query Service, Netzwerkzugriff
title: IP-Adressen-Zulassungsliste für Query Service
description: Diese Seite enthält aktualisierte IP-Bereiche, die Sie Ihrer Zulassungsliste hinzufügen können, um sicheren Zugriff auf den Query Service zu erhalten.
exl-id: f6745e0f-d387-45f2-9f72-054e721016ff
source-git-commit: e6c148b943c68bff5330c7ff021ffa88ba131639
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 4%

---

# Zulassungsliste von IP-Adressen {#ip-address-allow-list}

>[!IMPORTANT]
>
> * Adobe empfiehlt, diese Seite mit einem Lesezeichen zu versehen und alle drei Monate erneut zu besuchen, um nach den neuesten IP-Adressen zu suchen. Adobe stellt keine Benachrichtigung über neue IP-Bereiche bereit.
> * Ab dem 15. Oktober 2024 gelten nur die neuen IP-Bereiche für den Zugriff auf Query Service. Veraltete IP-Adressen funktionieren nicht mehr. Stellen Sie sicher, dass Ihre Zulassungsliste nur die neuen IPs enthält, um Dienstunterbrechungen zu vermeiden.

## Übersicht {#overview}

Sie können Netzwerkzugriffssteuerungen über Ihre Netzwerk-Firewall definieren. Durch Angabe des entsprechenden IP-Bereichs können Sie Traffic für den Zugriff auf Query Service zulassen.

Im Rahmen laufender Verbesserungen hat Adobe die IP-Bereiche für den Netzwerkzugriff auf den Query Service aktualisiert. Die vorherigen IP-Adressen werden jetzt nicht mehr unterstützt und nur die neuen IP-Adressen sind gültig. Es ist wichtig, Ihre Zulassungsliste zu aktualisieren, um die folgenden neuen IP-Bereiche einzuschließen, damit ein unterbrechungsfreier Dienst gewährleistet ist.

Adobe empfiehlt, je nach Region die folgenden regionsspezifischen IP-Bereiche zu einer Zulassungsliste hinzuzufügen. Wenn diese regionsspezifischen IP-Bereiche nicht hinzugefügt werden, kann dies zu Fehlern oder Dienstunterbrechungen führen.

## VA7: Kunden aus den USA und Amerika {#us-americas}

**Neue IP-Adresse:** 4.152.211.251

## NLD2: EMEA-Kunden {#emea}

**Neue IP-Adresse:** 108.141.12.47

## AUS5: APAC-Kunden {#apac}

**Neue IP-Adresse:** 40.82.220.111

## CAN2: Kanadische Kunden {#can2}

**Neue IP-Adresse:** 4.172.28.20

## GBR9: britische Kunden {#gbr9}

**Neue IP-Adresse:** 20.254.80.141

## IP-basierte Einschränkungen einrichten {#set-ip-restrictions}

Verwenden Sie die [API-Handbücher zur Autorisierung von Query Service](./auth-api/overview.md), um IP-basierte Einschränkungen einzurichten. Diese IP-basierten Einschränkungen stellen sicher, dass nur zugelassene Netzwerke und Clientcomputer über SQL in Adobe Experience Platform auf Daten zugreifen können. Erfahren Sie, wie Sie IP-Einschränkungen konfigurieren, durchsetzen und überwachen können, um hohe Sicherheitsstandards einzuhalten, mit Funktionen zum Echtzeit-Zugrifftracking und Warnhinweisen.

* [Handbuch &quot;Erste Schritte&quot;](./auth-api/getting-started.md)
* [Handbuch zum IP-Access-Endpunkt](./auth-api/ip-access.md)
* [IP-Validierungsendpoint-Handbuch](./auth-api/validate.md)
