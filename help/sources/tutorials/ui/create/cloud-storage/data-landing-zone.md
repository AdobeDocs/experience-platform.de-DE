---
title: Data Landing Zone über die Benutzeroberfläche mit Platform verbinden
description: Erfahren Sie, wie Sie mithilfe der Benutzeroberfläche von Platform einen Quell-Connector für die Data Landing Zone erstellen.
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: 22f3b76c02e641d2f4c0dd7c0e5cc93038782836
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 19%

---

# Verbinden von [!DNL Data Landing Zone] mit Platform über die Benutzeroberfläche

>[!IMPORTANT]
>
>Diese Seite ist spezifisch für die [!DNL Data Landing Zone] *source* Connector in Experience Platform. Informationen zum Herstellen einer Verbindung zum [!DNL Data Landing Zone] *Ziel* Connector, siehe [[!DNL Data Landing Zone] Zieldokumentationsseite](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] ist eine sichere, Cloud-basierte Dateispeicheranlage, mit der Dateien in Adobe Experience Platform importiert werden können. Daten werden automatisch aus der [!DNL Data Landing Zone] nach sieben Tagen.

In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Data Landing Zone] Quellverbindung über die Platform-Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

## Importieren von Dateien aus [!DNL Data Landing Zone] Platform

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchleiste finden.

Unter dem [!UICONTROL Cloud-Speicher] category, select [!DNL Data Landing Zone] und wählen Sie **[!UICONTROL Daten hinzufügen]**.

![Der Quellkatalog mit ausgewählter Data Landing Zone.](../../../../images/tutorials/create/dlz/catalog.png)

Die [!UICONTROL Daten hinzufügen] angezeigt werden. Sie erhalten eine Oberfläche, über die Sie die Daten auswählen und eine Vorschau der Daten anzeigen können, die Sie in Platform laden möchten.

* Der linke Teil der Benutzeroberfläche ist ein Ordner-Browser, der Ihnen eine Liste der Dateien aus Ihrem Container bereitstellt, die Sie dann in Platform laden können.
* Im rechten Bereich der Benutzeroberfläche können Sie eine Vorschau von bis zu 100 Datenzeilen aus einer kompatiblen Datei anzeigen.

Wählen Sie die Datei aus, die Sie zum Experience Platform bringen möchten, und lassen Sie einige Augenblicke zu, bis die richtige Oberfläche in einem Vorschaubildschirm aktualisiert wird.

![Die Oberfläche zum Hinzufügen von Daten des Arbeitsbereichs &quot;Quellen&quot;.](../../../../images/tutorials/create/dlz/add-data.png)

>[!TIP]
>
>Platform erkennt automatisch Eigenschaftsinformationen der ausgewählten Datei, einschließlich Informationen zum Datenformat der Datei, zum festgelegten Spaltentrennzeichen und zum Komprimierungstyp.

Über die Vorschau-Oberfläche können Sie den Inhalt und die Struktur einer Datei überprüfen. Standardmäßig zeigt die Vorschaufunktion die erste Datei im ausgewählten Ordner an.

Um eine andere Datei in der Vorschau anzuzeigen, wählen Sie das Vorschausymbol neben dem Namen der Datei aus, die Sie überprüfen möchten.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Die Datenvorschauseite des Arbeitsbereichs &quot;Quellen&quot;.](../../../../images/tutorials/create/dlz/file-detection.png)

Eine ausführliche, schrittweise Anleitung zum Erstellen eines Datenflusses für eine Cloud-Speicherquelle finden Sie im Tutorial unter [Erstellen eines Cloud-Speicher-Datenflusses zum Übertragen von Daten an Platform](../../dataflow/batch/cloud-storage.md).

## Abrufen Ihrer [!DNL Data Landing Zone] Anmeldeinformationen

[!DNL Data Landing Zone] ist eine Quelle, die mit Ihrer Adobe Experience Platform Sources-Lizenz geliefert wird. [!DNL Data Landing Zone] verwendet eine SAS-URI- und SAS-Token-basierte Authentifizierung. Sie können Ihre Authentifizierungsberechtigungen von der [!UICONTROL Quellen-Katalog] Seite.

Um Ihre Anmeldedaten abzurufen, wählen Sie die **[!UICONTROL Data Landing Zone]** und kopieren Sie dann Ihre Anmeldedaten aus der rechten Leiste, die angezeigt wird.

![Eine Liste der Ansichtsoptionen für die Dateneinstiegszone.](../../../../images/tutorials/create/dlz/view-credentials.png)

Es wird ein Popup angezeigt, in dem Ihr Containername, Ihr SAS-Token, der Name des Speicherkontos, der SAS-URI und das Ablaufdatum angezeigt werden.

## Aktualisieren Sie Ihre [!DNL Data Landing Zone] Anmeldeinformationen

Ihre [!DNL Data Landing Zone] Die Anmeldedaten laufen nach 90 Tagen automatisch ab und Sie müssen neue Anmeldedaten verwenden, um eine erneute Verbindung zu [!DNL Data Landing Zone] nach Ablauf. Ihre Datenflüsse in Experience Platform sind nicht von ablaufenden Anmeldedaten betroffen und Sie können weiterhin mit neuen und vorhandenen Datenflüssen mit Ihren neuen Anmeldedaten arbeiten.

Es gibt zwei Möglichkeiten, Ihre [!DNL Data Landing Zone] Anmeldeinformationen:

>[!BEGINTABS]

>[!TAB Quellkarte verwenden]

Um Ihre Anmeldedaten auf der Quellkatalogseite zu aktualisieren, wählen Sie die Auslassungszeichen (**`...`**) in der [!DNL Data Landing Zone] und wählen Sie **[!UICONTROL Anmeldeinformationen aktualisieren]**.

![Aktualisieren Sie die Anmeldeinformationen mithilfe der Quellkarte.](../../../../images/tutorials/create/dlz/refresh-with-card.png)

Es wird ein Popup-Fenster mit einer Aufforderung zur Bestätigung angezeigt, bevor Sie fortfahren können. Wenn Sie bereit sind, wählen Sie **[!UICONTROL Anmeldeinformationen aktualisieren]**.

![Das Bestätigungsfenster für Anmeldedaten aktualisieren.](../../../../images/tutorials/create/dlz/confirm.png)

>[!TAB Verwenden der rechten Leiste]

Um Ihre Anmeldedaten in der rechten Leiste zu aktualisieren, wählen Sie die **[!UICONTROL Data Landing Zone]** Quellkarte und wählen Sie **[!UICONTROL Mehr Aktionen]**. Wählen Sie als Nächstes **[!UICONTROL Anmeldeinformationen aktualisieren]** und bestätigen Sie dann mit dem sich öffnenden Popup-Fenster.

![Aktualisieren Sie die Anmeldeinformationen in der rechten Leiste.](../../../../images/tutorials/create/dlz/refresh-with-right-rail.png)

>[!ENDTABS]

## Nächste Schritte

In diesem Tutorial haben Sie auf Ihre [!DNL Data Landing Zone] Container hinzugefügt und gelernt, wie Sie Ihre Anmeldedaten abrufen und aktualisieren können. Sie können jetzt mit dem nächsten Tutorial zum [Erstellen eines Datenflusses zum Übertragen von Daten aus einem Cloud-Speicher in Platform](../../dataflow/batch/cloud-storage.md).
