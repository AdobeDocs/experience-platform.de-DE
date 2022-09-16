---
keywords: Experience Platform;Startseite;beliebte Themen;Richtliniendurchsetzung;Automatische Durchsetzung;API-basierte Durchsetzung;Data Governance
solution: Experience Platform
title: Richtliniendurchsetzung – Übersicht
topic-legacy: guide
description: 'Sobald Datennutzungskennzeichnungen auf Adobe Experience Platform-Datensätze angewendet und somit Datennutzungsrichtlinien für Marketing-Aktionen mit diesen Kennzeichnungen definiert wurden, können Sie die Richtlinien mithilfe von Data Governance-Funktionen durchsetzen und Datenvorgänge verhindern, bei denen Richtlinien verletzt werden. Es gibt zwei Methoden zur Durchsetzung von Richtlinien, die durch die Data Governance-Funktionen in Platform bereitgestellt werden: API-basierte Durchsetzung und automatische Durchsetzung.'
exl-id: d19d8060-85a1-405c-856d-f59041947a33
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 100%

---

# Richtliniendurchsetzung – Übersicht

Sobald Datennutzungskennzeichnungen auf Datensätze angewendet und somit Datennutzungsrichtlinien für Marketing-Aktionen mit diesen Kennzeichnungen definiert wurden, können Sie die Richtlinien mithilfe der Data Governance-Funktionen von Adobe Experience Platform durchsetzen und Datenvorgänge verhindern, bei denen Richtlinien verletzt werden.

Es gibt zwei Methoden zur Durchsetzung von Richtlinien, die durch die Data-Governance-Funktionen in bereitgestellt werden [!DNL Platform]: API-basierte Durchsetzung und automatische Durchsetzung

## API-basierte Durchsetzung

Die [!DNL Policy Service]-API stellt Endpunkte bereit, mit denen Sie Marketing-Aktionen für Datensätze oder beliebige Kombinationen von Datennutzungskennzeichnungen testen können, um festzustellen, ob Richtlinien verletzt werden. Je nach API-Antwort können Sie dann Protokolle in Ihrer Erlebnisanwendung einrichten, um die Einhaltung von Datennutzungsrichtlinien richtig durchzusetzen.

Anleitungen zum Auswerten von Richtlinien mit der API finden Sie im Tutorial zur [API-basierten Durchsetzung](./api-enforcement.md).

## Automatische Durchsetzung

Experience Platform nutzt die Ermittlung der Datenherkunft sowie Daten-Classification- und Richtlinienverwaltungsfunktionen, um automatisch Verstöße gegen Richtlinien zu bewerten und zu untersuchen. Weitere Informationen finden Sie in der Übersicht über [automatische Richtliniendurchsetzung](./auto-enforcement.md).
