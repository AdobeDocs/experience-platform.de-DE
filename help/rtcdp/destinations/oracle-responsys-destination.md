---
title: Oracle Responsys-Ziel
seo-title: Oracle Responsys-Ziel
description: Responsys ist ein Enterprise-E-Mail-Marketing-Tool für kanalübergreifende Marketing-Kampagnen, das von Oracle angeboten wird und der Personalisierung von Interaktionen über E-Mail, Mobile, Display und Social Media hinweg dient.
seo-description: Responsys ist ein Enterprise-E-Mail-Marketing-Tool für kanalübergreifende Marketing-Kampagnen, das von Oracle angeboten wird und der Personalisierung von Interaktionen über E-Mail, Mobile, Display und Social Media hinweg dient.
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 75%

---


# Oracle Responsys

## Übersicht

[Responsys](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) ist ein Enterprise-E-Mail-Marketing-Tool für kanalübergreifende Marketing-Kampagnen, das von Oracle angeboten wird und der Personalisierung von Interaktionen über E-Mail, Mobile, Display und Social Media hinweg dient.

To send segment data to Oracle Responsys, you must first [connect to the destination](#connect-destination) in Adobe Real-time Customer Data Platform, and then [set up a data import](#import-data-into-responsys) from your storage location into Oracle Responsys.

## Ziel verbinden {#connect-destination}

1. Wählen Sie unter **[!UICONTROL Verbindungen > Ziele]** die Option „Oracle Responsys“ und dann **[!UICONTROL Ziel verbinden]**.

   ![Mit Responsys verbinden](/help/rtcdp/destinations/assets/connect-oracle-responsys.png)

2. In the **[!UICONTROL Authentication]** step, if you had previously set up a connection to your cloud storage destination, select **[!UICONTROL Existing Account]** and select one of your existing connections. Sie können auch &quot; **[!UICONTROL Neues Konto]** &quot;auswählen, um eine neue Verbindung einzurichten. Geben Sie die Anmeldeinformationen für die Kontoauthentifizierung ein und wählen Sie **[!UICONTROL Mit Ziel verbinden]**. Bei Oracle Responsys können Sie zwischen **[!UICONTROL SFTP mit Passwort]** und **[!UICONTROL SFTP mit SSH-Schlüssel]** wählen. Fill in the information below, depending on your connection type, and select **[!UICONTROL Connect to destination]**.

   Bei Verbindungen des Typs **[!UICONTROL SFTP mit Passwort]** müssen Sie Domäne, Port, Benutzernamen und Kennwort angeben.
Bei Verbindungen des Typs **[!UICONTROL SFTP mit SSH-Schlüssel]** müssen Sie Domäne, Port, Benutzernamen und SSH-Schlüssel angeben.

   ![Responsys-Informationen ausfüllen](/help/rtcdp/destinations/assets/responsys-authentication.png)

3. In the **[!UICONTROL Setup]** step, fill in the relevant information for your destination as shown below:
   * **[!UICONTROL Name]**: Wählen Sie einen passenden Namen für Ihr Ziel.
   * **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für Ihr Ziel ein.
   * **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad Ihres Speicherorts an, an dem die Echtzeit-Kundendatenplattform Ihre Exportdaten als CSV- oder tabulatorgetrennte Dateien hinterlegen wird.
   * **[!UICONTROL Dateiformat]**: **CSV** oder **TAB_DELIMITED**. Wählen Sie das Dateiformat aus, mit dem Sie an Ihren Speicherort exportieren möchten.
   ![Responsys-Basisinformationen](/help/rtcdp/destinations/assets/responsys-basic-information.png)

4. Klicken Sie auf Ziel **[!UICONTROL erstellen]** , nachdem Sie die oben stehenden Felder ausgefüllt haben. Ihr Ziel ist nun verbunden und Sie können für das Ziel [Segmente aktivieren](/help/rtcdp/destinations/activate-destinations.md).

## Zielattribute {#destination-attributes}

Beim [Aktivieren von Segmenten](/help/rtcdp/destinations/activate-destinations.md) für das Oracle Responsys-Ziel empfehlen wir, eine eindeutige Kennung aus Ihrem [Vereinigungsschema](../../profile/home.md#profile-fragments-and-union-schemas) auszuwählen. Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weiterführende Informationen finden Sie unter [Auswählen, welche Schemafelder in Ihren exportierten Dateien als Zielattribute verwendet werden sollen](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) (in E-Mail-Marketing-Zielen).

## Datenimport in Oracle Responsys einrichten {#import-data-into-responsys}

Nachdem Sie die Echtzeit-Kundendatenplattform mit Ihrem Amazon S3- oder SFTP-Speicher verbunden haben, müssen Sie den Datenimport von Ihrem Speicherort zu Oracle Responsys einrichten. Weiterführende Informationen finden Sie unter [Kontakte oder Konten importieren](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) im Oracle Responsys Help Center.