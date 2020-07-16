---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tutorials zu Data Governance und Datenschutz
topic: tutorial
translation-type: tm+mt
source-git-commit: 5c5f6c4868e195aef76bacc0a1e5df3857647bde
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 43%

---


# [!DNL Data Governance] und [!DNL Privacy] Übungen

[!DNL Data Usage Labeling and Enforcement] (DULE) ist der Kernmechanismus der Adobe Experience Platform [!DNL Data Governanc]e. Mit den Funktionen DULE können Sie Datenverwendungsbeschriftungen auf Datensätze und Felder anwenden und diese entsprechend den entsprechenden Datenverwendungsrichtlinien kategorisieren. Before getting started with labels, please see the [Data Governance overview](../data-governance/home.md) for a more robust introduction to the DULE framework within [!DNL Platform].

Adobe Experience Platform [!DNL Privacy Service] provides a RESTful API and user interface that allow you to coordinate privacy and compliance requests across various solutions. Gehen Sie für weitere Informationen hierzu zunächst die [Übersicht über den Datenschutzdienst](../privacy-service/home.md) durch.

## Hinzufügen von Datennutzungsbeschriftungen

Mit Datennutzungsbeschriftungen können Sie Daten anhand der für diese Daten geltenden Nutzungsrichtlinien kategorisieren. Beschriftungen können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Best practices encourage labeling data as soon as it is ingested into [!DNL Experience Platform], or as soon as data becomes available for use in [!DNL Platform]. Datennutzungsbeschriftungen, die auf Datensatzebene angewendet werden, werden für alle Felder des Datensatzes übernommen. Außerdem können Beschriftungen direkt auf einzelne Felder (Spaltenüberschriften) in einem Datensatz angewendet werden, ohne dass eine Übernahme erfolgt. Näheres dazu, wie Sie Datennutzungsbeschriftungen auf Ihre Daten anwenden, finden Sie unter [Überblick über Datennutzungsbeschriftungen](../data-governance/labels/overview.md).

## Erstellen von Richtlinien zur Datennutzung

The DULE [!DNL Policy Service] API allows you to create and manage DULE policies to determine what marketing actions can be taken against data that contains certain DULE labels. Gehen Sie zum Einstieg den [Überblick über Richtlinien zur Datennutzung](../data-governance/policies/overview.md) durch.

## Durchsetzen von Richtlinien zur Datennutzung

Once you have created Data Usage Labeling and Enforcement (DULE) labels for your data, and have created DULE policies for marketing actions against those labels, you can use the DULE [!DNL Policy Service] API to evaluate whether a marketing action performed on a dataset, or an arbitrary group of DULE labels, constitutes a policy violation. Indem Sie Ihre eigenen internen Protokolle einrichten, können Sie Richtlinienverletzungen dann entsprechend der API-Antwort handhaben. Informationen zum Einstieg ins Thema finden Sie unter [Überblick über Richtliniendurchsetzung](../data-governance/enforcement/overview.md).

## Durchsetzen von Compliance-Vorgaben zur Datennutzung für ein Zielgruppensegment

Segments that are enabled for use in [!DNL Real-time Customer Profile] contain a merge policy ID within their segment definition. Diese Zusammenführungsrichtlinie gibt an, welche Datensätze in das Segment aufgenommen werden, für die wiederum über ihre Beschriftungen definiert ist, wie die in ihnen enthaltenen Daten genutzt werden dürfen. Eine schrittweise Anleitung dazu, wie Sie Compliance-Vorgaben zur Datennutzung für ein Zielgruppensegment durchsetzen, finden Sie in diesem [Tutorial](../segmentation/tutorials/governance.md).

## Get started with [!DNL Privacy Service]

[!DNL Privacy Service] bietet eine RESTful-API und eine Benutzeroberfläche, mit der Sie die persönlichen Daten Ihrer Betroffenen (Kunden) in allen Adobe Experience Cloud-Anwendungen verwalten können. [!DNL Privacy Service] bietet außerdem einen zentralen Audit- und Protokollierungsmechanismus, mit dem Sie auf den Status und die Ergebnisse von Aufträgen zugreifen können, an denen [!DNL Experience Cloud] Anwendungen beteiligt sind. For instructions showing how to create and monitor [!DNL Privacy Service] jobs, follow the steps provided in the [Privacy Service developer guide](../privacy-service/api/getting-started.md) or the [Privacy Service user guide](../privacy-service/ui/overview.md).