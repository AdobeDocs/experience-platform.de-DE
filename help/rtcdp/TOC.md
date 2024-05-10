---
product: adobe experience platform
solution: Real-Time Customer Data Platform
audience: user
user-guide-title: Handbuch zu Real-time Customer Data Platform
user-guide-description: Bringen Sie bekannte und anonyme Daten aus mehreren Unternehmensquellen zusammen, um Kundenprofile anzulegen, Zielgruppen aus diesen Profilen zu erstellen und diese Zielgruppen für Drittanbieterziele bereitzustellen.
role: Admin
source-git-commit: 9327cf8545caa306acd8077d089041d50a30e556
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 67%

---


# Hilfe zur Real-Time Customer Data Platform {#rtcdp}

* [Real-Time CDP-Dokumentation](home.md)
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
* Audience Manager und Real-Time CDP {#evolution}
   * [Wechsel von Audience Manager](aam-to-rtcdp.md)
* Account-Profile {#account}
   * [Übersicht über Account-Profile](accounts/account-profile-overview.md)
   * [Handbuch zur Benutzeroberfläche von Account-Profilen](accounts/account-profile-ui-guide.md)
* Administration {#admin}
   * [Administration – Übersicht](administration/admin-overview.md)
* Zielgruppen und Segmentierung {#segmentation}
   * [Segmentierung – Übersicht](segmentation/segmentation-overview.md)
   * [Segment Builder-Handbuch](segmentation/segment-builder-guide.md)
   * [Segmentierung in der Real-time CDP B2B Edition](segmentation/b2b.md)
   * [Kunden-KI](segmentation/customer-ai.md)
* Datensätze {#datasets}
   * [Datensätze](datasets/dataset.md)
   * [Datenqualität in Platform](datasets/data-quality.md)
* Ziele {#destinations}
   * [Ziele – Übersicht](destinations/overview.md)
   * [Ziele in der Real-time CDP B2B Edition](destinations/b2b.md)
* Schutzschilde {#guardrails}
   * [Übersicht über Real-Time CDP-Limits](guardrails/overview.md)
   * [Limits für die Datenerfassung](https://experienceleague.adobe.com/docs/experience-platform/ingestion/guardrails.html){target="_blank"}
   * [Limits für die [!DNL Edge Network Server API]](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/guardrails.html){target="_blank"}
   * [Limits [!DNL Real-Time Customer Profile] Daten und Segmentierung](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=de){target="_blank"}
   * [Limits [!DNL Identity Service] data](https://experienceleague.adobe.com/docs/experience-platform/identity/guardrails.html){target="_blank"}
   * [Limits [!DNL Query Service]](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html){target="_blank"}
   * [Limits für die Datenaktivierung über Ziele](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html){target="_blank"}
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
* Real-Time CDP B2B Edition – KI/ML-Dienste {#b2b-cdp-ai-ml}
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
   * [Überblick über Beispielanwendungsfälle](/help/rtcdp/use-case-guides/overview.md)
   * Kundenakquise {#customer-acquisition}
      * [Engage und Akquisition neuer Kunden ohne Abhängigkeit von Drittanbieter-Cookies](/help/rtcdp/partner-data/prospecting.md)
      * [Personalisieren von Onsite-Erlebnissen für unbekannte Besucher mithilfe der von Partnern unterstützten Besuchererkennung](/help/rtcdp/partner-data/onsite-personalization.md)
      * [Offsite-Retargeting nicht authentifizierter Benutzer](./partner-data/offsite-retargeting.md)
   * Profilanreicherung {#profile-enrichment}
      * [Ergänzen von Erstanbieterprofilen mit von Partnern bereitgestellten Attributen](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
   * Personalisierte Einblicke und Interaktion {#personalization-insights-engagement}
      * [einmaligen Kundenwert auf Lebenszeitwert erhöhen](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/evolve-one-time-value-to-lifetime-value.md)
      * [Intelligentes erneutes Ansprechen Ihrer Kunden](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md)
      * [Intelligentes erneutes Engagement Ihrer Kunden: Beispiele für Luma](/help/rtcdp/use-case-guides/intelligent-re-engagement/use-cases-luma.md)
* [Experience Platform – Versionshinweise](https://experienceleague.adobe.com/de/docs/experience-platform/release-notes/latest)
* [Glossar zu Experience Platform](https://docs.adobe.com/content/help/de-DE/experience-platform/landing/glossary.html)