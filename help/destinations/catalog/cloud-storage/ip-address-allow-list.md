---
keywords: IP-Adresse, IP-Bereich, Zulassungsliste-Ziele, Zulassungsliste
title: 'IP-Adressen-Zulassungsliste für Cloud-Speicher-Ziele '
type: Documentation
description: Diese Seite enthält IP-Bereiche, die Sie Ihrer Zulassungsliste hinzufügen können, um Daten sicher von Experience Platform auf Ihren SFTP-Server, Amazon S3 oder Azure Blob-Speicher zu exportieren.
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
source-git-commit: c4d8ae6de2e1bbf23a25a66bde5dc88c13a13402
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# IP-Adresse - Zulassungsliste für Cloud-Speicher-Ziele {#ip-address-allow-list}

>[!IMPORTANT]
>
> * Adobe empfiehlt, diese Seite mit einem Lesezeichen zu versehen und alle drei Monate erneut aufzurufen, um nach den neuesten IP-Adressen zu suchen. Adobe stellt keine Benachrichtigung über neue IP-Bereiche bereit.
> * Adobe unterstützt zwar Datenexporte an SFTP-Server, die empfohlenen Cloud-Speicherorte zum Exportieren von Daten sind jedoch [!DNL Amazon S3] und [!DNL Azure Blob].


## Übersicht {#overview}

Auf dieser Seite finden Sie IP-Bereiche, die Sie zu Ihrer Zulassungsliste hinzufügen können, um Daten sicher von der Experience Platform in Ihre [SFTP-Server](./sftp.md).

Sie können Netzwerkzugriffssteuerungen über Ihre Netzwerk-Firewall definieren. Durch Angabe des entsprechenden IP-Bereichs können Sie Traffic für den Datenübertragungsdienst zulassen.

Adobe empfiehlt, die folgenden IP-Bereiche einer Zulassungsliste hinzuzufügen, bevor Sie mit Zielverbindungen des Cloud-Speichers arbeiten. Wenn Sie Ihren regionsspezifischen IP-Bereich nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung der Zielverbindungen des Cloud-Speichers zu Fehlern oder Leistungseinbußen führen.

## Erforderlich für alle Kunden

* `52.247.108.70`

## US-Kunden

* `52.252.71.64/29`

## EMEA-Kunden

* `51.137.8.208/29`

## APAC-Kunden

* `20.53.201.168/29`
