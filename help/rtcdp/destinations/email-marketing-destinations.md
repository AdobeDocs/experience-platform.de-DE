---
title: E-Mail-Marketing-Ziele
seo-title: E-Mail-Marketing-Ziele
description: E-Mail-Dienstanbieter (ESPs) ermöglichen Ihnen die Verwaltung Ihrer E-Mail-Marketing-Aktivitäten, z. B. beim Senden von Werbe-Mail-Kampagnen.
seo-description: E-Mail-Dienstanbieter (ESPs) ermöglichen Ihnen die Verwaltung Ihrer E-Mail-Marketing-Aktivitäten, z. B. beim Senden von Werbe-Mail-Kampagnen.
translation-type: tm+mt
source-git-commit: 3c598454a868139b7604c5c7ca2b98fa0f1bb961
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 56%

---


# E-Mail-Marketing-Ziele {#email-marketing-destinations}

E-Mail-Dienstanbieter (ESPs) ermöglichen Ihnen die Verwaltung Ihrer E-Mail-Marketing-Aktivitäten, z. B. beim Senden von Werbe-Mail-Kampagnen. Die Echtzeit-Kundendatenplattform von Adobe arbeitet mit ESPs zusammen und bietet Ihnen die Möglichkeit, Segmente für E-Mail-Marketing-Ziele zu aktivieren.

Um für Ihre Kampagnen Segmente an E-Mail-Marketing-Ziele senden zu können, muss die Echtzeit-Kundendatenplattform von Adobe zunächst eine Verbindung mit dem Ziel herstellen.

Die Herstellung einer Verbindung zu E-Mail-Marketing-Zielen ist ein dreistufiger Prozess. Jeder der Schritte wird auf dieser Seite unten beschrieben.

Stellen Sie im Zielverbindungsfluss (wie im Abschnitt unten beschrieben) eine Verbindung zu Amazon S3 oder SFTP her. Die Echtzeit-Kundendatenplattform exportiert Ihre Segmente als `.csv`- oder `.txt`-Dateien und stellt sie an Ihrem gewünschten Speicherort bereit. Planen Sie den Datenimport in Ihre E-Mail-Marketing-Plattform vom Speicherort, der in der Echtzeit-Kundendatenplattform aktiviert ist. Das Verfahren zum Importieren von Daten ist je nach Partner unterschiedlich. Weiterführende Informationen finden Sie in den Artikeln zu den einzelnen Zielen.

## Schritt 1: Ziel verbinden {#connect-destination}

1. Wählen Sie unter **[!UICONTROL Verbindungen > Ziele]** das E-Mail-Marketing-Ziel, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **[!UICONTROL Ziel verbinden]**.

   ![Mit Ziel verbinden](/help/rtcdp/destinations/assets/connect-email-marketing.png)

2. In the **[!UICONTROL Authentication]** step, if you had previously set up a connection to your email marketing destination, select **[!UICONTROL Existing Account]** and select your existing connection. Or, you can select **[!UICONTROL New Account]** to set up a new connection to your email marketing destination. In der Auswahl **[!UICONTROL Verbindungstyp]** können Sie zwischen **Amazon S3**, **SFTP mit Kennwort**, **SFTP mit SSH-Schlüssel** wählen. Füllen Sie je nach Verbindungstyp die folgenden Informationen aus und wählen Sie dann **[!UICONTROL Verbinden]**.

   For **S3 connections**, you must provide your Amazon Access Key ID and Secret Access Key.

   For **SFTP with Password** connections, you must provide Domain, Port, Username, and Password for your SFTP server.

   For **SFTP with SSH Key** connections, you must provide Domain, Port, Username, and SSH Key for your SFTP server.

