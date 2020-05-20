---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Übersicht über die Durchsetzung der Richtlinien
topic: enforcement
translation-type: tm+mt
source-git-commit: d1659bbdd40cf1e598713f1fe1a6eeae8e8249cc
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# Übersicht über die Durchsetzung der Richtlinien

Sobald Datenverwendungsbeschriftungen auf Plattformdatasets angewendet wurden und für Marketingaktionen mit diesen Bezeichnungen Datenverwendungsrichtlinien definiert wurden, können Sie diese Richtlinien mithilfe der Datenverwaltungsfunktionen durchsetzen und Datenvorgänge verhindern, die Richtlinienverletzungen darstellen.

Es gibt zwei Methoden zur Durchsetzung von Richtlinien, die durch Data Governance-Funktionen auf der Plattform bereitgestellt werden: **API-basierte Durchsetzung** und **automatische Durchsetzung**.

## API-basierte Durchsetzung

Die Policy-Service-API bietet Endpunkte, mit denen Sie Marketingaktionen gegen Datensätze oder beliebige Kombinationen von Datenverwendungsbeschriftungen testen können, um festzustellen, ob Richtlinienverletzungen auftreten. Basierend auf der API-Antwort können Sie dann Protokolle in Ihrer Erlebnisanwendung einrichten, um die Einhaltung der Datenverwendungsrichtlinien ordnungsgemäß durchzusetzen.

Anweisungen zum Auswerten von Richtlinien mit der API finden Sie im Lernprogramm zur [Richtliniendurchsetzung](api-enforcement.md) .

## Automatische Durchsetzung

Bestimmte Anwendungen, die auf der Experience Platform basieren (z. B. die Echtzeit-Kundendatenplattform), bieten eine automatische Durchsetzung von Datenverwendungsrichtlinien. Jede Anwendung behält ihre eigene Methode bei, um Richtlinienverletzungen zu beheben und Schritte zur Problembehebung bereitzustellen.

Weitere Informationen zur Durchsetzung der Richtlinie zur automatischen Datenverwendung finden Sie in der Dokumentation der Plattform-basierten Anwendung, die Sie verwenden. Informationen zur automatischen Richtliniendurchsetzung in Echtzeit-CDP finden Sie in der Übersicht zur [Echtzeit-Datenverwaltung](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance).