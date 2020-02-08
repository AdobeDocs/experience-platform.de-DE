---
title: E-Mail-Marketingziele
seo-title: E-Mail-Marketingziele
description: E-Mail-Serviceanbieter (ESPs) ermöglichen Ihnen die Verwaltung Ihrer E-Mail-Marketingaktivitäten, z. B. zum Senden von Werbe-E-Mail-Kampagnen.
seo-description: E-Mail-Serviceanbieter (ESPs) ermöglichen Ihnen die Verwaltung Ihrer E-Mail-Marketingaktivitäten, z. B. zum Senden von Werbe-E-Mail-Kampagnen.
translation-type: tm+mt
source-git-commit: 463212a8fabb9dd5962b4d3f523a6f2d88bb1d9d

---


# E-Mail-Marketingziele {#email-marketing-destinations}

Mithilfe von E-Mail-Serviceanbietern (ESPs) können Sie Ihre E-Mail-Marketingaktivitäten verwalten, z. B. Werbe-E-Mail-Kampagnen. Die Adobe Echtzeit-Kundendatenplattform ist mit ESPs integriert, da Sie Segmente aktivieren können, um Marketingziele per E-Mail zu erreichen.

Um Segmente an E-Mail-Marketing-Ziele für Ihre Kampagnen zu senden, muss sich Adobe Echtzeit-CDP zunächst mit dem Ziel verbinden.

Die Verbindung zu E-Mail-Marketingzielen ist ein dreistufiger Prozess. Jeder der Schritte wird weiter unten auf dieser Seite beschrieben.

Stellen Sie im Verbindungsziel-Fluss, wie im Abschnitt unten beschrieben, eine Verbindung zu Amazon S3 oder SFTP her. Echtzeit-CDP exportiert Ihre Segmente als `.csv` oder `.txt` Dateien und liefert sie an Ihren gewünschten Speicherort. Planen Sie den Datenimport in Ihre E-Mail-Marketingplattform vom Speicherort, der in Echtzeit-CDP aktiviert ist. Der Prozess zum Importieren von Daten ist je nach Partner unterschiedlich. Weitere Informationen finden Sie in den Artikeln zu einzelnen Zielen.

## Schritt 1: Verbindungsziel {#connect-destination}

1. Wählen Sie unter **[!UICONTROL Verbindungen > Ziele]** das E-Mail-Marketingziel, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie dann **[!UICONTROL Connect-Ziel]**.

   ![Mit Ziel verbinden](/help/rtcdp/destinations/assets/connect-destination.png)

2. Wählen Sie im Verbindungsassistenten den **[!UICONTROL Verbindungstyp]** für Ihren Speicherort aus. Sie können zwischen **Amazon S3**, **SFTP mit Kennwort**, **SFTP mit SSH-Schlüssel** wählen. Füllen Sie die folgenden Informationen je nach Verbindungstyp aus und wählen Sie dann **[!UICONTROL Verbinden]**.

Für **S3-Verbindungen** müssen Sie die Zugriffsschlüssel-ID und den geheimen Zugriffsschlüssel angeben.

Für **SFTP mit Passwortverbindungen** müssen Sie Domäne, Port, Benutzername und Passwort angeben.

Für **SFTP mit SSH-Key** -Verbindungen müssen Sie Domäne, Port, Benutzername und SSH-Schlüssel angeben.

## Schritt 2: Wählen Sie, welche Schemafelder als Zielattribute in Ihren exportierten Dateien verwendet werden sollen {#destination-attributes}

In diesem Schritt wählen Sie die Felder aus, die in E-Mail-Marketing-Ziele exportiert werden sollen.

![Zielattribute](/help/rtcdp/destinations/assets/destination-attributes.png)

### Identität {#identity}

Es wird empfohlen, eine eindeutige Kennung aus Ihrem [Gewerkschaftsschema](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)auszuwählen. Das Feld, in dem die Identitäten Ihrer Benutzer eingegeben werden. In der Regel ist dieses Feld die E-Mail-Adresse, kann aber auch eine Treueprogramm-ID oder eine Telefonnummer sein. Die Tabelle unten enthält die gängigsten eindeutigen Bezeichner und deren XDM-Feld im einheitlichen Schema.

| Eindeutiger Bezeichner | XDM-Feld im einheitlichen Schema |
---------|----------
| Email Address | `personalEmail.address` |
| Telefon | `mobilePhone.number` |
| Kundentreueprogramm-ID | `Customer-defined XDM field` |

### Andere Zielattribute

Wählen Sie in der Feldauswahl &quot;Schema&quot;die anderen Felder aus, die Sie an das E-Mail-Ziel exportieren möchten. Einige der empfohlenen Optionen sind:

| Schema | XDM-Feld |
---------|----------
| Vorname | `person.name.firstName` |
| Nachname | `person.name.lastName` |
| Telefon | `mobilePhone.number` |
| Ort | `homeAddress.city` |
| Adresszustand | `homeAddress.stateProvince` |
| Postleitzahl der Adresse | `homeAddress.postalCode` |
| Geburtstag | `person.birthDayAndMonth` |

## Schritt 3 - Importieren von Daten aus Ihrem Speicherort in das Ziel

Informationen zum Importieren von Daten aus Ihrem Speicherort in Ziele finden Sie in den einzelnen Artikeln zu E-Mail-Marketingzielzielen:

* [Adobe Campaign](/help/rtcdp/destinations/adobe-campaign-destination.md#import-data-into-campaign)
* [Salesforce Marketing Cloud](/help/rtcdp/destinations/salesforce-marketing-cloud-destination.md#import-data-into-salesforce)
* [Oracle Eloqua](/help/rtcdp/destinations/oracle-eloqua-destination.md#import-data-into-eloqua)
* [Oracle Responsys](/help/rtcdp/destinations/oracle-responsys-destination.md#import-data-into-responsys)

## Aktivieren von Segmenten für E-Mail-Marketing-Ziele

Anweisungen zum Aktivieren von Segmenten für E-Mail-Marketing-Ziele finden Sie unter Daten [an Ziele](/help/rtcdp/destinations/activate-destinations.md)aktivieren.