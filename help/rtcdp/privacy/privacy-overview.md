---
title: Datenschutz in Echtzeit-Kundendatenprofil
seo-title: Datenschutz in Echtzeit-Kundendatenprofil
description: Mit dem Echtzeit-Kundendatenprofil können Sie den Prozess der Einhaltung der Datenschutzbestimmungen durch Ihre Datenvorgänge optimieren.
seo-description: Mit dem Echtzeit-Kundendatenprofil können Sie den Prozess der Einhaltung der Datenschutzbestimmungen durch Ihre Datenvorgänge optimieren.
translation-type: tm+mt
source-git-commit: 5d3bedd97208d9eed3977a35e16a10f4864aedd9

---


# Datenschutz in Echtzeit-CDP

Die Echtzeit-Kundendatenplattform (Echtzeit-CDP) hilft Marketingexperten, Daten aus mehreren Unternehmenssystemen zusammenzubringen, sodass sie ihre Kunden besser identifizieren, verstehen und ansprechen können. Adobe hält den Datenschutz von Verbraucherdaten als grundlegenden Designgrundsatz und bietet verschiedene Steuerelemente, mit denen Marketingexperten die Datenschutzdaten ihrer Kunden verwalten können.

Die meisten CDP-Funktionen in Echtzeit werden über Adobe Experience Platform bereitgestellt. Dieses Dokument enthält Informationen zu den verschiedenen Technologien zur Verbesserung des Datenschutzes, die von CDP in Echtzeit unterstützt werden, sowie Links zur Experience Platform-Dokumentation.

## Datenschutzdienst

Mit dem Adobe Experience Platform Privacy Service können Sie den Prozess der Einhaltung von Datenschutzbestimmungen wie der Allgemeinen Datenschutzverordnung (GDPR) und dem California Consumer Privacy Act (CCPA) optimieren. Da CDP in Echtzeit Experience Platform-Funktionen für die Datenerfassung und -speicherung nutzt, sollten die Zugriffs- und Löschanforderungen für GDPR und CCPA innerhalb der Plattform verwaltet werden. Eine detailliertere Einführung des Dienstes finden Sie im Übersichtsdokument zum [Datenschutzdienst](https://www.adobe.io/apis/experiencecloud/gdpr/docs/alldocs.html#!api-specification/markdown/narrative/technical_overview/privacy_service_overview/privacy_service_overview.md) .

Es gibt zwei Methoden zum Übermitteln einzelner GDPR- und CCPA-Datenanforderungen für den Zugriff auf und das Löschen von Kundendaten:

* Verwenden Sie die Benutzeroberfläche[ des ](https://gdprui.cloud.adobe.io/)Datenschutzdienstes, um Anforderungen in einem visuellen Arbeitsbereich zu erstellen und zu überwachen und zu löschen. Eine schrittweise Anleitung finden Sie im Tutorial[ zur Benutzeroberfläche des ](https://www.adobe.io/apis/experiencecloud/gdpr/docs/alldocs.html#!api-specification/markdown/narrative/tutorials/privacy_service_tutorial/privacy_service_ui_tutorial.md)Datenschutzdienstes.
* Verwenden Sie die [Datenschutzdienst-API](https://www.adobe.io/apis/experiencecloud/gdpr/api-reference.html) , um Zugriff zu verwalten und Anforderungen mit RESTful-API-Aufrufen zu löschen. Eine schrittweise Anleitung finden Sie im Tutorial[ zur API des ](https://www.adobe.io/apis/experiencecloud/gdpr/docs/alldocs.html#!api-specification/markdown/narrative/tutorials/privacy_service_tutorial/privacy_service_api_tutorial.md)Datenschutzdienstes.

<!-- (Capability will not be available for November GA) 
## Opt-out capabilities

Real-time CDP provides two types of consumer opt-out capabilities:

1. **General opt-out**: (Waiting on info)
1. **Segment-level opt-out of sale**: Opt-out of sale requests are captured using the Profile Privacy mixin (see the section on "Handling opt-out requests" in the [Real-time Customer Profile overview](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md) for more information). Using this, you can exclude users who have opted out from a segment using boolean logic ("AND NOT") in the segment predicate.
-->

## Nächste Schritte

Dieses Dokument enthält eine kurze Einführung in die Datenschutzfunktionen von Echtzeit-CDP. Ausführlichere Informationen zu Best Practices und Schritten zum Senden von Zugriffs-/Löschanfragen finden Sie in der Dokumentation zum [Datenschutzdienst](https://www.adobe.io/apis/experiencecloud/gdpr/docs.html).