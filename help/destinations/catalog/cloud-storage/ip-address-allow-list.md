---
title: IP-Adressen-Zulassungsliste für dateibasierte Cloud-Speicher-Ziele
type: Documentation
description: Auf dieser Seite finden Sie IP-Bereiche, die Sie Ihrer Zulassungsliste hinzufügen können, um Daten sicher von Experience Platform an Cloud-Speicher-Ziele zu exportieren.
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
source-git-commit: 1d8ba11b1043fa68bf3c0205e8cecc2de8910234
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 6%

---

# IP-Adresse Zulassungsliste für dateibasierte Cloud-Speicher-Ziele {#ip-address-allow-list-cloud-storage}

>[!IMPORTANT]
>
> * Adobe empfiehlt, diese Seite mit einem Lesezeichen zu versehen und alle drei Monate erneut zu besuchen, um nach den neuesten IP-Adressen zu suchen. Adobe stellt keine Benachrichtigung über neue IP-Bereiche bereit.
> * Während Adobe Datenexporte an SFTP-Server unterstützt, sind die empfohlenen Cloud-Speicherorte für den Datenexport folgende: [!DNL Amazon S3] und [!DNL Azure Blob].

## Anwendbarkeit {#applicability}

Die IP-Bereichsinformationen auf dieser Seite gelten für die folgenden dateibasierten Cloud-Speicher-Connectoren im Zielkatalog:

* [[!UICONTROL Amazon S3]](./amazon-s3.md)
* [[!UICONTROL Google Cloud Storage]](google-cloud-storage.md)
* [SFTP](./sftp.md)

>[!IMPORTANT]
>
>Die auf dieser Seite dokumentierten IP-Bereiche sind *not* unterstützt für die folgenden dateibasierten Cloud-Speicher-Ziele: [!UICONTROL Azure Blob], [!UICONTROL Azure Data Lake Storage Gen2] und [!UICONTROL Data Landing Zone].

## Übersicht {#overview}

Auf dieser Seite finden Sie IP-Bereiche, die Sie Ihrer Zulassungsliste hinzufügen können, um Daten sicher von Experience Platform an mehrere Cloud-Speicher-Ziele zu exportieren.

Sie können Netzwerkzugriffssteuerungen über Ihre Netzwerk-Firewall definieren. Durch Angabe des entsprechenden IP-Bereichs können Sie Traffic für den Datenübertragungsdienst zulassen.

Adobe empfiehlt, dass Sie die folgenden IP-Bereiche zu einer Zulassungsliste hinzufügen, bevor Sie mit Cloud-Speicher-Zielverbindungen arbeiten. Wenn Sie Ihren regionsspezifischen IP-Bereich nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung der Zielverbindungen des Cloud-Speichers zu Fehlern oder Leistungseinbußen führen.

## Erforderlich für alle Kunden {#all-customers}

* `52.247.108.70`

## US-Kunden {#us-customers}

* `52.252.71.64/29`

## Kanada-Kunden {#canada-customers}

* `20.220.135.16/29`

## EMEA-Kunden {#emea-customers}

* `51.137.8.208/29`

## UK-Kunden {#uk-customers}

* `20.26.133.96/29`

## APAC-Kunden {#apac-customers}

* `20.53.201.168/29`
