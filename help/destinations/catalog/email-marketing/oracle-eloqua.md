---
keywords: E-Mail; E-Mail; E-Mail; E-Mail-Ziele; oracle eloqua; oracle
title: Oracle Eloqua-Verbindung
description: Oracle Eloqua ist eine Software-as-a-Service (SaaS)-Plattform für Marketing-Automatisierung von Oracle, die B2B-Marketer und -Teams bei der Verwaltung von Marketing-Kampagnen und Lead-Generierung für den Vertrieb unterstützt.
exl-id: 6eaa79ff-8874-423b-bdff-aa04f6101a53
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 28%

---

# [!DNL Oracle Eloqua]-Verbindung

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/)[!DNL Oracle] ist eine Software-as-a-Service (SaaS)-Plattform für Marketing-Automatisierung von , die B2B-Marketer und -Teams bei der Verwaltung von Marketing-Kampagnen und Lead-Generierung für den Vertrieb unterstützt.

So senden Sie Segmentdaten an [!DNL Oracle Eloqua], müssen Sie zuerst [Ziel verbinden](#connect-destination) in Adobe Experience Platform und dann [Datenimport einrichten](#import-data-into-eloqua) von Ihrem Speicherort zu [!DNL Oracle Eloqua].

## Exportart und -frequenz {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm Profilattribute im [Zielaktivierungs-Workflow](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Mehr dazu [Batch-dateibasierte Ziele](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## IP-Adressen-Zulassungsliste {#allow-list}

Beim Einrichten von E-Mail-Marketing-Zielen mit SFTP-Speicher empfiehlt Adobe, bestimmte IP-Bereiche zu Ihrer Zulassungsliste hinzuzufügen.

Siehe [IP-Adressen-Zulassungsliste für Cloud-Speicher-Ziele](../cloud-storage/ip-address-allow-list.md) , wenn Sie Ihrer Zulassungsliste Adobe-IPs hinzufügen müssen.

## Herstellen einer Verbindung mit der Datenbank {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

Dieses Ziel unterstützt die folgenden Verbindungstypen:

* **[!UICONTROL SFTP mit Kennwort]**
* **[!UICONTROL SFTP mit SSH-Schlüssel]**

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* Für **[!UICONTROL SFTP mit Kennwort]** -Verbindungen, müssen Sie Folgendes bereitstellen:
   * [!UICONTROL Domain]
   * [!UICONTROL Port]
   * [!UICONTROL Benutzername]
   * [!UICONTROL Passwort]
* Für **[!UICONTROL SFTP mit SSH-Schlüssel]** -Verbindungen, müssen Sie Folgendes bereitstellen:
   * [!UICONTROL Domäne]
   * [!UICONTROL Port]
   * [!UICONTROL Benutzername]
   * [!UICONTROL SSH-Schlüssel]

* Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um eine Verschlüsselung mit PGP/GPG zu Ihren exportierten Dateien unter dem **[!UICONTROL Schlüssel]** Abschnitt. Ihr öffentlicher Schlüssel muss als [!DNL Base64] kodierter String.
* **[!UICONTROL Name]**: Wählen Sie einen passenden Namen für Ihr Ziel.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für Ihr Ziel ein.
* **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad an Ihrem Speicherort an, an dem Platform Ihre Exportdaten als CSV-Dateien hinterlegt.
* **[!UICONTROL Dateiformat]**: Auswählen **CSV** , um CSV-Dateien an Ihren Speicherort zu exportieren.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen über den Status des Datenflusses an Ihr Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnungen finden Sie im Handbuch zu [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung angegeben haben, wählen Sie **[!UICONTROL Nächste]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Siehe [Aktivieren von Zielgruppendaten für Batch-Profil-Export-Ziele](../../ui/activate-batch-profile-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

### Zielattribute {#destination-attributes}

Beim Aktivieren von Segmenten für dieses Ziel empfiehlt Adobe, eine eindeutige Kennung aus Ihrem [Vereinigungsschema](../../../profile/home.md#profile-fragments-and-union-schemas). Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weitere Informationen finden Sie unter [Best Practices beim Aktivieren von Zielgruppen für E-Mail-Marketing-Ziele](overview.md#best-practices).

## Exportierte Daten {#exported-data}

Für [!DNL Oracle Eloqua] Ziele, erstellt Platform eine `.csv` -Datei in dem von Ihnen angegebenen Speicherort gespeichert. Weitere Informationen zu den Dateien finden Sie unter [Segmentaktivierung überprüfen](../../ui/activate-batch-profile-destinations.md#verify) im Tutorial zur Segmentaktivierung.

## Datenimport einrichten in [!DNL Oracle Eloqua] {#import-data-into-eloqua}

Nach Anschluss [!DNL Platform] auf [!DNL SFTP] speichern, müssen Sie den Datenimport von Ihrem Speicherort zu [!DNL Oracle Eloqua]. Informationen dazu finden Sie unter [Kontakte oder Konten importieren](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) im [!DNL Oracle Eloqua Help Center].
