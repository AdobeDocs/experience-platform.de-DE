---
title: Datenschutz im Echtzeit-Kundendatenprofil
seo-title: Datenschutz im Echtzeit-Kundendatenprofil
description: Mit dem Echtzeit-Kundendatenprofil können Sie die Einhaltung von Datenschutzbestimmungen bei Ihren Datenvorgängen optimieren.
seo-description: Mit dem Echtzeit-Kundendatenprofil können Sie die Einhaltung von Datenschutzbestimmungen bei Ihren Datenvorgängen optimieren.
translation-type: ht
source-git-commit: 5d3bedd97208d9eed3977a35e16a10f4864aedd9

---


# Datenschutz in der Echtzeit-Kundendatenplattform

Mit der Echtzeit-Kundendatenplattform können Marketer Daten aus verschiedenen Unternehmenssystemen zusammenführen, damit sich Kunden besser ermitteln, verstehen und ansprechen lassen. Adobe betrachtet den Schutz von Kundendaten als grundlegendes Design-Prinzip und bietet verschiedene Steuerelemente, mit denen Marketer den Datenschutz von Kunden verwalten können.

Die meisten Funktionen der Echtzeit-Kundendatenplattform werden über Adobe Experience Platform bereitgestellt. Das vorliegende Dokument enthält Informationen über die verschiedenen Technologien zur Verbesserung des Datenschutzes, die von der Echtzeit-Kundendatenplattform unterstützt werden, sowie Links zur Experience Platform-Dokumentation, die weiterführende Informationen bieten.

## Privacy Service

Mit Adobe Experience Platform Privacy Service können Sie die Einhaltung von Datenschutzbestimmungen wie der Datenschutz-Grundverordnung (DSGVO) und dem California Consumer Privacy Act (CCPA) optimieren. Da die Echtzeit-Kundendatenplattform zur Datenerfassung und -speicherung Experience Platform-Funktionen nutzt, sollten Zugriffs- und Löschanfragen für DSGVO und CCPA innerhalb von Platform verwaltet werden. Eine genauere Einführung in den Dienst finden Sie im Dokument [Privacy Service – Übersicht](https://www.adobe.io/apis/experiencecloud/gdpr/docs/alldocs.html#!api-specification/markdown/narrative/technical_overview/privacy_service_overview/privacy_service_overview.md).

Es gibt zwei Methoden für die Übermittlung einzelner DSGVO- und CCPA-Anfragen von Datensubjekten bezüglich des Zugriffs auf und des Löschens von Kundendaten:

* Verwenden Sie die [Benutzeroberfläche von Privacy Service](https://gdprui.cloud.adobe.io/), um Zugriffs- und Löschanfragen in einem visuellen Arbeitsbereich zu erstellen und zu überwachen. Eine schrittweise Anleitung dazu finden Sie im [Tutorial zur Benutzeroberfläche von Privacy Service](https://www.adobe.io/apis/experiencecloud/gdpr/docs/alldocs.html#!api-specification/markdown/narrative/tutorials/privacy_service_tutorial/privacy_service_ui_tutorial.md).
* Verwenden Sie die [Privacy Service-API](https://www.adobe.io/apis/experiencecloud/gdpr/api-reference.html), um Zugriffs- und Löschanfragen mit RESTful-API-Aufrufen zu verwalten. Eine schrittweise Anleitung dazu finden Sie im [Tutorial zur Privacy Service-API](https://www.adobe.io/apis/experiencecloud/gdpr/docs/alldocs.html#!api-specification/markdown/narrative/tutorials/privacy_service_tutorial/privacy_service_api_tutorial.md).

<!-- (Capability will not be available for November GA) 
## Opt-out capabilities

Real-time CDP provides two types of consumer opt-out capabilities:

1. **General opt-out**: (Waiting on info)
1. **Segment-level opt-out of sale**: Opt-out of sale requests are captured using the Profile Privacy mixin (see the section on "Handling opt-out requests" in the [Real-time Customer Profile overview](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md) for more information). Using this, you can exclude users who have opted out from a segment using boolean logic ("AND NOT") in the segment predicate.
-->

## Nächste Schritte

Das vorliegende Dokument beinhaltet eine kurze Einführung in die Datenschutzfunktionen der Echtzeit-Kundendatenplattform. Ausführlichere Informationen zu Best Practices sowie zum Senden von Zugriffs- und Löschanfragen finden Sie in der [Privacy Service-Dokumentation](https://www.adobe.io/apis/experiencecloud/gdpr/docs.html).