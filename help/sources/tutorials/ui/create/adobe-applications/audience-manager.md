---
keywords: Experience Platform;Home;beliebte Themen;Audience Manager-Quell-Connector;Audience Manager;Audience Manager-Connector
title: Erstellen einer Adobe Audience Manager Source-Verbindung über die Benutzeroberfläche
description: Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Quellverbindung für Adobe Audience Manager, um Customer Experience Event-Daten über die Benutzeroberfläche in Experience Platform zu importieren.
exl-id: 90c4a719-aaad-4687-afd8-7a1c0c56f744
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 21%

---

# Adobe Audience Manager-Quellverbindung über die Benutzeroberfläche erstellen

Dieses Tutorial führt Sie durch die Schritte zum Erstellen eines Quell-Connectors für Adobe Audience Manager, um Customer Experience Event-Daten über die Benutzeroberfläche in Experience Platform zu importieren.

## Erstellen einer Quellverbindung mit Adobe Audience Manager

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchleiste finden.

Wählen Sie unter [!UICONTROL Adobe] die Option **[!UICONTROL Adobe Audience Manager]** und dann **[!UICONTROL Einrichten]** aus.

![Katalog](../../../../images/tutorials/create/aam/catalog.png)

### Merkmale und Segmente auswählen

>[!NOTE]
>
>Sie können keine regionalen Daten aus der Audience Manager-Quelle in Experience Platform aufnehmen. Wenn Sie Analytics-Anwendungsfälle haben, für die regionale Daten erforderlich sind, verwenden Sie bitte den [Analytics-Quell-Connector](../adobe-applications/analytics.md).

Der Schritt [!UICONTROL Auswählen von Eigenschaften und ]&quot; wird angezeigt und bietet Ihnen eine interaktive Oberfläche zum Durchsuchen und Auswählen Ihrer Eigenschaften, Segmente und Daten.

* Das linke Bedienfeld der Benutzeroberfläche enthält die Optionen [!UICONTROL Merkmale und Segmente auswählen] sowie ein hierarchisches Verzeichnis aller verfügbaren Segmente.
* Die rechte Hälfte der Benutzeroberfläche ermöglicht es Ihnen, mit ausgewählten Segmenten zu interagieren und bestimmte Daten auszuwählen, die Sie verwenden möchten.

![add-data](../../../../images/tutorials/create/aam/add-data.png)

Um durch verfügbare Segmente zu navigieren, wählen Sie den Ordner, auf den Sie zugreifen möchten, aus dem Bedienfeld [!UICONTROL Alle Segmente] aus. Wenn Sie einen Ordner auswählen, können Sie die Hierarchie eines Ordners durchlaufen und erhalten eine Liste von Segmenten, durch die gefiltert werden soll.

![segment-folder](../../../../images/tutorials/create/aam/segment-folder.png)

Nachdem Sie die gewünschten Segmente identifiziert und ausgewählt haben, wird rechts ein neues Bedienfeld mit der Liste der ausgewählten Elemente angezeigt. Sie können weiterhin auf verschiedene Ordner zugreifen und verschiedene Segmente für Ihre Verbindung auswählen. Wenn Sie weitere Segmente auswählen, wird das Bedienfeld auf der rechten Seite aktualisiert.

![select-data](../../../../images/tutorials/create/aam/select-data.png)

Alternativ können Sie die Kästchen **[!UICONTROL Alle Segmente auswählen]** und **[!UICONTROL Alle Eigenschaften auswählen]** auswählen. Wenn Sie alle Segmente auswählen, werden Audience Manager-Segmente zu Experience Platform hinzugefügt, während bei Auswahl aller Eigenschaften alle First-Party-Eigenschaften von Audience Manager aktiviert sind.

>[!WARNING]
>
>Die Aufnahme umfangreicher Audience Manager-Segmentpopulationen hat einen direkten Einfluss auf Ihre Gesamtprofilanzahl, wenn Sie zum ersten Mal ein Audience Manager-Segment mithilfe der Audience Manager-Quelle an Experience Platform senden. Das bedeutet, dass die Auswahl aller Segmente eine Profilanzahl ergeben kann, die über Ihrer Lizenznutzungsberechtigung liegt. Bitte überprüfen Sie Ihre [Lizenznutzungsbeschränkung](../../../../../dashboards/guides/license-usage.md) bevor Sie fortfahren.

Wenn Sie fertig sind, klicken Sie auf **[!UICONTROL Weiter]**

![alle Segmente](../../../../images/tutorials/create/aam/all-segments.png)

Der Schritt [!UICONTROL Überprüfen] wird angezeigt, sodass Sie Ihre ausgewählten Eigenschaften und Segmente überprüfen können, bevor sie mit Experience Platform verbunden werden. Die Details lassen sich wie folgt kategorisieren:

* **[!UICONTROL Verbindung]**: Zeigt die Quellplattform und den Status der Verbindung an.
* **[!UICONTROL Ausgewählte Daten]**: Zeigt die Anzahl der ausgewählten Segmente und aktivierten Eigenschaften an.

![überprüfen](../../../../images/tutorials/create/aam/review.png)

Nachdem Sie Ihren Datenfluss überprüft haben, klicken Sie auf **[!UICONTROL Beenden]** und gewähren Sie etwas Zeit für die Erstellung des Datenflusses.

## Nächste Schritte

Während ein Audience Manager-Datenfluss aktiv ist, werden eingehende Daten automatisch in Echtzeit-Kundenprofile aufgenommen. Sie können jetzt diese eingehenden Daten verwenden und Zielgruppensegmente mithilfe des Segmentierungs-Services von Experience Platform erstellen. Weiterführende Informationen finden Sie in folgenden Dokumenten:

* [Übersicht zum Echtzeit-Kundenprofil](../../../../../profile/home.md)
* [Übersicht über den Segmentierungs-Service](../../../../../segmentation/home.md)
