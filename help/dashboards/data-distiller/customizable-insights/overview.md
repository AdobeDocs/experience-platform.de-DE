---
title: Anpassbare Insights für erweiterte App-Berichte
description: Erfahren Sie, wie Sie mit SQL-Abfragen Einblicke in Ihre benutzerdefinierten Dashboards generieren können.
exl-id: c60a9218-4ac0-4638-833b-bdbded36ddf5
source-git-commit: 5bb954da7c1e05922a4e0f8d0bc7d3ab5c8e0e58
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Anpassbare Insights für erweiterte App-Berichte

Verwenden Sie benutzerdefinierte SQL-Abfragen, um Einblicke aus verschiedenen strukturierten Datensätzen effektiv zu extrahieren. Technische Mitarbeiter können den Abfragepro-Modus verwenden, um komplexe Analysen mit SQL durchzuführen und diese Analyse dann über Diagramme in Ihrem benutzerdefinierten Dashboard für nicht technische Benutzer freizugeben oder in CSV-Dateien zu exportieren. Diese Methode der Insight-Erstellung eignet sich gut für Tabellen mit klaren Beziehungen und ermöglicht eine stärkere Anpassung innerhalb Ihrer Einblicke und Filter, die für Nischenanwendungsfälle geeignet sind.

>[!IMPORTANT]
>
>Der Pro-Modus für Abfragen steht nur Benutzern zur Verfügung, die die [Data Distiller SKU](../../../query-service/data-distiller/overview.md) erworben haben.

Um Einblicke aus SQL zu generieren, müssen Sie zunächst ein Dashboard erstellen.

## Benutzerdefiniertes Dashboard erstellen {#create-custom-dashboard}

Um ein benutzerdefiniertes Dashboard zu erstellen, wählen Sie im linken Navigationsbereich die Option **[!UICONTROL Dashboards]** aus, um den Arbeitsbereich &quot;Dashboards&quot;zu öffnen. Wählen Sie dann **[!UICONTROL Dashboard erstellen]** aus.

![Der Dashboard-Bestand mit Dashboard erstellen-Markierung.](../../images/customizable-insights/create-dashboard.png)

Das Dialogfeld **[!UICONTROL Dashboard erstellen]** wird angezeigt. Es gibt zwei Optionen, aus denen Sie Ihre Dashboard-Erstellungsmethode auswählen können. Um Ihre Einblicke zu erstellen, können Sie entweder ein vorhandenes Datenmodell mit dem Designmodus [[!UICONTROL Geführter Entwurf]](../../user-defined-dashboards.md) oder Ihre eigene SQL mit dem Pro-Modus [!UICONTROL Abfrage] verwenden.

<!-- Maybe reference Guided design mode in other places on UDD doc. -->

Die Verwendung eines vorhandenen Datenmodells bietet die Vorteile eines strukturierten, effizienten und skalierbaren Frameworks, das auf Ihre spezifischen Geschäftsanforderungen zugeschnitten ist. Informationen zum [Erstellen von Einblicken aus einem vorhandenen Datenmodell](../../user-defined-dashboards.md#create-widget) finden Sie im Handbuch zum benutzerdefinierten Dashboard.

Insights, die aus SQL-Abfragen generiert werden, bieten deutlich mehr Flexibilität und Anpassung. Technische Mitarbeiter können den Abfragepro-Modus verwenden, um eine komplexe Analyse von SQL durchzuführen und diese Analyse dann über diese Dashboard-Funktion für nicht technische Benutzer freizugeben. Wählen Sie **[!UICONTROL promode abfragen]** gefolgt von **[!UICONTROL save]**.

>[!NOTE]
>
>Nachdem Sie eine Auswahl getroffen haben, können Sie diese Auswahl in diesem Dashboard nicht mehr ändern. Stattdessen müssen Sie ein neues Dashboard mit einer anderen Dashboard-Erstellungsmethode erstellen.

![ Das Dialogfeld [!UICONTROL Dashboard erstellen] mit Abfrage pro -Modus und Speichern hervorgehoben.](../../images/customizable-insights/query-pro-mode.png)

## Erstellen eines Diagramms {#create-a-chart}

Eine schrittweise Anleitung zum Erstellen eines Diagramms mit SQL finden Sie im Leitfaden [query pro mode](./query-pro-mode.md) .
