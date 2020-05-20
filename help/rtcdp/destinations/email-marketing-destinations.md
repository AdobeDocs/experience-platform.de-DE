---
title: E-Mail-Marketing-Ziele
seo-title: E-Mail-Marketing-Ziele
description: E-Mail-Dienstanbieter (ESPs) ermöglichen Ihnen die Verwaltung Ihrer E-Mail-Marketing-Aktivitäten, z. B. beim Senden von Werbe-Mail-Kampagnen.
seo-description: E-Mail-Dienstanbieter (ESPs) ermöglichen Ihnen die Verwaltung Ihrer E-Mail-Marketing-Aktivitäten, z. B. beim Senden von Werbe-Mail-Kampagnen.
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 100%

---


# E-Mail-Marketing-Ziele {#email-marketing-destinations}

E-Mail-Dienstanbieter (ESPs) ermöglichen Ihnen die Verwaltung Ihrer E-Mail-Marketing-Aktivitäten, z. B. beim Senden von Werbe-Mail-Kampagnen. Die Echtzeit-Kundendatenplattform von Adobe arbeitet mit ESPs zusammen und bietet Ihnen die Möglichkeit, Segmente für E-Mail-Marketing-Ziele zu aktivieren.

Um für Ihre Kampagnen Segmente an E-Mail-Marketing-Ziele senden zu können, muss die Echtzeit-Kundendatenplattform von Adobe zunächst eine Verbindung mit dem Ziel herstellen.

Die Herstellung einer Verbindung zu E-Mail-Marketing-Zielen ist ein dreistufiger Prozess. Jeder der Schritte wird auf dieser Seite unten beschrieben.

Stellen Sie im Zielverbindungsfluss (wie im Abschnitt unten beschrieben) eine Verbindung zu Amazon S3 oder SFTP her. Die Echtzeit-Kundendatenplattform exportiert Ihre Segmente als `.csv`- oder `.txt`-Dateien und stellt sie an Ihrem gewünschten Speicherort bereit. Planen Sie den Datenimport in Ihre E-Mail-Marketing-Plattform vom Speicherort, der in der Echtzeit-Kundendatenplattform aktiviert ist. Das Verfahren zum Importieren von Daten ist je nach Partner unterschiedlich. Weiterführende Informationen finden Sie in den Artikeln zu den einzelnen Zielen.

## Schritt 1: Ziel verbinden {#connect-destination}

1. Wählen Sie unter **[!UICONTROL Verbindungen > Ziele]** das E-Mail-Marketing-Ziel, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **[!UICONTROL Ziel verbinden]**.

   ![Mit Ziel verbinden](/help/rtcdp/destinations/assets/connect-destination.png)

2. Wählen Sie im Verbindungsassistenten den **[!UICONTROL Verbindungstyp]** für Ihren Speicherort aus. Sie können zwischen **Amazon S3**, **SFTP mit Passwort** und **SFTP mit SSH-Schlüssel** wählen. Füllen Sie je nach Verbindungstyp die folgenden Informationen aus und wählen Sie dann **[!UICONTROL Verbinden]**.

Bei Verbindungen des Typs **S3** müssen Sie die Zugriffsschlüsselkennung und den geheimen Zugriffsschlüssel angeben.

Bei Verbindungen des Typs **SFTP mit Passwort** müssen Sie Domäne, Port, Benutzernamen und Kennwort angeben.

Bei Verbindungen des Typs **SFTP mit SSH-Schlüssel** müssen Sie Domäne, Port, Benutzernamen und SSH-Schlüssel angeben.

## Schritt 2: Auswählen, welche Schemafelder in Ihren exportierten Dateien als Zielattribute verwendet werden sollen {#destination-attributes}

In diesem Schritt wählen Sie die Felder aus, die an E-Mail-Marketing-Ziele exportiert werden sollen.

![Zielattribute](/help/rtcdp/destinations/assets/destination-attributes.png)

### Identität {#identity}

Es wird empfohlen, eine eindeutige Kennung aus Ihrem [Vereinigungsschema](../../profile/home.md#profile-fragments-and-union-schemas) auszuwählen. Das ist das Feld, aus dem die Identitäten Ihrer Benutzer übernommen werden. In der Regel besteht das Feld aus der E-Mail-Adresse, es kann aber auch eine Treueprogramm-Kennung oder eine Telefonnummer sein. In der folgenden Tabelle sehen Sie die gängigsten eindeutigen Kennungen und deren XDM-Feld im einheitlichen Schema.

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