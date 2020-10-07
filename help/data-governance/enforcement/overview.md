---
keywords: Experience Platform;home;popular topics;Policy enforcement;Automatic enforcement;API-based enforcement;data governance
solution: Experience Platform
title: Übersicht über die Durchsetzung von Richtlinien
topic: enforcement
description: Sobald Datenverwendungsbeschriftungen auf Adobe Experience Platform-Datensätze angewendet wurden und für Marketingaktionen mit diesen Bezeichnungen Richtlinien zur Datenverwendung definiert wurden, können Sie diese Richtlinien mithilfe der Datenverwaltungsfunktionen durchsetzen und Datenvorgänge verhindern, die Richtlinienverletzungen darstellen. Es gibt zwei Methoden zur Durchsetzung von Richtlinien, die durch die Datenverwaltungsfunktionen auf Plattform, API-basierte Durchsetzung und automatische Durchsetzung bereitgestellt werden.
translation-type: tm+mt
source-git-commit: 28b733a16b067f951a885c299d59e079f0074df8
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 16%

---


# Übersicht über die Durchsetzung von Richtlinien

Once data usage labels have been applied to [!DNL Platform] datasets, and data usage policies have been defined for marketing actions against those labels, [!DNL Data Governance] capabilities allow you to enforce those policies and prevent data operations that constitute policy violations.

Es gibt zwei Methoden zur Durchsetzung von Richtlinien, die durch [!DNL Data Governance] Funktionen bereitgestellt werden: [!DNL Platform]API-basierte Durchsetzung und automatische Durchsetzung.

## API-basierte Durchsetzung

The [!DNL Policy Service] API provides endpoints that allow you to test marketing actions against datasets or arbitrary combinations of data usage labels in order to check if any policy violations occur. Je nach API-Antwort können Sie dann Protokolle in Ihrer Erlebnisanwendung einrichten, um die Einhaltung von Datennutzungsrichtlinien richtig durchzusetzen.

Anweisungen zum Auswerten von Richtlinien mit der API finden Sie im Tutorial zur [Richtliniendurchsetzung](api-enforcement.md).

## Automatische Durchsetzung

Bestimmte Anwendungen, die auf [!DNL Experience Platform] (z. B. [!DNL Real-time Customer Data Platform]) aufbauen, bieten eine automatische Durchsetzung von Datenverwendungsrichtlinien. Jede Anwendung behält ihre eigene Methode bei, um Richtlinienverletzungen zu beheben und Schritte zur Problembehebung bereitzustellen.

Weitere Informationen zur Durchsetzung der Richtlinie zur automatischen Datenverwendung finden Sie in der Dokumentation der [!DNL Platform]verwendeten Anwendung. Informationen zur automatischen Richtliniendurchsetzung in Echtzeit-CDP finden Sie in der Übersicht zur [Echtzeit-Datenverwaltung](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance).