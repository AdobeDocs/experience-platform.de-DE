---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Übersicht über die Durchsetzung von Richtlinien
topic: enforcement
translation-type: tm+mt
source-git-commit: 1a835c6c20c70bf03d956c601e2704b68d4f90fa
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 21%

---


# Übersicht über die Durchsetzung von Richtlinien

Once data usage labels have been applied to [!DNL Platform] datasets, and data usage policies have been defined for marketing actions against those labels, [!DNL Data Governance] capabilities allow you to enforce those policies and prevent data operations that constitute policy violations.

Es gibt zwei Methoden zur Durchsetzung von Richtlinien, die durch [!DNL Data Governance] Funktionen bereitgestellt werden: [!DNL Platform]**API-basierte Durchsetzung** und **automatische Durchsetzung**.

## API-basierte Durchsetzung

The [!DNL Policy Service] API provides endpoints that allow you to test marketing actions against datasets or arbitrary combinations of data usage labels in order to check if any policy violations occur. Je nach API-Antwort können Sie dann Protokolle in Ihrer Erlebnisanwendung einrichten, um die Einhaltung von Datennutzungsrichtlinien richtig durchzusetzen.

Anweisungen zum Auswerten von Richtlinien mit der API finden Sie im Tutorial zur [Richtliniendurchsetzung](api-enforcement.md).

## Automatische Durchsetzung

Bestimmte Anwendungen, die auf [!DNL Experience Platform] (z. B. [!DNL Real-time Customer Data Platform]) aufbauen, bieten eine automatische Durchsetzung von Datenverwendungsrichtlinien. Jede Anwendung behält ihre eigene Methode bei, um Richtlinienverletzungen zu beheben und Schritte zur Problembehebung bereitzustellen.

Weitere Informationen zur Durchsetzung der Richtlinie zur automatischen Datenverwendung finden Sie in der Dokumentation der [!DNL Platform]verwendeten Anwendung. Informationen zur automatischen Richtliniendurchsetzung in Echtzeit-CDP finden Sie in der Übersicht zur [Echtzeit-Datenverwaltung](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance).