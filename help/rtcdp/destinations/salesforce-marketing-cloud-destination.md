---
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: Salesforce Marketing Cloud ist eine digitale Marketing-Suite, die früher als ExactTarget bezeichnet wurde und mit der Sie Reisen für Besucher und Kunden erstellen und anpassen können, um deren Erlebnis zu personalisieren.
seo-description: Salesforce Marketing Cloud ist eine digitale Marketing-Suite, die früher als ExactTarget bezeichnet wurde und mit der Sie Reisen für Besucher und Kunden erstellen und anpassen können, um deren Erlebnis zu personalisieren.
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Salesforce Marketing Cloud

## Übersicht

[Salesforce Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/email-marketing/) ist eine digitale Marketing-Suite, die früher als ExactTarget bezeichnet wurde und mit der Sie Reisen für Besucher und Kunden erstellen und anpassen können, um deren Erlebnis zu personalisieren.

Um Segmentdaten an die Salesforce Marketing Cloud zu senden, müssen Sie zunächst das Ziel[ in Adobe Echtzeit-CDP ](#connect-destination)verbinden und dann einen Datenimport[ von Ihrem Speicherort in die Salesforce Marketing Cloud ](#import-data-into-salesforce)einrichten.

## Ziel verbinden {#connect-destination}

1. Wählen Sie unter **[!UICONTROL Verbindungen > Ziele]** Salesforce Marketing Cloud und wählen Sie dann **[!UICONTROL Connect-Ziel]**.

   ![Verbindung zu Salesforce](/help/rtcdp/destinations/assets/connect-salesforce.png)

1. Wählen Sie im Verbindungsziel-Assistenten den **[!UICONTROL Verbindungstyp]** für Ihren Speicherort aus. Bei Salesforce Marketing Cloud können Sie zwischen **SFTP mit Kennwort** und **SFTP mit SSH-Schlüssel** wählen. Füllen Sie die folgenden Informationen je nach Verbindungstyp aus und wählen Sie **[!UICONTROL Verbinden]**.

   ![Salesforce-Assistenten einrichten](/help/rtcdp/destinations/assets/salesforce-step1.png)

   Für **SFTP mit Passwortverbindungen** müssen Sie Domäne, Port, Benutzername und Passwort angeben.
Für **SFTP mit SSH-Key** -Verbindungen müssen Sie Domäne, Port, Benutzername und SSH-Schlüssel angeben.

   ![Salesforce-Informationen ausfüllen](/help/rtcdp/destinations/assets/salesforce-wizard.png)

1. Geben Sie in den **Basisinformationen** die relevanten Informationen für Ihr Ziel ein, wie nachfolgend gezeigt:
   * **Name**: Wählen Sie einen relevanten Namen für Ihr Ziel.
   * **Beschreibung**: Geben Sie eine Beschreibung für Ihr Ziel ein.
   * **Ordnerpfad**: Geben Sie den Pfad in Ihrem Speicherort an, in dem CDP Ihre Exportdaten in Echtzeit als CSV- oder tabulatorgetrennte Dateien hinterlegt.
   * **Dateiformat**: **CSV** oder **TAB_DELIMITED**. Wählen Sie das Dateiformat aus, das Sie an Ihren Speicherort exportieren möchten.
   ![Grundlegende Informationen](/help/rtcdp/destinations/assets/salesforce-basic-information.png)

1. Klicken Sie auf **Erstellen** , nachdem Sie die Felder in den **Grundinformationen** ausgefüllt haben. Ihr Ziel ist nun verbunden und Sie können Segmente[ an das Ziel ](/help/rtcdp/destinations/activate-destinations.md)aktivieren.

## Zielattribute {#destination-attributes}

Beim [Aktivieren von Segmenten](/help/rtcdp/destinations/activate-destinations.md) in das Ziel der Salesforce Marketing Cloud sollten Sie eine eindeutige Kennung aus Ihrem [Gewerkschaftsschema](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)auswählen. Wählen Sie den eindeutigen Bezeichner und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weitere Informationen finden Sie unter [Auswählen, welche Schemafelder als Zielattribute in Ihren exportierten Dateien](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) in E-Mail-Marketing-Zielen verwendet werden sollen.

## Einrichten des Datenimports in die Salesforce Marketing Cloud {#import-data-into-salesforce}

Nachdem Sie die Echtzeit-CDP mit Ihrem Amazon S3- oder SFTP-Speicher verbunden haben, müssen Sie den Datenimport von Ihrem Speicherort in die Salesforce Marketing Cloud einrichten. Weitere Informationen dazu finden Sie unter [Importieren von Abonnenten aus einer Datei](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&type=5) in die Marketing Cloud im Salesforce-Hilfe-Center.