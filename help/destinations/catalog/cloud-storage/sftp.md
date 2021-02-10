---
keywords: SFTP;SFTP
title: SFTP-Verbindung
description: Stellen Sie mit Ihrem SFTP-Server eine aktive ausgehende Verbindung her, um durch Trennzeichen getrennte Datendateien regelmäßig aus Experience Platform zu exportieren.
translation-type: tm+mt
source-git-commit: e13a19640208697665b0a7e0106def33fd1e456d
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 39%

---


# SFTP-Verbindung

Stellen Sie mit Ihrem SFTP-Server eine aktive ausgehende Verbindung her, um durch Trennzeichen getrennte Datendateien regelmäßig aus Experience Platform zu exportieren.

## Exporttyp {#export-type}

**Profil-basiert** : Sie exportieren alle Segmentmitglieder zusammen mit den gewünschten Segmentfeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm &quot;Attribute auswählen&quot;des Arbeitsablaufs für die  [Ziel-Aktivierung](../../ui/activate-destinations.md#select-attributes) ausgewählt.

![SFTP-Profil-basierter Exporttyp](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Ziel verbinden {#connect-destination}

Anweisungen zum Herstellen einer Verbindung mit Ihren Cloud-Speicher-Zielen, einschließlich SFTP, finden Sie unter [Workflow für Cloud-Speicher-Ziele](./workflow.md).

Geben Sie für SFTP-Ziele im Workflow zur Erstellung eines Ziels im Schritt **Authentifizierung** die folgenden Daten ein:

* **Host**: Die Adresse Ihres SFTP-Datenspeicherung-Speicherorts
* **Benutzername**: Der Benutzername für die Anmeldung beim Speicherort der SFTP-Datenspeicherung
* **Kennwort**: Das Kennwort zum Anmelden beim Speicherort der SFTP-Datenspeicherung

## Exportierte Daten {#exported-data}

Bei SFTP-Zielen erstellt Platform eine tabulatorgetrennte Datei `.txt` oder `.csv` im angegebenen Speicherort der Datenspeicherung. Weitere Informationen zu den Aktivierungen finden Sie unter [E-Mail-Marketing-Ziele und Cloud-Datenspeicherung-Ziele](../../ui/activate-destinations.md#esp-and-cloud-storage) im Tutorial zur Segmentbildung.