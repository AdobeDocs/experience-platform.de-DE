---
keywords: E-Mail;E-Mail;E-Mail;E-Mail-Ziele
title: E-Mail-Marketing-Ziele – Übersicht
type: Tutorial
description: E-Mail-Dienstanbieter (ESPs) ermöglichen Ihnen die Verwaltung Ihrer E-Mail-Marketing-Aktivitäten, z. B. beim Senden von Werbe-Mail-Kampagnen.
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: a21abb44bb9cbe6fefa0ff70a1ff19e31cc0c7de
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 21%

---

# E-Mail-Marketing-Ziele – Übersicht {#email-marketing-destinations}

E-Mail-Dienstanbieter (ESPs) ermöglichen Ihnen die Verwaltung Ihrer E-Mail-Marketing-Aktivitäten, z. B. beim Senden von Werbe-Mail-Kampagnen. Adobe Experience Platform kann mit ESPs integriert werden, indem Sie Segmente aktivieren können, um E-Mail-Marketing-Ziele zu erreichen.

Um Segmente an E-Mail-Marketingziele für Ihre Kampagnen zu senden, muss die Plattform zuerst eine Verbindung zum Ziel herstellen.

Die Verbindung zu E-Mail-Marketingzielen erfolgt in drei Schritten ([configure destination](#connect-destination), [activate segments](#select-segments), [import data from Datenspeicherung location into the destination](#import-data-into-destination)). Jeder der Schritte wird auf dieser Seite unten beschrieben.

Stellen Sie im Verbindungsziel-Fluss, wie im Abschnitt unten beschrieben, eine Verbindung zu [!DNL Amazon S3] oder [!DNL SFTP] her. Plattform exportiert Ihre Segmente als `.csv`-Dateien und liefert sie an Ihren bevorzugten Speicherort. Planen Sie den Datenimport in Ihre E-Mail-Marketingplattform von dem in [!DNL Platform] aktivierten Speicherort der Datenspeicherung. Das Verfahren zum Importieren von Daten ist je nach Partner unterschiedlich. Lesen Sie die Artikel zu den einzelnen Zielen, um weitere Informationen zu erhalten.

## Ziel {#connect-destination} konfigurieren

Wählen Sie unter **[!UICONTROL Verbindungen]** > **[!UICONTROL Ziele]** das E-Mail-Marketingziel, mit dem Sie eine Verbindung herstellen möchten, und wählen Sie **[!UICONTROL Konfigurieren]**.

![Mit Ziel verbinden](../../assets/catalog/email-marketing/overview/connect-email-marketing.png)

Wenn Sie im Schritt **[!UICONTROL Konto]** zuvor eine Verbindung zu Ihrem E-Mail-Marketingziel eingerichtet haben, wählen Sie **[!UICONTROL Vorhandenes Konto]** und wählen Sie Ihre bestehende Verbindung aus. Sie können auch **[!UICONTROL Neues Konto]** auswählen, um eine neue Verbindung zu Ihrem E-Mail-Marketingziel einzurichten. In der Auswahl **[!UICONTROL Verbindungstyp]** können Sie zwischen [!UICONTROL Amazon S3], [!UICONTROL Blaue Blase], [!UICONTROL SFTP mit Kennwort] oder [!UICONTROL SFTP mit SSH-Schlüssel] wählen. Füllen Sie je nach Verbindungstyp die folgenden Informationen aus und wählen Sie dann **[!UICONTROL Verbinden]**.

- Für **S3-Verbindungen** müssen Sie Ihre Amazon-Zugriffsschlüssel-ID und den geheimen Zugriffsschlüssel angeben.
- Für Verbindungen mit **SFTP mit Kennwort** müssen Sie Domäne, Port, Benutzername und Kennwort für Ihren SFTP-Server angeben.
- Für Verbindungen mit **SFTP mit SSH-Schlüssel** müssen Sie Domäne, Port, Benutzername und SSH-Schlüssel für Ihren SFTP-Server angeben.

Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien unter dem Abschnitt **[!UICONTROL Schlüssel]** Verschlüsselung hinzuzufügen. Ihr öffentlicher Schlüssel muss als [!DNL Base64] kodierte Zeichenfolge geschrieben werden.

Geben Sie im Schritt **[!UICONTROL Authentifizierung]** einen Namen und eine Beschreibung für Ihr neues Ziel sowie das Dateiformat für die exportierten Dateien ein.

Wenn Sie im vorherigen Schritt die Option &quot;Amazon S3&quot;als Datenspeicherung ausgewählt haben, fügen Sie den Behälternamen und den Ordnerpfad in das Ziel der Cloud-Datenspeicherung ein, an das die Dateien gesendet werden sollen. Geben Sie für die Option &quot;SFTP-Datenspeicherung&quot;den Ordnerpfad ein, unter dem die Dateien bereitgestellt werden sollen.

In diesem Schritt können Sie auch jede Marketingaktion auswählen, die auf dieses Ziel angewendet werden soll. Marketingaktionen geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von der Adobe definierten Marketingaktionen auswählen oder eine eigene Marketingaktion erstellen. Weitere Informationen zu Marketingaktionen finden Sie unter [Übersicht über Datenverwendungsrichtlinien](../../../data-governance/policies/overview.md).

![Email-Setup](../../assets/catalog/email-marketing/overview/email-setup-step.png)

## Wählen Sie die Segmentmitglieder aus, die Sie in Ihre Zielexporte aufnehmen möchten {#select-segments}

Wählen Sie auf der Seite **[!UICONTROL Segmente]** auswählen, welche Segmente an das Ziel gesendet werden sollen. Weitere Informationen zu den Feldern finden Sie in den folgenden Abschnitten.

![Segmente auswählen](../../assets/common/email-select-segments.png)

## Dateinamen konfigurieren

Weitere Informationen zu den Optionen für den Segmentplan und die Bearbeitung von Dateinamen finden Sie im Schritt [Konfigurieren](../../ui/activate-destinations.md#configure) im Tutorial Ziele aktivieren.

## Attribute auswählen - Wählen Sie aus, welche Schema-Felder als Zielattribute in den exportierten Dateien verwendet werden sollen.{#destination-attributes}

In diesem Schritt wählen Sie die Felder aus, die in E-Mail-Marketing-Ziele exportiert werden sollen, und markieren, welche Felder obligatorisch sind.
Weitere Informationen zu diesem Schritt finden Sie im Schritt [Attribute auswählen](../../ui/activate-destinations.md#select-attributes) im Lernprogramm Ziele aktivieren.

## Identität {#identity}

Adobe empfiehlt, dass Sie im Schema [Vereinigung](../../../profile/home.md#profile-fragments-and-union-schemas) einen eindeutigen Bezeichner auswählen. Das Feld, in dem Ihre Benutzeridentitäten eingegeben werden. In der Regel besteht das Feld aus der E-Mail-Adresse, es kann aber auch eine Treueprogramm-Kennung oder eine Telefonnummer sein. In der folgenden Tabelle finden Sie die gängigsten eindeutigen Bezeichner und deren XDM-Feld im Schema.

| Eindeutige Kennung | XDM-Feld im einheitlichen Schema |
----------------- | ---------------------------
| E-Mail-Adresse | `personalEmail.address` |
| Telefon | `mobilePhone.number` |
| Treueprogramm-Kennung | `Customer-defined XDM field` |

## Andere Zielattribute

Wählen Sie in der Schemafeldauswahl die anderen Felder aus, die Sie an das E-Mail-Ziel exportieren möchten. Zu den empfohlenen Optionen gehören:

| Schema | XDM-Feld |
------ | ---------
| Vorname | `person.name.firstName` |
| Nachname | `person.name.lastName` |
| Telefon | `mobilePhone.number` |
| Adresse Ort | `homeAddress.city` |
| Adresse Bundesland | `homeAddress.stateProvince` |
| Adresse Postleitzahl | `homeAddress.postalCode` |
| Geburtstag | `person.birthDayAndMonth` |
| Segmentmitgliedschaft | `segmentMembership.status` |

## Importieren Sie Daten von Ihrem Speicherort für die Datenspeicherung in das Ziel {#import-data-into-destination}

Lesen Sie die einzelnen Artikel zum E-Mail-Marketing-Ziel, um zu erfahren, wie Sie Daten aus Ihrer Datenspeicherung in Ziele importieren:

- [Adobe Campaign](./adobe-campaign.md#import-data-into-campaign)
- [Oracle Eloqua](./oracle-eloqua.md#import-data-into-eloqua)
- [Oracle Responsys](./oracle-responsys.md#import-data-into-responsys)
- [Salesforce Marketing Cloud](./salesforce-marketing-cloud.md#import-data-into-salesforce)

## Segmente für E-Mail-Marketing-Ziele aktivieren

Anweisungen zum Aktivieren von Segmenten für E-Mail-Marketing-Ziele finden Sie unter [Aktivieren von Profilen und Segmenten für ein Ziel](../../ui/activate-destinations.md).

## Zusätzliche Ressourcen

- [Aktivieren von Daten an Ziele](../../ui/activate-destinations.md)
- [Erstellen Sie E-Mail-Marketingziele und aktivieren Sie Daten mit der Flow Service API](../../api/email-marketing.md)
