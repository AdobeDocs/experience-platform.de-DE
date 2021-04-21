---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Data Governance und Datenschutz – Tutorials
topic-legacy: tutorial
type: Tutorial
description: Dieses Dokument bietet einen Überblick über die verschiedenen Schulungen zu Adobe Experience Platform Data Governance und Adobe Experience Platform Privacy Service.
exl-id: c3cef447-b343-445b-a3ed-54f873f6dfb9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 41%

---

# [!DNL Data Governance] und  [!DNL Privacy] Tutorials

Mit der Adobe Experience Platform-Datenverwaltung können Sie Datenverwendungsbeschriftungen auf Datensätze und Felder anwenden, diese entsprechend den entsprechenden Datenverwendungsrichtlinien kategorisieren und bei bestimmten Aktionen für diese Datensätze und/oder Felder auf Richtlinienverletzungen hin bewerten. Bevor Sie mit den in diesem Dokument aufgelisteten Tutorials beginnen, lesen Sie bitte die [[!DNL Data Governance] overview](../data-governance/home.md) für eine stabilere Einführung in das Framework.

Adobe Experience Platform [!DNL Privacy Service] bietet eine RESTful-API und eine Benutzeroberfläche, mit der Sie Datenschutz- und Compliance-Anfragen lösungsübergreifend koordinieren können. Gehen Sie für weitere Informationen hierzu zunächst die [Übersicht über den Datenschutzdienst](../privacy-service/home.md) durch.

## Hinzufügen von Datennutzungsbeschriftungen

Mit Datennutzungsbeschriftungen können Sie Daten anhand der für diese Daten geltenden Nutzungsrichtlinien kategorisieren. Beschriftungen können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Bewährte Verfahren fördern die Kennzeichnung von Daten, sobald diese in [!DNL Experience Platform] aufgenommen werden oder sobald Daten für die Verwendung in [!DNL Platform] verfügbar sind. Datennutzungsbeschriftungen, die auf Datensatzebene angewendet werden, werden für alle Felder des Datensatzes übernommen. Außerdem können Beschriftungen direkt auf einzelne Felder (Spaltenüberschriften) in einem Datensatz angewendet werden, ohne dass eine Übernahme erfolgt. Näheres dazu, wie Sie Datennutzungsbeschriftungen auf Ihre Daten anwenden, finden Sie unter [Überblick über Datennutzungsbeschriftungen](../data-governance/labels/overview.md).

## Erstellen von Richtlinien zur Datennutzung

Mit der API [!DNL Policy Service] können Sie Datenverwendungsrichtlinien erstellen und verwalten, um festzustellen, welche Marketingaktionen für Daten mit bestimmten Beschriftungen durchgeführt werden können. Gehen Sie zum Einstieg den [Überblick über Richtlinien zur Datennutzung](../data-governance/policies/overview.md) durch.

## Durchsetzen von Richtlinien zur Datennutzung

Nachdem Sie Nutzungsbezeichnungen für Ihre Daten hinzugefügt und Richtlinien für Marketingaktionen für diese Bezeichnungen erstellt haben, können Sie mit dem [!DNL Policy Service API] bewerten, ob eine Marketingaktion eine Richtlinienverletzung darstellt, wenn sie mit einem Dataset oder einer beliebigen Gruppe von Gebrauchsbezeichnungen ausgeführt wird. Sie können dann eigene interne Protokolle einrichten, um mit Richtlinienverletzungen je nach API-Antwort umzugehen. Informationen zum Einstieg ins Thema finden Sie unter [Überblick über Richtliniendurchsetzung](../data-governance/enforcement/overview.md).

## Durchsetzen von Compliance-Vorgaben zur Datennutzung für ein Zielgruppensegment

Segmente, die für die Verwendung in [!DNL Real-time Customer Profile] aktiviert sind, enthalten eine Richtlinie-ID zum Zusammenführen innerhalb ihrer Segmentdefinition. Diese Zusammenführungsrichtlinie enthält Informationen darüber, welche Datensätze in das Segment eingeschlossen werden sollen, die wiederum alle entsprechenden Beschriftungen zur Datennutzung enthalten. Spezifische Schritte zum Einhalten der Datennutzungs-Compliance für ein Zielgruppensegment finden Sie im [Tutorial zur Datennutzungs-Compliance für Segmente](../segmentation/tutorials/governance.md).

## Erste Schritte mit [!DNL Privacy Service]

[!DNL Privacy Service] bietet eine RESTful API und eine Benutzeroberfläche, mit der Sie die personenbezogenen Daten Ihrer Betroffenen (Kunden) in allen Adobe Experience Cloud-Anwendungen verwalten können. [!DNL Privacy Service] bietet außerdem einen zentralen Audit- und Protokollierungsmechanismus, mit dem Sie auf den Status und die Ergebnisse von Aufträgen zugreifen können, die  [!DNL Experience Cloud] Anwendungen betreffen. Anweisungen zum Erstellen und Überwachen von [!DNL Privacy Service]-Aufträgen finden Sie im [Privacy Service-Entwicklerhandbuch](../privacy-service/api/getting-started.md) oder im [Privacy Service-Benutzerhandbuch](../privacy-service/ui/overview.md).
