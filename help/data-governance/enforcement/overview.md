---
keywords: Experience Platform;Startseite;beliebte Themen;Richtliniendurchsetzung;Automatische Durchsetzung;API-basierte Durchsetzung;Data Governance
solution: Experience Platform
title: Richtliniendurchsetzung – Übersicht
topic-legacy: guide
description: Erfahren Sie, wie Datennutzungsrichtlinien in Adobe Experience Platform durchgesetzt werden.
exl-id: d19d8060-85a1-405c-856d-f59041947a33
source-git-commit: 6f79b1a03a75558d1a25f0375e8393ad56756d80
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 48%

---

# Richtliniendurchsetzung – Übersicht

Einmal [Datennutzungsbezeichnungen](../labels/overview.md) angewendet wurden und [Datennutzungsrichtlinien](../policies/overview.md) definiert wurden, können Sie diese Richtlinien durchsetzen, um Datenvorgänge zu verhindern, die Richtlinienverletzungen darstellen.

>[!NOTE]
>
>Dieses Dokument konzentriert sich auf die Durchsetzung von Datennutzungsrichtlinien. Informationen zu Zugriffssteuerungsrichtlinien finden Sie im Handbuch unter [attributbasierte Zugriffssteuerung](../../access-control/abac/overview.md).

Es gibt zwei Methoden zur Durchsetzung von Richtlinien in Adobe Experience Platform: automatische Durchsetzung und API-basierte Durchsetzung.

## Automatische Durchsetzung

Experience Platform nutzt die Ermittlung der Datenherkunft sowie Daten-Classification- und Richtlinienverwaltungsfunktionen, um automatisch Verstöße gegen Richtlinien zu bewerten und zu untersuchen. Weitere Informationen finden Sie in der Übersicht über [automatische Richtliniendurchsetzung](./auto-enforcement.md).

## API-basierte Durchsetzung

Die [!DNL Policy Service]-API stellt Endpunkte bereit, mit denen Sie Marketing-Aktionen für Datensätze oder beliebige Kombinationen von Datennutzungskennzeichnungen testen können, um festzustellen, ob Richtlinien verletzt werden. Basierend auf der API-Antwort können Sie dann Protokolle in Ihrer Erlebnisanwendung einrichten, um die Einhaltung von Data Governance-Richtlinien angemessen durchzusetzen.

Anleitungen zum Auswerten von Richtlinien mit der API finden Sie im Tutorial zur [API-basierten Durchsetzung](./api-enforcement.md).
