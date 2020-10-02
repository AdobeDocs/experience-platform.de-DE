---
keywords: SFTP;sftp
title: SFTP-Ziel
seo-title: SFTP-Ziel
description: Stellen Sie mit Ihrem SFTP-Server eine aktive ausgehende Verbindung her, um durch Trennzeichen getrennte Datendateien regelmäßig aus Experience Platform zu exportieren.
seo-description: Stellen Sie mit Ihrem SFTP-Server eine aktive ausgehende Verbindung her, um durch Trennzeichen getrennte Datendateien regelmäßig aus Experience Platform zu exportieren.
translation-type: tm+mt
source-git-commit: d0a04c61bfe4024a2bb45ea7babab9073fcd6c22
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 60%

---


# SFTP-Ziel

## Übersicht

Stellen Sie mit Ihrem SFTP-Server eine aktive ausgehende Verbindung her, um durch Trennzeichen getrennte Datendateien regelmäßig aus Experience Platform zu exportieren.

## Exporttyp {#export-type}

**Profil-Export** : Sie exportieren alle Segmentmitglieder zusammen mit den gewünschten Segmentfeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm &quot;Attribute auswählen&quot;des Arbeitsablaufs für die [Ziel-Aktivierung](/help/rtcdp/destinations/activate-destinations.md#select-attributes)ausgewählt.

![SFTP-Profil-basierter Exporttyp](/help/rtcdp/destinations/assets/sftp-export-type.png)

## Ziel verbinden {#connect-destination}

Anweisungen zum Herstellen einer Verbindung mit Ihren Cloud-Speicher-Zielen, einschließlich SFTP, finden Sie unter [Workflow für Cloud-Speicher-Ziele](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md).

Geben Sie für SFTP-Ziele im Workflow zur Erstellung eines Ziels im Schritt **Authentifizierung** die folgenden Daten ein:

* **Host**: die Adresse Ihres SFTP-Speicherorts
* **Benutzername**: der Benutzername, mit dem Sie sich bei Ihrem SFTP-Speicherort anmelden
* **Passwort**: das Passwort, mit dem Sie sich beim SFTP-Speicherort anmelden

## Exportierte Daten {#exported-data}

For SFTP destinations, Adobe Real-time CDP creates a tab-delimited `.txt` or `.csv` file in the storage location that you provided. Weitere Informationen zu den Dateien finden Sie unter [E-Mail-Marketing-Ziele und Cloud-Datenspeicherung-Ziele](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) im Tutorial zur Aktivierung von Segmenten.