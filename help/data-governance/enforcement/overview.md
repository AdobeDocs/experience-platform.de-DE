---
keywords: Experience Platform;Home;beliebte Themen;Richtliniendurchsetzung;Automatische Durchsetzung;API-basierte Durchsetzung;Datenverwaltung
solution: Experience Platform
title: Übersicht über die Richtliniendurchsetzung
topic-legacy: guide
description: Sobald Datenverwendungsbeschriftungen auf Adobe Experience Platform-Datensätze angewendet wurden und für Marketingaktionen mit diesen Bezeichnungen Richtlinien zur Datenverwendung definiert wurden, können Sie diese Richtlinien mithilfe der Datenverwaltungsfunktionen durchsetzen und Datenvorgänge verhindern, die Richtlinienverletzungen darstellen. Es gibt zwei Methoden zur Durchsetzung von Richtlinien, die durch die Datenverwaltungsfunktionen auf Plattform, API-basierte Durchsetzung und automatische Durchsetzung bereitgestellt werden.
exl-id: d19d8060-85a1-405c-856d-f59041947a33
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 10%

---

# Übersicht über die Durchsetzung von Richtlinien

Sobald Datenverwendungsbeschriftungen auf Datasets angewendet wurden und für Marketingaktionen mit diesen Bezeichnungen Richtlinien zur Datenverwendung definiert wurden, können Sie mit den Adobe Experience Platform-Funktionen zur Datenverwaltung diese Richtlinien durchsetzen und Datenvorgänge verhindern, die Richtlinienverletzungen darstellen.

Es gibt zwei Methoden zur Richtliniendurchsetzung, die von [!DNL Data Governance]-Funktionen für [!DNL Platform] bereitgestellt werden: API-basierte Durchsetzung und automatische Durchsetzung.

## API-basierte Durchsetzung

Die [!DNL Policy Service]-API stellt Endpunkte bereit, mit denen Sie Marketingaktionen gegen Datasets oder beliebige Kombinationen von Datenverwendungsbeschriftungen testen können, um festzustellen, ob Richtlinienverletzungen auftreten. Je nach API-Antwort können Sie dann Protokolle in Ihrer Erlebnisanwendung einrichten, um die Einhaltung von Datennutzungsrichtlinien richtig durchzusetzen.

Anweisungen zum Auswerten von Richtlinien mit der API finden Sie im Tutorial [API-basierte Durchsetzung](./api-enforcement.md).

## Automatische Durchsetzung

Die Experience Platform nutzt Datenlinien, Datenklassifizierungs- und Richtlinienverwaltungsfunktionen, um automatisch Verstöße gegen Richtlinien zu bewerten und zu untersuchen. Weitere Informationen finden Sie in der Übersicht über [automatische Richtliniendurchsetzung](./auto-enforcement.md).
