---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Übersicht über die Datenverwendung
topic: labels
translation-type: tm+mt
source-git-commit: d4964231ee957349f666eaf6b0f5729d19c408de
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# Übersicht über die Datenverwendung

Die Datenverwendung - Kennzeichnung und Durchsetzung (DULE) ist der Kernmechanismus der Datenverwaltung in der Adobe Experience Platform. Mit den Funktionen DULE können Sie Datenverwendungsbeschriftungen auf Datensätze und Felder anwenden und diese entsprechend den entsprechenden Datenverwendungsrichtlinien kategorisieren.

Dieses Dokument bietet eine Übersicht über die Datenverwendungsbeschriftungen in [!DNL Experience Platform]. Bevor Sie dieses Handbuch lesen, lesen Sie sich die Übersicht über die [Datenverwaltung](../home.md) durch, um eine solidere Einführung in das DUL-Framework zu erhalten.

## Informationen zu den Datenverwendungsbeschreibungen

Mit Datenverwendungsbeschriftungen können Sie Datensätze und Felder entsprechend den für diese Daten geltenden Nutzungsrichtlinien kategorisieren. Bezeichnungen können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Bewährte Verfahren fördern die Kennzeichnung von Daten, sobald sie in aufgenommen werden [!DNL Experience Platform]oder sobald Daten zur Verwendung in [!DNL Platform]vorliegen.

Datenverwendungsbeschriftungen, die auf Datensatzebene angewendet werden, werden auf alle Felder im Datensatz übertragen. Bezeichnungen können auch direkt auf einzelne Felder (Spaltenüberschriften) in einem Datensatz angewendet werden, ohne dass eine Weitergabe erfolgt.

Weitere Informationen zu den verfügbaren Datenverwendungsbeschriftungen in [!DNL Experience Platform] und den von ihnen dargestellten Verwendungsrichtlinien finden Sie im Handbuch zu den [unterstützten Datenverwendungsbeschriftungen](reference.md).

## Beschriftungsvererbung für Audiencen

Alle vom [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) erstellten Segmentsegmente übernehmen die Gebrauchsbeschriftungen der zugehörigen Datensätze. Dies ermöglicht Anwendungen, die auf [!DNL Experience Platform] (z. B. [!DNL Real-time Customer Data Platform]) aufbauen, eine automatische Durchsetzung der Datenverwendungsrichtlinien bei der Aktivierung von Segmenten an Ziele zu ermöglichen.

Neben der Vererbung von Bezeichnungen auf Datensatzebene übernehmen Segmente standardmäßig alle Bezeichnungen auf Feldebene aus den zugehörigen Datensätzen. Je nachdem, wie Ihre [!DNL Platform]basierte Anwendung Segmente verbraucht, können Sie potenziell angeben, welche Felder verwendet werden, wodurch verhindert wird, dass das Segment Beschriftungen aus ausgeschlossenen Feldern erbt.

Weitere Informationen zur Funktionsweise der automatischen Datendurchsetzung in Echtzeit-CDP finden Sie in der Übersicht [zur](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)Adobe Echtzeit-Datenverwaltung.

<!-- (Add after DEC mapping reference is added to AAM docs to link out to)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent labels and marketing actions recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to data usage labels in Platform, please refer to the [Audience Manager documentation](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/data-export-controls.html).
-->

## Nächste Schritte

Nachdem Sie die Bezeichnungen für die Datenverwendung eingeführt haben, können Sie das [Benutzerhandbuch](user-guide.md) lesen, um zu erfahren, wie Bezeichnungen in der [!DNL Experience Platform] Benutzeroberfläche verwaltet werden. Anweisungen zum Verwalten von Bezeichnungen mit APIs finden Sie im entsprechenden Abschnitt im Entwicklerhandbuch für den [Katalogdienst](../../catalog/api/labels.md).