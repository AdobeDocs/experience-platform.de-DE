---
title: Adobe Campaign
seo-title: Adobe Campaign
description: Adobe Campaign ist eine Reihe von Lösungen, mit denen Sie Kampagnen personalisieren und über alle Ihre Online- und Offlinekanäle hinweg bereitstellen können.
seo-description: Adobe Campaign ist eine Reihe von Lösungen, mit denen Sie Kampagnen personalisieren und über alle Ihre Online- und Offlinekanäle hinweg bereitstellen können.
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Adobe Campaign

## Übersicht

Adobe Campaign ist eine Reihe von Lösungen, mit denen Sie Kampagnen personalisieren und über alle Ihre Online- und Offlinekanäle hinweg bereitstellen können. Weitere Informationen finden Sie unter [Info zu Adobe Campaign Classic](https://docs.adobe.com/content/help/en/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) .

Um Segmentdaten an Adobe Campaign zu senden, müssen Sie zuerst das Ziel[ in der Adobe Echtzeit-Kundendatenplattform ](#connect-destination)verbinden und dann einen Datenimport[ von Ihrem Speicherort in Adobe Campaign ](#import-data-into-campaign)einrichten.

## Ziel verbinden {#connect-destination}

1. Wählen Sie unter **[!UICONTROL Verbindungen > Ziele]** Adobe Campaign und dann **[!UICONTROL Connect-Ziel]**.

   ![Verbindung zur Adobe-Kampagne](/help/rtcdp/destinations/assets/connect-adobe-campaign.png)

1. Wählen Sie im Verbindungsziel-Assistenten den **[!UICONTROL Verbindungstyp]** für Ihren Speicherort aus. Für Adobe Campaign können Sie zwischen **Amazon S3**, **SFTP mit Kennwort** und **SFTP mit SSH-Schlüssel** wählen. Füllen Sie die folgenden Informationen je nach Verbindungstyp aus und wählen Sie dann **[!UICONTROL Verbinden]**.

   ![Einrichten des Kampagnenassistenten](/help/rtcdp/destinations/assets/adobe-campaign-wizard.png)

   Für **S3** -Verbindungen müssen Sie die Zugriffsschlüssel-ID und den geheimen Zugriffsschlüssel angeben.
Für **SFTP mit Passwortverbindungen** müssen Sie Domäne, Port, Benutzername und Passwort angeben.
Für **SFTP mit SSH-Key** -Verbindungen müssen Sie Domäne, Port, Benutzername und SSH-Schlüssel angeben.

   ![Kampagneninformationen ausfüllen](/help/rtcdp/destinations/assets/adobe-campaign-step2.png)

1. Geben Sie in den **Basisinformationen** die relevanten Informationen für Ihr Ziel ein, wie nachfolgend gezeigt:
   * **Name**: Wählen Sie einen relevanten Namen für Ihr Ziel.
   * **Beschreibung**: Geben Sie eine Beschreibung für Ihr Ziel ein.
   * **Behältername**: *Für S3-Verbindungen*. Geben Sie den Speicherort Ihres S3-Behälters ein, in dem CDP Ihre Exportdaten als CSV- oder tabulatorgetrennte Dateien hinterlegt.
   * **Ordnerpfad**: Geben Sie den Pfad in Ihrem Speicherort an, in dem CDP Ihre Exportdaten in Echtzeit als CSV- oder tabulatorgetrennte Dateien hinterlegt.
   * **Dateiformat**: **CSV** oder **TAB_DELIMITED**. Wählen Sie das Dateiformat aus, das Sie an Ihren Speicherort exportieren möchten.
   ![Grundlegende Kampagneninformationen](/help/rtcdp/destinations/assets/adobe-campaign-basic-information.png)

1. Klicken Sie auf **Erstellen** , nachdem Sie die Felder in den **Grundinformationen** ausgefüllt haben. Ihr Ziel ist nun verbunden und Sie können Segmente[ an das Ziel ](/help/rtcdp/destinations/activate-destinations.md)aktivieren.

## Zielattribute {#destination-attributes}

Beim [Aktivieren von Segmenten](/help/rtcdp/destinations/activate-destinations.md) in das Adobe Campaign-Ziel sollten Sie eine eindeutige Kennung aus Ihrem [Gewerkschaftsschema](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)auswählen. Wählen Sie den eindeutigen Bezeichner und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weitere Informationen finden Sie unter [Auswählen, welche Schemafelder als Zielattribute in Ihren exportierten Dateien](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) in E-Mail-Marketing-Zielen verwendet werden sollen.


## Einrichten des Datenimports in Adobe Campaign {#import-data-into-campaign}

Nachdem Sie die Echtzeit-CDP mit Ihrem Amazon S3- oder SFTP-Speicher verbunden haben, müssen Sie den Datenimport von Ihrem Speicherort in Adobe Campaign einrichten. Informationen dazu finden Sie unter Daten [importieren](https://docs.adobe.com/content/help/en/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) in der Hilfe zu Adobe Campaign.