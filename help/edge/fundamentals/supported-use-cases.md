---
title: Unterstützte Anwendungsfälle mit dem Adobe Experience Platform Web SDK
description: Erfahren Sie, welche Anwendungsfälle vom Adobe Experience Platform Web SDK unterstützt werden.
keywords: Web SDK;Anwendungsfälle
exl-id: e0643c2c-ceb3-4ea2-aafa-1e18e0c66453
source-git-commit: ed092b85d74eaa0fdc29f3a8d28f84fe81ccca17
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 20%

---

# Unterstützte Anwendungsfälle

Auf dieser Seite werden die unterstützten Anwendungsfälle für das Web SDK mit Links zu zusätzlichen Informationen aufgeführt.

## Allgemein

| Anwendungsfall | Weitere Informationen |
| --- | --- |
| Einfaches optimiertes SDK |  |
| Globales Datenerfassungsnetzwerk |  |
| Kursbezogene Zustimmung |  |
| Kundenzustimmung nach verschiedenen Standards sammeln | <ul><li>[Adobe Consensus 2.0-Unterstützung](../../landing/governance-privacy-security/consent/adobe/overview.md)</li><li>[IAB TCF 2.0-Unterstützung](../../landing/governance-privacy-security/consent/iab/overview.md)</li><li>[SDK integrieren, um Zustimmungssignale an Edge Network zu senden](../../landing/governance-privacy-security/consent/sdk.md)</li></ul> |
| ECID-Unterstützung | Informationen zum Abrufen der ECID finden Sie in unserer Dokumentation [hier](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#first-party-identity) und [hier](https://experienceleague.adobe.com/docs/experience-platform/edge/extension/accessing-the-ecid.html?lang=en#extension) |
| Erfassen mehrerer Entitäten |  |
| Unterstützung von Gerätediagrammen (öffentlich/privat) | [Dokumentation](https://experienceleague.adobe.com/docs/analytics/components/cda/device-graph.html?lang=en) |
| Senden von Daten an mehrere Organisationen auf der Seite | [Dokumentation](./interacting-with-multiple-properties.md) |
| Detaillierte Fehlerberichte und -protokolle |  |
| Clientseitige und serverseitige Trace-Anforderungen |  |
| Tag-Erweiterung | [Dokumente zur Web SDK-Erweiterung](../../tags/extensions/web/sdk/overview.md) |
| Debugging-Tools verfügbar | [Debugger-](https://experienceleague.adobe.com/docs/debugger-learn/tutorials/experience-platform-debugger/introduction-to-the-experience-platform-debugger.html?lang=en) Erweiterung und  [Griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon) |

{style=&quot;table-layout:auto&quot;}

## Adobe Experience Platform

| Anwendungsfall | Weitere Informationen |
| --- | --- |
| Senden von Erlebnisereignissen |  |
| Offer Decisioning | [Dokumentation](../personalization/offer-decisioning/offer-decisioning-overview.md) |
| Wenn der Datensatz für das Profil aktiviert ist, Möglichkeit, Daten in Echtzeit an das Echtzeit-Kundendatenprofil zu senden |  |
| Senden von Daten an Customer Journey Analytics in Echtzeit |  |
| Einverständnis zum Profil schreiben | [Dokumentation](../../landing/governance-privacy-security/consent/sdk.md) |
| Übermitteln von Daten Server-seitig in Echtzeit an Dritte | [Dokumentation](../../tags/ui/event-forwarding/overview.md) |
| Unterstützung von Identitäts-Namespaces |  |

{style=&quot;table-layout:auto&quot;}

## Adobe Analytics

| Anwendungsfall | Weitere Informationen |
| --- | --- |
| Analytics for Target (A4T) |  |
| Keine Latenz von Analytics for Target (A4T) |  |
| Multi-Suite-Tagging |  |
| Bot-Filterung |  |
| Props, eVars und Ereignisse |  |
| ListVar-Unterstützung für Adobe Analytics |  |
| Betriebssystem und Browserversion |  |
| Vordefinierte Variablen | [Automatisch zugeordnete Variablen](../data-collection/adobe-analytics/automatically-mapped-vars.md) |
| VISTA-Regeln/Verarbeitungsregeln |  |
| Unterstützung von Besucherattributen |  |
| Unterstützung von Exitlinks |  |
| Benutzerspezifische Links/Downloadlinks |  |
| Status- und Aktionsverfolgung |  |
| Ereignis-Serialisierung für Standardereignisse |  |
| Variable „products“ | [Dokumentation](../data-collection/collect-commerce-data.md#actions-related-to-products) |

{style=&quot;table-layout:auto&quot;}

## Adobe Target

| Anwendungsfall | Weitere Informationen |
| --- | --- |
| Alle Aktivitätstypen |  |
| Unterstützung nativer und SPA Visual Experience Composer | [Dokumentation](../personalization/adobe-target/spa-implementation.md) |
| Form-Based Composer |  |
| Unterstützung für globale Mbox | [Dokumentation](../personalization/rendering-personalization-content.md#automatically-rendering-content) |
| Benutzerdefinierte Mboxes | [Dokumentation](../personalization/rendering-personalization-content.md#manually-rendering-content) |
| Analytics for Target (A4T) |  |
| Umgebungsunterstützung |  |
| Workspace-Unterstützung |  |
| QA-Links in Adobe Target |  |
| Targeting auf Basis von Geo/Gerät in Adobe Target |  |
| Unterstützung von Besucherattributen |  |
| Profilskripte |  |
| XDM wird zu Mbox-Parametern |  |
| Unterstützte Umleitungsangebote mit A4T-Reporting | [Dokumentation](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=en) |
| Aktualisieren des Target-Profils | [Dokumentation](../personalization/adobe-target/target-overview.md#single-profile-update) |
| Empfehlungen |  |
| mBox-Drittanbieter-ID |  |
| Antwort-Token | [Dokumentation](../personalization/adobe-target/accessing-response-tokens.md) |

{style=&quot;table-layout:auto&quot;}

## Adobe Audience Manager

| Anwendungsfall | Weitere Informationen |
| --- | --- |
| Audience Analytics |  |
| Segmentfreigabe an Adobe Analytics |  |
| Unterstützung von Besucherattributen |  |
| Partnersynchronisierungen |  |
| URL-Ziele |  |
| Cookie-Ziele |  |
| Umgebungsunterstützung |  |
| Synchronisieren von Adobe Experience Platform-Namespaces mit Audience Manager-Datenquellen |  |
| Authentifizierte oder bekannte IDs |  |

{style=&quot;table-layout:auto&quot;}
