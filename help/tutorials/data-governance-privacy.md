---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Übungen zur Datenverwaltung und zum Datenschutz
topic: tutorial
translation-type: tm+mt
source-git-commit: ee08f43400fa72abce95ed52aff879f954f4b4d6
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---


# Übungen zur Datenverwaltung und zum Datenschutz

Die Datenbenennung und -durchsetzung (DULE) ist der Kernmechanismus der Datenverwaltung in der Adobe Experience Platform. Mit den Funktionen DULE können Sie Datenverwendungsbeschriftungen auf Datensätze und Felder anwenden und diese entsprechend den entsprechenden Datenverwendungsrichtlinien kategorisieren. Bevor Sie mit den Etiketten beginnen, lesen Sie bitte die Übersicht über die [Datenverwaltung](../data-governance/home.md) für eine solidere Einführung in das DUL-Framework innerhalb der Plattform.

Der Datenschutzdienst für Adobe Experience Platform bietet eine RESTful-API und eine Benutzeroberfläche, mit der Sie Datenschutz- und Compliance-Anfragen lösungsübergreifend koordinieren können. Um mehr zu erfahren, lesen Sie zunächst die Übersicht über den [Datenschutzdienst](../privacy-service/home.md).

## Hinzufügen

Mit Datenverwendungsbeschriftungen können Sie Datensätze und Felder entsprechend den für diese Daten geltenden Nutzungsrichtlinien kategorisieren. Bezeichnungen können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Bewährte Verfahren fördern die Kennzeichnung von Daten, sobald diese in die Experience Platform aufgenommen werden oder sobald Daten für die Verwendung in der Plattform verfügbar sind. Datenverwendungsbeschriftungen, die auf Datensatzebene angewendet werden, werden auf alle Felder im Datensatz übertragen. Bezeichnungen können auch direkt auf einzelne Felder (Spaltenüberschriften) in einem Datensatz angewendet werden, ohne dass eine Weitergabe erfolgt. Informationen zum Anwenden von Bezeichnungen zur Datenverwendung auf Ihre Daten finden Sie in der Übersicht über die [Datenverwendung](../data-governance/labels/overview.md).

## Datenverwendungsrichtlinien erstellen

Mit der DUL Policy Service API können Sie DULE-Richtlinien erstellen und verwalten, um festzustellen, welche Marketingaktionen für Daten mit bestimmten DUL-Beschriftungen durchgeführt werden können. Lesen Sie zunächst die Übersicht über die [Datenverwendungsrichtlinien](../data-governance/policies/overview.md).

## Datenverwendungsrichtlinien erzwingen

Nachdem Sie die Beschriftungen für die Datenverwendung und die Durchsetzung (DULE) für Ihre Daten erstellt und DAULE-Richtlinien für Marketingaktionen für diese Beschriftungen erstellt haben, können Sie mit der API für den DUL-Policy-Dienst bewerten, ob eine Marketingaktion, die auf einem Dataset ausgeführt wird, oder eine beliebige Gruppe von DUL-Beschriftungen eine Richtlinienverletzung darstellt. Sie können dann Ihre eigenen internen Protokolle einrichten, um Richtlinienverletzungen basierend auf der API-Antwort zu behandeln. Besuchen Sie zunächst die Übersicht über die [Richtliniendurchsetzung](../data-governance/enforcement/overview.md).

## Erzwingen der Datenverwendungskonformität für ein Audiencen-Segment

Segmente, die für die Verwendung im Echtzeit-Kundensegment aktiviert sind, enthalten eine Richtlinie-ID zum Zusammenführen innerhalb ihrer Segmentdefinition. Diese Richtlinie zum Zusammenführen enthält Informationen darüber, welche Datensätze in das Segment eingeschlossen werden sollen, die wiederum alle entsprechenden Beschriftungen zur Datenverwendung enthalten. Spezifische Schritte zum Erzwingen der Einhaltung von Datenverwendungsbedingungen für ein Segmentsegment finden Sie im [Tutorial zur Segmentkonformität](../segmentation/tutorials/governance.md).

## Erste Schritte mit dem Datenschutzdienst

Der Datenschutzdienst bietet eine RESTful-API und eine Benutzeroberfläche, mit der Sie die personenbezogenen Daten Ihrer betroffenen Personen (Kunden) in allen Adobe Experience Cloud-Anwendungen verwalten können. Der Datenschutzdienst bietet außerdem einen zentralen Prüfungs- und Protokollierungsmechanismus, mit dem Sie auf den Status und die Ergebnisse von Aufträgen zugreifen können, die Experience Cloud-Anwendungen betreffen. Anweisungen zum Erstellen und Überwachen von Aufträgen im Datenschutzdienst finden Sie im Entwicklerhandbuch [zum](../privacy-service/api/getting-started.md) Datenschutzdienst oder im Benutzerhandbuch [zum](../privacy-service/ui/overview.md)Datenschutzdienst.