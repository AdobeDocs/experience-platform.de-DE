---
keywords: Datenverwaltung rtcdp;rtcdp Datenverwaltung;Datenverwaltung in Echtzeit für Kundendaten-Profil;Datenschutz rtcdp;rtcdp Privatsphäre
title: Datenschutz im Echtzeit-Kundendatenprofil
seo-title: Datenschutz im Echtzeit-Kundendatenprofil
description: Mit dem Echtzeit-Kundendatenprofil können Sie die Einhaltung von Datenschutzbestimmungen bei Ihren Datenvorgängen optimieren.
seo-description: Mit dem Echtzeit-Kundendatenprofil können Sie die Einhaltung von Datenschutzbestimmungen bei Ihren Datenvorgängen optimieren.
translation-type: tm+mt
source-git-commit: 49c984a60fd699706eec508ec1d786340df40b57
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 19%

---


# Datenschutz in [!DNL Real-time CDP]

[!DNL Real-time Customer Data Platform] ([!DNL Real-time CDP]) hilft Marketingexperten, Daten aus mehreren Unternehmenssystemen zusammenzubringen, sodass sie ihre Kunden besser identifizieren, verstehen und ansprechen können. Adobe betrachtet den Schutz von Kundendaten als grundlegendes Design-Prinzip und bietet verschiedene Steuerelemente, mit denen Marketer den Datenschutz von Kunden verwalten können.

Die meisten [!DNL Real-time CDP] Funktionen werden von Adobe Experience Platform betrieben. Dieses Dokument enthält Informationen zu den verschiedenen Technologien zur Datenschutzverbesserung, die von [!DNL Real-time CDP] unterstützt werden, sowie Links zur [!DNL Experience Platform]-Dokumentation.

## Kundenzugriff berücksichtigen und Anforderungen löschen

Rechtliche Datenschutzbestimmungen wie die [!DNL General Data Protection Regulation] (GDPR) und die [!DNL California Consumer Privacy Act] (CCPA) geben Kunden das Recht, den Zugriff auf oder die Löschung der von ihnen erfassten personenbezogenen Daten anzufordern. Da [!DNL Real-time CDP] die Funktionen [!DNL Experience Platform] für die Datenerfassung und Datenspeicherung nutzt, sollten Kundenanforderungen zum Zugriff und Löschen ihrer personenbezogenen Daten innerhalb von [!DNL Platform] verwaltet werden. Weitere Informationen finden Sie unter [Adobe Experience Platform Privacy Service](../../privacy-service/home.md).

## Ausschluss-Funktionen

[!DNL Real-time CDP] ermöglicht es Kunden, ihre personenbezogenen Daten in Anwendungsfällen mit Segmentierung Opt-out. Die Ausschluss-Voreinstellungen der Kunden werden von [!DNL Real-time Customer Profile] erfasst und gespeichert. Sie können erzwungen werden, indem Benutzer ausgeschlossen werden, die sich mit boolescher Logik (&quot;AND NOT&quot;) in der Segmentvorhersage für ein Segment entschieden haben.

Weitere Informationen finden Sie im Dokument zu [Ausstiegsanfragen](../../segmentation/honoring-opt-outs.md) in der Dokumentation zum Adobe Experience Platform-Segmentdienst.

## IAB TCF 2.0-Unterstützung

[!DNL Real-time CDP] basiert auf Adobe Experience Platform, das Teil der  [Händlerliste ](https://iabeurope.eu/vendor-list-tcf-v2-0/) für die  [!DNL Transparency & Consent Framework (TCF)]ist, wie in der  [!DNL Interactive Advertising Bureau (IAB)]. In Übereinstimmung mit den Anforderungen von TCF 2.0 können Sie mit Platform detaillierte Daten zur Kundeneinwilligung sammeln und diese in Ihre gespeicherten Profil integrieren. Diese Daten zur Einwilligung können dann je nach Anwendungsfall in die Segmente der exportierten Audience einbezogen werden.

Weitere Informationen finden Sie unter [IAB TCF 2.0-Unterstützung in Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md).

## Nächste Schritte

In diesem Dokument erhalten Sie eine kurze Einführung in die Datenschutzfunktionen von [!DNL Real-time CDP]. Weitere Informationen zu den einzelnen Funktionen finden Sie in der Dokumentation zu den einzelnen Funktionen.