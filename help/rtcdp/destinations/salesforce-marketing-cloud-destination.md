---
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: Salesforce Marketing Cloud ist eine Digital-Marketing-Suite, die früher als ExactTarget bekannt war und mit der Sie Journeys für Besucher und Kunden erstellen und anpassen können, um deren Erlebnis zu personalisieren.
seo-description: Salesforce Marketing Cloud ist eine Digital-Marketing-Suite, die früher als ExactTarget bekannt war und mit der Sie Journeys für Besucher und Kunden erstellen und anpassen können, um deren Erlebnis zu personalisieren.
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87

---


# Salesforce Marketing Cloud

## Übersicht

[Salesforce Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/email-marketing/) ist eine Digital-Marketing-Suite, die früher als ExactTarget bekannt war und mit der Sie Journeys für Besucher und Kunden erstellen und anpassen können, um deren Erlebnis zu personalisieren.

Um Segmentdaten an Salesforce Marketing Cloud zu senden, müssen Sie zunächst in der Echtzeit-Kundendatenplattform von Adobe das [Ziel verbinden](#connect-destination) und dann einen [Datenimport einrichten](#import-data-into-salesforce) von Ihrem Speicherort zu Salesforce Marketing Cloud.

## Ziel verbinden {#connect-destination}

1. Wählen Sie **[!UICONTROL Connections > Destinations]** Salesforce Marketing Cloud und dann **[!UICONTROL Connect destination]**.

   ![Mit Salesforce verbinden](/help/rtcdp/destinations/assets/connect-salesforce.png)

2. Wenn Sie zuvor eine Verbindung zum Ziel Ihrer Cloud-Datenspeicherung eingerichtet haben, wählen Sie **[!UICONTROL Authentication]** im Schritt eine der vorhandenen Verbindungen aus **[!UICONTROL Existing Account]** und wählen Sie sie aus. Sie können auch eine neue Verbindung einrichten **[!UICONTROL New Account]** . Geben Sie Ihre Kontoauthentifizierungsdaten ein und wählen Sie **[!UICONTROL Connect to destination]**. Bei Salesforce Marketing Cloud können Sie zwischen **[!UICONTROL SFTP with Password]** und **[!UICONTROL SFTP with SSH Key]** wählen. Fill in the information below, depending on your connection type, and select **[!UICONTROL Connect to destination]**.

   For **[!UICONTROL SFTP with Password]** connections, you must provide Domain, Port, Username, and Password.
Für **[!UICONTROL SFTP with SSH Key]** Verbindungen müssen Sie Domäne, Anschluss, Benutzername und SSH-Schlüssel angeben.

   ![Salesforce-Informationen ausfüllen](/help/rtcdp/destinations/assets/salesforce-authenticate.png)

3. In the **[!UICONTROL Setup]** step, fill in the relevant information for your destination as shown below:
   * **[!UICONTROL Name]**: Wählen Sie einen passenden Namen für Ihr Ziel.
   * **[!UICONTROL Description]**: Geben Sie eine Beschreibung für Ihr Ziel ein.
   * **[!UICONTROL Folder Path]**: Geben Sie den Pfad in Ihrer Datenspeicherung an, in dem CDP Ihre Exportdaten als CSV- oder tabulatorgetrennte Dateien hinterlegt.
   * **[!UICONTROL File Format]**: **[!UICONTROL CSV]** oder **[!UICONTROL TAB_DELIMITED]**. Wählen Sie das Dateiformat aus, mit dem Sie an Ihren Speicherort exportieren möchten.
   ![Salesforce-Basisinformationen](/help/rtcdp/destinations/assets/salesforce-basic-information.png)

4. Klicken Sie auf **[!UICONTROL Create destination]** , nachdem Sie die oben stehenden Felder ausgefüllt haben. Ihr Ziel ist nun verbunden und Sie können für das Ziel [Segmente aktivieren](/help/rtcdp/destinations/activate-destinations.md).

## Zielattribute {#destination-attributes}

Beim [Aktivieren von Segmenten](/help/rtcdp/destinations/activate-destinations.md) für das Salesforce Marketing Cloud-Ziel empfehlen wir, eine eindeutige Kennung aus Ihrem [Vereinigungsschema](../../profile/home.md#profile-fragments-and-union-schemas) auszuwählen. Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weiterführende Informationen finden Sie unter [Auswählen, welche Schemafelder in Ihren exportierten Dateien als Zielattribute verwendet werden sollen](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) (in E-Mail-Marketing-Zielen).

## Datenimport in Salesforce Marketing Cloud einrichten {#import-data-into-salesforce}

Nachdem Sie die Echtzeit-Kundendatenplattform mit Ihrem Amazon S3- oder SFTP-Speicher verbunden haben, müssen Sie den Datenimport von Ihrem Speicherort zu Salesforce Marketing Cloud einrichten. Weiterführende Informationen finden Sie im Salesforce Help Center unter [Abonnenten aus einer Datei in Marketing Cloud importieren](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&type=5).