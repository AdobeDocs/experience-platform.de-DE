---
keywords: SFTP; SFTP
title: SFTP-Verbindung
description: Erstellen Sie eine ausgehende Live-Verbindung zu Ihrem SFTP-Server, um durch Trennzeichen getrennte Datendateien regelmäßig aus Adobe Experience Platform zu exportieren.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 0b094e635e6d22e58e5aa79a374df0879167a833
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 7%

---

# SFTP-Verbindung

## Übersicht {#overview}

Erstellen Sie eine ausgehende Live-Verbindung zu Ihrem SFTP-Server, um durch Trennzeichen getrennte Datendateien regelmäßig aus Adobe Experience Platform zu exportieren.

>[!IMPORTANT]
>
> Experience Platform unterstützt zwar Datenexporte an SFTP-Server, die empfohlenen Cloud-Speicherorte zum Exportieren von Daten sind jedoch [!DNL Amazon S3] und [!DNL Azure Blob].

## Exportart und -frequenz {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm Profilattribute im [Zielaktivierungs-Workflow](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Mehr dazu [Batch-dateibasierte Ziele](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

![SFTP-profilbasierter Exporttyp](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Herstellen einer Verbindung mit der Datenbank {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Verbindungsparameter {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="RSA-öffentlicher Schlüssel"
>abstract="Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien Verschlüsselung hinzuzufügen. Ihr öffentlicher Schlüssel muss als Base64-kodierte Zeichenfolge geschrieben werden."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="SSH-Schlüssel"
>abstract="Der SSH-Schlüssel erfordert eine Base64-Zeichenfolge."

Wann [Verbindung](../../ui/connect-destination.md) zu diesem Ziel hinzufügen, müssen Sie die folgenden Informationen angeben:

#### Authentifizierungsinformationen {#authentication-information}

Wenn Sie die **[!UICONTROL Grundlegende Authentifizierung]** Typ, um eine Verbindung zu Ihrem SFTP-Speicherort herzustellen:

![Grundlegende SFTP-Zielauthentifizierung](../..//assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL Host]**: Die Adresse Ihres SFTP-Speicherorts;
* **[!UICONTROL Benutzername]**: Der Benutzername für die Anmeldung bei Ihrem SFTP-Speicherort.
* **[!UICONTROL Passwort]**: Das Kennwort für die Anmeldung bei Ihrem SFTP-Speicherort.
* **[!UICONTROL Verschlüsselungsschlüssel]**: Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien Verschlüsselung hinzuzufügen. Ihr öffentlicher Schlüssel muss als [!DNL Base64] kodierter String.
   * Beispiel: `----BEGIN PGP PUBLIC KEY BLOCK---- {Base64-encoded string} ----END PGP PUBLIC KEY BLOCK----`. Unten finden Sie ein Beispiel für einen korrekt formatierten PGP-Schlüssel, bei dem der mittlere Teil gekürzt ist.

      ![PGP-Schlüssel](../..//assets/catalog/cloud-storage/sftp/pgp-key.png)


Wenn Sie die **[!UICONTROL SFTP mit SSH-Schlüssel]** Authentifizierungstyp für die Verbindung mit Ihrem SFTP-Speicherort:

![SFTP-Ziel-SSH-Schlüsselauthentifizierung](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL Domäne]**: Geben Sie die IP-Adresse oder den Domänennamen Ihres SFTP-Kontos ein.
* **[!UICONTROL Port]**: Der von Ihrem SFTP-Speicherort verwendete Port;
* **[!UICONTROL Benutzername]**: Der Benutzername für die Anmeldung bei Ihrem SFTP-Speicherort.
* **[!UICONTROL SSH-Schlüssel]**: Der SSH-Schlüssel zum Anmelden bei Ihrem SFTP-Speicherort.
* **[!UICONTROL Verschlüsselungsschlüssel]**: Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien Verschlüsselung hinzuzufügen. Ihr öffentlicher Schlüssel muss als [!DNL Base64] kodierter String.
   * Beispiel: `----BEGIN PGP PUBLIC KEY BLOCK---- {Base64-encoded string} ----END PGP PUBLIC KEY BLOCK----`. Unten finden Sie ein Beispiel für einen korrekt formatierten PGP-Schlüssel, bei dem der mittlere Teil gekürzt ist.

      ![PGP-Schlüssel](../..//assets/catalog/cloud-storage/sftp/pgp-key.png)

#### Zieldetails {#destination-details}

Geben Sie nach Herstellung der Authentifizierungsverbindung zum SFTP-Speicherort die folgenden Informationen für das Ziel ein:

![Verfügbare Zieldetails für SFTP-Ziel](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL Name]**: Geben Sie einen Namen ein, der Ihnen bei der Identifizierung dieses Ziels in der Benutzeroberfläche von Experience Platform hilft;
* **[!UICONTROL Beschreibung]**: eine Beschreibung für dieses Ziel eingeben;
* **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad zum Ordner in Ihrem SFTP-Speicherort ein, in den die Dateien exportiert werden sollen.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Siehe [Aktivieren von Zielgruppendaten für Batch-Profil-Export-Ziele](../../ui/activate-batch-profile-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

## Exportierte Daten {#exported-data}

Für [!DNL SFTP] Ziele, erstellt Platform eine `.csv` -Datei in dem von Ihnen angegebenen Speicherort gespeichert. Weitere Informationen zu den Dateien finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profil-Export-Ziele](../../ui/activate-batch-profile-destinations.md) im Tutorial zur Segmentaktivierung.

## IP-Adressen-Zulassungsliste

Siehe [IP-Adressen-Zulassungsliste für Cloud-Speicher-Ziele](ip-address-allow-list.md) , wenn Sie einer Zulassungsliste Adobe-IPs hinzufügen müssen.
