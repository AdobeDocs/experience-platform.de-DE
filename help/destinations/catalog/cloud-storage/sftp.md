---
keywords: SFTP;SFTP
title: SFTP-Verbindung
description: Erstellen Sie eine Live-ausgehende Verbindung mit Ihrem SFTP-Server, um in regelmäßigen Abständen durch Trennzeichen getrennte Datendateien aus Adobe Experience Platform zu exportieren.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 8%

---


# SFTP-Verbindung

## Übersicht {#overview}

Erstellen Sie eine Live-ausgehende Verbindung mit Ihrem SFTP-Server, um in regelmäßigen Abständen durch Trennzeichen getrennte Datendateien aus Adobe Experience Platform zu exportieren.

>[!IMPORTANT]
>
> Während Adobe Datenexporte auf SFTP-Server unterstützt, werden für den Datenexport in die Cloud die Speicherorte [!DNL Amazon S3] und [!DNL Azure Blob] empfohlen.

## Exporttyp {#export-type}

**Profil-basiert** : Sie exportieren alle Segmentmitglieder zusammen mit den gewünschten Segmentfeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm &quot;Attribute auswählen&quot;des Arbeitsablaufs für die  [Ziel-Aktivierung](../../ui/activate-destinations.md#select-attributes) ausgewählt.

![SFTP-Profil-basierter Exporttyp](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Ziel verbinden {#connect-destination}

Anweisungen zum Herstellen einer Verbindung mit Ihren Cloud-Datenspeicherung-Zielen, einschließlich SFTP, finden Sie im Arbeitsablauf [Cloud-Datenspeicherung-Ziele ](./workflow.md).

Geben Sie für SFTP-Ziele im Workflow zur Erstellung eines Ziels im Schritt **Authentifizierung** die folgenden Daten ein:

* **Host**: Die Adresse Ihres SFTP-Datenspeicherung-Speicherorts
* **Benutzername**: Der Benutzername für die Anmeldung beim Speicherort der SFTP-Datenspeicherung
* **Kennwort**: Das Kennwort zum Anmelden beim Speicherort der SFTP-Datenspeicherung

## Exportierte Daten {#exported-data}

Bei SFTP-Zielen erstellt Platform eine tabulatorgetrennte Datei `.txt` oder `.csv` im angegebenen Speicherort der Datenspeicherung. Weitere Informationen zu den Aktivierungen finden Sie unter [E-Mail-Marketing-Ziele und Cloud-Datenspeicherung-Ziele](../../ui/activate-destinations.md#esp-and-cloud-storage) im Tutorial zur Segmentbildung.

## Zulassungsliste der IP-Adresse

Informationen zum Hinzufügen von IPs zu einer Zulassungsliste finden Sie unter [IP-Adresse-Zulassungsliste für Cloud-Datenspeicherung-Ziele](./ip-address-allow-list.md).