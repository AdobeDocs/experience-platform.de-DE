---
keywords: Experience Platform; Startseite; beliebte Themen; Audience Manager-Quell-Connector; Audience Manager; Audience Manager-Connector
title: Erstellen einer Adobe Audience Manager Source-Verbindung in der Benutzeroberfläche
description: Dieses Tutorial führt Sie durch die Schritte, die zum Erstellen einer Quellverbindung für Adobe Audience Manager erforderlich sind, um Verbrauchererlebnisereignisdaten über die Benutzeroberfläche in Platform einzubringen.
exl-id: 90c4a719-aaad-4687-afd8-7a1c0c56f744
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 29%

---

# Adobe Audience Manager-Quellverbindung über die Benutzeroberfläche erstellen

In diesem Tutorial werden Sie durch die Schritte geführt, die zum Erstellen eines Quell-Connectors für Adobe Audience Manager erforderlich sind, um Verbrauchererlebnisereignisdaten über die Benutzeroberfläche in Platform einzubringen.

## Erstellen einer Quellverbindung mit Adobe Audience Manager

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchleiste finden.

Wählen Sie unter [!UICONTROL Adobe Application] den Eintrag **[!UICONTROL Adobe Audience Manager]** und dann **[!UICONTROL Set up]**.

![Katalog](../../../../images/tutorials/create/aam/catalog.png)

### Merkmale und Segmente auswählen

>[!NOTE]
>
>Sie können keine Regionaldaten von der Audience Manager-Quelle zu Experience Platform erfassen. Wenn Sie Analytics-Anwendungsfälle haben, für die regionale Daten erforderlich sind, verwenden Sie bitte den [Analytics-Quell-Connector](../adobe-applications/analytics.md).

Der Schritt [!UICONTROL Eigenschaften und Segmente auswählen] wird angezeigt und bietet eine interaktive Oberfläche, über die Sie Ihre Eigenschaften, Segmente und Daten untersuchen und auswählen können.

* Der linke Bereich der Benutzeroberfläche enthält die Optionen [!UICONTROL Eigenschaften und Segmente auswählen] sowie ein hierarchisches Verzeichnis aller für Sie verfügbaren Segmente.
* In der rechten Hälfte der Benutzeroberfläche können Sie mit ausgewählten Segmenten interagieren und bestimmte Daten auswählen, die Sie verwenden möchten.

![add-data](../../../../images/tutorials/create/aam/add-data.png)

Um durch verfügbare Segmente zu navigieren, wählen Sie den Ordner, auf den Sie zugreifen möchten, aus dem Bedienfeld [!UICONTROL Alle Segmente] aus. Durch die Auswahl eines Ordners können Sie die Hierarchie eines Ordners durchlaufen und erhalten eine Liste von Segmenten, nach denen gefiltert werden soll.

![segment-folder](../../../../images/tutorials/create/aam/segment-folder.png)

Nachdem Sie die gewünschten Segmente identifiziert und ausgewählt haben, wird rechts ein neues Bedienfeld mit Ihrer Liste der ausgewählten Elemente angezeigt. Sie können weiterhin auf verschiedene Ordner zugreifen und verschiedene Segmente für Ihre Verbindung auswählen. Wenn Sie weitere Segmente auswählen, wird das Bedienfeld auf der rechten Seite aktualisiert.

![select-data](../../../../images/tutorials/create/aam/select-data.png)

Alternativ können Sie die Felder **[!UICONTROL Alle Segmente auswählen]** und **[!UICONTROL Alle Eigenschaften auswählen]** auswählen. Wenn Sie alle Audience Manager auswählen, gelangen die Segmentsegmente in Platform. Bei Auswahl aller Eigenschaften werden alle Erstanbietereigenschaften aus dem Audience Manager aktiviert.

>[!WARNING]
>
>Die Aufnahme umfangreicher Audience Manager-Segmentpopulationen hat einen direkten Einfluss auf Ihre Gesamtprofilanzahl, wenn Sie zum ersten Mal ein Audience Manager-Segment mithilfe der Audience Manager-Quelle an Platform senden. Das bedeutet, dass die Auswahl aller Segmente eine Profilanzahl ergeben kann, die über Ihrer Lizenznutzungsberechtigung liegt. Überprüfen Sie Ihre [Lizenz-Nutzungslimit](../../../../../dashboards/guides/license-usage.md) , bevor Sie fortfahren.

Nachdem Sie fertig sind, wählen Sie **[!UICONTROL Weiter]** aus

![all-segments](../../../../images/tutorials/create/aam/all-segments.png)

Der Schritt [!UICONTROL Überprüfen] wird angezeigt, mit dem Sie Ihre ausgewählten Eigenschaften und Segmente überprüfen können, bevor sie mit Platform verbunden sind. Die Details lassen sich wie folgt kategorisieren:

* **[!UICONTROL Verbindung]**: Zeigt die Quellplattform und den Status der Verbindung an.
* **[!UICONTROL Ausgewählte Daten]**: Zeigt die Anzahl der ausgewählten Segmente und aktivierten Eigenschaften an.

![überprüfen](../../../../images/tutorials/create/aam/review.png)

Nachdem Sie Ihren Datenfluss überprüft haben, klicken Sie auf **[!UICONTROL Beenden]** und gewähren Sie etwas Zeit für die Erstellung des Datenflusses.

## Nächste Schritte

Während ein Audience Manager-Datenfluss aktiv ist, werden eingehende Daten automatisch in Echtzeit-Kundenprofile aufgenommen. Sie können diese eingehenden Daten jetzt verwenden und Zielgruppensegmente mithilfe des Segmentierungsdienstes von Platform erstellen. Weiterführende Informationen finden Sie in folgenden Dokumenten:

* [Übersicht zum Echtzeit-Kundenprofil](../../../../../profile/home.md)
* [Übersicht über den Segmentierungs-Service](../../../../../segmentation/home.md)
