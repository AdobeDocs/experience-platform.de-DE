---
title: Adobe Campaign
seo-title: Adobe Campaign
description: Adobe Campaign umfasst verschiedene Lösungen, mit denen Sie Kampagnen über alle Ihre Online- und Offline-Kanäle hinweg personalisieren und bereitstellen können.
seo-description: Adobe Campaign umfasst verschiedene Lösungen, mit denen Sie Kampagnen über alle Ihre Online- und Offline-Kanäle hinweg personalisieren und bereitstellen können.
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87

---


# Adobe Campaign

## Übersicht

Adobe Campaign umfasst verschiedene Lösungen, mit denen Sie Kampagnen über alle Ihre Online- und Offline-Kanäle hinweg personalisieren und bereitstellen können. Weiterführende Informationen finden Sie unter [Info zu Adobe Campaign Classic](https://docs.adobe.com/content/help/en/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html).

Zum Senden von Segmentdaten an Adobe Campaign müssen Sie zuerst in der Echtzeit-Kundendatenplattform von Adobe das [Ziel verbinden](#connect-destination) und dann einen [Datenimport](#import-data-into-campaign) von Ihrem Speicherort zu Adobe Campaign einrichten.

## Ziel verbinden {#connect-destination}

1. Wählen Sie **[!UICONTROL Connections > Destinations]** unter &quot;Adobe Campaign&quot;die Option **[!UICONTROL Connect destination]**.

   ![Mit Adobe Campaign verbinden](/help/rtcdp/destinations/assets/connect-adobe-campaign.png)

1. In the Connect destination workflow, select the **[!UICONTROL Connection type]** for your storage location. Bei Adobe Campaign können Sie zwischen **[!UICONTROL Amazon S3]** und **[!UICONTROL SFTP with Password]** wählen **[!UICONTROL SFTP with SSH Key]**. Fill in the information below, depending on your connection type, then select **[!UICONTROL Connect]**.

   ![Assistent zum Einrichten von Campaign](/help/rtcdp/destinations/assets/adobe-campaign-wizard.png)

   Bei Verbindungen des Typs **[!UICONTROL Amazon S3]** müssen Sie die Zugriffsschlüsselkennung und den geheimen Zugriffsschlüssel angeben.
For **[!UICONTROL SFTP with Password]** connections, you must provide Domain, Port, Username, and Password.
Für **[!UICONTROL SFTP with SSH Key]** Verbindungen müssen Sie Domäne, Anschluss, Benutzername und SSH-Schlüssel angeben.

   ![Campaign-Informationen ausfüllen](/help/rtcdp/destinations/assets/adobe-campaign-step2.png)

1. In **[!UICONTROL Basic Information]**, fill in the relevant information for your destination, as shown below:
   * **[!UICONTROL Name]**: Wählen Sie einen passenden Namen für Ihr Ziel.
   * **[!UICONTROL Description]**: Geben Sie eine Beschreibung für Ihr Ziel ein.
   * **[!UICONTROL Bucket Name]**: *Für S3-Verbindungen*. Geben Sie den Speicherort Ihres S3-Buckets ein, an dem die Echtzeit-Kundendatenplattform Ihre Exportdaten als CSV- oder tabulatorgetrennte Dateien hinterlegen wird.
   * **[!UICONTROL Folder Path]**: Geben Sie den Pfad in Ihrer Datenspeicherung an, in dem CDP Ihre Exportdaten als CSV- oder tabulatorgetrennte Dateien hinterlegt.
   * **[!UICONTROL File Format]**: **CSV** oder **TAB_DELIMITED**. Wählen Sie das Dateiformat aus, mit dem Sie an Ihren Speicherort exportieren möchten.
   ![Allgemeine Informationen zu Campaign](/help/rtcdp/destinations/assets/adobe-campaign-basic-information.png)

1. Klicken Sie auf **[!UICONTROL Create]** , nachdem Sie die oben stehenden Felder ausgefüllt haben. Ihr Ziel ist nun verbunden und Sie können für das Ziel [Segmente aktivieren](/help/rtcdp/destinations/activate-destinations.md).

## Zielattribute {#destination-attributes}

Beim [Aktivieren von Segmenten](/help/rtcdp/destinations/activate-destinations.md) für das Adobe Campaign-Ziel empfehlen wir, eine eindeutige Kennung aus Ihrem [Vereinigungsschema](../../profile/home.md#profile-fragments-and-union-schemas) auszuwählen. Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weiterführende Informationen finden Sie unter [Auswählen, welche Schemafelder in Ihren exportierten Dateien als Zielattribute verwendet werden sollen](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) (in E-Mail-Marketing-Zielen).


## Datenimport in Adobe Campaign einrichten {#import-data-into-campaign}

Nachdem Sie die Echtzeit-Kundendatenplattform mit Ihrem Amazon S3- oder SFTP-Speicher verbunden haben, müssen Sie den Datenimport von Ihrem Speicherort zu Adobe Campaign einrichten. Weiterführende Informationen finden Sie in der Hilfsdokumentation zu Adobe Campaign unter [Importieren von Daten](https://docs.adobe.com/content/help/en/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html).