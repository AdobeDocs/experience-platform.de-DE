---
title: Anpassbare Insights für erweiterte App-Berichte
description: Erfahren Sie, wie Sie mit SQL-Abfragen Einblicke in Ihre benutzerdefinierten Dashboards generieren können.
source-git-commit: 17ad52864bbca09844c0241b6451e6811bd8f413
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Anpassbare Insights für erweiterte App-Berichte

Verwenden Sie benutzerdefinierte SQL-Abfragen, um Einblicke aus verschiedenen strukturierten Datensätzen effektiv zu extrahieren. Technische Mitarbeiter können den Abfragepro-Modus verwenden, um komplexe Analysen mit SQL durchzuführen und diese Analyse dann über Diagramme in Ihrem benutzerdefinierten Dashboard für nicht technische Benutzer freizugeben oder in CSV-Dateien zu exportieren. Diese Methode der Insight-Erstellung eignet sich gut für Tabellen mit klaren Beziehungen und ermöglicht eine stärkere Anpassung innerhalb Ihrer Einblicke und Filter, die für Nischenanwendungsfälle geeignet sind.

>[!IMPORTANT]
>
>Der Pro-Modus Abfrage steht nur Benutzern zur Verfügung, die die [Data Distiller SKU](../../../query-service/data-distiller/overview.md).

Um Einblicke aus SQL zu generieren, müssen Sie zunächst ein Dashboard erstellen.

## Benutzerdefiniertes Dashboard erstellen {#create-custom-dashboard}

Um ein benutzerdefiniertes Dashboard zu erstellen, wählen Sie **[!UICONTROL Dashboards]** über das linke Navigationsfenster, um den Arbeitsbereich Dashboards zu öffnen. Wählen Sie als Nächstes **[!UICONTROL Dashboard erstellen]**.

![Das Dashboard-Inventar mit Dashboard erstellen wurde hervorgehoben.](../../images/customizable-insights/create-dashboard.png)

Die **[!UICONTROL Dashboard erstellen]** angezeigt. Es gibt zwei Optionen, aus denen Sie Ihre Dashboard-Erstellungsmethode auswählen können. Um Ihre Einblicke zu erstellen, können Sie entweder ein vorhandenes Datenmodell mit dem [[!UICONTROL Geführter Designmodus]](../../user-defined-dashboards.md) oder Ihre eigene SQL mit dem [!UICONTROL Abfragepro-Modus].

<!-- Maybe reference Guided design mode in other places on UDD doc. -->

Die Verwendung eines vorhandenen Datenmodells bietet die Vorteile eines strukturierten, effizienten und skalierbaren Frameworks, das auf Ihre spezifischen Geschäftsanforderungen zugeschnitten ist. Erfahren Sie mehr über [Einblicke aus einem vorhandenen Datenmodell erstellen](../../user-defined-dashboards.md#create-widget), siehe Handbuch für benutzerdefinierte Dashboards.

Insights, die aus SQL-Abfragen generiert werden, bieten deutlich mehr Flexibilität und Anpassung. Technische Mitarbeiter können den Abfragepro-Modus verwenden, um eine komplexe Analyse von SQL durchzuführen und diese Analyse dann über diese Dashboard-Funktion für nicht technische Benutzer freizugeben. Auswählen **[!UICONTROL Abfragepro-Modus]** gefolgt von **[!UICONTROL Speichern]**.

>[!NOTE]
>
>Nachdem Sie eine Auswahl getroffen haben, können Sie diese Auswahl in diesem Dashboard nicht mehr ändern. Stattdessen müssen Sie ein neues Dashboard mit einer anderen Dashboard-Erstellungsmethode erstellen.

![Die [!UICONTROL Dashboard erstellen] Dialog mit Query pro mode und Save hervorgehoben.](../../images/customizable-insights/query-pro-mode.png)

## Erstellen eines Diagramms {#create-a-chart}

Siehe [Anleitung zum Abfragenmodus](./query-pro-mode.md) für eine schrittweise Anleitung zum Erstellen eines Diagramms mit SQL.
