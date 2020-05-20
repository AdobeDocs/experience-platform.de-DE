---
title: Datenschutz im Echtzeit-Kundendatenprofil
seo-title: Datenschutz im Echtzeit-Kundendatenprofil
description: Mit dem Echtzeit-Kundendatenprofil können Sie die Einhaltung von Datenschutzbestimmungen bei Ihren Datenvorgängen optimieren.
seo-description: Mit dem Echtzeit-Kundendatenprofil können Sie die Einhaltung von Datenschutzbestimmungen bei Ihren Datenvorgängen optimieren.
translation-type: tm+mt
source-git-commit: a1161630c8edae107b784f32ee20af225f9f8c46
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 97%

---


# Datenschutz in der Echtzeit-Kundendatenplattform

Mit der Echtzeit-Kundendatenplattform können Marketer Daten aus verschiedenen Unternehmenssystemen zusammenführen, damit sich Kunden besser ermitteln, verstehen und ansprechen lassen. Adobe betrachtet den Schutz von Kundendaten als grundlegendes Design-Prinzip und bietet verschiedene Steuerelemente, mit denen Marketer den Datenschutz von Kunden verwalten können.

Die meisten Funktionen der Echtzeit-Kundendatenplattform werden über Adobe Experience Platform bereitgestellt. Das vorliegende Dokument enthält Informationen über die verschiedenen Technologien zur Verbesserung des Datenschutzes, die von der Echtzeit-Kundendatenplattform unterstützt werden, sowie Links zur Experience Platform-Dokumentation, die weiterführende Informationen bieten.

## Privacy Service

Mit Adobe Experience Platform Privacy Service können Sie die Einhaltung von Datenschutzbestimmungen wie der Datenschutz-Grundverordnung (DSGVO) und dem California Consumer Privacy Act (CCPA) optimieren. Da die Echtzeit-Kundendatenplattform zur Datenerfassung und -speicherung Experience Platform-Funktionen nutzt, sollten Zugriffs- und Löschanfragen für DSGVO und CCPA innerhalb von Platform verwaltet werden. Eine genauere Einführung in den Dienst finden Sie im Dokument [Privacy Service – Übersicht](../../privacy-service/home.md).

Es gibt zwei Methoden für die Übermittlung einzelner DSGVO- und CCPA-Anfragen von Datensubjekten bezüglich des Zugriffs auf und des Löschens von Kundendaten:

* Verwenden Sie die [Benutzeroberfläche von Privacy Service](https://gdprui.cloud.adobe.io/), um Zugriffs- und Löschanfragen in einem visuellen Arbeitsbereich zu erstellen und zu überwachen. Eine schrittweise Anleitung dazu finden Sie im [Tutorial zur Benutzeroberfläche von Privacy Service](../../privacy-service/ui/overview.md).
* Verwenden Sie die [Privacy Service-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml), um Zugriffs- und Löschanfragen mit RESTful-API-Aufrufen zu verwalten. Eine schrittweise Anleitung dazu finden Sie im [Tutorial zur Privacy Service-API](../../privacy-service/api/getting-started.md).

<!-- (Capability will not be available for November GA) 
## Opt-out capabilities

Real-time CDP provides two types of consumer opt-out capabilities:

1. **General opt-out**: (Waiting on info)
1. **Segment-level opt-out of sale**: Opt-out of sale requests are captured using the Profile Privacy mixin (see the section on "Handling opt-out requests" in the [Real-time Customer Profile overview](../../profile/home.md) for more information). Using this, you can exclude users who have opted out from a segment using boolean logic ("AND NOT") in the segment predicate.
-->

## Nächste Schritte

Das vorliegende Dokument beinhaltet eine kurze Einführung in die Datenschutzfunktionen der Echtzeit-Kundendatenplattform. Ausführlichere Informationen zu Best Practices sowie zum Senden von Zugriffs- und Löschanfragen finden Sie in der [Privacy Service-Dokumentation](../../privacy-service/home.md).