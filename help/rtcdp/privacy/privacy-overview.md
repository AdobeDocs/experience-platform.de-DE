---
keywords: data governance rtcdp;rtcdp data governance;real time customer data profile data governance;privacy rtcdp;rtcdp privacy
title: Datenschutz im Echtzeit-Kundendatenprofil
seo-title: Datenschutz im Echtzeit-Kundendatenprofil
description: Mit dem Echtzeit-Kundendatenprofil können Sie die Einhaltung von Datenschutzbestimmungen bei Ihren Datenvorgängen optimieren.
seo-description: Mit dem Echtzeit-Kundendatenprofil können Sie die Einhaltung von Datenschutzbestimmungen bei Ihren Datenvorgängen optimieren.
translation-type: tm+mt
source-git-commit: 1eaadb1877cc5221bf6b0b8eed042287e59155bf
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 21%

---


# Datenschutz in [!DNL Real-time CDP]

[!DNL Real-time Customer Data Platform] ([!DNL Real-time CDP]) hilft Marketingexperten, Daten aus mehreren Unternehmenssystemen zusammenzubringen, sodass sie ihre Kunden besser identifizieren, verstehen und ansprechen können. Adobe betrachtet den Schutz von Kundendaten als grundlegendes Design-Prinzip und bietet verschiedene Steuerelemente, mit denen Marketer den Datenschutz von Kunden verwalten können.

The majority of [!DNL Real-time CDP] capabilities are powered by Adobe Experience Platform. This document provides information about the various privacy enhancement technologies supported by [!DNL Real-time CDP], with links to [!DNL Experience Platform] documentation for more information.

## Kundenzugriff berücksichtigen und Anforderungen löschen

Rechtliche Datenschutzbestimmungen wie der [!DNL General Data Protection Regulation] (GDPR) und der [!DNL California Consumer Privacy Act] (CCPA) geben den Kunden das Recht, den Zugang zu den von ihnen erfassten personenbezogenen Daten oder deren Löschung zu beantragen. Da [!DNL Real-time CDP] die [!DNL Experience Platform] Funktionen zur Datenerfassung und -Datenspeicherung genutzt werden, sollten Kundenanfragen zum Zugriff auf und Löschen ihrer personenbezogenen Daten innerhalb von [!DNL Platform]verwaltet werden. See the overview on [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) for more information.

## Ausschluss-Funktionen

[!DNL Real-time CDP] ermöglicht es Kunden, ihre personenbezogenen Daten in Anwendungsfällen mit Segmentierung Opt-out. Die Abmeldeeinstellungen der Kunden werden von erfasst und gespeichert [!DNL Real-time Customer Profile]und können erzwungen werden, indem Benutzer ausgeschlossen werden, die sich mit boolescher Logik (&quot;AND NOT&quot;) in der Segmentvorhersage für ein Segment entschieden haben.

Weitere Informationen finden Sie im Dokument zur [Erfüllung von Abmeldeanfragen](../../segmentation/honoring-opt-outs.md) in der Dokumentation zum Adobe Experience Platform-Segmentdienst.

## IAB TCF 2.0-Unterstützung

[!DNL Real-time CDP] ist Teil der Liste [des registrierten](https://iabeurope.eu/vendor-list-tcf-v2-0/) Anbieters für die [!DNL Transparency & Consent Framework] (TCF), wie im [!DNL Interactive Advertising Bureau] (IAB) beschrieben. In Übereinstimmung mit den Anforderungen von TCF 2.0 [!DNL Real-time CDP] können Sie detaillierte Daten zur Kundeneinwilligung sammeln und in Ihre gespeicherten Kundendaten integrieren. Diese Daten zur Einwilligung können dann je nach Anwendungsfall in die Segmente der exportierten Audience einbezogen werden.

Weitere Informationen finden Sie in der Übersicht zur Unterstützung von [IAB TCF 2.0 in [!DNL Real-time CDP]](./iab/overview.md) .

## Nächste Schritte

This document provided a brief introduction to the privacy capabilities of [!DNL Real-time CDP]. Weitere Informationen zu den einzelnen Funktionen finden Sie in der Dokumentation zu den einzelnen Funktionen.