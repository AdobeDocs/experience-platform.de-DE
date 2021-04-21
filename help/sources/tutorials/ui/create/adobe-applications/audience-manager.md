---
keywords: Experience Platform;Home;beliebte Themen;Audience Manager-Quellanschluss;Audience Manager;Audience-Manager-Anschluss
solution: Experience Platform
title: Erstellen einer Adobe Audience Manager-Quellverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Dieses Lernprogramm führt Sie durch die Schritte zum Erstellen von Quell-Connectors für Adobe Audience Manager, um Verbrauchererlebnis-Ereignis-Daten über die Benutzeroberfläche in Platform einzubringen.
exl-id: 90c4a719-aaad-4687-afd8-7a1c0c56f744
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 2%

---

# Erstellen einer Adobe Audience Manager-Quellverbindung in der Benutzeroberfläche

Dieses Lernprogramm führt Sie durch die Schritte zum Erstellen eines Quell-Connectors für Adobe Audience Manager, um Verbrauchererlebnis-Ereignis-Daten über die Benutzeroberfläche in Platform einzubringen.

## Erstellen einer Quellverbindung mit Adobe Audience Manager

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] zeigt eine Reihe von Quellen an, für die Sie ein Konto erstellen können.

Wählen Sie unter der Kategorie [!UICONTROL Adobe applications] **[!UICONTROL Adobe Audience Manager]** und dann **[!UICONTROL Configure]**.

![Katalog](../../../../images/tutorials/create/aam/catalog.png)

Der Schritt [!UICONTROL Eigenschaften und Segmente auswählen] wird angezeigt und bietet eine interaktive Oberfläche, über die Sie Ihre Eigenschaften, Segmente und Daten untersuchen und auswählen können.

* Das linke Bedienfeld der Oberfläche enthält die Optionen [!UICONTROL Eigenschaften und Segmente auswählen] sowie ein hierarchisches Verzeichnis aller verfügbaren Segmente.
* In der rechten Hälfte der Oberfläche können Sie mit ausgewählten Segmenten interagieren und bestimmte Daten aufrufen, die Sie verwenden möchten.

![add-data](../../../../images/tutorials/create/aam/add-data.png)

Um durch verfügbare Segmente zu navigieren, wählen Sie den Ordner aus dem Bedienfeld [!UICONTROL Alle Segmente] aus, auf den Sie zugreifen möchten. Wenn Sie einen Ordner auswählen, können Sie die Ordnerhierarchie durchlaufen und eine Liste von Segmenten zum Durchsuchen bereitstellen.

![segment-folder](../../../../images/tutorials/create/aam/segment-folder.png)

Nachdem Sie die gewünschten Segmente identifiziert und ausgewählt haben, wird auf der rechten Seite ein neuer Bereich mit Ihrer Liste der ausgewählten Elemente angezeigt. Sie können weiterhin auf verschiedene Ordner zugreifen und verschiedene Segmente für Ihre Verbindung auswählen. Wenn Sie weitere Segmente auswählen, wird das Bedienfeld auf der rechten Seite aktualisiert.

![select-data](../../../../images/tutorials/create/aam/select-data.png)

Alternativ können Sie die Felder **[!UICONTROL Alle Segmente]** und **[!UICONTROL Alle Eigenschaften]** auswählen. Wenn Sie alle Audience Manager auswählen, werden alle Segmente zur Plattform gebracht, während bei Auswahl aller Eigenschaften alle Eigenschaften des Erstanbieters aus dem Audience Manager aktiviert werden.

Sobald Sie fertig sind, wählen Sie **[!UICONTROL Weiter]**

![alle Segmente](../../../../images/tutorials/create/aam/all-segments.png)

Der Schritt [!UICONTROL Überprüfen] wird angezeigt, mit dem Sie die ausgewählten Eigenschaften und Segmente überprüfen können, bevor sie mit der Plattform verbunden sind. Details werden in den folgenden Kategorien gruppiert:

* **[!UICONTROL Verbindung]**: Zeigt die Quellplattform und den Status der Verbindung an.
* **[!UICONTROL Ausgewählte Daten]**: Zeigt die Anzahl der ausgewählten Segmente und aktivierten Eigenschaften an.

![überprüfen](../../../../images/tutorials/create/aam/review.png)

Nachdem Sie den Datenfluss überprüft haben, wählen Sie **[!UICONTROL Fertig stellen]** und lassen Sie etwas Zeit für die Erstellung des Datenflusses zu.

## Nächste Schritte

Während ein Audience Manager-Datendurchlauf aktiv ist, werden eingehende Daten automatisch in Echtzeit-Kundendaten erfasst. Sie können diese eingehenden Daten jetzt nutzen und mit dem Plattformsegmentierungsdienst Audiencen erstellen. Weitere Informationen finden Sie in den folgenden Dokumenten:

* [Übersicht über das Echtzeit-Kundenprofil](../../../../../profile/home.md)
* [Übersicht über den Segmentierungsdienst](../../../../../segmentation/home.md)
