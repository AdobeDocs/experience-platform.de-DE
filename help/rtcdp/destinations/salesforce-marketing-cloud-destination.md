---
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: Salesforce Marketing Cloud ist eine Digital-Marketing-Suite, die früher als ExactTarget bekannt war und mit der Sie Journeys für Besucher und Kunden erstellen und anpassen können, um deren Erlebnis zu personalisieren.
seo-description: Salesforce Marketing Cloud ist eine Digital-Marketing-Suite, die früher als ExactTarget bekannt war und mit der Sie Journeys für Besucher und Kunden erstellen und anpassen können, um deren Erlebnis zu personalisieren.
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 83%

---


# Salesforce Marketing Cloud

## Übersicht

[Salesforce Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/email-marketing/) ist eine Digital-Marketing-Suite, die früher als ExactTarget bekannt war und mit der Sie Journeys für Besucher und Kunden erstellen und anpassen können, um deren Erlebnis zu personalisieren.

Um Segmentdaten an Salesforce Marketing Cloud zu senden, müssen Sie zunächst in der Echtzeit-Kundendatenplattform von Adobe das [Ziel verbinden](#connect-destination) und dann einen [Datenimport einrichten](#import-data-into-salesforce) von Ihrem Speicherort zu Salesforce Marketing Cloud.

## Ziel verbinden {#connect-destination}

1. Wählen Sie unter **[!UICONTROL Verbindungen > Ziele]** die Option „Salesforce Marketing Cloud“ und wählen Sie dann **[!UICONTROL Ziel verbinden]**.

   ![Mit Salesforce verbinden](/help/rtcdp/destinations/assets/connect-salesforce.png)

2. In the **[!UICONTROL Authentication]** step, if you had previously set up a connection to your cloud storage destination, select **[!UICONTROL Existing Account]** and select one of your existing connections. Sie können auch &quot; **[!UICONTROL Neues Konto]** &quot;auswählen, um eine neue Verbindung einzurichten. Geben Sie die Anmeldeinformationen für die Kontoauthentifizierung ein und wählen Sie **[!UICONTROL Mit Ziel verbinden]**. Bei Salesforce Marketing Cloud können Sie zwischen **[!UICONTROL SFTP mit Passwort]** und **[!UICONTROL SFTP mit SSH-Schlüssel]** wählen. Fill in the information below, depending on your connection type, and select **[!UICONTROL Connect to destination]**.

   Bei Verbindungen des Typs **[!UICONTROL SFTP mit Passwort]** müssen Sie Domäne, Port, Benutzernamen und Kennwort angeben.
Bei Verbindungen des Typs **[!UICONTROL SFTP mit SSH-Schlüssel]** müssen Sie Domäne, Port, Benutzernamen und SSH-Schlüssel angeben.

   ![Salesforce-Informationen ausfüllen](/help/rtcdp/destinations/assets/salesforce-authenticate.png)

3. In the **[!UICONTROL Setup]** step, fill in the relevant information for your destination as shown below:
   * **[!UICONTROL Name]**: Wählen Sie einen passenden Namen für Ihr Ziel.
   * **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für Ihr Ziel ein.
   * **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad Ihres Speicherorts an, an dem die Echtzeit-Kundendatenplattform Ihre Exportdaten als CSV- oder tabulatorgetrennte Dateien hinterlegen wird.
   * **[!UICONTROL Dateiformat]**: **[!UICONTROL CSV]** oder **[!UICONTROL TAB_DELIMITED]**. Wählen Sie das Dateiformat aus, mit dem Sie an Ihren Speicherort exportieren möchten.
   ![Salesforce-Basisinformationen](/help/rtcdp/destinations/assets/salesforce-basic-information.png)

4. Klicken Sie auf Ziel **[!UICONTROL erstellen]** , nachdem Sie die oben stehenden Felder ausgefüllt haben. Ihr Ziel ist nun verbunden und Sie können für das Ziel [Segmente aktivieren](/help/rtcdp/destinations/activate-destinations.md).

## Zielattribute {#destination-attributes}

Beim [Aktivieren von Segmenten](/help/rtcdp/destinations/activate-destinations.md) für das Salesforce Marketing Cloud-Ziel empfehlen wir, eine eindeutige Kennung aus Ihrem [Vereinigungsschema](../../profile/home.md#profile-fragments-and-union-schemas) auszuwählen. Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weiterführende Informationen finden Sie unter [Auswählen, welche Schemafelder in Ihren exportierten Dateien als Zielattribute verwendet werden sollen](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) (in E-Mail-Marketing-Zielen).

## Datenimport in Salesforce Marketing Cloud einrichten {#import-data-into-salesforce}

Nachdem Sie die Echtzeit-Kundendatenplattform mit Ihrem Amazon S3- oder SFTP-Speicher verbunden haben, müssen Sie den Datenimport von Ihrem Speicherort zu Salesforce Marketing Cloud einrichten. Weiterführende Informationen finden Sie im Salesforce Help Center unter [Abonnenten aus einer Datei in Marketing Cloud importieren](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5).