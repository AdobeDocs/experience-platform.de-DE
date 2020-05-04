---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Datenschutzdienst und Experience Cloud-Anwendungen
topic: overview
translation-type: tm+mt
source-git-commit: 14cd3d17c7d9ba602d02925abddec9e0b246a8c8

---


# Datenschutzdienst und Experience Cloud-Anwendungen

Der Datenschutzdienst für Adobe Experience Platform wurde zur Unterstützung von Datenschutzanforderungen für mehrere Adobe Experience Cloud-Anwendungen entwickelt. Jede Anwendung unterstützt verschiedene Produktwerte und IDs zur Identifizierung von Datensubjekten.

Dieses Dokument dient als Referenz für die Experience Cloud-Anwendungsdokumentation, in der beschrieben wird, wie Sie diese Anwendung für datenschutzbezogene Vorgänge konfigurieren. Dazu gehört auch die Formatierung und Beschriftung Ihrer Daten. Es werden zwei Kategorien von Anträgen behandelt:

* [In den Datenschutzdienst integrierte Anwendungen](#integrated): Anwendungen, die Zugriff-, Löschungs- oder Ausschluss-Anfragen an den Datenschutzdienst senden können.
* [Selbstbedienungsanwendungen](#self-serve): Anwendungen, die ihre Datenschutzanforderungen intern verwalten müssen und nicht direkt mit dem Datenschutzdienst kommunizieren können.

In der Dokumentation zu Ihren Experience Cloud-Anwendungen erfahren Sie, wie Sie Ihre Datenschutzanforderungen formatieren und welche Werte für diese Anforderungen unterstützt werden.

## Anwendungen, die in den Datenschutzdienst integriert sind {#integrated}

Im Folgenden finden Sie eine Liste von Experience Cloud-Anwendungen, die in den Datenschutzdienst integriert sind, einschließlich der Funktionen des Datenschutzdienstes, mit denen sie kompatibel sind, und Links zur Dokumentation, um weitere Informationen zu erhalten.

| Anwendung | Zugriff/Löschen | Ausschluss vom Verkauf | Dokumentation und Überlegungen |
--- | :---: | :---: | ---
| Adobe Advertising Cloud | ✓ | ✓ | <ul><li>[Dokumentation aufrufen/löschen](https://docs.adobe.com/content/help/en/advertising-cloud/all/privacy/ad-cloud-gdpr.html) </li><li>Die Advertising Cloud nutzt die bestehenden globalen Abmeldefunktionen des Adobe Datenschutzzentrums. Weitere Informationen finden Sie im Handbuch zum [Erstellen von Datenschutzanforderungen](https://docs.adobe.com/content/help/de-DE/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#opt-out-requests) .</li></ul> |
| Adobe Analytics | ✓ | ✓ | <ul><li>[Dokumentation aufrufen/löschen](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-overview.html)</li><li>Analytics verarbeitet Ausschluss-Anfragen mithilfe von Variablen des [Privacy Berichte](https://docs.adobe.com/content/help/de-DE/analytics/admin/data-governance/consent-variables.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | <ul><li>[Dokumentation aufrufen/löschen](https://docs.adobe.com/content/help/de-DE/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[Dokumentation zur Abmeldung](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | <ul><li>[Dokumentation aufrufen/löschen](https://docs.campaign.adobe.com/doc/standard/getting_started/de/ACS_GDPR.html)</li><li>[Dokumentation zur Abmeldung](../segmentation/honoring-opt-outs.md)</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | <ul><li>[Dokumentation zum Data Lake aufrufen/löschen](../catalog/privacy.md)</li><li>[Dokumentation für Echtzeit-Kundendaten aufrufen/löschen](../profile/privacy.md)</li><li>Experience Platform berücksichtigt [Abmeldeanforderungen für Audiencen-Segmente](../segmentation/honoring-opt-outs.md).</li></ul> |
| Adobe Primetime-Authentifizierung | ✓ | K. A. | <ul><li>[Dokumentation aufrufen/löschen](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>Primetime ist nicht in der Lage, Daten zu übertragen. Daher sind Ausschlussanträge nicht möglich.</li></ul> |
| Adobe Target | ✓ | K. A. | <ul><li>[Dokumentation aufrufen/löschen](https://docs.adobe.com/content/help/de-DE/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.translate.html)</li><li>Die Zielgruppe kann keine Daten übertragen, daher sind Ausschlussanträge nicht möglich.</li></ul> |

<!-- (To include once access/delete documentation is available)
Adobe Customer Attributes (CRS) | ✓ | N/A | <ul><li>Customer Attributes does not have the capability to transfer data, therefore opt-out-of-sale requests are not applicable.</li></ul>
-->

## Selbstbedienungsanwendungen {#self-serve}

Im Folgenden finden Sie eine Liste von Experience Cloud-Anwendungen, die nicht in den Datenschutzdienst integriert sind und ihre Datenschutzbelange intern verwalten müssen. Links zur Dokumentation der einzelnen Anwendungen sowie Beschreibungen des Inhalts der Dokumentation werden bereitgestellt.

| Anwendung | Beschreibung der Dokumentation |
| ------- | ----------- |
| [Adobe Campaign Classic](https://docs.campaign.adobe.com/doc/AC/getting_started/DE/ACC_GDPR.html) | Eine Übersicht über die GDPR-Funktionen von Adobe Campaign Classic. |
| [Adobe Dynamischer Tag-Manager](https://docs.adobe.com/content/help/en/dtm/using/tools/opt-in.html) | Schritte, die verhindern, dass Adobe-Tags ausgelöst werden, bis die Zustimmung erteilt wurde. |
| [Adobe Experience Manager](https://helpx.adobe.com/experience-manager/6-4/managing/using/gdpr-compliance.html) | Eine Übersicht darüber, wie ein Datenschutzadministrator oder AEM-Administrator GDPR-Anforderungen bearbeiten kann. |
| [Adobe Experience Manager Livefyre](https://docs.adobe.com/content/help/en/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Schritte zum Erstellen des Zugriffs auf GDPR und Löschen von Anforderungen mit Livefyre. |
| [Adobe Experience Platform Launch](https://docs.adobelaunch.com/client-side-information/deploy-javascript-tags-to-opt-in-to-launch) | Anleitung für Entwickler zur Verwendung von Erweiterungen und Rule Builder zum Definieren von Opt-in- und Opt-out-Lösungen. |
