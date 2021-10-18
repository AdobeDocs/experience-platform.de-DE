---
keywords: Data Governance rtcdp;rtcdp Data Governance;Echtzeit-Data Profil Data Governance;Datenschutz rtcdp;rtcdp privacy
title: Datenschutz in Real-time Customer Data Platform
seo-title: Privacy in Real-time Customer Data Platform
description: Mit Real-time Customer Data Platform können Sie die Einhaltung von Datenschutzbestimmungen bei Ihren Datenvorgängen optimieren.
seo-description: Real-time Customer Data Platform allows you to streamline the process of keeping your data operations compliant with privacy regulations.
exl-id: bcb0e42e-4549-4952-bb69-5534aee353f8
source-git-commit: f193787ac27e30c69d25418656ae9c59c89622dc
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 7%

---

# Datenschutz in Real-time Customer Data Platform

[!DNL Real-time Customer Data Platform] ([!DNL Real-time CDP]) hilft Marketing-Experten, Daten aus verschiedenen Unternehmenssystemen zusammenzuführen, sodass sie ihre Kunden besser identifizieren, verstehen und ansprechen können. Adobe betrachtet den Schutz von Kundendaten als grundlegendes Design-Prinzip und bietet verschiedene Steuerelemente, mit denen Marketer den Datenschutz von Kunden verwalten können.

Die meisten Funktionen von [!DNL Real-time CDP] werden von Adobe Experience Platform unterstützt. Dieses Dokument enthält Informationen zu den verschiedenen Technologien zur Verbesserung des Datenschutzes, die von [!DNL Real-time CDP] unterstützt werden, sowie Links zur [!DNL Experience Platform]-Dokumentation für weitere Informationen.

## Berücksichtigung von Zugriffs- und Löschanfragen von Kunden

Durch gesetzliche Datenschutzbestimmungen wie die [!DNL General Data Protection Regulation] (DSGVO) und die [!DNL California Consumer Privacy Act] (CCPA) erhalten Kunden das Recht, Zugang zu den von Ihnen erfassten personenbezogenen Daten oder deren Löschung anzufordern. Da [!DNL Real-time CDP] die [!DNL Experience Platform]-Funktionen für die Datenerfassung und -speicherung nutzt, sollten Kundenanfragen zum Zugriff auf und Löschen ihrer personenbezogenen Daten innerhalb von [!DNL Platform] verwaltet werden. Weitere Informationen finden Sie in der Übersicht zu [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) .

## Opt-out-Funktionen

[!DNL Real-time CDP] ermöglicht es Kunden, die Aufnahme ihrer personenbezogenen Daten in Segmentierungsanwendungsfälle abzuwählen. Die Opt-out-Voreinstellungen von Kunden werden von [!DNL Real-time Customer Profile] erfasst und gespeichert und können erzwungen werden, indem Benutzer ausgeschlossen werden, die sich mit boolescher Logik (&quot;AND NOT&quot;) im Segmentprädikat von einem Segment abgemeldet haben.

Weitere Informationen finden Sie im Dokument [Berücksichtigung von Opt-out-Anfragen](../../segmentation/consents.md) in der Dokumentation zum Adobe Experience Platform Segmentation Service .

## IAB TCF 2.0-Unterstützung

[!DNL Real-time CDP] basiert auf Adobe Experience Platform, das Teil der registrierten  [Anbieterliste ](https://iabeurope.eu/vendor-list-tcf-v2-0/) für die ist,  [!DNL Transparency & Consent Framework (TCF)]wie im  [!DNL Interactive Advertising Bureau (IAB)]beschrieben. In Übereinstimmung mit den TCF 2.0-Anforderungen können Sie mit Platform detaillierte Kundenzustimmungsdaten erfassen und in Ihre gespeicherten Kundenprofile integrieren. Diese Einwilligungsdaten können dann je nach Anwendungsfall in exportierte Zielgruppensegmente einbezogen werden.

Weitere Informationen finden Sie in der Übersicht über die [IAB TCF 2.0-Unterstützung in Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md) .

## Nächste Schritte

Dieses Dokument bietet eine kurze Einführung in die Datenschutzfunktionen von [!DNL Real-time CDP]. Weitere Informationen zu den einzelnen Funktionen finden Sie in der Dokumentation zu den einzelnen Funktionen in diesem Handbuch.
