---
keywords: IP-Adresse, IP-Bereich, Zulassungsliste-Ziele
title: 'Zulassungsliste der IP-Adresse für Cloud-Datenspeicherung-Ziele '
type: Dokumentation
description: Diese Seite enthält IP-Bereiche, die Sie zu Ihrer Zulassungsliste hinzufügen können, um Daten sicher von der Experience Platform auf Ihren SFTP-Server, Amazon S3 oder die Azurblase-Datenspeicherung zu exportieren.
translation-type: tm+mt
source-git-commit: 7d7568de57cf79843a833a05b9bdfa6eb048bdbc
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---


# Zulassungsliste der IP-Adresse für Cloud-Datenspeicherung-Ziele {#ip-address-allow-list}

## Übersicht {#overview}

>[!IMPORTANT]
>
> * Adobe empfiehlt, dass Sie diese Seite mit einem Lesezeichen versehen und alle drei Monate erneut aufrufen, um nach den neuesten IP-Adressen zu suchen. Adobe stellt keine Benachrichtigung über neue IP-Bereiche bereit.
> * Während Adobe Datenexporte auf SFTP-Server unterstützt, werden für den Datenexport in die Cloud die Speicherorte [!DNL Amazon S3] und [!DNL Azure Blob] empfohlen.


Diese Seite enthält IP-Bereiche, die Sie Ihrer Zulassungsliste hinzufügen können, um Daten sicher von der Experience Platform in die Datenspeicherung [SFTP-Server](./sftp.md), [Amazon S3](./amazon-s3.md) oder [Blaue Blase](./azure-blob.md) zu exportieren.

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