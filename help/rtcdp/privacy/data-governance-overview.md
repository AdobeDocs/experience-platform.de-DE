---
title: Überblick über die Datenverwaltung
seo-title: Datenverwaltung in Echtzeit-Plattform für Kundendaten
description: 'Mit der Datenverwaltung können Sie Kundendaten verwalten und die Einhaltung von Vorschriften, Einschränkungen und Richtlinien für die Datenverwendung sicherstellen. '
seo-description: 'Mit der Datenverwaltung können Sie Kundendaten verwalten und die Einhaltung von Vorschriften, Einschränkungen und Richtlinien für die Datenverwendung sicherstellen. '
translation-type: tm+mt
source-git-commit: c583d0ab89dad61e00ba117f7f2e0ec5ab427745

---


# Datenverwaltung in Echtzeit-CDP

Die Echtzeit-Customer Data Platform (Echtzeit-CDP) bringt Daten aus mehreren Unternehmenssystemen zusammen, sodass Marketingexperten ihre Kunden besser identifizieren, verstehen und ansprechen können. Diese Daten unterliegen ggf. Nutzungsbeschränkungen, die von Ihrer Organisation oder durch gesetzliche Bestimmungen festgelegt werden. Daher ist es wichtig sicherzustellen, dass CDP in Echtzeit bei der Verarbeitung Ihrer Daten mit den Nutzungsrichtlinien konform ist.

Mit Adobe Experience Platform Data Governance können Sie Kundendaten verwalten und die Einhaltung von Vorschriften, Einschränkungen und Richtlinien für die Datenverwendung sicherstellen. Es spielt eine Schlüsselrolle in CDP in Echtzeit, da Sie Nutzungsrichtlinien definieren, Ihre Daten auf der Grundlage dieser Richtlinien kategorisieren und bei bestimmten Marketingaktionen auf Richtlinienverletzungen prüfen können.

Die Echtzeit-CDP basiert auf der Adobe Experience Platform. Daher werden die meisten Funktionen zur Datenverwaltung in der Experience Platform-Dokumentation behandelt. Dieses Dokument soll die Übersicht[ zur ](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html#!api-specification/markdown/narrative/technical_overview/data_governance/dule_overview.md)Datenverwaltung für Experience Platform ergänzen und die Governance-Funktionen in Echtzeit-CDP umreißen. Folgende Themen werden behandelt:

* [Anwenden von Nutzungsbeschriftungen auf Ihre Daten](#apply-usage-labels-to-your-data)
* [Richtlinien zur Datenverwendung verwalten](#manage-data-usage-policies)
* [Erzwingen der Datenauslastung](#enforce-data-usage-compliance)

## Anwenden von Nutzungsbeschriftungen auf Ihre Daten

Mit der Datenverwaltung können Sie Nutzungsbezeichnungen auf Ihre Daten anwenden, entweder auf der Ebene des Datensatzes oder auf der Ebene des Datensatzes. Mit Datenverwendungsbeschriftungen können Sie Daten entsprechend den für diese Daten geltenden Nutzungsrichtlinien kategorisieren.

Detaillierte Informationen zum Arbeiten mit Datenverwendungsbeschriftungen finden Sie im Benutzerhandbuch[ für die ](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html#!api-specification/markdown/narrative/tutorials/dule/dule_working_with_labels.md)Datenverwendungsbeschriftung für Adobe Experience Platform.

<!-- (To be included after destinations support is available -- January 2020)
## Set restrictions on destinations

You can set data usage restrictions on a destination by defining the marketing use cases for that destination. Defining use cases for destinations allows you to check for usage policy violations and ensure that any profiles or segments sent to that destination are compatible with Data Governance rules.

Marketing use cases can be defined during the _Setup_ phase for the _Edit Destination_ workflow. See the destination documentation for more information. 
-->


## Richtlinien zur Datenverwendung verwalten

Damit Datenverwendungsbeschriftungen die Datenkonformität effektiv unterstützen können, müssen Datenverwendungsrichtlinien definiert und aktiviert werden. Datenverwendungsrichtlinien sind Regeln, die die Arten von Marketingaktionen beschreiben, die Sie für Daten innerhalb von Echtzeit-CDP ausführen dürfen oder von denen Sie eingeschränkt sind. Weitere Informationen finden Sie im Abschnitt &quot;Datenverwendungsrichtlinien&quot;im Überblick über die [Datenverwaltung](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html#!api-specification/markdown/narrative/technical_overview/data_governance/dule_overview.md) der Experience Platform.

Adobe Experience Platform bietet mehrere **Kernrichtlinien** für gängige Anwendungsfälle für Kundenerlebnisse. Diese Richtlinien können angezeigt werden, indem Sie eine Anforderung an die [DLE Policy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)richten, wie im Abschnitt &quot;Alle Richtlinien auflisten&quot;im Entwicklerhandbuch für [Policy Service](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html#!api-specification/markdown/narrative/technical_overview/data_governance/dule_policy_service_developer_guide.md)dargestellt. Sie können auch eigene **benutzerdefinierte Richtlinien** erstellen, um benutzerdefinierte Verwendungsbeschränkungen zu modellieren, wie im Abschnitt &quot;Eine Richtlinie erstellen&quot;im Entwicklerhandbuch dargestellt.

## Erzwingen der Datenauslastung

Sobald Daten beschriftet und Nutzungsrichtlinien definiert sind, können Sie die Einhaltung von Richtlinien durch die Datennutzung erzwingen. Weitere Informationen finden Sie im Tutorial zur [Erzwingung der Einhaltung von Datenverwendungsbestimmungen für Zielgruppensegmente](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/dule/data_governance_and_segmentation.md) .

## Nächste Schritte

Nachdem Sie die wichtigsten Data Governance-Funktionen in Echtzeit-CDP und deren Aktivierung durch Experience Platform eingeführt haben, lesen Sie bitte die [Dokumentation zur Datenverwaltung auf der Adobe Experience Platform](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html). Die Dokumentation bietet einen Überblick über die wesentlichen Konzepte der Datenverwaltung sowie schrittweise Arbeitsabläufe zur Verwaltung von Datenverwendungsbeschriftungen und -richtlinien.