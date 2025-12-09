---
description: Erfahren Sie, wie Sie über die Benutzeroberfläche einen Adobe Analytics-Quell-Connector erstellen, um Klassifizierungsdaten in Adobe Experience Platform zu importieren.
title: Erstellen einer Adobe Analytics Source-Verbindung für Klassifizierungsdaten in der Benutzeroberfläche
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
source-git-commit: dfc8a1d51e6dd25210a0b6f24dad4d0f00052414
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 16%

---

# Erstellen einer Adobe Analytics-Quellverbindung für Klassifizierungsdaten in der Benutzeroberfläche

>[!TIP]
>
>Standardmäßig werden Adobe Analytics-Klassifizierungsdaten wöchentlich aktualisiert. Die Datenaufnahme für Ihre Klassifizierungsdaten wird sieben Tage nach der ersten Einrichtung Ihres Datenflusses verarbeitet. Der erste Ladevorgang nimmt die gesamten Daten auf und die anschließende wöchentliche Aufnahme führt inkrementelle Daten aus.

In diesem Tutorial erfahren Sie, wie Sie Ihre Adobe Analytics-Klassifizierungsdaten über die Benutzeroberfläche in Adobe Experience Platform aufnehmen.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Vor der Verwendung des Analytics Classifications Source Connectors müssen Ihre Daten in die neue Klassifizierungs-Infrastruktur von Adobe Analytics migriert worden sein. Wenden Sie sich zur Bestätigung des Migrationsstatus Ihrer Daten an Ihr Adobe-Accountteam.

## Klassifizierungen auswählen

Wählen Sie in der Benutzeroberfläche von Experience Platform in der linken Navigationsleiste die Option **[!UICONTROL Sources]** , um auf den [!UICONTROL Sources]-Arbeitsbereich zuzugreifen. Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie **&#x200B; Adobe-Programme &#x200B;** [!UICONTROL Adobe Analytics] **&#x200B; und dann &#x200B;** [!UICONTROL Set up]** aus.

>[!TIP]
>
>Quellen im Quellkatalog zeigen die **[!UICONTROL Set up]** an, wenn kein authentifiziertes Konto vorhanden ist. Nach der Authentifizierung eines Kontos ändert sich die Option in **[!UICONTROL Add data]**.

![Der Quellkatalog in der Experience Platform-Benutzeroberfläche mit ausgewählter Adobe Analytics-Quelle.](../../../../images/tutorials/create/classifications/catalog.png)

Wählen Sie als Nächstes [!UICONTROL Classifications] und dann die Klassifizierungsdatensätze aus, die Sie in Experience Platform aufnehmen möchten. Alternativ können Sie die Suche verwenden, um nach bestimmten Klassifizierungen zu filtern und auszuwählen.

Sie können bis zu 30 verschiedene Klassifizierungsdatensätze auswählen, die in Experience Platform importiert werden sollen. Alle von Ihnen ausgewählten Datensätze werden in der rechten Leiste angezeigt. Wenn Sie fertig sind, wählen Sie [!UICONTROL Next] aus, um fortzufahren.

![Die Seite „Klassifizierungen“ mit mehreren ausgewählten Klassifizierungsdatensätzen.](../../../../images/tutorials/create/classifications/select.png)

## Überprüfen der Klassifizierungen

Der Schritt **[!UICONTROL Review]** wird angezeigt, in dem Sie die ausgewählten Klassifizierungsdatensätze überprüfen können, bevor sie erstellt werden. Die Details lassen sich wie folgt kategorisieren:

* **[!UICONTROL Connection]**: Zeigt die Quellplattform und den Status der Verbindung an.
* **[!UICONTROL Data type]**: Zeigt die Anzahl der ausgewählten Klassifizierungen an.
* **[!UICONTROL Scheduling]**: Zeigt die Häufigkeit der Synchronisierung für Klassifizierungsdaten an. **Hinweis**: Klassifizierungsdaten werden wöchentlich aktualisiert.

Nachdem Sie Ihren Datenfluss überprüft haben, klicken Sie auf **[!UICONTROL Finish]** und gewähren Sie etwas Zeit für die Erstellung des Datenflusses.

![Die Überprüfungsseite für Adobe Analytics-Klassifizierungsdaten.](../../../../images/tutorials/create/classifications/review.png)

## Nächste Schritte

In diesem Tutorial haben Sie einen Analytics Classifications Data-Connector erstellt, der Klassifizierungsdaten in Experience Platform einbringt. In den folgenden Dokumenten finden Sie weitere Informationen zu [!DNL Analytics] und Klassifizierungsdaten:

* [Übersicht über den Adobe Analytics-Quell-Connector](../../../../connectors/adobe-applications/analytics.md)
* [Erstellen einer Analytics-Quellverbindung für Report Suite-Daten in der Benutzeroberfläche](./analytics.md)
* [Über Klassifizierungen](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html?lang=de)
