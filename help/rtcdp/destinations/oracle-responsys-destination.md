---
title: Oracle Responsys-Ziel
seo-title: Oracle Responsys-Ziel
description: Responsys ist ein Enterprise-E-Mail-Marketing-Tool für kanalübergreifende Marketing-Kampagnen, das von Oracle angeboten wird und der Personalisierung von Interaktionen über E-Mail, Mobile, Display und Social Media hinweg dient.
seo-description: Responsys ist ein Enterprise-E-Mail-Marketing-Tool für kanalübergreifende Marketing-Kampagnen, das von Oracle angeboten wird und der Personalisierung von Interaktionen über E-Mail, Mobile, Display und Social Media hinweg dient.
translation-type: ht
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Oracle Responsys

## Übersicht

[Responsys](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) ist ein Enterprise-E-Mail-Marketing-Tool für kanalübergreifende Marketing-Kampagnen, das von Oracle angeboten wird und der Personalisierung von Interaktionen über E-Mail, Mobile, Display und Social Media hinweg dient.

Zum Senden von Segmentdaten an Oracle Responsys müssen Sie zunächst in der Echtzeit-Kundendatenplattform von Adobe das [Ziel verbinden](#connect-destination) und dann einen [Datenimport einrichten](#import-data-into-responsys) von Ihrem Speicherort zu Oracle Responsys.

## Ziel verbinden {#connect-destination}

1. Wählen Sie unter **[!UICONTROL Verbindungen > Ziele]** die Option „Oracle Responsys“ und dann **[!UICONTROL Ziel verbinden]**.

   ![Mit Responsys verbinden](/help/rtcdp/destinations/assets/connect-oracle-responsys.png)

1. Wählen Sie im Zielverbindungsassistenten den **[!UICONTROL Verbindungstyp]** für Ihren Speicherort aus. Bei Oracle Responsys können Sie zwischen **SFTP mit Passwort** und **SFTP mit SSH-Schlüssel** wählen. Füllen Sie je nach Verbindungstyp die folgenden Informationen aus und wählen Sie **[!UICONTROL Verbinden]**.

   ![Assistent zum Einrichten von Responsys](/help/rtcdp/destinations/assets/responsys-wizard.png)

   Bei Verbindungen des Typs **SFTP mit Passwort** müssen Sie Domäne, Port, Benutzernamen und Kennwort angeben.
Bei Verbindungen des Typs **SFTP mit SSH-Schlüssel** müssen Sie Domäne, Port, Benutzernamen und SSH-Schlüssel angeben.

   ![Responsys-Informationen ausfüllen](/help/rtcdp/destinations/assets/responsys-step2.png)

1. Geben Sie unter **Grundlegende Informationen** die entsprechenden Informationen für Ihr Ziel ein, wie nachfolgend dargestellt:
   * **Name**: Wählen Sie einen passenden Namen für Ihr Ziel.
   * **Beschreibung**: Geben Sie eine Beschreibung für Ihr Ziel ein.
   * **Ordnerpfad**: Geben Sie den Pfad Ihres Speicherorts an, an dem die Echtzeit-Kundendatenplattform Ihre Exportdaten als CSV- oder tabulatorgetrennte Dateien hinterlegen wird.
   * **Dateiformat**: **CSV** oder **TAB_DELIMITED**. Wählen Sie das Dateiformat aus, mit dem Sie an Ihren Speicherort exportieren möchten.
   ![Responsys-Basisinformationen](/help/rtcdp/destinations/assets/responsys-basic-information.png)

1. Klicken Sie auf **Erstellen**, nachdem Sie die Felder unter **Grundlegende Informationen** ausgefüllt haben. Ihr Ziel ist nun verbunden und Sie können für das Ziel [Segmente aktivieren](/help/rtcdp/destinations/activate-destinations.md).

## Zielattribute {#destination-attributes}

Beim [Aktivieren von Segmenten](/help/rtcdp/destinations/activate-destinations.md) für das Oracle Responsys-Ziel empfehlen wir, eine eindeutige Kennung aus Ihrem [Vereinigungsschema](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md) auszuwählen. Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weiterführende Informationen finden Sie unter [Auswählen, welche Schemafelder in Ihren exportierten Dateien als Zielattribute verwendet werden sollen](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) (in E-Mail-Marketing-Zielen).

## Datenimport in Oracle Responsys einrichten {#import-data-into-responsys}

Nachdem Sie die Echtzeit-Kundendatenplattform mit Ihrem Amazon S3- oder SFTP-Speicher verbunden haben, müssen Sie den Datenimport von Ihrem Speicherort zu Oracle Responsys einrichten. Weiterführende Informationen finden Sie unter [Kontakte oder Konten importieren](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) im Oracle Responsys Help Center.