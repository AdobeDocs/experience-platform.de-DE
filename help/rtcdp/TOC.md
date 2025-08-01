---
product: adobe experience platform
solution: Real-Time Customer Data Platform
audience: user
user-guide-title: Handbuch zu Real-time Customer Data Platform
user-guide-description: Bringen Sie bekannte und anonyme Daten aus mehreren Unternehmensquellen zusammen, um Kundenprofile anzulegen, Zielgruppen aus diesen Profilen zu erstellen und diese Zielgruppen für Drittanbieterziele bereitzustellen.
role: Admin
source-git-commit: 74a73b568c850f8e749afea039afd2821858bd69
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 60%

---


# Hilfe zur Real-Time Customer Data Platform {#rtcdp}

* [Dokumentation zu Real-Time CDP](home.md)
* Erste Schritte {#intro}
   * Real-Time CDP {#rtcdp-intro}
      * [Real-Time CDP – Übersicht](overview.md)
      * [Erste Schritte mit Real-time CDP](get-started.md)
      * [Startseite](home-page-dashboards.md)
   * Real-Time CDP B2B Edition {#rtcdpb2b-intro}
      * [Real-Time CDP B2B Edition – Übersicht](b2b-overview.md)
      * [Beispielanwendungsfall](./b2b-use-case.md)
      * [Tutorial mit der Beschreibung aller Schritte](./b2b-tutorial.md)
      * [Leitlinien für die Real-time CDP B2B Edition](b2b-guardrails.md)
      * [Architekturaktualisierungen für Real-Time CDP B2B edition](b2b-architecture-upgrade.md)
* Audience Manager und Real-Time CDP {#evolution}
   * [Wechsel von Audience Manager](aam-to-rtcdp.md)
* Kontoprofile {#account}
   * [Übersicht über Account-Profile](accounts/account-profile-overview.md)
   * [Handbuch zur Benutzeroberfläche von Account-Profilen](accounts/account-profile-ui-guide.md)
* Administration {#admin}
   * [Administration – Übersicht](administration/admin-overview.md)
* Zielgruppen und Segmentierung {#segmentation}
   * [Segmentierung – Übersicht](segmentation/segmentation-overview.md)
   * [Audience Builder-Handbuch](segmentation/audience-builder.md)
   * [Segmentierung in der Real-time CDP B2B Edition](segmentation/b2b.md)
   * [Kunden-KI](segmentation/customer-ai.md)
* Datensätze {#datasets}
   * [Datensätze](datasets/dataset.md)
   * [Datenqualität in Experience Platform](datasets/data-quality.md)
* Ziele {#destinations}
   * [Ziele – Übersicht](destinations/overview.md)
   * [Ziele in der Real-time CDP B2B Edition](destinations/b2b.md)
* Leitlinien {#guardrails}
   * [Übersicht über Real-Time CDP-Schutzmechanismen](guardrails/overview.md)
   * [Schutzmaßnahmen bei der Datenaufnahme](https://experienceleague.adobe.com/docs/experience-platform/ingestion/guardrails.html?lang=de){target="_blank"}
   * [Leitplanken für den [!DNL Edge Network API]](https://developer.adobe.com/data-collection-apis/docs/getting-started/guardrails/){target="_blank"}
   * [Leitplanken für  [!DNL Real-Time Customer Profile]  und Segmentierung](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=de){target="_blank"}
   * [Leitplanken für [!DNL Identity Service] data](https://experienceleague.adobe.com/docs/experience-platform/identity/guardrails.html?lang=de){target="_blank"}
   * [Schutzmaßnahmen für [!DNL Query Service]](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=de){target="_blank"}
   * [Leitplanken für die Datenaktivierung durch Ziele](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html?lang=de){target="_blank"}
* Identitäten {#identity}
   * [Identitäten und Identity-Namespaces](profile/identities-overview.md)
* Zusammenführungsrichtlinien {#merge-policies}
   * [Zusammenführungsrichtlinien – Übersicht](profile/merge-policies.md)
* Datenschutz und Data Governance {#privacy}
   * [Datenschutz – Übersicht](privacy/privacy-overview.md)
   * [Data Governance – Übersicht](privacy/data-governance-overview.md)
* Profile {#profile}
   * [Profil – Übersicht](profile/profile-overview.md)
   * [Profil durchsuchen](profile/profile-browse.md)
* KI-/ML-Services von Real-Time CDP B2B edition {#b2b-cdp-ai-ml}
   * [Verwandte Konten](b2b-ai-ml-services/related-accounts.md)
   * [Lead-Konto-Zuordnung](b2b-ai-ml-services/lead-to-account-matching.md)
   * Prädiktives Lead- und Konto-Scoring {#predictive-lead-and-account-scoring-intro}
      * [Prädiktives Lead- und Konto-Scoring – Übersicht](b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
      * [Verwalten von prädiktivem Lead- und Konto-Scoring](b2b-ai-ml-services/manage-predictive-lead-and-account-scoring.md)
* Schemata {#schemas}
   * [Übersicht über Schemata](schemas/overview.md)
   * [Schemata in der Real-time CDP B2B Edition](schemas/b2b.md)
* Quellen {#sources}
   * [Quellen – Übersicht](sources/sources-overview.md)
   * [Quellen in der Real-time CDP B2B Edition](sources/b2b.md)
* Anwendungsfälle {#use-cases}
   * [Übersicht über Beispielanwendungsfälle](/help/rtcdp/use-case-guides/overview.md)
   * Kundenakquise {#customer-acquisition}
      * [Kundengewinnung und -gewinnung ohne Abhängigkeit von Drittanbieter-Cookies](/help/rtcdp/partner-data/prospecting.md)
      * [Personalisieren von Onsite-Erlebnissen für unbekannte Besucher mithilfe der partnergestützten Besuchererkennung](/help/rtcdp/partner-data/onsite-personalization.md)
      * [Offsite-Retargeting nicht authentifizierter Benutzer](./partner-data/offsite-retargeting.md)
      * [Nicht authentifiziertes Server-seitiges Retargeting](./partner-data/unauthenticated-retargeting.md)
   * Profilanreicherung {#profile-enrichment}
      * [Ergänzen von Erstanbieterprofilen mit von Partnern bereitgestellten Attributen](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
   * Personalisierte Einblicke und Interaktion {#personalization-insights-engagement}
      * [Weiterentwicklung des einmaligen Kundenwerts zum Lebenszeitwert](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/evolve-one-time-value-to-lifetime-value.md)
      * [Kunden auf intelligente Weise wieder ansprechen](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md)
      * [Kunden intelligent wieder ansprechen: Luma-Beispiele](/help/rtcdp/use-case-guides/intelligent-re-engagement/use-cases-luma.md)
* [Experience Platform – Versionshinweise](https://experienceleague.adobe.com/de/docs/experience-platform/release-notes/latest)
* [Glossar zu Experience Platform](https://docs.adobe.com/content/help/de-DE/experience-platform/landing/glossary.html)