---
title: Oracle Responsys-Ziel
seo-title: Oracle Responsys-Ziel
description: Antworten ist ein Enterprise-E-Mail-Marketing-Tool für kanalübergreifende Marketingkampagnen, die von Oracle angeboten werden, um Interaktionen über E-Mail, Mobilgeräte, Display und Social zu personalisieren.
seo-description: Antworten ist ein Enterprise-E-Mail-Marketing-Tool für kanalübergreifende Marketingkampagnen, die von Oracle angeboten werden, um Interaktionen über E-Mail, Mobilgeräte, Display und Social zu personalisieren.
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Oracle Responsys

## Übersicht

[Antworten](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) ist ein Enterprise-E-Mail-Marketing-Tool für kanalübergreifende Marketingkampagnen, die von Oracle angeboten werden, um Interaktionen über E-Mail, Mobilgeräte, Display und Social zu personalisieren.

Um Segmentdaten an Oracle-Antworten zu senden, müssen Sie zunächst das Ziel[ in der Adobe Echtzeit-Kundendatenplattform ](#connect-destination)verbinden und dann einen Datenimport[ von Ihrem Speicherort in Oracle-Antworten ](#import-data-into-responsys)einrichten.

## Ziel verbinden {#connect-destination}

1. Wählen Sie unter **[!UICONTROL Verbindungen > Ziele]** die Option Oracle-Antworten und dann **[!UICONTROL Connect-Ziel]**.

   ![Mit Antworten verbinden](/help/rtcdp/destinations/assets/connect-oracle-responsys.png)

1. Wählen Sie im Verbindungsziel-Assistenten den **[!UICONTROL Verbindungstyp]** für Ihren Speicherort aus. Bei Oracle-Antworten können Sie zwischen **SFTP mit Kennwort** und **SFTP mit SSH-Schlüssel** wählen. Füllen Sie die folgenden Informationen je nach Verbindungstyp aus und wählen Sie **[!UICONTROL Verbinden]**.

   ![Assistenten zum Einrichten von Antworten](/help/rtcdp/destinations/assets/responsys-wizard.png)

   Für **SFTP mit Passwortverbindungen** müssen Sie Domäne, Port, Benutzername und Passwort angeben.
Für **SFTP mit SSH-Key** -Verbindungen müssen Sie Domäne, Port, Benutzername und SSH-Schlüssel angeben.

   ![Informationen zu Antworten ausfüllen](/help/rtcdp/destinations/assets/responsys-step2.png)

1. Geben Sie in den **Basisinformationen** die relevanten Informationen für Ihr Ziel ein, wie nachfolgend gezeigt:
   * **Name**: Wählen Sie einen relevanten Namen für Ihr Ziel.
   * **Beschreibung**: Geben Sie eine Beschreibung für Ihr Ziel ein.
   * **Ordnerpfad**: Geben Sie den Pfad in Ihrem Speicherort an, in dem CDP Ihre Exportdaten in Echtzeit als CSV- oder tabulatorgetrennte Dateien hinterlegt.
   * **Dateiformat**: **CSV** oder **TAB_DELIMITED**. Wählen Sie das Dateiformat aus, das Sie an Ihren Speicherort exportieren möchten.
   ![Grundlegende Informationen](/help/rtcdp/destinations/assets/responsys-basic-information.png)

1. Klicken Sie auf **Erstellen** , nachdem Sie die Felder in den **Grundinformationen** ausgefüllt haben. Ihr Ziel ist nun verbunden und Sie können Segmente[ an das Ziel ](/help/rtcdp/destinations/activate-destinations.md)aktivieren.

## Zielattribute {#destination-attributes}

Beim [Aktivieren von Segmenten](/help/rtcdp/destinations/activate-destinations.md) in das Oracle Responses-Ziel sollten Sie eine eindeutige Kennung aus Ihrem [Gewerkschaftsschema](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)auswählen. Wählen Sie den eindeutigen Bezeichner und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weitere Informationen finden Sie unter [Auswählen, welche Schemafelder als Zielattribute in Ihren exportierten Dateien](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) in E-Mail-Marketing-Zielen verwendet werden sollen.

## Datenimport in Oracle Responsys einrichten {#import-data-into-responsys}

Nachdem Sie die Echtzeit-CDP mit Ihrem Amazon S3- oder SFTP-Speicher verbunden haben, müssen Sie den Datenimport von Ihrem Speicherort in Oracle Responsys einrichten. Weitere Informationen dazu finden Sie unter [Importieren von Kontakten oder Konten](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) im Oracle Response Center.