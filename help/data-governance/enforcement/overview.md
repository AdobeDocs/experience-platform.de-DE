---
keywords: Experience Platform;home;popular topics;Policy enforcement;Automatic enforcement;API-based enforcement;data governance
solution: Experience Platform
title: Übersicht über die Durchsetzung von Richtlinien
topic: enforcement
description: Sobald Datenverwendungsbeschriftungen auf Adobe Experience Platform-Datensätze angewendet wurden und für Marketingaktionen mit diesen Bezeichnungen Richtlinien zur Datenverwendung definiert wurden, können Sie diese Richtlinien mithilfe der Datenverwaltungsfunktionen durchsetzen und Datenvorgänge verhindern, die Richtlinienverletzungen darstellen. Es gibt zwei Methoden zur Durchsetzung von Richtlinien, die durch die Datenverwaltungsfunktionen auf Plattform, API-basierte Durchsetzung und automatische Durchsetzung bereitgestellt werden.
translation-type: tm+mt
source-git-commit: 30733f2274ff8cb9ae73cf2b9f7f0219fefbd393
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 12%

---


# Übersicht über die Durchsetzung von Richtlinien

Sobald Datenverwendungsbezeichnungen auf [!DNL Platform]-Datensätze angewendet wurden und für Marketingaktionen mit diesen Bezeichnungen Datenverwendungsrichtlinien definiert wurden, können Sie mithilfe der [!DNL Data Governance]-Funktionen diese Richtlinien durchsetzen und Datenoperationen verhindern, die Richtlinienverletzungen darstellen.

Es gibt zwei Methoden zur Richtliniendurchsetzung, die von [!DNL Data Governance]-Funktionen für [!DNL Platform] bereitgestellt werden: API-basierte Durchsetzung und automatische Durchsetzung.

## API-basierte Durchsetzung

Die [!DNL Policy Service]-API stellt Endpunkte bereit, mit denen Sie Marketingaktionen gegen Datasets oder beliebige Kombinationen von Datenverwendungsbeschriftungen testen können, um festzustellen, ob Richtlinienverletzungen auftreten. Je nach API-Antwort können Sie dann Protokolle in Ihrer Erlebnisanwendung einrichten, um die Einhaltung von Datennutzungsrichtlinien richtig durchzusetzen.

Anweisungen zum Auswerten von Richtlinien mit der API finden Sie im Tutorial [API-basierte Durchsetzung](./api-enforcement.md).

## Automatische Durchsetzung

Die Experience Platform nutzt Datenlinien, Datenklassifizierungs- und Richtlinienverwaltungsfunktionen, um automatisch Verstöße gegen Richtlinien zu bewerten und zu untersuchen. Weitere Informationen finden Sie in der Übersicht über [automatische Richtliniendurchsetzung](./auto-enforcement.md).