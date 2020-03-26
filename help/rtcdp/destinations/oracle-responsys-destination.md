---
title: Oracle Responsys-Ziel
seo-title: Oracle Responsys-Ziel
description: Responsys ist ein Enterprise-E-Mail-Marketing-Tool für kanalübergreifende Marketing-Kampagnen, das von Oracle angeboten wird und der Personalisierung von Interaktionen über E-Mail, Mobile, Display und Social Media hinweg dient.
seo-description: Responsys ist ein Enterprise-E-Mail-Marketing-Tool für kanalübergreifende Marketing-Kampagnen, das von Oracle angeboten wird und der Personalisierung von Interaktionen über E-Mail, Mobile, Display und Social Media hinweg dient.
translation-type: tm+mt
source-git-commit: c3fe5753fb23f99076f9c85b4e07af2d25a121a9

---


# Oracle Responsys

## Übersicht

[Responsys](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) ist ein Enterprise-E-Mail-Marketing-Tool für kanalübergreifende Marketing-Kampagnen, das von Oracle angeboten wird und der Personalisierung von Interaktionen über E-Mail, Mobile, Display und Social Media hinweg dient.

To send segment data to Oracle Responsys, you must first [connect to the destination](#connect-destination) in Adobe Real-time Customer Data Platform, and then [set up a data import](#import-data-into-responsys) from your storage location into Oracle Responsys.

## Ziel verbinden {#connect-destination}

1. Wählen Sie **[!UICONTROL Connections > Destinations]** unter &quot;Oracle-Antworten&quot;die Option **[!UICONTROL Connect destination]**.

   ![Mit Responsys verbinden](/help/rtcdp/destinations/assets/connect-oracle-responsys.png)

2. Wenn Sie im Schritt **Authentifizierung** zuvor eine Verbindung zu Ihrem Cloud-Datenspeicherung-Ziel eingerichtet haben, wählen Sie eine Ihrer bestehenden Verbindungen aus **[!UICONTROL Existing Account]** und wählen Sie sie aus. Sie können auch eine neue Verbindung einrichten **[!UICONTROL New Account]** . Geben Sie Ihre Kontoauthentifizierungsdaten ein und wählen Sie **[!UICONTROL Connect to destination]**. Bei Oracle Responsys können Sie zwischen **SFTP mit Passwort** und **SFTP mit SSH-Schlüssel** wählen. Fill in the information below, depending on your connection type, and select **[!UICONTROL Connect to destination]**.

   Bei Verbindungen des Typs **SFTP mit Passwort** müssen Sie Domäne, Port, Benutzernamen und Kennwort angeben.
Bei Verbindungen des Typs **SFTP mit SSH-Schlüssel** müssen Sie Domäne, Port, Benutzernamen und SSH-Schlüssel angeben.

   ![Responsys-Informationen ausfüllen](/help/rtcdp/destinations/assets/responsys-authentication.png)

3. In the **Setup** step, fill in the relevant information for your destination as shown below:
   * **Name**: Wählen Sie einen passenden Namen für Ihr Ziel.
   * **Beschreibung**: Geben Sie eine Beschreibung für Ihr Ziel ein.
   * **Ordnerpfad**: Geben Sie den Pfad Ihres Speicherorts an, an dem die Echtzeit-Kundendatenplattform Ihre Exportdaten als CSV- oder tabulatorgetrennte Dateien hinterlegen wird.
   * **Dateiformat**: **CSV** oder **TAB_DELIMITED**. Wählen Sie das Dateiformat aus, mit dem Sie an Ihren Speicherort exportieren möchten.
   ![Responsys-Basisinformationen](/help/rtcdp/destinations/assets/responsys-basic-information.png)

4. Klicken Sie auf Ziel **erstellen** , nachdem Sie die oben stehenden Felder ausgefüllt haben. Ihr Ziel ist nun verbunden und Sie können für das Ziel [Segmente aktivieren](/help/rtcdp/destinations/activate-destinations.md).

## Zielattribute {#destination-attributes}

Beim [Aktivieren von Segmenten](/help/rtcdp/destinations/activate-destinations.md) für das Oracle Responsys-Ziel empfehlen wir, eine eindeutige Kennung aus Ihrem [Vereinigungsschema](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md) auszuwählen. Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weiterführende Informationen finden Sie unter [Auswählen, welche Schemafelder in Ihren exportierten Dateien als Zielattribute verwendet werden sollen](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) (in E-Mail-Marketing-Zielen).

## Datenimport in Oracle Responsys einrichten {#import-data-into-responsys}

Nachdem Sie die Echtzeit-Kundendatenplattform mit Ihrem Amazon S3- oder SFTP-Speicher verbunden haben, müssen Sie den Datenimport von Ihrem Speicherort zu Oracle Responsys einrichten. Weiterführende Informationen finden Sie unter [Kontakte oder Konten importieren](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) im Oracle Responsys Help Center.