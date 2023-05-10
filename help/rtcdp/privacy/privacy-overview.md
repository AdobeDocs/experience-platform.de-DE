---
keywords: Data Governance rtcdp;rtcdp Data Governance;Data Governance für Echtzeit-Kundenprofil-Daten;Datenschutz rtcdp;rtcdp Datenschutz
title: Datenschutz in Real-time Customer Data Platform
description: Mit Adobe Real-time Customer Data Platform können Sie die Einhaltung von Datenschutzbestimmungen bei Ihren Datenvorgängen optimieren.
exl-id: bcb0e42e-4549-4952-bb69-5534aee353f8
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 100%

---

# Datenschutz in Real-time Customer Data Platform

Mit [!DNL Adobe Real-Time Customer Data Platform] ([!DNL Real-Time CDP]) können Marketing-Fachleute Daten aus verschiedenen Unternehmenssystemen zusammenführen, damit sich Kundinnen und Kunden besser ermitteln, verstehen und ansprechen lassen. Adobe betrachtet den Schutz von Kundendaten als grundlegendes Design-Prinzip und bietet verschiedene Steuerelemente, mit denen Marketing-Fachleute den Datenschutz ihrer Kundinnen und Kunden verwalten können.

Die meisten Funktionen von [!DNL Real-Time CDP] werden über Adobe Experience Platform bereitgestellt. Das vorliegende Dokument enthält Informationen über die verschiedenen Technologien zur Verbesserung des Datenschutzes, die von [!DNL Real-Time CDP] unterstützt werden, sowie Links zur [!DNL Experience Platform]-Dokumentation, die weiterführende Informationen bietet.

## Berücksichtigung kundenseitiger Zugriffs- und Löschanfragen

Rechtliche Datenschutzbestimmungen wie die [!DNL General Data Protection Regulation] (DSGVO) und der [!DNL California Consumer Privacy Act] (CCPA) geben Kundinnen und Kunden das Recht, Auskunft über die zu ihnen erfassten personenbezogenen Daten oder deren Löschung zu verlangen. Da [!DNL Real-Time CDP] [!DNL Experience Platform]-Funktionen für die Datenerfassung und -speicherung nutzt, sollten Kundenanfragen zur Auskunft zu und Löschung von personenbezogenen Daten in [!DNL Platform] abgewickelt werden. Weiterführende Informationen finden Sie in der Übersicht zu [Adobe Experience Platform Privacy Service](../../privacy-service/home.md).

>[!IMPORTANT]
>
> Datenschutzanfragen, die über Adobe Experience Platform Privacy Service für Adobe Marketo Engage eingereicht werden, gelten nur für Kundinnen und Kunden von Real-Time CDP B2B.

## Opt-out-Funktionen

[!DNL Real-Time CDP] ermöglicht es Kundinnen und Kunden, die Aufnahme ihrer personenbezogenen Daten in Segmentierungsanwendungsfälle abzuwählen. Die kundenseitigen Opt-out-Voreinstellungen werden von [!DNL Real-Time Customer Profile] erfasst und gespeichert und können erzwungen werden, indem Benutzende ausgeschlossen werden, die sich mit boolescher Logik („AND NOT“) im Segmentprädikat von einem Segment abgemeldet haben.

Weitere Informationen finden Sie im Dokument zu [Berücksichtigung von Opt-out-Anfragen](../../segmentation/consents.md) in der Dokumentation zum Segmentierungs-Service in Adobe Experience Platform.

## IAB TCF 2.0-Unterstützung

[!DNL Real-Time CDP] basiert auf Adobe Experience Platform, das Teil der registrierten [Anbieterliste](https://iabeurope.eu/vendor-list-tcf-v2-0/) für den [!DNL Transparency & Consent Framework (TCF)] ist, wie vom [!DNL Interactive Advertising Bureau (IAB)] beschrieben. In Übereinstimmung mit den TCF 2.0-Anforderungen können Sie mit Platform detaillierte Kundeneinverständnisdaten erfassen und in Ihre gespeicherten Kundenprofile integrieren. Diese Einverständnisdaten können dann je nach Anwendungsfall bei der Frage berücksichtigt werden, ob bestimmte Profile in exportierte Zielgruppensegmente einbezogen werden.

Weiterführende Informationen finden Sie in der Übersicht zur [IAB TCF 2.0-Unterstützung in Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md).

## Nächste Schritte

Dieses Dokument beinhaltet eine kurze Einführung in die Datenschutzfunktionen von [!DNL Real-Time CDP]. Weitere Informationen zu den einzelnen Funktionen finden Sie in der in diesem Handbuch in Form von Links referenzierten Dokumentation.
