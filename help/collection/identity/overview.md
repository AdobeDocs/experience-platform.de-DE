---
title: Identität in der Datenerfassung
description: Erfahren Sie, wie die Datenerfassung ECIDs, CORE-IDs, First-Party-Persistenz und identityMap in Web-Implementierungen verwendet.
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---

# Identität in der Datenerfassung

Die Datenerfassung von Adobe verwendet Identitätssignale, um wiederkehrende Besucher zu erkennen und Kontext über Erlebnisse hinweg zu übertragen. Wenn ein Besucher Ihre Site erreicht, generiert die Edge Network eine Experience Cloud ID (ECID) und speichert sie in einem Erstanbieter-Cookie. Diese ECID ist die primäre Gerätekennung, die in allen Adobe Experience Cloud-Programmen verwendet wird, und bildet die Grundlage, auf der Analysen, Personalisierung und Zielgruppenaktivierung aufbauen. In Ihrer -Implementierung können Sie über den [`getIdentity`](/help/collection/js/commands/getidentity.md)-Befehl Client-seitig auf die ECID des Besuchers zugreifen. Auf der Datenstromebene können Sie [Datenvorbereitung für die Datenerfassung) verwenden, um &#x200B;](/help/datastreams/data-prep.md) ECID einem benutzerdefinierten XDM-Feld zuzuordnen, bevor sie nachgelagerte Services erreicht.

