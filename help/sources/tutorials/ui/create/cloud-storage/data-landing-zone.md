---
title: Verbinden der Data Landing Zone mit Experience Platform über die Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Experience Platform-Benutzeroberfläche einen Quell-Connector für die Data Landing Zone erstellen.
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 10%

---

# Verbinden von [!DNL Data Landing Zone] mit Experience Platform über die Benutzeroberfläche

>[!IMPORTANT]
>
>Diese Seite ist spezifisch für den [!DNL Data Landing Zone]-Quell *Connector* Experience Platform. Informationen zum Herstellen einer Verbindung zum [!DNL Data Landing Zone]-*-*-Connector finden Sie auf [[!DNL Data Landing Zone] Zieldokumentationsseite](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] ist eine sichere, Cloud-basierte Dateispeichereinrichtung, um Dateien in Adobe Experience Platform zu importieren. Daten werden nach sieben Tagen automatisch aus dem [!DNL Data Landing Zone] gelöscht.

In diesem Tutorial finden Sie die Schritte zum Erstellen einer [!DNL Data Landing Zone]-Quellverbindung mithilfe der Benutzeroberfläche von Experience Platform.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

## Dateien von [!DNL Data Landing Zone] nach Experience Platform übertragen

>[!IMPORTANT]
>
> Um eine Verbindung zur Quelle herzustellen, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Quellen anzeigen]** und **[!UICONTROL Quellen verwalten]** . Lesen Sie die [Übersicht über die Zugriffssteuerung](../../../../../access-control/home.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchleiste finden.

Wählen Sie unter der Kategorie [!UICONTROL Cloud] die Option [!DNL Data Landing Zone] und dann **[!UICONTROL Daten hinzufügen]** aus.

![Der Quellkatalog mit ausgewählter Data Landing Zone.](../../../../images/tutorials/create/dlz/catalog.png)

Der Schritt [!UICONTROL Daten hinzufügen] wird angezeigt und bietet Ihnen eine Schnittstelle zur Auswahl und Vorschau der Daten, die Sie an Experience Platform übermitteln möchten.

* Der linke Teil der Benutzeroberfläche ist ein Ordnerbrowser, der eine Liste von Dateien aus Ihrem Container bereitstellt, die Sie dann in Experience Platform importieren können.
* Im rechten Teil der Benutzeroberfläche können Sie eine Vorschau von bis zu 100 Datenzeilen aus einer kompatiblen Datei anzeigen.

Wählen Sie die Datei aus, die Sie in Experience Platform importieren möchten, und warten Sie einige Augenblicke, bis die richtige Benutzeroberfläche in einem Vorschaubildschirm aktualisiert ist.

![Die Schnittstelle „Daten hinzufügen“ des Arbeitsbereichs „Quellen“.](../../../../images/tutorials/create/dlz/add-data.png)

>[!TIP]
>
>Experience Platform erkennt automatisch Eigenschafteninformationen der ausgewählten Datei, einschließlich Informationen zum Datenformat der Datei, zum angegebenen Spaltentrennzeichen und zum Komprimierungstyp.

In der Vorschauoberfläche können Sie den Inhalt und die Struktur einer Datei überprüfen. Standardmäßig zeigt die Vorschau-Benutzeroberfläche die erste Datei in dem ausgewählten Ordner an.

Um eine andere Datei in der Vorschau anzuzeigen, klicken Sie auf das Vorschausymbol neben dem Namen der Datei, die Sie überprüfen möchten.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Die Datenvorschauseite des Arbeitsbereichs „Quellen“.](../../../../images/tutorials/create/dlz/file-detection.png)

Eine detaillierte, schrittweise Anleitung zum Erstellen eines Datenflusses für eine Cloud-Speicherquelle finden Sie im Tutorial zum [&#x200B; eines Cloud-Datenflusses, um Daten in Experience Platform zu übertragen](../../dataflow/batch/cloud-storage.md).

## Abrufen Ihrer [!DNL Data Landing Zone] Anmeldedaten

[!DNL Data Landing Zone] ist eine -Quelle, die mit Ihrer Adobe Experience Platform-Quelllizenz geliefert wird. [!DNL Data Landing Zone] verwendet einen SAS-URI und eine auf SAS-Token basierende Authentifizierung. Sie können Ihre Authentifizierungsberechtigungen von der Seite [!UICONTROL Quellkatalog] abrufen.

Um Ihre Anmeldedaten abzurufen, wählen Sie die Karte **[!UICONTROL Data Landing Zone]** und kopieren Sie Ihre Anmeldedaten aus der rechten Leiste, die angezeigt wird.

![Eine Liste der Ansichtsoptionen für die Data Landing Zone.](../../../../images/tutorials/create/dlz/view-credentials.png)

Ein Pop-up wird angezeigt, in dem Ihr Container-Name, SAS-Token, Name des Speicherkontos, SAS-URI und Ablaufdatum angezeigt werden.

## [!DNL Data Landing Zone] aktualisieren

Ihre [!DNL Data Landing Zone]-Anmeldeinformationen laufen nach 90 Tagen automatisch ab und Sie müssen neue Anmeldeinformationen verwenden, um nach ihrem Ablauf erneut eine Verbindung zu [!DNL Data Landing Zone] herzustellen. Ihre Datenflüsse in Experience Platform sind von ablaufenden Anmeldeinformationen nicht betroffen, und Sie können mit Ihren neuen Anmeldeinformationen weiterhin mit neuen und vorhandenen Datenflüssen arbeiten.

Es gibt zwei Möglichkeiten, Ihre [!DNL Data Landing Zone]-Anmeldedaten zu aktualisieren:

>[!BEGINTABS]

>[!TAB Verwenden Sie die Quellkarte]

Um Ihre Anmeldeinformationen auf der Seite mit dem Quellkatalog zu aktualisieren, wählen Sie die Auslassungszeichen (**`...`**) auf der Karte [!DNL Data Landing Zone] und dann **[!UICONTROL Anmeldeinformationen aktualisieren]** aus.

![Aktualisieren Sie die Anmeldeinformationen mithilfe der Quellkarte.](../../../../images/tutorials/create/dlz/refresh-with-card.png)

Es wird ein Popup-Fenster angezeigt, in dem Sie zur Bestätigung aufgefordert werden, bevor Sie fortfahren können. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Anmeldedaten aktualisieren]** aus.

![Bestätigungsfenster für die Aktualisierung der Anmeldeinformationen.](../../../../images/tutorials/create/dlz/confirm.png)

>[!TAB Verwenden Sie die rechte Leiste]

Um Ihre Anmeldeinformationen über die rechte Leiste zu aktualisieren, wählen Sie die Quellkarte **[!UICONTROL Data Landing Zone]** und dann **[!UICONTROL Weitere Aktionen]** aus. Wählen Sie als Nächstes **[!UICONTROL Anmeldeinformationen aktualisieren]** und bestätigen Sie dann, indem Sie das Popup-Fenster verwenden, das angezeigt wird.

![Aktualisieren von Anmeldeinformationen über die rechte Leiste.](../../../../images/tutorials/create/dlz/refresh-with-right-rail.png)

>[!ENDTABS]

## Nächste Schritte

In diesem Tutorial haben Sie auf Ihren [!DNL Data Landing Zone]-Container zugegriffen und gelernt, Ihre Anmeldeinformationen abzurufen und zu aktualisieren. Sie können jetzt mit dem nächsten Tutorial zum Erstellen [&#x200B; Datenflusses fortfahren, um Daten von einem Cloud-Speicher in Experience Platform zu übertragen](../../dataflow/batch/cloud-storage.md).
