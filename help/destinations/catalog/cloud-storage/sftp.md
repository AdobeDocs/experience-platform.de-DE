---
keywords: SFTP;SFTP
title: SFTP-Verbindung
description: Erstellen Sie eine Live-ausgehende Verbindung mit Ihrem SFTP-Server, um in regelmäßigen Abständen durch Trennzeichen getrennte Datendateien aus Adobe Experience Platform zu exportieren.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: a21abb44bb9cbe6fefa0ff70a1ff19e31cc0c7de
workflow-type: tm+mt
source-wordcount: '230'
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

Für [!DNL SFTP]-Ziele erstellt Platform eine tabulatorgetrennte `.csv`-Datenspeicherung im angegebenen Speicherort. Weitere Informationen zu den Aktivierungen finden Sie unter [E-Mail-Marketing-Ziele und Cloud-Datenspeicherung-Ziele](../../ui/activate-destinations.md#esp-and-cloud-storage) im Tutorial zur Segmentbildung.

## Zulassungsliste der IP-Adresse

Informationen zum Hinzufügen von IPs zu einer Zulassungsliste finden Sie unter [IP-Adresse-Zulassungsliste für Cloud-Datenspeicherung-Ziele](./ip-address-allow-list.md).
