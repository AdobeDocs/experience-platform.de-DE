---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Übersicht über die Durchsetzung der Richtlinien
topic: enforcement
translation-type: tm+mt
source-git-commit: 1a835c6c20c70bf03d956c601e2704b68d4f90fa
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Übersicht über die Durchsetzung der Richtlinien

Sobald Datenverwendungsbeschriftungen auf [!DNL Platform] Datensätze angewendet wurden und für Marketingaktionen mit diesen Bezeichnungen Datenverwendungsrichtlinien definiert wurden, können Sie diese Richtlinien durchsetzen und Datenoperationen verhindern, die Richtlinienverletzungen darstellen, [!DNL Data Governance] die Sie nutzen können.

Es gibt zwei Methoden zur Durchsetzung von Richtlinien, die durch [!DNL Data Governance] Funktionen bereitgestellt werden: [!DNL Platform]**API-basierte Durchsetzung** und **automatische Durchsetzung**.

## API-basierte Durchsetzung

Die [!DNL Policy Service] API bietet Endpunkte, mit denen Sie Marketingaktionen gegen Datensätze oder beliebige Kombinationen von Datenverwendungsbeschriftungen testen können, um zu prüfen, ob Richtlinienverletzungen auftreten. Basierend auf der API-Antwort können Sie dann Protokolle in Ihrer Erlebnisanwendung einrichten, um die Einhaltung der Datenverwendungsrichtlinien ordnungsgemäß durchzusetzen.

Anweisungen zum Auswerten von Richtlinien mit der API finden Sie im Lernprogramm zur [Richtliniendurchsetzung](api-enforcement.md) .

## Automatische Durchsetzung

Bestimmte Anwendungen, die auf [!DNL Experience Platform] (z. B. [!DNL Real-time Customer Data Platform]) aufbauen, bieten eine automatische Durchsetzung von Datenverwendungsrichtlinien. Jede Anwendung behält ihre eigene Methode bei, um Richtlinienverletzungen zu beheben und Schritte zur Problembehebung bereitzustellen.

Weitere Informationen zur Durchsetzung der Richtlinie zur automatischen Datenverwendung finden Sie in der Dokumentation der [!DNL Platform]verwendeten Anwendung. Informationen zur automatischen Richtliniendurchsetzung in Echtzeit-CDP finden Sie in der Übersicht zur [Echtzeit-Datenverwaltung](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance).