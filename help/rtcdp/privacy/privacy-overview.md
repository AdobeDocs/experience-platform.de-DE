---
keywords: Data Governance rtcdp;rtcdp Data Governance;Echtzeit-Data Profil Data Governance;Datenschutz rtcdp;rtcdp privacy
title: Datenschutz in Real-time Customer Data Platform
description: Mit Real-time Customer Data Platform können Sie die Einhaltung von Datenschutzbestimmungen bei Ihren Datenvorgängen optimieren.
exl-id: bcb0e42e-4549-4952-bb69-5534aee353f8
source-git-commit: ad0d38cbd249642d582a807c5679065827f57717
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 6%

---

# Datenschutz in Real-time Customer Data Platform

[!DNL Real-time Customer Data Platform] ([!DNL Real-time CDP]) hilft Marketern, Daten aus verschiedenen Unternehmenssystemen zusammenzuführen, sodass sie ihre Kunden besser identifizieren, verstehen und ansprechen können. Adobe betrachtet den Schutz von Kundendaten als grundlegendes Design-Prinzip und bietet verschiedene Steuerelemente, mit denen Marketer den Datenschutz von Kunden verwalten können.

Die Mehrheit der [!DNL Real-time CDP] Funktionen werden von Adobe Experience Platform unterstützt. Dieses Dokument enthält Informationen zu den verschiedenen Technologien zur Datenschutzverbesserung, die von [!DNL Real-time CDP], mit Links zu [!DNL Experience Platform] Dokumentation finden Sie weitere Informationen.

## Berücksichtigung von Zugriffs- und Löschanfragen von Kunden

Rechtliche Datenschutzbestimmungen wie die [!DNL General Data Protection Regulation] (DSGVO) und die [!DNL California Consumer Privacy Act] (CCPA) geben Kunden das Recht, Zugang zu den von ihnen erfassten personenbezogenen Daten oder deren Löschung anzufordern. Seit [!DNL Real-time CDP] nutzt [!DNL Experience Platform] Funktionen für die Datenerfassung und -speicherung, sollten Kundenanfragen für den Zugriff auf und die Löschung ihrer personenbezogenen Daten in [!DNL Platform]. Siehe Übersicht unter [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) für weitere Informationen.

>[!IMPORTANT]
>
> Datenschutzanfragen, die von Adobe Experience Platform Privacy Service für Adobe Marketo Engage gesendet werden, gelten nur für B2B-Kunden mit Echtzeit-Kundendatenplattform.

## Opt-out-Funktionen

[!DNL Real-time CDP] ermöglicht es Kunden, die Aufnahme ihrer personenbezogenen Daten in Segmentierungsanwendungsfälle abzuwählen. Die Opt-out-Voreinstellungen von Kunden werden erfasst und gespeichert von [!DNL Real-time Customer Profile]und können erzwungen werden, indem Benutzer ausgeschlossen werden, die sich mit boolescher Logik (&quot;AND NOT&quot;) in der Segmenteigenschaft von einem Segment abgemeldet haben.

Siehe Dokument unter [Berücksichtigung von Opt-out-Anfragen](../../segmentation/consents.md) Weitere Informationen finden Sie in der Dokumentation zu Adobe Experience Platform Segmentation Service .

## IAB TCF 2.0-Unterstützung

[!DNL Real-time CDP] basiert auf Adobe Experience Platform, das Teil der registrierten [Anbieterliste](https://iabeurope.eu/vendor-list-tcf-v2-0/) für [!DNL Transparency & Consent Framework (TCF)], wie in der [!DNL Interactive Advertising Bureau (IAB)]. In Übereinstimmung mit den TCF 2.0-Anforderungen können Sie mit Platform detaillierte Kundenzustimmungsdaten erfassen und in Ihre gespeicherten Kundenprofile integrieren. Diese Einwilligungsdaten können dann je nach Anwendungsfall in exportierte Zielgruppensegmente einbezogen werden.

Siehe Übersicht unter [IAB TCF 2.0-Unterstützung für Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md) für weitere Informationen.

## Nächste Schritte

In diesem Dokument erhalten Sie eine kurze Einführung in die Datenschutzfunktionen von [!DNL Real-time CDP]. Weitere Informationen zu den einzelnen Funktionen finden Sie in der Dokumentation zu den einzelnen Funktionen in diesem Handbuch.
