---
keywords: email;Email;e-mail;email destinations
title: E-Mail-Marketing-Ziele
seo-title: E-Mail-Marketing-Ziele
type: Tutorial
description: E-Mail-Dienstanbieter (ESPs) ermöglichen Ihnen die Verwaltung Ihrer E-Mail-Marketing-Aktivitäten, z. B. beim Senden von Werbe-Mail-Kampagnen.
seo-description: E-Mail-Dienstanbieter (ESPs) ermöglichen Ihnen die Verwaltung Ihrer E-Mail-Marketing-Aktivitäten, z. B. beim Senden von Werbe-Mail-Kampagnen.
translation-type: tm+mt
source-git-commit: 42b694c532f140b51913ba5ceb0aaeacc2263039
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 42%

---


# E-Mail-Marketing-Ziele {#email-marketing-destinations}

E-Mail-Dienstanbieter (ESPs) ermöglichen Ihnen die Verwaltung Ihrer E-Mail-Marketing-Aktivitäten, z. B. beim Senden von Werbe-Mail-Kampagnen. Die Echtzeit-Kundendatenplattform von Adobe arbeitet mit ESPs zusammen und bietet Ihnen die Möglichkeit, Segmente für E-Mail-Marketing-Ziele zu aktivieren.

Um für Ihre Kampagnen Segmente an E-Mail-Marketing-Ziele senden zu können, muss die Echtzeit-Kundendatenplattform von Adobe zunächst eine Verbindung mit dem Ziel herstellen.

Die Herstellung einer Verbindung zu E-Mail-Marketing-Zielen ist ein dreistufiger Prozess. Jeder der Schritte wird auf dieser Seite unten beschrieben.

Stellen Sie im Zielverbindungsfluss (wie im Abschnitt unten beschrieben) eine Verbindung zu Amazon S3 oder SFTP her. Die Echtzeit-Kundendatenplattform von Adobe exportiert Ihre Segmente als `.csv`- oder `.txt`-Dateien und stellt sie an Ihrem gewünschten Speicherort bereit. Planen Sie den Datenimport in Ihre E-Mail-Marketing-Plattform vom Speicherort, der in der Echtzeit-Kundendatenplattform von Adobe aktiviert ist. Das Verfahren zum Importieren von Daten ist je nach Partner unterschiedlich. Weiterführende Informationen finden Sie in den Artikeln zu den einzelnen Zielen.

## Ziel konfigurieren {#connect-destination}

In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, select the email marketing destination that you want to connect to, then select **[!UICONTROL Configure]**.

![Mit Ziel verbinden](./assets/connect-email-marketing.png)

In the **[!UICONTROL Authentication]** step, if you had previously set up a connection to your email marketing destination, select **[!UICONTROL Existing Account]** and select your existing connection. Or, you can select **[!UICONTROL New Account]** to set up a new connection to your email marketing destination. In der Auswahl für den **[!UICONTROL Verbindungstyp]** können Sie zwischen Amazon S3, SFTP mit Kennwort oder SFTP mit SSH-Schlüssel wählen. Füllen Sie je nach Verbindungstyp die folgenden Informationen aus und wählen Sie dann **[!UICONTROL Verbinden]**.

- For **S3 connections**, you must provide your Amazon Access Key ID and Secret Access Key.
- For **SFTP with Password** connections, you must provide Domain, Port, Username, and Password for your SFTP server.
- For **SFTP with SSH Key** connections, you must provide Domain, Port, Username, and SSH Key for your SFTP server.

Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Verschlüsselung zu den exportierten Dateien im Abschnitt **[!UICONTROL Schlüssel]** hinzuzufügen. Beachten Sie, dass dieser öffentliche Schlüssel als Base64-kodierte Zeichenfolge geschrieben werden **muss** .

Geben Sie im Schritt **[!UICONTROL Setup]** einen Namen und eine Beschreibung für Ihr neues Ziel sowie das Dateiformat für die exportierten Dateien ein.

Wenn Sie im vorherigen Schritt die Option &quot;Amazon S3&quot;als Datenspeicherung ausgewählt haben, fügen Sie den Behälternamen und den Ordnerpfad in das Ziel der Cloud-Datenspeicherung ein, an das die Dateien gesendet werden sollen. Geben Sie für die Option &quot;SFTP-Datenspeicherung&quot;den Ordnerpfad ein, unter dem die Dateien bereitgestellt werden sollen.

