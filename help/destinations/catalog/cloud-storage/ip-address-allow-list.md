---
keywords: IP-Adresse, IP-Bereich, Zulassungsliste-Ziele, Zulassungsliste
title: 'Zulassungsliste der IP-Adresse für Cloud-Datenspeicherung-Ziele '
type: Documentation
description: Diese Seite enthält IP-Bereiche, die Sie zu Ihrer Zulassungsliste hinzufügen können, um Daten sicher von der Experience Platform auf Ihren SFTP-Server, Amazon S3 oder die Azurblase-Datenspeicherung zu exportieren.
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
translation-type: tm+mt
source-git-commit: 4cc7fb2714f6df8065a0531f7e507983940d662c
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# Zulassungsliste der IP-Adresse für Cloud-Datenspeicherung-Ziele {#ip-address-allow-list}

>[!IMPORTANT]
>
> * Adobe empfiehlt, dass Sie diese Seite mit einem Lesezeichen versehen und alle drei Monate erneut aufrufen, um nach den neuesten IP-Adressen zu suchen. Adobe stellt keine Benachrichtigung über neue IP-Bereiche bereit.
> * Während Adobe Datenexporte auf SFTP-Server unterstützt, werden für den Datenexport in die Cloud die Speicherorte [!DNL Amazon S3] und [!DNL Azure Blob] empfohlen.


## Übersicht {#overview}

Diese Seite enthält IP-Bereiche, die Sie zu Ihrer Zulassungsliste hinzufügen können, um Daten sicher von der Experience Platform in den [SFTP-Server](./sftp.md) zu exportieren.

Sie können Netzwerk-Zugriffskontrollen über Ihre Netzwerk-Firewall definieren. Durch Angabe des entsprechenden IP-Bereichs können Sie Traffic für den Datenübertragungsdienst zulassen.

Adobe empfiehlt, dass Sie die folgenden IP-Bereiche zu einer Zulassungsliste hinzufügen, bevor Sie mit den Zielverbindungen der Cloud-Datenspeicherung arbeiten. Wenn Sie Ihren regionsspezifischen IP-Bereich nicht zu Ihrer Zulassungsliste hinzufügen, kann dies zu Fehlern oder Leistungseinbußen führen, wenn Sie die Zielverbindungen der Cloud-Datenspeicherung verwenden.

## Erforderlich für alle Kunden

* `52.247.108.70`

## US-Kunden

* `52.252.71.64/29`

## EMEA-Kunden

* `51.137.8.208/29`

## APAC-Kunden

* `20.53.201.168/29`
