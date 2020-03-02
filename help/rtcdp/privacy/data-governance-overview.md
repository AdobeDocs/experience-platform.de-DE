---
title: Data Governance – Übersicht
seo-title: Data Governance in der Echtzeit-Kundendatenplattform
description: 'Mit Data Governance können Sie Kundendaten verwalten und bei der Verwendung von Daten die Einhaltung von Vorschriften, Einschränkungen und Richtlinien sicherstellen. '
seo-description: 'Mit Data Governance können Sie Kundendaten verwalten und bei der Verwendung von Daten die Einhaltung von Vorschriften, Einschränkungen und Richtlinien sicherstellen. '
translation-type: ht
source-git-commit: c583d0ab89dad61e00ba117f7f2e0ec5ab427745

---


# Data Governance in der Echtzeit-Kundendatenplattform

Die Echtzeit-Kundendatenplattform führt Daten aus verschiedenen Unternehmenssystemen zusammen, damit Marketer ihre Kunden besser ermitteln, verstehen und ansprechen können. Diese Daten können Nutzungsbeschränkungen unterliegen, die von Ihrem Unternehmen oder durch gesetzliche Bestimmungen festgelegt werden. Daher muss sichergestellt sein, dass die Echtzeit-Kundendatenplattform bei der Verarbeitung Ihrer Daten mit den Nutzungsrichtlinien konform ist.

Mit Data Governance in Adobe Experience Platform können Sie Kundendaten verwalten und bei der Verwendung von Daten die Einhaltung von Vorschriften, Einschränkungen und Richtlinien sicherstellen. Data Governance spielt in der Echtzeit-Kundendatenplattform eine zentrale Rolle und erlaubt es Ihnen, Nutzungsrichtlinien zu definieren, Daten anhand dieser Richtlinien zu kategorisieren und bei Ausführung bestimmter Marketing-Aktionen auf Richtlinienverletzungen zu prüfen.

Die Echtzeit-Kundendatenplattform basiert auf Adobe Experience Platform. Daher werden die meisten Data Governance-Funktionen in der Experience Platform-Dokumentation behandelt. Dieses Dokument dient als Ergänzung zu [Data Governance – Übersicht](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html#!api-specification/markdown/narrative/technical_overview/data_governance/dule_overview.md) für Experience Platform und bietet Informationen zu den Governance-Funktionen, die in der Echtzeit-Kundendatenplattform verfügbar sind. Folgende Themen werden behandelt:

* [Nutzungsbezeichnungen auf Daten anwenden](#apply-usage-labels-to-your-data)
* [Richtlinien zur Datennutzung verwalten](#manage-data-usage-policies)
* [Einhaltung von Datennutzungsrichtlinien durchsetzen](#enforce-data-usage-compliance)

## Nutzungsbezeichnungen auf Daten anwenden

Mit Data Governance können Sie Nutzungsbezeichnungen auf Ihre Daten anwenden, entweder auf der Datensatz- oder der Datensatzfeldebene. Mit Datennutzungsbezeichnungen können Sie Daten anhand der für diese Daten geltenden Nutzungsrichtlinien kategorisieren.

Genauere Informationen zum Arbeiten mit Datennutzungsbezeichnungen finden Sie im [Benutzerhandbuch für Datennutzungsbezeichnungen](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html#!api-specification/markdown/narrative/tutorials/dule/dule_working_with_labels.md) für Adobe Experience Platform.

<!-- (To be included after destinations support is available -- January 2020)
## Set restrictions on destinations

You can set data usage restrictions on a destination by defining the marketing use cases for that destination. Defining use cases for destinations allows you to check for usage policy violations and ensure that any profiles or segments sent to that destination are compatible with Data Governance rules.

Marketing use cases can be defined during the _Setup_ phase for the _Edit Destination_ workflow. See the destination documentation for more information. 
-->


## Richtlinien zur Datennutzung verwalten

Damit Datennutzungsbezeichnungen die Datenkonformität effektiv unterstützen können, müssen Sie Datennutzungsrichtlinien definieren und aktivieren. Datennutzungsrichtlinien sind Regeln, die die Arten von Marketing-Aktionen beschreiben, die Sie für Daten in der Echtzeit-Kundendatenplattform ausführen bzw. nicht ausführen dürfen. Weiterführende Informationen dazu finden Sie im Abschnitt „Datennutzungsrichtlinien“ unter [Data Governance – Übersicht](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html#!api-specification/markdown/narrative/technical_overview/data_governance/dule_overview.md) für Experience Platform.

Adobe Experience Platform bietet verschiedene **zentrale Richtlinien** für gängige Anwendungsfälle bei Kundenerlebnissen. Diese Richtlinien können angezeigt werden, indem Sie eine Anfrage an die [DULE Policy Service-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) richten, wie im Abschnitt „Alle Richtlinien auflisten“ des [Policy Service-Entwicklerhandbuchs](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html#!api-specification/markdown/narrative/technical_overview/data_governance/dule_policy_service_developer_guide.md) dargestellt. Alternativ können Sie eigene **benutzerdefinierte Richtlinien** erstellen, um benutzerdefinierte Nutzungsbeschränkungen zu modellieren (wie im Abschnitt „Richtlinie erstellen“ des Entwicklerhandbuchs beschrieben).

## Einhaltung von Datennutzungsrichtlinien durchsetzen

Nachdem Sie Daten gekennzeichnet und Nutzungsrichtlinien definiert haben, können Sie die Einhaltung von Datennutzungsrichtlinien erzwingen. Weiterführende Informationen finden Sie im Tutorial zum [Erzwingen der Einhaltung von Datennutzungsrichtlinien für Zielgruppensegmente](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/dule/data_governance_and_segmentation.md).

## Nächste Schritte

Nach der Vorstellung der wichtigsten Data Governance-Funktionen in der Echtzeit-Kundendatenplattform und deren Aktivierung durch Experience Platform lesen Sie nun die [Data Governance-Dokumentation für Adobe Experience Platform](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html). Die Dokumentation bietet einen Überblick über wesentliche Data Governance-Konzepte sowie schrittweise Workflows zum Verwalten von Datennutzungsbezeichnungen und -richtlinien.