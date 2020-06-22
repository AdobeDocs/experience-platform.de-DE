---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Übersicht über die Datenverwendung
topic: labels
translation-type: tm+mt
source-git-commit: e3c69589e0d4f8224b74a663b23f67e6731ddec4
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---


# Übersicht über die Datenverwendung

Die Datenverwendung - Kennzeichnung und Durchsetzung (DULE) ist der Kernmechanismus der Datenverwaltung in der Adobe Experience Platform. Mit den Funktionen DULE können Sie Datenverwendungsbeschriftungen auf Datensätze und Felder anwenden und diese entsprechend den entsprechenden Datenverwendungsrichtlinien kategorisieren.

Dieses Dokument bietet einen Überblick über die Beschriftungen für die Datenverwendung (auch als DULE-Beschriftungen bezeichnet) in der Experience Platform. Bevor Sie dieses Handbuch lesen, lesen Sie sich die Übersicht über die [Datenverwaltung](../home.md) durch, um eine solidere Einführung in das DUL-Framework zu erhalten.

## Informationen zu den Datenverwendungsbeschreibungen

Mit Datenverwendungsbeschriftungen können Sie Datensätze und Felder entsprechend den für diese Daten geltenden Nutzungsrichtlinien kategorisieren. Bezeichnungen können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Bewährte Verfahren fördern die Kennzeichnung von Daten, sobald diese in die Experience Platform aufgenommen werden oder sobald Daten für die Verwendung in der Platform verfügbar sind.

Datenverwendungsbeschriftungen, die auf Datensatzebene angewendet werden, werden auf alle Felder im Datensatz übertragen. Bezeichnungen können auch direkt auf einzelne Felder (Spaltenüberschriften) in einem Datensatz angewendet werden, ohne dass eine Weitergabe erfolgt.

Weitere Informationen zu den verfügbaren Datenverwendungsbeschriftungen in der Experience Platform und den von ihnen dargestellten Verwendungsrichtlinien finden Sie im Handbuch zu den [unterstützten Datenverwendungsbeschriftungen](reference.md).

## Beschriftungsvererbung für Audiencen

Alle vom [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) erstellten Segmentsegmente übernehmen die Gebrauchsbeschriftungen der zugehörigen Datensätze. Auf diese Weise können auf Experience Platform aufbauende Anwendungen (wie z. B. die Echtzeit-Platform von Kundendaten) eine automatische Durchsetzung der Datenverwendungsrichtlinien beim Aktivieren von Segmenten in Ziele bereitstellen.

Neben der Vererbung von Bezeichnungen auf Datensatzebene übernehmen Segmente standardmäßig alle Bezeichnungen auf Feldebene aus den zugehörigen Datensätzen. Je nachdem, wie Ihre Platform-basierte Anwendung Segmente verbraucht, können Sie potenziell angeben, welche Felder verwendet werden, wodurch verhindert wird, dass das Segment Beschriftungen von ausgeschlossenen Feldern übernimmt.

Weitere Informationen zur Funktionsweise der automatischen Datendurchsetzung in Echtzeit-CDP finden Sie in der Übersicht zur [Echtzeit-Datenverwaltung](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance).

<!-- (Add after DEC mapping reference is added to AAM docs to link out to)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent labels and marketing actions recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to data usage labels in Platform, please refer to the [Audience Manager documentation](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/data-export-controls.html).
-->

## Nächste Schritte

Nachdem Sie die Bezeichnungen für die Datenverwendung eingeführt haben, können Sie das [Benutzerhandbuch](user-guide.md) lesen, um zu erfahren, wie Bezeichnungen in der Benutzeroberfläche der Experience Platform verwaltet werden. Anweisungen zum Verwalten von Bezeichnungen mit APIs finden Sie im entsprechenden Abschnitt im Entwicklerhandbuch für den [Katalogdienst](../../catalog/api/labels.md).