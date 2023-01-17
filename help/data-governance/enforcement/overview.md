---
keywords: Experience Platform;Startseite;beliebte Themen;Richtliniendurchsetzung;Automatische Durchsetzung;API-basierte Durchsetzung;Data Governance
solution: Experience Platform
title: Richtliniendurchsetzung – Übersicht
description: Erfahren Sie, wie die Datennutzungsrichtlinien auf Adobe Experience Platform durchgesetzt werden.
exl-id: d19d8060-85a1-405c-856d-f59041947a33
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 100%

---

# Richtliniendurchsetzung – Übersicht

Sobald [Datennutzungskennzeichnungen](../labels/overview.md) angewendet und [Datennutzungsrichtlinien](../policies/overview.md) definiert wurden, können Sie diese Richtlinien durchsetzen, um Datenoperationen zu verhindern, die eine Verletzung der Richtlinien darstellen würden.

>[!NOTE]
>
>Dieses Dokument konzentriert sich auf die Durchsetzung von Datennutzungsrichtlinien. Informationen zu den Richtlinien für die Zugriffssteuerung finden Sie im Handbuch zur [attributbasierten Zugriffssteuerung](../../access-control/abac/overview.md).

Es gibt zwei Methoden zur Durchsetzung von Richtlinien auf Adobe Experience Platform: automatische Durchsetzung und API-basierte Durchsetzung.

## Automatische Durchsetzung

Experience Platform nutzt die Ermittlung der Datenherkunft sowie Daten-Classification- und Richtlinienverwaltungsfunktionen, um automatisch Verstöße gegen Richtlinien zu bewerten und zu untersuchen. Weitere Informationen finden Sie in der Übersicht über [automatische Richtliniendurchsetzung](./auto-enforcement.md).

## API-basierte Durchsetzung

Die [!DNL Policy Service]-API stellt Endpunkte bereit, mit denen Sie Marketing-Aktionen für Datensätze oder beliebige Kombinationen von Datennutzungskennzeichnungen testen können, um festzustellen, ob Richtlinien verletzt werden. Auf der Grundlage der API-Antwort können Sie dann innerhalb Ihrer Erlebnisanwendung Protokolle einrichten, um die Einhaltung der Data-Governance-Richtlinien angemessen durchzusetzen.

Anleitungen zum Auswerten von Richtlinien mit der API finden Sie im Tutorial zur [API-basierten Durchsetzung](./api-enforcement.md).
