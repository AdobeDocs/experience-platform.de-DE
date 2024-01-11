---
title: SFTP-Ziele für die IP-Adressen-Zulassungsliste
type: Documentation
description: Diese Seite enthält IP-Bereiche, die Sie Ihrer Zulassungsliste hinzufügen können, um Daten sicher von Experience Platform auf Ihren SFTP-Server zu exportieren.
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
source-git-commit: 52186e03ba2a9d8b105d01ebfcd9be7666bfb6ff
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 8%

---

# IP-Adressen-Zulassungsliste für SFTP-Ziele {#ip-address-allow-list-sftp}

>[!IMPORTANT]
>
> * Adobe empfiehlt, diese Seite mit einem Lesezeichen zu versehen und alle drei Monate erneut zu besuchen, um nach den neuesten IP-Adressen zu suchen. Adobe stellt keine Benachrichtigung über neue IP-Bereiche bereit.
> * Während Adobe Datenexporte an SFTP-Server unterstützt, sind die empfohlenen Cloud-Speicherorte für den Datenexport folgende: [!DNL Amazon S3] und [!DNL Azure Blob].

## Übersicht {#overview}

Auf dieser Seite finden Sie IP-Bereiche, die Sie zu Ihrer Zulassungsliste hinzufügen können, um Daten sicher von Experience Platform in Ihre [SFTP-Server](./sftp.md).

Sie können Netzwerkzugriffssteuerungen über Ihre Netzwerk-Firewall definieren. Durch Angabe des entsprechenden IP-Bereichs können Sie Traffic für den Datenübertragungsdienst zulassen.

Adobe empfiehlt, dass Sie die folgenden IP-Bereiche zu einer Zulassungsliste hinzufügen, bevor Sie mit Cloud-Speicher-Zielverbindungen arbeiten. Wenn Sie Ihren regionsspezifischen IP-Bereich nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung der Zielverbindungen des Cloud-Speichers zu Fehlern oder Leistungseinbußen führen.

## Erforderlich für alle Kunden

* `52.247.108.70`

## US-Kunden

* `52.252.71.64/29`

## Kanada-Kunden

* `20.220.135.16/29`

## EMEA-Kunden

* `51.137.8.208/29`

## UK-Kunden

* `20.26.133.96/29`

## APAC-Kunden

* `20.53.201.168/29`