Die ECID identifiziert ein Gerät, keine Person. Um eine Aktivität mit einer bekannten Person zu verknüpfen, können Sie neben der ECID zusätzliche Kennungen wie eine CRM-ID oder eine Hash-E-Mail senden, indem Sie die XDM-[`identityMap`](./identity-map.md) verwenden. Adobe empfiehlt, einen Namespace auf Personenebene als [primäre Identität](/help/tags/extensions/client/web-sdk/data-element-types.md#identity-map) festzulegen, sofern verfügbar.

Über die standardmäßige ECID hinaus unterstützt die Datenerfassung je nach Implementierung zusätzliche Identitätssignale:

* **Erstanbieter-Geräte-IDs (FPIDs)**: Geräte-IDs, die Sie in der von Ihnen verwalteten Infrastruktur generieren und verwalten. Edge Network verwendet einen FPID zum [&#x200B; (Seed) der ECID](./fpid.md), sodass Sie eine höhere Cookie-Persistenz in eigenen Eigenschaften erzielen, wenn Browser-Einschränkungen die Lebensdauer von Adobe-verwalteten Cookies verkürzen.
* **CORE IDs**: Eine separate, demdex-basierte Kennung, die an Identitäts-Workflows von Drittanbietern beteiligt ist, wenn Drittanbieter-Cookies verfügbar sind. Die CORE-ID unterscheidet sich von der ECID und kann über [`getIdentity`](/help/collection/js/commands/getidentity.md) abgerufen werden. Weitere Informationen dazu, wie Identitätskontexte von Erstanbietern und Drittanbietern zusammenarbeiten, finden Sie unter [Einheitliche Identitätsunterstützung](./unified-identity-support.md).

Wenn Sie ein Upgrade von der Besucher-API durchführen oder das ältere Identitätsverhalten abstimmen, finden Sie weitere Informationen unter Migrieren vorhandener AMCV-Cookies [`idMigrationEnabled`](/help/collection/js/commands/configure/idmigrationenabled.md).

## Sammlung von Erstanbietern und Drittanbietern {#first-party-and-third-party-collection}

Web SDK setzt Identitäts[Cookies](https://experienceleague.adobe.com/de/docs/core-services/interface/data-collection/cookies/web-sdk) (z. B. `kndctr_` Cookies) immer als Erstanbieter-Cookies in Ihrer Domain, unabhängig davon, welcher Endpunkt die Datenerfassungsanfrage erhält. Der Sammlungsendpunkt (die Domain, an die Ihre Implementierung Daten sendet) ist eine separate Auswahl, die beeinflusst, wie Browser und Netzwerkrichtlinien die Anfrage selbst behandeln.

**Erstanbieterererfassung** leitet Datenerfassungsanfragen über eine Domain, die Ihr Unternehmen kontrolliert (z. B. `data.example.com`), mithilfe eines CNAME, der auf Adobes Edge Network verweist. Da die Anfrage in Ihrer Domain verbleibt, ist es weniger wahrscheinlich, dass sie durch Werbe-Blocker oder Browser-Netzwerkbeschränkungen blockiert wird. Die First-Party-Erfassung ist auch eine Voraussetzung für das Festlegen [First-Party-Geräte-IDs](./fpid.md) aus Ihrer eigenen Server-Infrastruktur, was die dauerhafteste verfügbare Identitätsstrategie ist. Adobe empfiehlt die Verwendung des von [Adobe verwalteten Zertifikatprogramms](https://experienceleague.adobe.com/de/docs/core-services/interface/data-collection/adobe-managed-cert) zum Konfigurieren der Erstanbieter-Datenerfassung für Ihre Implementierung.

**Drittanbietersammlung** sendet Anfragen direkt an eine Adobe-eigene [`edgeDomain`](/help/collection/js/commands/configure/edgedomain.md) (z. B. `example.data.adobedc.net`). Während Identitäts-Cookies in Ihrer Domain weiterhin als Erstanbieter festgelegt werden, geht die Anfrage selbst an eine Drittanbieterdomäne, die von einigen Browsern und Anzeigenblockern eingeschränkt werden kann.

## Auswählen des richtigen Identitätsmusters {#choose-your-path}

* **Stärkung der Identitätspersistenz in eigenen Eigenschaften**: Verwenden Sie [Erstanbieter-Geräte-IDs](./fpid.md) wenn Browser-Einschränkungen die Cookie-Lebensdauer verkürzen und Sie eine stärkere Kontinuität für Analysen und Personalisierung auf Sites benötigen, die Sie steuern.
* **Identität von einer App an mobiles Web übergeben**: Verwenden Sie [Identitätsfreigabe von Mobile zu Web](./mobile-to-web.md), wenn der Besucher in Ihrer mobilen App beginnt und in einer WebView oder mobilen Web-Seite fortfährt.
* **Identität domänenübergreifend kontinuierlich beibehalten**: Verwenden Sie [Domain-übergreifende Freigabe](./cross-domain-sharing.md), wenn Besucher zwischen Web-Eigenschaften wechseln, denen Ihr Unternehmen gehört, und Sie konsistente Berichte und Personalisierungen wünschen.
* **Kombinieren Sie die Persistenz von Erstanbietern mit der Aktivierung** Drittanbietern: Verwenden Sie [Unterstützung für einheitliche &#x200B;](./unified-identity-support.md)), wenn Sie neben unterstützten Aktivierungsflüssen von Drittanbietern eine dauerhafte Identifizierung von Erstanbietern benötigen.
* **Kennungen auf Personenebene senden**: Verwenden Sie [`identityMap`](./identity-map.md), um CRM-IDs, Hash-E-Mails und andere Kennungen auf Personenebene zusammen mit der ECID zu senden, damit nachgelagerte Services Aktivitäten mit einer bekannten Person verknüpfen können.
* **Auswirkungen von Einverständnis auf Identität verstehen**: Lesen Sie [Einverständnis und Identität](./consent.md) um zu erfahren, wie `defaultConsent` und `setConsent` steuern, wann die Web-SDK eine ECID generiert, Cookies setzt und Daten sendet.

Hilfe bei der Diagnose von Identitätsproblemen wie Besucherzuwachs, ECID-Inkonsistenzen oder FPID-Problemen finden Sie [Fehlerbehebung bei Identitätsproblemen](./troubleshooting.md).
