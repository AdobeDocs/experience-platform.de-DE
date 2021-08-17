---
keywords: SFTP; SFTP
title: SFTP-Verbindung
description: Erstellen Sie eine ausgehende Live-Verbindung zu Ihrem SFTP-Server, um durch Trennzeichen getrennte Datendateien regelmäßig aus Adobe Experience Platform zu exportieren.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 8d1594aeb1d6671eec187643245d940ed3ff74cd
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---

# SFTP-Verbindung

## Übersicht {#overview}

Erstellen Sie eine ausgehende Live-Verbindung zu Ihrem SFTP-Server, um durch Trennzeichen getrennte Datendateien regelmäßig aus Adobe Experience Platform zu exportieren.

>[!IMPORTANT]
>
> Adobe unterstützt zwar Datenexporte an SFTP-Server, die empfohlenen Cloud-Speicherorte zum Exportieren von Daten sind jedoch [!DNL Amazon S3] und [!DNL Azure Blob].

## Exporttyp {#export-type}

**Profilbasiert**  - Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm &quot;Attribute auswählen&quot;des  [Zielaktivierungs-Workflows](../../ui/activate-destinations.md#select-attributes) ausgewählt.

![SFTP-profilbasierter Exporttyp](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Mit Ziel verbinden {#connect}

Um eine Verbindung zu diesem Ziel herzustellen, führen Sie die Schritte aus, die im Tutorial [Zielkonfiguration](../../ui/connect-destination.md) beschrieben sind.

### Verbindungsparameter {#parameters}

Während [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **Host**: Die Adresse Ihres SFTP-Speicherorts
* **Benutzername**: Der Benutzername für die Anmeldung bei Ihrem SFTP-Speicherort
* **Kennwort**: Das Kennwort für die Anmeldung bei Ihrem SFTP-Speicherort
* **[!UICONTROL Name]**: Geben Sie einen Namen ein, der Ihnen bei der Identifizierung dieses Ziels hilft.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung dieses Ziels ein.
* **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad zum Zielordner ein, der die exportierten Dateien hosten soll.

Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien Verschlüsselung hinzuzufügen. Ihr öffentlicher Schlüssel muss als [!DNL Base64] kodierte Zeichenfolge geschrieben werden.

## Exportierte Daten {#exported-data}

Für [!DNL SFTP]-Ziele erstellt Platform eine tabulatorgetrennte `.csv`-Datei am von Ihnen angegebenen Speicherort. Weitere Informationen zu den Dateien finden Sie unter [E-Mail-Marketing-Ziele und Cloud-Speicher-Ziele](../../ui/activate-destinations.md#esp-and-cloud-storage) im Tutorial zur Segmentaktivierung.

## IP-Adressen-Zulassungsliste

Informationen zum Hinzufügen von Adobe-IPs zu einer Zulassungsliste finden Sie unter [IP-Adressen-Zulassungsliste für Cloud-Speicher-Ziele](ip-address-allow-list.md) .
