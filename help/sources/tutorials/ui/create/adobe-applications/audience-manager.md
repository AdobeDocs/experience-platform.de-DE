---
keywords: Experience Platform; Startseite; beliebte Themen; Audience Manager-Quell-Connector; Audience Manager; Audience Manager-Connector
solution: Experience Platform
title: Erstellen einer Adobe Audience Manager-Quellverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: In diesem Tutorial werden Sie durch die Schritte geführt, die zum Erstellen von Quell-Connectoren für Adobe Audience Manager erforderlich sind, um Verbrauchererlebnisereignisdaten über die Benutzeroberfläche in Platform einzubringen.
exl-id: 90c4a719-aaad-4687-afd8-7a1c0c56f744
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 11%

---

# Erstellen einer Adobe Audience Manager-Quellverbindung über die Benutzeroberfläche

In diesem Tutorial werden Sie durch die Schritte geführt, die zum Erstellen eines Quell-Connectors für Adobe Audience Manager erforderlich sind, um Verbrauchererlebnisereignisdaten über die Benutzeroberfläche in Platform einzubringen.

## Erstellen einer Quellverbindung mit Adobe Audience Manager

Anmelden bei [Adobe Experience Platform](https://platform.adobe.com) und wählen Sie **[!UICONTROL Quellen]** über die linke Navigationsleiste, um auf die [!UICONTROL Quellen] Arbeitsbereich. Der Bildschirm [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Unter dem [!UICONTROL Adobe Apps] category, select **[!UICONTROL Adobe Audience Manager]** und wählen Sie **[!UICONTROL Konfigurieren]**.

![Katalog](../../../../images/tutorials/create/aam/catalog.png)

Die [!UICONTROL Eigenschaften und Segmente auswählen] angezeigt werden. Sie erhalten eine interaktive Oberfläche, über die Sie Ihre Eigenschaften, Segmente und Daten untersuchen und auswählen können.

* Das linke Bedienfeld der Benutzeroberfläche enthält die [!UICONTROL Eigenschaften und Segmente auswählen] Optionen sowie ein hierarchisches Verzeichnis aller für Sie verfügbaren Segmente.
* In der rechten Hälfte der Benutzeroberfläche können Sie mit ausgewählten Segmenten interagieren und bestimmte Daten auswählen, die Sie verwenden möchten.

![add-data](../../../../images/tutorials/create/aam/add-data.png)

Um durch verfügbare Segmente zu navigieren, wählen Sie den Ordner aus, auf den Sie zugreifen möchten. [!UICONTROL Alle Segmente] Bereich. Durch die Auswahl eines Ordners können Sie die Hierarchie eines Ordners durchlaufen und erhalten eine Liste von Segmenten, nach denen gefiltert werden soll.

![segment-folder](../../../../images/tutorials/create/aam/segment-folder.png)

Nachdem Sie die gewünschten Segmente identifiziert und ausgewählt haben, wird rechts ein neues Bedienfeld mit Ihrer Liste der ausgewählten Elemente angezeigt. Sie können weiterhin auf verschiedene Ordner zugreifen und verschiedene Segmente für Ihre Verbindung auswählen. Wenn Sie weitere Segmente auswählen, wird das Bedienfeld auf der rechten Seite aktualisiert.

![select-data](../../../../images/tutorials/create/aam/select-data.png)

Alternativ können Sie die **[!UICONTROL Alle Segmente auswählen]** und **[!UICONTROL Alle Eigenschaften auswählen]** Boxen. Wenn Sie alle Audience Manager auswählen, gelangen die Segmentsegmente in Platform. Bei Auswahl aller Eigenschaften werden alle Erstanbietereigenschaften aus dem Audience Manager aktiviert.

Nachdem Sie fertig sind, wählen Sie **[!UICONTROL Nächste]**

![Alle Segmente](../../../../images/tutorials/create/aam/all-segments.png)

Die [!UICONTROL Überprüfen] angezeigt, sodass Sie Ihre ausgewählten Eigenschaften und Segmente überprüfen können, bevor sie mit Platform verbunden sind. Die Details lassen sich wie folgt kategorisieren:

* **[!UICONTROL Verbindung]**: Zeigt die Quellplattform und den Status der Verbindung an.
* **[!UICONTROL Ausgewählte Daten]**: Zeigt die Anzahl der ausgewählten Segmente und aktivierten Eigenschaften an.

![überprüfen](../../../../images/tutorials/create/aam/review.png)

Nachdem Sie Ihren Datenfluss überprüft haben, wählen Sie **[!UICONTROL Beenden]** und lassen Sie etwas Zeit für die Erstellung des Datenflusses zu.

## Nächste Schritte

Während ein Audience Manager-Datenfluss aktiv ist, werden eingehende Daten automatisch in Echtzeit-Kundenprofile aufgenommen. Sie können diese eingehenden Daten jetzt verwenden und Zielgruppensegmente mithilfe des Segmentierungsdienstes von Platform erstellen. Weiterführende Informationen finden Sie in folgenden Dokumenten:

* [Übersicht über das Echtzeit-Kundenprofil](../../../../../profile/home.md)
* [Übersicht über den Segmentierungsdienst](../../../../../segmentation/home.md)
