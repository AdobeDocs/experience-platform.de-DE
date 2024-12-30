---
keywords: IP-Adresse, IP-Bereich, Zulassungsliste auf die Zulassungsliste setzte,, Abfrage-Service, Netzwerkzugriff
title: AUF DIE ZULASSUNGSLISTE SETZEN IP-Adresse für den Abfrage-Service
description: Auf dieser Seite finden Sie aktualisierte IP-Bereiche, die Sie Ihrer Zulassungsliste hinzufügen können, um einen sicheren Zugriff auf den Abfrage-Service zu ermöglichen.
exl-id: f6745e0f-d387-45f2-9f72-054e721016ff
source-git-commit: ac29d10d3774a736d1e54255508ba244ff72f278
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 4%

---

# Zulassungsliste von IP-Adressen {#ip-address-allow-list}

>[!IMPORTANT]
>
> * Adobe empfiehlt, ein Lesezeichen für diese Seite zu setzen und sie alle drei Monate erneut aufzurufen, um nach den neuesten IP-Adressen zu suchen. Adobe bietet keine Benachrichtigung über neue IP-Bereiche.
> * Ab dem 15. Oktober 2024 sind nur die neuen IP-Bereiche für den Zugriff auf den Abfrage-Service gültig. Veraltete IP-Adressen funktionieren nicht mehr. Stellen Sie sicher, dass Ihre Zulassungsliste nur die neuen IPs enthält, um Service-Unterbrechungen zu vermeiden.

## Übersicht {#overview}

Sie können Netzwerkzugriffssteuerungen über Ihre Netzwerk-Firewall definieren. Durch Angabe des entsprechenden IP-Bereichs können Sie Traffic für den Zugriff auf den Abfrage-Service zulassen.

Im Rahmen laufender Verbesserungen hat Adobe die IP-Bereiche für den Netzwerkzugriff auf den Abfrage-Service aktualisiert. Die vorherigen IP-Adressen werden jetzt nicht mehr unterstützt, und nur die neuen IP-Adressen sind gültig. Es ist wichtig, dass Sie Ihre -Zulassungsliste aktualisieren, um die folgenden neuen IP-Bereiche einzuschließen, um einen unterbrechungsfreien Service aufrechtzuerhalten.

Adobe empfiehlt, je nach Region die folgenden regionsspezifischen IP-Bereiche zu einer Zulassungsliste hinzuzufügen. Wenn diese regionsspezifischen IP-Bereiche nicht hinzugefügt werden, kann dies zu Fehlern oder Service-Unterbrechungen führen.

## VA7: Kunden in den USA und Amerika {#us-americas}

**Neue IP:** 4.152.211.251

## NLD2: EMEA-Kunden {#emea}

**Neue IP:** 108.141.12.47

## AUS5: APAC-Kunden {#apac}

**Neue IP:** 40.82.220.111

## CAN2: Kanadische Kunden {#can2}

**Neue IP:** 4.172.28.20

## GBR9: Kunden in Großbritannien {#gbr9}

**Neue IP:** 20.254.80.141

## Einrichten von IP-basierten Einschränkungen {#set-ip-restrictions}

Verwenden Sie die [Handbücher zur Data Distiller-Autorisierungs](./auth-api/overview.md)API, um IP-basierte Einschränkungen einzurichten. Diese IP-basierten Einschränkungen stellen sicher, dass nur genehmigte Netzwerke und Client-Computer über SQL in Adobe Experience Platform auf Daten zugreifen können. Erfahren Sie, wie Sie IP-Einschränkungen konfigurieren, durchsetzen und überwachen können, um hohe Sicherheitsstandards zu erfüllen, einschließlich Funktionen für Echtzeit-Zugriffsverfolgung und -Warnmeldungen.

* [Erste Schritte](./auth-api/getting-started.md)
* [Handbuch für IP-Zugriffsendpunkte](./auth-api/ip-access.md)
* [Handbuch zum IP-Validierungsendpunkt](./auth-api/validate.md)
