---
title: Datenschutz im Echtzeit-Kundendatenprofil
seo-title: Datenschutz im Echtzeit-Kundendatenprofil
description: Mit dem Echtzeit-Kundendatenprofil können Sie die Einhaltung von Datenschutzbestimmungen bei Ihren Datenvorgängen optimieren.
seo-description: Mit dem Echtzeit-Kundendatenprofil können Sie die Einhaltung von Datenschutzbestimmungen bei Ihren Datenvorgängen optimieren.
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 61%

---


# Datenschutz in der Echtzeit-Kundendatenplattform

[!DNL Real-time Customer Data Platform] (Echtzeit-CDP) hilft Marketingexperten, Daten aus mehreren Unternehmenssystemen zusammenzubringen, sodass sie ihre Kunden besser identifizieren, verstehen und ansprechen können. Adobe betrachtet den Schutz von Kundendaten als grundlegendes Design-Prinzip und bietet verschiedene Steuerelemente, mit denen Marketer den Datenschutz von Kunden verwalten können.

Die meisten Funktionen der Echtzeit-Kundendatenplattform werden über Adobe Experience Platform bereitgestellt. This document provides information about the various privacy enhancement technologies supported by Real-time CDP, with links to [!DNL Experience Platform] documentation for more information.

## [!DNL Privacy Service]

Adobe Experience Platform [!DNL Privacy Service] allows you to streamline the process of keeping your data operations compliant with privacy regulations such as the [!DNL General Data Protection Regulation] (GDPR) and the [!DNL California Consumer Privacy Act] (CCPA). Since Real-time CDP leverages [!DNL Experience Platform] capabilities for data collection and storage, the access and delete requests for GDPR and CCPA should be managed within [!DNL Platform]. Eine genauere Einführung in den Dienst finden Sie im Dokument [Privacy Service – Übersicht](../../privacy-service/home.md).

Es gibt zwei Methoden für die Übermittlung einzelner DSGVO- und CCPA-Anfragen von Datensubjekten bezüglich des Zugriffs auf und des Löschens von Kundendaten:

* Use the [!DNL Privacy Service UI](https://gdprui.cloud.adobe.io/) to create and monitor access and delete requests within a visual workspace. Eine schrittweise Anleitung dazu finden Sie im [Tutorial zur Benutzeroberfläche von Privacy Service](../../privacy-service/ui/overview.md).
* Use the [!DNL Privacy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) to manage access and delete requests with RESTful API calls. Eine schrittweise Anleitung dazu finden Sie im [Tutorial zur Privacy Service-API](../../privacy-service/api/getting-started.md).

<!-- (Capability will not be available for November GA) 
## Opt-out capabilities

Real-time CDP provides two types of consumer opt-out capabilities:

1. **General opt-out**: (Waiting on info)
1. **Segment-level opt-out of sale**: Opt-out of sale requests are captured using the Profile Privacy mixin (see the section on "Handling opt-out requests" in the [Real-time Customer Profile overview](../../profile/home.md) for more information). Using this, you can exclude users who have opted out from a segment using boolean logic ("AND NOT") in the segment predicate.
-->

## Nächste Schritte

Das vorliegende Dokument beinhaltet eine kurze Einführung in die Datenschutzfunktionen der Echtzeit-Kundendatenplattform. Ausführlichere Informationen zu Best Practices sowie zum Senden von Zugriffs- und Löschanfragen finden Sie in der [Privacy Service-Dokumentation](../../privacy-service/home.md).