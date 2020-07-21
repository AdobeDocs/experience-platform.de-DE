---
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: Salesforce Marketing Cloud ist eine Digital-Marketing-Suite, die früher als ExactTarget bekannt war und mit der Sie Journeys für Besucher und Kunden erstellen und anpassen können, um deren Erlebnis zu personalisieren.
seo-description: Salesforce Marketing Cloud ist eine Digital-Marketing-Suite, die früher als ExactTarget bekannt war und mit der Sie Journeys für Besucher und Kunden erstellen und anpassen können, um deren Erlebnis zu personalisieren.
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 75%

---


# [!DNL Salesforce Marketing Cloud]

## Übersicht

[!DNL Salesforce Marketing Cloud](https://www.salesforce.com/de/products/marketing-cloud/email-marketing/) ist eine Digital-Marketing-Suite, die früher als ExactTarget bekannt war und mit der Sie Journeys für Besucher und Kunden erstellen und anpassen können, um deren Erlebnis zu personalisieren.

To send segment data to [!DNL Salesforce Marketing Cloud], you must first [connect the destination](#connect-destination) in Adobe Real-time CDP, and then [set up a data import](#import-data-into-salesforce) from your storage location into [!DNL Salesforce Marketing Cloud].

## Ziel verbinden {#connect-destination}

1. In **[!UICONTROL Connections > Destinations]**, select [!DNL Salesforce Marketing Cloud], then select **[!UICONTROL Connect destination]**.

   ![Mit Salesforce verbinden](/help/rtcdp/destinations/assets/connect-salesforce.png)

2. Wenn Sie im Schritt **[!UICONTROL Authentifizieren]** zuvor eine Verbindung zu Ihrem Cloud-Speicher-Ziel eingerichtet haben, wählen Sie **[!UICONTROL Vorhandenes Konto]** und eine Ihrer bestehenden Verbindungen aus. Sie können auch **[!UICONTROL Neues Konto]** auswählen, um eine neue Verbindung einzurichten. Geben Sie die Anmeldedaten für die Kontoauthentifizierung ein und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus. For [!DNL Salesforce Marketing Cloud], you can select between **[!UICONTROL SFTP with Password]** and **[!UICONTROL SFTP with SSH Key]**. Füllen Sie je nach Verbindungstyp die folgenden Informationen aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

   Bei Verbindungen des Typs **[!UICONTROL SFTP mit Passwort]** müssen Sie Domäne, Port, Benutzernamen und Kennwort angeben.
Bei Verbindungen des Typs **[!UICONTROL SFTP mit SSH-Schlüssel]** müssen Sie Domäne, Port, Benutzernamen und SSH-Schlüssel angeben.

   ![Salesforce-Informationen ausfüllen](/help/rtcdp/destinations/assets/salesforce-authenticate.png)

3. Geben Sie im **[!UICONTROL Setup-Schritt]** die entsprechenden Informationen für Ihr Ziel ein (wie folgt):
   * **[!UICONTROL Name]**: Wählen Sie einen passenden Namen für Ihr Ziel.
   * **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für Ihr Ziel ein.
   * **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad Ihres Speicherorts an, an dem die Echtzeit-Kundendatenplattform Ihre Exportdaten als CSV- oder tabulatorgetrennte Dateien hinterlegen wird.
   * **[!UICONTROL Dateiformat]**: **[!UICONTROL CSV]** oder **[!UICONTROL TAB_DELIMITED]**. Wählen Sie das Dateiformat aus, mit dem Sie an Ihren Speicherort exportieren möchten.

   ![Salesforce-Basisinformationen](/help/rtcdp/destinations/assets/salesforce-basic-information.png)

4. Klicken Sie auf **[!UICONTROL Ziel erstellen]**, nachdem Sie die oben stehenden Felder ausgefüllt haben. Ihr Ziel ist nun verbunden und Sie können für das Ziel [Segmente aktivieren](/help/rtcdp/destinations/activate-destinations.md).

## Zielattribute {#destination-attributes}

When [activating segments](/help/rtcdp/destinations/activate-destinations.md) to the [!DNL Salesforce Marketing Cloud] destination, we recommend that you select a unique identifier from your [union schema](../../profile/home.md#profile-fragments-and-union-schemas). Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weiterführende Informationen finden Sie unter [Auswählen, welche Schemafelder in Ihren exportierten Dateien als Zielattribute verwendet werden sollen](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) (in E-Mail-Marketing-Zielen).

## Set up data import into [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

After connecting Real-time CDP to your Amazon S3 or SFTP storage, you must set up the data import from your storage location into [!DNL Salesforce Marketing Cloud]. To learn how to accomplish this, see [Importing Subscribers into Marketing Cloud from a File](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5) in the [!DNL Salesforce Help Center].