In diesem Schritt können Sie auch einen beliebigen Anwendungsfall für das Marketing auswählen, der für dieses Ziel gelten soll. Anwendungsfälle für das Marketing geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von der Adobe definierten Anwendungsfällen für das Marketing auswählen oder einen eigenen Anwendungsfall für das Marketing erstellen. Weitere Informationen zu Anwendungsfällen für das Marketing finden Sie auf der Seite [Datenverwaltung in Echtzeit-CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) . Informationen zu den einzelnen Anwendungsfällen für Marketingzwecke, die von der Adobe definiert wurden, finden Sie in der Übersicht über [Datenverwendungsrichtlinien](/help/data-governance/policies/overview.md#core-actions).

![Email-Setup](./assets/email-setup-step.png)

## Wählen Sie die Segmentmitglieder aus, die in die Zielexporte einbezogen werden sollen {#select-segments}

On the **[!UICONTROL Select Segments]** page, select which segments to send to the destination. Weitere Informationen zu den Feldern finden Sie in den folgenden Abschnitten.

![Segmente auswählen](/help/rtcdp/destinations/assets/email-select-segments.png)

## Dateinamen konfigurieren

Weitere Informationen zu den Dateinamenbearbeitungsoptionen finden Sie im Lernprogramm Ziele aktivieren im Schritt [konfigurieren](/help/rtcdp/destinations/activate-destinations.md#configure) .

## Select attributes - Select which schema fields to use as destination attributes in your exported files {#destination-attributes}

In diesem Schritt wählen Sie die Felder aus, die in E-Mail-Marketing-Ziele exportiert werden sollen, und markieren, welche Felder obligatorisch sind.

![Zielattribute](/help/rtcdp/destinations/assets/recommended-attributes.png)

Weitere Informationen zu diesem Schritt finden Sie im Schritt [Attribute](/help/rtcdp/destinations/activate-destinations.md#select-attributes) auswählen im Lernprogramm Ziele aktivieren.

### Identität {#identity}

Es wird empfohlen, eine eindeutige Kennung aus Ihrem [Vereinigungsschema](../../profile/home.md#profile-fragments-and-union-schemas) auszuwählen. Das ist das Feld, aus dem die Identitäten Ihrer Benutzer übernommen werden. In der Regel besteht das Feld aus der E-Mail-Adresse, es kann aber auch eine Treueprogramm-Kennung oder eine Telefonnummer sein. In der folgenden Tabelle finden Sie die gängigsten eindeutigen Bezeichner und deren XDM-Feld im Schema.

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
| Segmentmitgliedschaft | `segmentMembership.status` |

## Importieren von Daten von Ihrem Speicherort in die Datenspeicherung

Informationen zum Importieren von Daten aus Ihrem Speicherort in Ziele finden Sie in den Artikeln zu den einzelnen E-Mail-Marketing-Zielen:

- [Adobe Campaign](/help/rtcdp/destinations/adobe-campaign-destination.md#import-data-into-campaign)
- [Salesforce Marketing Cloud](/help/rtcdp/destinations/salesforce-marketing-cloud-destination.md#import-data-into-salesforce)
- [Oracle Eloqua](/help/rtcdp/destinations/oracle-eloqua-destination.md#import-data-into-eloqua)
- [Oracle Responsys](/help/rtcdp/destinations/oracle-responsys-destination.md#import-data-into-responsys)

## Segmente für E-Mail-Marketing-Ziele aktivieren

Anweisungen zum Aktivieren von Segmenten für E-Mail-Marketing-Ziele finden Sie unter [Daten für Ziele aktivieren](/help/rtcdp/destinations/activate-destinations.md).

## Zusätzliche Ressourcen

- [Aktivieren von Daten an Ziele](/help/rtcdp/destinations/activate-destinations.md)
- [Erstellen Sie E-Mail-Marketingziele und aktivieren Sie Daten mit der Flow Service API](https://docs.adobe.com/content/help/en/experience-platform/tutorials/destinations/email-marketing-api.html)