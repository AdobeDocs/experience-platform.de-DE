---
description: Erfahren Sie, wie Sie einen Adobe Analytics-Quell-Connector über die Benutzeroberfläche erstellen, um Klassifizierungsdaten in Adobe Experience Platform zu importieren.
title: Erstellen einer Adobe Analytics Source-Verbindung für Classification-Daten in der Benutzeroberfläche
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
source-git-commit: 02b5c5f963c21247adbb1d13114f92b22f8758de
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 15%

---

# Erstellen einer Adobe Analytics-Quellverbindung für Klassifizierungsdaten in der Benutzeroberfläche

>[!TIP]
>
>Standardmäßig werden Adobe Analytics-Klassifizierungsdaten wöchentlich aktualisiert. Die Datenerfassung für Ihre Classification-Daten wird sieben Tage nach der Ersteinrichtung Ihres Datenflusses verarbeitet. Beim ersten Laden werden die gesamten Daten erfasst und die darauf folgende wöchentliche Erfassung führt inkrementelle Daten aus.

In diesem Tutorial erfahren Sie, wie Sie Ihre Adobe Analytics-Klassifizierungsdaten über die Benutzeroberfläche in Adobe Experience Platform erfassen.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): Experience Platform stellt virtuelle Sandboxes bereit, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen aufteilen, um die Entwicklung und Weiterentwicklung von Programmen für digitale Erlebnisse zu erleichtern.

Für den Quell-Connector für Analytics-Classifications müssen Ihre Daten vor der Verwendung in die neue Classification-Infrastruktur von Adobe Analytics migriert worden sein. Wenden Sie sich zur Bestätigung des Migrationsstatus Ihrer Daten an Ihr Adobe-Account-Team.

## Auswählen Ihrer Classifications

Wählen Sie in der Experience Platform-Benutzeroberfläche im linken Navigationsbereich **[!UICONTROL Quellen]** aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie *Adobe Applications* die Option **[!UICONTROL Adobe Analytics]** und dann **[!UICONTROL Set up]**.

>[!TIP]
>
>Quellen im Quellkatalog zeigen die Option **[!UICONTROL Einrichten]** an, wenn kein authentifiziertes Konto vorhanden ist. Sobald ein Konto authentifiziert wurde, ändert sich die Option in **[!UICONTROL Daten hinzufügen]**.

![Der Quellkatalog in der Experience Platform-Benutzeroberfläche mit der ausgewählten Adobe Analytics-Quelle.](../../../../images/tutorials/create/classifications/catalog.png)

Wählen Sie als Nächstes [!UICONTROL Klassifizierungen] und dann die Klassifizierungsdatensätze aus, die Sie auf Experience Platform erfassen möchten.

Sie können bis zu 30 verschiedene Classification-Datensätze auswählen, die in Experience Platform integriert werden können. Alle ausgewählten Datensätze werden in der rechten Leiste angezeigt. Wenn Sie fertig sind, wählen Sie [!UICONTROL Weiter] aus, um fortzufahren.

![Die Klassifizierungsseite mit mehreren ausgewählten Klassifizierungsdatensätzen.](../../../../images/tutorials/create/classifications/select.png)

## Überprüfen Sie Ihre Klassifizierungen

Der Schritt **[!UICONTROL Überprüfen]** wird angezeigt, mit dem Sie Ihre ausgewählten Klassifizierungsdatensätze überprüfen können, bevor sie erstellt werden. Die Details lassen sich wie folgt kategorisieren:

* **[!UICONTROL Verbindung]**: Zeigt die Quellplattform und den Status der Verbindung an.
* **[!UICONTROL Datentyp]**: Zeigt die Anzahl der ausgewählten Klassifizierungen an.
* **[!UICONTROL Planung]**: Zeigt die Häufigkeit der Synchronisierung für Classification-Daten an. **Hinweis**: Klassifizierungsdaten werden wöchentlich aktualisiert.

Nachdem Sie Ihren Datenfluss überprüft haben, klicken Sie auf **[!UICONTROL Beenden]** und lassen Sie die Erstellung des Datenflusses etwas Zeit zu.

![Die Überprüfungsseite für Adobe Analytics-Klassifizierungsdaten.](../../../../images/tutorials/create/classifications/review.png)

## Nächste Schritte

In diesem Tutorial haben Sie einen Connector für Analytics-Klassifizierungen erstellt, der Klassifizierungsdaten in Experience Platform integriert. Weitere Informationen zu [!DNL Analytics] und Klassifizierungsdaten finden Sie in den folgenden Dokumenten:

* [Übersicht über den Quell-Connector von Adobe Analytics](../../../../connectors/adobe-applications/analytics.md)
* [Erstellen einer Analytics-Quellverbindung für Report Suite-Daten in der Benutzeroberfläche](./analytics.md)
* [Über Klassifizierungen](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)
