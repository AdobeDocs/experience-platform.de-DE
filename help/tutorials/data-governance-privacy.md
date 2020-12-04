---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Data Governance und Datenschutz – Tutorials
topic: tutorial
type: Tutorial
description: Dieses Dokument bietet einen Überblick über die verschiedenen Schulungen zu Adobe Experience Platform Data Governance und Adobe Experience Platform Privacy Service.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 41%

---


# [!DNL Data Governance] und [!DNL Privacy] Tutorials

Mit der Adobe Experience Platform-Datenverwaltung können Sie Datenverwendungsbeschriftungen auf Datensätze und Felder anwenden, diese entsprechend den entsprechenden Datenverwendungsrichtlinien kategorisieren und bei bestimmten Aktionen für diese Datensätze und/oder Felder auf Richtlinienverletzungen hin bewerten. Bevor Sie mit den in diesem Dokument aufgelisteten Tutorials beginnen, finden Sie in der [[!DNL Data Governance] Übersicht](../data-governance/home.md) eine solidere Einführung in das Framework.

Adobe Experience Platform [!DNL Privacy Service] provides a RESTful API and user interface that allow you to coordinate privacy and compliance requests across various solutions. Gehen Sie für weitere Informationen hierzu zunächst die [Übersicht über den Datenschutzdienst](../privacy-service/home.md) durch.

## Hinzufügen von Datennutzungsbeschriftungen

Mit Datennutzungsbeschriftungen können Sie Daten anhand der für diese Daten geltenden Nutzungsrichtlinien kategorisieren. Beschriftungen können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Best practices encourage labeling data as soon as it is ingested into [!DNL Experience Platform], or as soon as data becomes available for use in [!DNL Platform]. Datennutzungsbeschriftungen, die auf Datensatzebene angewendet werden, werden für alle Felder des Datensatzes übernommen. Außerdem können Beschriftungen direkt auf einzelne Felder (Spaltenüberschriften) in einem Datensatz angewendet werden, ohne dass eine Übernahme erfolgt. Näheres dazu, wie Sie Datennutzungsbeschriftungen auf Ihre Daten anwenden, finden Sie unter [Überblick über Datennutzungsbeschriftungen](../data-governance/labels/overview.md).

## Erstellen von Richtlinien zur Datennutzung

The [!DNL Policy Service] API allows you to create and manage data usage policies to determine what marketing actions can be taken against data that contains certain usage labels. Gehen Sie zum Einstieg den [Überblick über Richtlinien zur Datennutzung](../data-governance/policies/overview.md) durch.

## Durchsetzen von Richtlinien zur Datennutzung

Nachdem Sie Nutzungsbezeichnungen für Ihre Daten hinzugefügt und Richtlinien für Marketingaktionen für diese Bezeichnungen erstellt haben, können Sie mit der [!DNL Policy Service API] bewerten, ob eine Marketingaktion eine Richtlinienverletzung darstellt, wenn sie mit einem Datensatz oder einer beliebigen Gruppe von Gebrauchsbezeichnungen ausgeführt wird. Sie können dann eigene interne Protokolle einrichten, um mit Richtlinienverletzungen je nach API-Antwort umzugehen. Informationen zum Einstieg ins Thema finden Sie unter [Überblick über Richtliniendurchsetzung](../data-governance/enforcement/overview.md).

## Durchsetzen von Compliance-Vorgaben zur Datennutzung für ein Zielgruppensegment

Segments that are enabled for use in [!DNL Real-time Customer Profile] contain a merge policy ID within their segment definition. Diese Zusammenführungsrichtlinie enthält Informationen darüber, welche Datensätze in das Segment eingeschlossen werden sollen, die wiederum alle entsprechenden Beschriftungen zur Datennutzung enthalten. Spezifische Schritte zum Einhalten der Datennutzungs-Compliance für ein Zielgruppensegment finden Sie im [Tutorial zur Datennutzungs-Compliance für Segmente](../segmentation/tutorials/governance.md).

## Erste Schritte mit [!DNL Privacy Service]

[!DNL Privacy Service] bietet eine RESTful API und eine Benutzeroberfläche, mit der Sie die personenbezogenen Daten Ihrer Betroffenen (Kunden) in allen Adobe Experience Cloud-Anwendungen verwalten können. [!DNL Privacy Service] bietet außerdem einen zentralen Audit- und Protokollierungsmechanismus, mit dem Sie auf den Status und die Ergebnisse von Aufträgen zugreifen können, an denen [!DNL Experience Cloud] Anwendungen beteiligt sind. For instructions showing how to create and monitor [!DNL Privacy Service] jobs, follow the steps provided in the [Privacy Service developer guide](../privacy-service/api/getting-started.md) or the [Privacy Service user guide](../privacy-service/ui/overview.md).