---
keywords: SFTP;sftp
title: SFTP-Ziel
seo-title: SFTP-Ziel
description: Stellen Sie mit Ihrem SFTP-Server eine aktive ausgehende Verbindung her, um durch Trennzeichen getrennte Datendateien regelmäßig aus Experience Platform zu exportieren.
seo-description: Stellen Sie mit Ihrem SFTP-Server eine aktive ausgehende Verbindung her, um durch Trennzeichen getrennte Datendateien regelmäßig aus Experience Platform zu exportieren.
translation-type: tm+mt
source-git-commit: cbd748c1881c61f5e636567d94b68f2cf7302fa5
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 77%

---


# SFTP-Ziel

## Übersicht

Stellen Sie mit Ihrem SFTP-Server eine aktive ausgehende Verbindung her, um durch Trennzeichen getrennte Datendateien regelmäßig aus Experience Platform zu exportieren.

Führen Sie zum Exportieren von Daten die folgenden Schritte aus:

## Ziel verbinden {#connect-destination}

Anweisungen zum Herstellen einer Verbindung mit Ihren Cloud-Speicher-Zielen, einschließlich SFTP, finden Sie unter [Workflow für Cloud-Speicher-Ziele](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md).

Geben Sie für SFTP-Ziele im Workflow zur Erstellung eines Ziels im Schritt **Authentifizierung** die folgenden Daten ein:

* **Host**: die Adresse Ihres SFTP-Speicherorts
* **Benutzername**: der Benutzername, mit dem Sie sich bei Ihrem SFTP-Speicherort anmelden
* **Passwort**: das Passwort, mit dem Sie sich beim SFTP-Speicherort anmelden

## Exportierte Daten {#exported-data}

For SFTP destinations, Adobe Real-time CDP creates a tab-delimited `.txt` or `.csv` file in the storage location that you provided. Weitere Informationen zu den Dateien finden Sie unter [E-Mail-Marketing-Ziele und Cloud-Datenspeicherung-Ziele](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) im Tutorial zur Aktivierung von Segmenten.