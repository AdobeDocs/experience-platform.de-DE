---
keywords: E-Mail; E-Mail; E-Mail; E-Mail-Ziele
title: E-Mail-Marketing-Ziele – Übersicht
type: Tutorial
description: E-Mail-Dienstanbieter (ESPs) ermöglichen Ihnen die Verwaltung Ihrer E-Mail-Marketing-Aktivitäten, z. B. beim Senden von Werbe-Mail-Kampagnen.
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: d3e1bc9bc075117dcc96c85b8b9c81d6ee617d29
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 21%

---

# E-Mail-Marketing-Ziele – Übersicht {#email-marketing-destinations}

E-Mail-Dienstanbieter (ESPs) ermöglichen Ihnen die Verwaltung Ihrer E-Mail-Marketing-Aktivitäten, z. B. beim Senden von Werbe-Mail-Kampagnen. Adobe Experience Platform lässt sich mit ESPs integrieren, indem es Ihnen ermöglicht, Segmente für E-Mail-Marketing-Ziele zu aktivieren.

Um für Ihre Kampagnen Segmente an E-Mail-Marketing-Ziele zu senden, muss Platform zunächst eine Verbindung zum Ziel herstellen.

Die Verbindung zu E-Mail-Marketing-Zielen ist ein dreistufiger Prozess ([Konfigurieren des Ziels](#connect-destination), [Aktivieren von Segmenten](#select-segments), [Importieren von Daten vom Speicherort in das Ziel](#import-data-into-destination)). Jeder der Schritte wird auf dieser Seite unten beschrieben.

Stellen Sie im Zielfluss &quot;Verbindung&quot;wie im folgenden Abschnitt beschrieben eine Verbindung zu [!DNL Amazon S3] oder [!DNL SFTP] her. Platform exportiert Ihre Segmente als `.csv`-Dateien und stellt sie an Ihrem gewünschten Speicherort bereit. Planen Sie Ihren Datenimport in Ihre E-Mail-Marketing-Plattform vom Speicherort, der in [!DNL Platform] aktiviert ist. Das Verfahren zum Importieren von Daten ist je nach Partner unterschiedlich. Weitere Informationen finden Sie in den Artikeln zu den einzelnen Zielen .

## Konfigurieren des Ziels {#connect-destination}

Wählen Sie unter **[!UICONTROL Verbindungen]** > **[!UICONTROL Ziele]** das E-Mail-Marketing-Ziel, mit dem Sie eine Verbindung herstellen möchten, und dann **[!UICONTROL Konfigurieren]**.

![Mit Ziel verbinden](../../assets/catalog/email-marketing/overview/connect-email-marketing.png)

Wenn Sie im Schritt **[!UICONTROL Konto]** zuvor eine Verbindung zu Ihrem E-Mail-Marketing-Ziel eingerichtet haben, wählen Sie **[!UICONTROL Vorhandenes Konto]** und wählen Sie Ihre bestehende Verbindung aus. Sie können auch **[!UICONTROL Neues Konto]** auswählen, um eine neue Verbindung zu Ihrem E-Mail-Marketing-Ziel einzurichten. In der Auswahl **[!UICONTROL Verbindungstyp]** können Sie zwischen [!UICONTROL Amazon S3], [!UICONTROL Azure Blob], [!UICONTROL SFTP mit Kennwort] oder [!UICONTROL SFTP mit SSH-Schlüssel] wählen. Füllen Sie je nach Verbindungstyp die folgenden Informationen aus und wählen Sie dann **[!UICONTROL Verbinden]**.

- Bei Verbindungen des Typs **S3** müssen Sie die Amazon-Zugriffsschlüsselkennung und den geheimen Zugriffsschlüssel angeben.
- Bei Verbindungen des Typs **SFTP mit Kennwort** müssen Sie Domäne, Port, Benutzernamen und Kennwort für Ihren SFTP-Server angeben.
- Bei Verbindungen des Typs **SFTP mit SSH-Schlüssel** müssen Sie Domäne, Port, Benutzernamen und SSH-Schlüssel für Ihren SFTP-Server angeben.

Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien unter dem Abschnitt **[!UICONTROL Schlüssel]** Verschlüsselung hinzuzufügen. Ihr öffentlicher Schlüssel muss als [!DNL Base64] kodierte Zeichenfolge geschrieben werden.

Geben Sie im Schritt **[!UICONTROL Authentifizierung]** einen Namen und eine Beschreibung für Ihr neues Ziel sowie das Dateiformat für die exportierten Dateien ein.

Wenn Sie im vorherigen Schritt Amazon S3 als Speicheroption ausgewählt haben, geben Sie den Behälternamen und den Ordnerpfad in Ihr Cloud-Speicher-Ziel ein, an dem die Dateien bereitgestellt werden sollen. Geben Sie für die SFTP-Speicheroption den Ordnerpfad ein, unter dem die Dateien bereitgestellt werden sollen.

In diesem Schritt können Sie auch eine beliebige Marketing-Aktion auswählen, die auf dieses Ziel angewendet werden soll. Marketing-Aktionen geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von der Adobe definierten Marketing-Aktionen auswählen oder eine eigene Marketing-Aktion erstellen. Weitere Informationen zu Marketing-Aktionen finden Sie unter [Übersicht über Datennutzungsrichtlinien](../../../data-governance/policies/overview.md).

![Schritt zur E-Mail-Einrichtung](../../assets/catalog/email-marketing/overview/email-setup-step.png)

## Wählen Sie aus, welche Segmentmitglieder Sie in Ihre Zielexporte aufnehmen möchten {#select-segments}

Wählen Sie auf der Seite **[!UICONTROL Segmente]** auswählen, welche Segmente an das Ziel gesendet werden sollen. Weitere Informationen zu den Feldern finden Sie in den folgenden Abschnitten.

![Segmente auswählen](../../assets/common/email-select-segments.png)

## Dateinamen konfigurieren

Informationen zu den Optionen für Segmentzeitplan und Dateinamenbearbeitung finden Sie im Schritt [Konfigurieren](../../ui/activate-destinations.md#configure) im Tutorial zum Aktivieren von Zielen.

## Attribute auswählen - Wählen Sie aus, welche Schemafelder in Ihren exportierten Dateien als Zielattribute verwendet werden sollen {#destination-attributes}

In diesem Schritt wählen Sie die Felder aus, die an E-Mail-Marketing-Ziele exportiert werden sollen, und markieren, welche Felder Pflichtfelder sind.
Weitere Informationen zu diesem Schritt finden Sie im Schritt [Attribute auswählen](../../ui/activate-destinations.md#select-attributes) im Tutorial zum Aktivieren von Zielen.

## Identität {#identity}

Adobe empfiehlt, eine eindeutige Kennung aus Ihrem [Vereinigungsschema](../../../profile/home.md#profile-fragments-and-union-schemas) auszuwählen. Dies ist das Feld, aus dem Ihre Benutzeridentitäten abgeleitet werden. In der Regel besteht das Feld aus der E-Mail-Adresse, es kann aber auch eine Treueprogramm-Kennung oder eine Telefonnummer sein. In der folgenden Tabelle finden Sie die gängigsten eindeutigen Kennungen und deren XDM-Feld im Schema.

| Eindeutige Kennung | XDM-Feld im einheitlichen Schema |
|----------------- | ---------------------------|
| E-Mail-Adresse | `personalEmail.address` |
| Telefon | `mobilePhone.number` |
| Treueprogramm-Kennung | `Customer-defined XDM field` |

## Andere Zielattribute

Wählen Sie in der Schemafeldauswahl die anderen Felder aus, die Sie an das E-Mail-Ziel exportieren möchten. Zu den empfohlenen Optionen gehören:

| Schema | XDM-Feld |
|------ | ---------|
| Vorname | `person.name.firstName` |
| Nachname | `person.name.lastName` |
| Telefon | `mobilePhone.number` |
| Adresse Ort | `homeAddress.city` |
| Adresse Bundesland | `homeAddress.stateProvince` |
| Adresse Postleitzahl | `homeAddress.postalCode` |
| Geburtstag | `person.birthDayAndMonth` |
| Segmentmitgliedschaft | `segmentMembership.status` |

## Importieren Sie Daten von Ihrem Speicherort in das Ziel {#import-data-into-destination}

Lesen Sie die einzelnen Artikel zu E-Mail-Marketing-Zielen , um zu erfahren, wie Sie Daten von Ihrem Speicherort in Ziele importieren:

- [Adobe Campaign](./adobe-campaign.md#import-data-into-campaign)
- [Oracle Eloqua](./oracle-eloqua.md#import-data-into-eloqua)
- [Oracle Responsys](./oracle-responsys.md#import-data-into-responsys)
- [Salesforce Marketing Cloud](./salesforce-marketing-cloud.md#import-data-into-salesforce)

## Segmente für E-Mail-Marketing-Ziele aktivieren

Anweisungen zum Aktivieren von Segmenten für E-Mail-Marketing-Ziele finden Sie unter [Profile und Segmente für ein Ziel aktivieren](../../ui/activate-destinations.md).

## Zusätzliche Ressourcen

- [Daten für Ziele aktivieren](../../ui/activate-destinations.md)
- [Erstellen von E-Mail-Marketing-Zielen und Aktivieren von Daten mithilfe der Flow Service-API](../../api/email-marketing.md)
