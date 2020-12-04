---
keywords: email;Email;e-mail;email destinations;salesforce;salesforce destination
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: Salesforce Marketing Cloud ist eine Digital-Marketing-Suite, die früher als ExactTarget bekannt war und mit der Sie Journeys für Besucher und Kunden erstellen und anpassen können, um deren Erlebnis zu personalisieren.
seo-description: Salesforce Marketing Cloud ist eine Digital-Marketing-Suite, die früher als ExactTarget bekannt war und mit der Sie Journeys für Besucher und Kunden erstellen und anpassen können, um deren Erlebnis zu personalisieren.
translation-type: tm+mt
source-git-commit: f2fdc3b75d275698a4b1e4c8969b1b840429c919
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 66%

---


# [!DNL Salesforce Marketing Cloud]

## Übersicht

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/de/products/marketing-cloud/email-marketing/) ist eine Digital-Marketing-Suite, die früher als ExactTarget bekannt war und mit der Sie Journeys für Besucher und Kunden erstellen und anpassen können, um deren Erlebnis zu personalisieren.

To send segment data to [!DNL Salesforce Marketing Cloud], you must first [connect the destination](#connect-destination) in Real-time CDP, and then [set up a data import](#import-data-into-salesforce) from your storage location into [!DNL Salesforce Marketing Cloud].

## Exporttyp {#export-type}

**Profil-basiert** - Sie exportieren alle Segmentmitglieder zusammen mit den gewünschten Segmentfeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm &quot;Attribute auswählen&quot;des Arbeitsablaufs für die [Ziel-Aktivierung](../../ui/activate-destinations.md#select-attributes)ausgewählt.

## Ziel verbinden {#connect-destination}

In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, select [!DNL Salesforce Marketing Cloud], then select **[!UICONTROL Connect destination]**.

![Mit Salesforce verbinden](../../assets/catalog/email-marketing/salesforce/catalog.png)

Wenn Sie im Schritt **[!UICONTROL Authentifizieren]** zuvor eine Verbindung zu Ihrem Cloud-Speicher-Ziel eingerichtet haben, wählen Sie **[!UICONTROL Vorhandenes Konto]** und eine Ihrer bestehenden Verbindungen aus. Sie können auch **[!UICONTROL Neues Konto]** auswählen, um eine neue Verbindung einzurichten. Geben Sie die Anmeldedaten für die Kontoauthentifizierung ein und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus. For [!DNL Salesforce Marketing Cloud], you can select between **[!UICONTROL SFTP with Password]** and **[!UICONTROL SFTP with SSH Key]**. Füllen Sie je nach Verbindungstyp die folgenden Informationen aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

Bei Verbindungen des Typs **[!UICONTROL SFTP mit Passwort]** müssen Sie Domäne, Port, Benutzernamen und Kennwort angeben.

Bei Verbindungen des Typs **[!UICONTROL SFTP mit SSH-Schlüssel]** müssen Sie Domäne, Port, Benutzernamen und SSH-Schlüssel angeben.

![Salesforce-Informationen ausfüllen](../../assets/catalog/email-marketing/salesforce/account-info.png)

Geben Sie im **[!UICONTROL Setup-Schritt]** die entsprechenden Informationen für Ihr Ziel ein (wie folgt):
- **[!UICONTROL Name]**: Wählen Sie einen passenden Namen für Ihr Ziel.
- **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für Ihr Ziel ein.
- **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad Ihres Speicherorts an, an dem die Echtzeit-Kundendatenplattform Ihre Exportdaten als CSV- oder tabulatorgetrennte Dateien hinterlegen wird.
- **[!UICONTROL Dateiformat]**: **[!UICONTROL CSV]** oder **[!UICONTROL TAB_DELIMITED]**. Wählen Sie das Dateiformat aus, mit dem Sie an Ihren Speicherort exportieren möchten.

![Salesforce-Basisinformationen](../../assets/catalog/email-marketing/salesforce/basic-information.png)

Klicken Sie auf **[!UICONTROL Ziel erstellen]**, nachdem Sie die oben stehenden Felder ausgefüllt haben. Ihr Ziel ist nun verbunden und Sie können für das Ziel [Segmente aktivieren](../../ui/activate-destinations.md).

## Aktivieren von Segmenten {#activate-segments}

Informationen zum Workflow für die Segmentaktivierung finden Sie unter [Profile und Segmente für ein Ziel aktivieren](../../ui/activate-destinations.md).

## Zielattribute {#destination-attributes}

When [activating segments](../../ui/activate-destinations.md) to the [!DNL Salesforce Marketing Cloud] destination, we recommend that you select a unique identifier from your [union schema](../../../profile/home.md#profile-fragments-and-union-schemas). Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weiterführende Informationen finden Sie unter [Auswählen, welche Schemafelder in Ihren exportierten Dateien als Zielattribute verwendet werden sollen](./overview.md#destination-attributes) (in E-Mail-Marketing-Zielen).

## Exportierte Daten {#exported-data}

For [!DNL Salesforce Marketing Cloud] destinations, Real-time CDP creates a tab-delimited `.txt` or `.csv` file in the storage location that you provided. Weitere Informationen zu den Dateien finden Sie unter [E-Mail-Marketing-Ziele und Cloud-Datenspeicherung-Ziele](../../ui/activate-destinations.md#esp-and-cloud-storage) im Tutorial zur Aktivierung von Segmenten.

## Set up data import into [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

After connecting Real-time CDP to your [!DNL Amazon S3] or SFTP storage, you must set up the data import from your storage location into [!DNL Salesforce Marketing Cloud]. To learn how to accomplish this, see [Importing Subscribers into Marketing Cloud from a File](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5) in the [!DNL Salesforce Help Center].