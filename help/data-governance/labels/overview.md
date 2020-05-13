---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Übersicht über die Datenverwendung
topic: labels
translation-type: tm+mt
source-git-commit: 4b6b9ca5ae7861f8e8b974550be14fbce6efdcf1
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---


# Übersicht über die Datenverwendung

Die Datenbenennung und -durchsetzung (DULE) ist der Kernmechanismus der Datenverwaltung in der Adobe Experience Platform. Mit den Funktionen DULE können Sie Datenverwendungsbeschriftungen auf Datensätze und Felder anwenden und diese entsprechend den entsprechenden Datenverwendungsrichtlinien kategorisieren.

Dieses Dokument bietet einen Überblick über die Beschriftungen für die Datenverwendung (auch als DULE-Beschriftungen bezeichnet) in Experience Platform. Bevor Sie dieses Handbuch lesen, lesen Sie sich die Übersicht über die [Datenverwaltung](../home.md) durch, um eine solidere Einführung in das DUL-Framework zu erhalten.

## Informationen zu den Datenverwendungsbeschreibungen

Mit Datenverwendungsbeschriftungen können Sie Datensätze und Felder entsprechend den für diese Daten geltenden Nutzungsrichtlinien kategorisieren. Bezeichnungen können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Bewährte Verfahren fördern die Kennzeichnung von Daten, sobald diese in die Experience Platform aufgenommen werden oder sobald Daten für die Verwendung in der Plattform verfügbar sind.

Datenverwendungsbeschriftungen, die auf Datensatzebene angewendet werden, werden auf alle Felder im Datensatz übertragen. Bezeichnungen können auch direkt auf einzelne Felder (Spaltenüberschriften) in einem Datensatz angewendet werden, ohne dass eine Weitergabe erfolgt.

Weitere Informationen zu den verfügbaren Datenverwendungsbeschriftungen in Experience Platform und den Verwendungsrichtlinien, die sie darstellen, finden Sie im Handbuch zu den [unterstützten Datenverwendungsbeschriftungen](reference.md).

## Beschriftungsvererbung für Audiencen

Alle vom [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) erstellten Segmentsegmente übernehmen die Gebrauchsbeschriftungen der zugehörigen Datensätze. Auf diese Weise können auf der Experience Platform aufbauende Anwendungen (wie z. B. Echtzeit-Kundendatenplattform) eine automatische Durchsetzung der Datenverwendungsrichtlinien bei der Aktivierung von Segmenten an Ziele bereitstellen.

Neben der Vererbung von Bezeichnungen auf Datensatzebene übernehmen Segmente standardmäßig alle Bezeichnungen auf Feldebene aus den zugehörigen Datensätzen. Je nachdem, wie Ihre plattformbasierte Anwendung Segmente verbraucht, können Sie potenziell angeben, welche Felder verwendet werden, wodurch verhindert wird, dass das Segment Beschriftungen aus ausgeschlossenen Feldern erbt.

Weitere Informationen zur Funktionsweise der automatischen Datendurchsetzung in Echtzeit-CDP finden Sie in der Übersicht zur [Echtzeit-Datenverwaltung](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance).

## Nächste Schritte

Nachdem Sie die Beschriftungen für die Datenverwendung eingeführt haben, können Sie das [Benutzerhandbuch](user-guide.md) lesen, um zu erfahren, wie Sie Beschriftungen in der Benutzeroberfläche der Experience Platform verwalten. Anweisungen zum Verwalten von Bezeichnungen mit APIs finden Sie im entsprechenden Abschnitt im Entwicklerhandbuch für den [Katalogdienst](../../catalog/api/labels.md).