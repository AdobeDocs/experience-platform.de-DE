---
title: Oracle Responsys-Ziel
seo-title: Oracle Responsys-Ziel
description: Responsys ist ein Enterprise-E-Mail-Marketing-Tool für kanalübergreifende Marketing-Kampagnen, das von Oracle angeboten wird und der Personalisierung von Interaktionen über E-Mail, Mobile, Display und Social Media hinweg dient.
seo-description: Responsys ist ein Enterprise-E-Mail-Marketing-Tool für kanalübergreifende Marketing-Kampagnen, das von Oracle angeboten wird und der Personalisierung von Interaktionen über E-Mail, Mobile, Display und Social Media hinweg dient.
translation-type: tm+mt
source-git-commit: 336aa90cf1e059a92a36dd0ef3222ef6a6f5123b

---


# Oracle Responsys

## Übersicht

[Responsys](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) ist ein Enterprise-E-Mail-Marketing-Tool für kanalübergreifende Marketing-Kampagnen, das von Oracle angeboten wird und der Personalisierung von Interaktionen über E-Mail, Mobile, Display und Social Media hinweg dient.

To send segment data to Oracle Responsys, you must first [connect to the destination](#connect-destination) in Adobe Real-time Customer Data Platform, and then [set up a data import](#import-data-into-responsys) from your storage location into Oracle Responsys.

## Ziel verbinden {#connect-destination}

1. Wählen Sie **[!UICONTROL Connections > Destinations]** unter &quot;Oracle-Antworten&quot;die Option **[!UICONTROL Connect destination]**.

   ![Mit Responsys verbinden](/help/rtcdp/destinations/assets/connect-oracle-responsys.png)

2. Wenn Sie zuvor eine Verbindung zum Ziel Ihrer Cloud-Datenspeicherung eingerichtet haben, wählen Sie **[!UICONTROL Authentication]** im Schritt eine der vorhandenen Verbindungen aus **[!UICONTROL Existing Account]** und wählen Sie sie aus. Sie können auch eine neue Verbindung einrichten **[!UICONTROL New Account]** . Geben Sie Ihre Kontoauthentifizierungsdaten ein und wählen Sie **[!UICONTROL Connect to destination]**. Bei Oracle-Antworten können Sie zwischen **[!UICONTROL SFTP with Password]** und **[!UICONTROL SFTP with SSH Key]** wählen. Fill in the information below, depending on your connection type, and select **[!UICONTROL Connect to destination]**.

   For **[!UICONTROL SFTP with Password]** connections, you must provide Domain, Port, Username, and Password.
Für **[!UICONTROL SFTP with SSH Key]** Verbindungen müssen Sie Domäne, Anschluss, Benutzername und SSH-Schlüssel angeben.

   ![Responsys-Informationen ausfüllen](/help/rtcdp/destinations/assets/responsys-authentication.png)

3. In the **[!UICONTROL Setup]** step, fill in the relevant information for your destination as shown below:
   * **[!UICONTROL Name]**: Wählen Sie einen passenden Namen für Ihr Ziel.
   * **[!UICONTROL Description]**: Geben Sie eine Beschreibung für Ihr Ziel ein.
   * **[!UICONTROL Folder Path]**: Geben Sie den Pfad in Ihrer Datenspeicherung an, in dem CDP Ihre Exportdaten als CSV- oder tabulatorgetrennte Dateien hinterlegt.
   * **[!UICONTROL File Format]**: **CSV** oder **TAB_DELIMITED**. Wählen Sie das Dateiformat aus, mit dem Sie an Ihren Speicherort exportieren möchten.
   ![Responsys-Basisinformationen](/help/rtcdp/destinations/assets/responsys-basic-information.png)

4. Klicken Sie auf **[!UICONTROL Create destination]** , nachdem Sie die oben stehenden Felder ausgefüllt haben. Ihr Ziel ist nun verbunden und Sie können für das Ziel [Segmente aktivieren](/help/rtcdp/destinations/activate-destinations.md).

## Zielattribute {#destination-attributes}

Beim [Aktivieren von Segmenten](/help/rtcdp/destinations/activate-destinations.md) für das Oracle Responsys-Ziel empfehlen wir, eine eindeutige Kennung aus Ihrem [Vereinigungsschema](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md) auszuwählen. Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weiterführende Informationen finden Sie unter [Auswählen, welche Schemafelder in Ihren exportierten Dateien als Zielattribute verwendet werden sollen](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) (in E-Mail-Marketing-Zielen).

## Datenimport in Oracle Responsys einrichten {#import-data-into-responsys}

Nachdem Sie die Echtzeit-Kundendatenplattform mit Ihrem Amazon S3- oder SFTP-Speicher verbunden haben, müssen Sie den Datenimport von Ihrem Speicherort zu Oracle Responsys einrichten. Weiterführende Informationen finden Sie unter [Kontakte oder Konten importieren](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) im Oracle Responsys Help Center.