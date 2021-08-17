---
keywords: E-Mail; E-Mail; E-Mail; E-Mail-Ziele; oracle responsys-Ziel
title: Oracle Responsys-Verbindung
description: Responsys ist ein Enterprise-E-Mail-Marketing-Tool für kanalübergreifende Marketing-Kampagnen, das von Oracle angeboten wird und der Personalisierung von Interaktionen über E-Mail, Mobile, Display und Social Media hinweg dient.
exl-id: 70f2f601-afee-4315-bf7a-ed2c92397ebe
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 23%

---

# [!DNL Oracle Responsys] connection

## Übersicht {#overview}

[Responsys](https://www.oracle.com/cx/marketing/campaign-management/)[!DNL Oracle] ist ein Enterprise-E-Mail-Marketing-Tool für kanalübergreifende Marketing-Kampagnen, das von angeboten wird und der Personalisierung von Interaktionen über E-Mail, Mobile, Display und Social Media hinweg dient.

Um Segmentdaten an [!DNL Oracle Responsys] zu senden, müssen Sie zunächst [eine Verbindung zum Ziel](#connect-destination) in Adobe Experience Platform herstellen und dann [einen Datenimport einrichten](#import-data-into-responsys) von Ihrem Speicherort zu [!DNL Oracle Responsys].

## Exporttyp {#export-type}

**Profilbasiert**  - Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm &quot;Attribute auswählen&quot;des  [Zielaktivierungs-Workflows](../../ui/activate-destinations.md#select-attributes) ausgewählt.

## IP-Adressen-Zulassungsliste {#allow-list}

Beim Einrichten von E-Mail-Marketing-Zielen mit SFTP-Speicher empfiehlt Adobe, bestimmte IP-Bereiche zu Ihrer Zulassungsliste hinzuzufügen.

Informationen zum Hinzufügen von Adobe-IPs zu Ihrer Zulassungsliste finden Sie unter [IP-Adressen-Zulassungsliste für Cloud-Speicher-Ziele](../cloud-storage/ip-address-allow-list.md) .

## Mit Ziel verbinden {#connect}

Um eine Verbindung zu diesem Ziel herzustellen, führen Sie die Schritte aus, die im Tutorial [Zielkonfiguration](../../ui/connect-destination.md) beschrieben sind.

Dieses Ziel unterstützt die folgenden Verbindungstypen:

* **[!UICONTROL SFTP mit Kennwort]**
* **[!UICONTROL SFTP mit SSH-Schlüssel]**

### Verbindungsparameter {#parameters}

Während [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* Für Verbindungen des Typs **[!UICONTROL SFTP mit Kennwort]** müssen Sie Folgendes angeben:
   * [!UICONTROL Domäne]
   * [!UICONTROL Port]
   * [!UICONTROL Benutzername]
   * [!UICONTROL Passwort]
* Für Verbindungen des Typs **[!UICONTROL SFTP mit SSH-Schlüssel]** müssen Sie Folgendes angeben:
   * [!UICONTROL Domäne]
   * [!UICONTROL Port]
   * [!UICONTROL Benutzername]
   * [!UICONTROL SSH-Schlüssel]
* Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um eine Verschlüsselung mit PGP/GPG zu Ihren exportierten Dateien im Abschnitt **[!UICONTROL Schlüssel]** hinzuzufügen. Ihr öffentlicher Schlüssel muss als [!DNL Base64] kodierte Zeichenfolge geschrieben werden.
* **[!UICONTROL Name]**: Wählen Sie einen passenden Namen für Ihr Ziel.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für Ihr Ziel ein.
* **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad an Ihrem Speicherort an, an dem Platform Ihre Exportdaten als CSV- oder tabulatorgetrennte Dateien hinterlegt.
* **[!UICONTROL Dateiformat]**: **CSV** oder **TAB_DELIMITED**. Wählen Sie das Dateiformat aus, mit dem Sie an Ihren Speicherort exportieren möchten.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

## Aktivieren von Segmenten für dieses Ziel {#activate}

Anweisungen zum Aktivieren von Zielgruppensegmenten für Ziele finden Sie unter [Aktivieren von Profilen und Segmenten für ein Ziel](../../ui/activate-destinations.md) .

## Zielattribute {#destination-attributes}

Wenn Sie [Segmente](../../ui/activate-destinations.md) für dieses Ziel aktivieren, empfiehlt Adobe, eine eindeutige Kennung aus Ihrem [Vereinigungsschema](../../../profile/home.md#profile-fragments-and-union-schemas) auszuwählen. Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weitere Informationen finden Sie unter [Auswählen, welche Schemafelder in Ihren exportierten Dateien als Zielattribute verwendet werden sollen](./overview.md#destination-attributes).

## Exportierte Daten {#exported-data}

Für [!DNL Oracle Responsys]-Ziele erstellt Platform eine tabulatorgetrennte `.csv`-Datei am von Ihnen angegebenen Speicherort. Weitere Informationen zu den Dateien finden Sie unter [E-Mail-Marketing-Ziele und Cloud-Speicher-Ziele](../../ui/activate-destinations.md#esp-and-cloud-storage) im Tutorial zur Segmentaktivierung.

## Datenimport in [!DNL Oracle Responsys] einrichten {#import-data-into-responsys}

Nachdem Sie [!DNL Platform] mit Ihrem [!DNL SFTP]-Speicher verbunden haben, müssen Sie den Datenimport von Ihrem Speicherort zu [!DNL Oracle Responsys] einrichten. Weitere Informationen dazu finden Sie unter [Importieren von Kontakten oder Konten](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) in der [!DNL Oracle Responsys Help Center].
