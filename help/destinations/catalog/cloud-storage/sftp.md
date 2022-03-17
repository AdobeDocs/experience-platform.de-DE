---
keywords: SFTP; SFTP
title: SFTP-Verbindung
description: Erstellen Sie eine ausgehende Live-Verbindung zu Ihrem SFTP-Server, um durch Trennzeichen getrennte Datendateien regelmäßig aus Adobe Experience Platform zu exportieren.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 691e3181e05a24b6bb0ebbe8e0f797a2b4c572d2
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 2%

---

# SFTP-Verbindung

## Übersicht {#overview}

Erstellen Sie eine ausgehende Live-Verbindung zu Ihrem SFTP-Server, um durch Trennzeichen getrennte Datendateien regelmäßig aus Adobe Experience Platform zu exportieren.

>[!IMPORTANT]
>
> Adobe unterstützt zwar Datenexporte an SFTP-Server, die empfohlenen Cloud-Speicherorte zum Exportieren von Daten sind jedoch [!DNL Amazon S3] und [!DNL Azure Blob].

## Exportart und -frequenz {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm Profilattribute im [Zielaktivierungs-Workflow](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Mehr dazu [Batch-dateibasierte Ziele](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

![SFTP-profilbasierter Exporttyp](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Mit Ziel verbinden {#connect}

Gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md).

### Verbindungsparameter {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="RSA-öffentlicher Schlüssel"
>abstract="Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien Verschlüsselung hinzuzufügen. Ihr öffentlicher Schlüssel muss als Base64-kodierte Zeichenfolge geschrieben werden."

while [Einrichten](../../ui/connect-destination.md) An diesem Ziel müssen Sie die folgenden Informationen angeben:

* **Host**: Die Adresse Ihres SFTP-Speicherorts
* **Benutzername**: Der Benutzername für die Anmeldung bei Ihrem SFTP-Speicherort
* **Passwort**: Das Kennwort für die Anmeldung bei Ihrem SFTP-Speicherort
* **[!UICONTROL Name]**: Geben Sie einen Namen ein, der Ihnen bei der Identifizierung dieses Ziels hilft.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung dieses Ziels ein.
* **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad zum Zielordner ein, der die exportierten Dateien hosten soll.

Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien Verschlüsselung hinzuzufügen. Ihr öffentlicher Schlüssel muss als [!DNL Base64] kodierter String.

## Exportierte Daten {#exported-data}

Für [!DNL SFTP] Ziele, erstellt Platform eine `.csv` -Datei in dem von Ihnen angegebenen Speicherort gespeichert. Weitere Informationen zu den Dateien finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profil-Export-Ziele](../../ui/activate-batch-profile-destinations.md) im Tutorial zur Segmentaktivierung.

## IP-Adressen-Zulassungsliste

Siehe [IP-Adressen-Zulassungsliste für Cloud-Speicher-Ziele](ip-address-allow-list.md) , wenn Sie einer Zulassungsliste Adobe-IPs hinzufügen müssen.