3. Geben Sie im Schritt **[!UICONTROL Setup]** einen **[!UICONTROL Namen]** und eine **[!UICONTROL Beschreibung]** für Ihr neues Ziel sowie das **[!UICONTROL Dateiformat]** für die exportierten Dateien ein. <br>
Wenn Sie im vorherigen Schritt Amazon S3 als Option für die Datenspeicherung ausgewählt haben, fügen Sie den **[!UICONTROL Behälternamen]** und den **[!UICONTROL Ordnerpfad]** in das Ziel Ihrer Cloud-Datenspeicherung ein, an dem die Dateien bereitgestellt werden sollen. Geben Sie für die Option &quot;SFTP-Datenspeicherung&quot;den **[!UICONTROL Ordnerpfad]** ein, unter dem die Dateien bereitgestellt werden sollen. <br>
In diesem Schritt können Sie auch einen beliebigen **[!UICONTROL Marketing-Anwendungsfall]** auswählen, der für dieses Ziel gelten soll. Anwendungsfälle für das Marketing geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von Adobe definierten Anwendungsfällen für das Marketing auswählen oder einen eigenen Anwendungsfall für das Marketing erstellen. Weitere Informationen zu Anwendungsfällen für das Marketing finden Sie auf der Seite [Datenverwaltung in Echtzeit-CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) . Informationen zu den einzelnen von Adobe definierten Anwendungsfällen für Marketing finden Sie in der Übersicht über die [Datenverwendungsrichtlinien](/help/data-governance/policies/overview.md#core-actions). <br>
   ![Email-Setup](/help/rtcdp/destinations/assets/email-setup-step.png)

## Schritt 2: Wählen Sie die Segmentmitglieder aus, die in Ihre Zielexporte einbezogen werden sollen {#select-segments}

On the **[!UICONTROL Select Segments]** page, select which segments to send to the destination. Weitere Informationen zu den Feldern finden Sie in den folgenden Abschnitten.

![Segmente auswählen](/help/rtcdp/destinations/assets/email-select-segments.png)

## Schritt 3: Auswählen, welche Schemafelder in Ihren exportierten Dateien als Zielattribute verwendet werden sollen {#destination-attributes}

In diesem Schritt wählen Sie die Felder aus, die an E-Mail-Marketing-Ziele exportiert werden sollen.

![Zielattribute](/help/rtcdp/destinations/assets/destination-attributes.png)

### Identität {#identity}

Es wird empfohlen, eine eindeutige Kennung aus Ihrem [Vereinigungsschema](../../profile/home.md#profile-fragments-and-union-schemas) auszuwählen. Das ist das Feld, aus dem die Identitäten Ihrer Benutzer übernommen werden. In der Regel besteht das Feld aus der E-Mail-Adresse, es kann aber auch eine Treueprogramm-Kennung oder eine Telefonnummer sein. In der folgenden Tabelle finden Sie die gängigsten eindeutigen Bezeichner und deren XDM-Feld im Schema Vereinigung.

| Eindeutige Kennung | XDM-Feld im einheitlichen Schema |
---------|----------
| E-Mail-Adresse | `personalEmail.address` |
| Telefon | `mobilePhone.number` |
| Treueprogramm-Kennung | `Customer-defined XDM field` |

### Andere Zielattribute

Wählen Sie in der Schemafeldauswahl die anderen Felder aus, die Sie an das E-Mail-Ziel exportieren möchten. Zu den empfohlenen Optionen gehören:

| Schema | XDM-Feld |
---------|----------
| Vorname | `person.name.firstName` |
| Nachname | `person.name.lastName` |
| Telefon | `mobilePhone.number` |
| Adresse Ort | `homeAddress.city` |
| Adresse Bundesland | `homeAddress.stateProvince` |
| Adresse Postleitzahl | `homeAddress.postalCode` |
| Geburtstag | `person.birthDayAndMonth` |

## Schritt 3: Daten aus Ihrem Speicherort in das Ziel importieren

Informationen zum Importieren von Daten aus Ihrem Speicherort in Ziele finden Sie in den Artikeln zu den einzelnen E-Mail-Marketing-Zielen:

* [Adobe Campaign](/help/rtcdp/destinations/adobe-campaign-destination.md#import-data-into-campaign)
* [Salesforce Marketing Cloud](/help/rtcdp/destinations/salesforce-marketing-cloud-destination.md#import-data-into-salesforce)
* [Oracle Eloqua](/help/rtcdp/destinations/oracle-eloqua-destination.md#import-data-into-eloqua)
* [Oracle Responsys](/help/rtcdp/destinations/oracle-responsys-destination.md#import-data-into-responsys)

## Segmente für E-Mail-Marketing-Ziele aktivieren

Anweisungen zum Aktivieren von Segmenten für E-Mail-Marketing-Ziele finden Sie unter [Daten für Ziele aktivieren](/help/rtcdp/destinations/activate-destinations.md).