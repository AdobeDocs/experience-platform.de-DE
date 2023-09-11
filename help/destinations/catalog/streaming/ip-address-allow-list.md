---
keywords: IP-Adresse, IP-Bereich, Zulassungsliste-Ziele, Zulassungsliste-Ziel, Streaming-Ziele für Zulassungslisten
title: IP-Adressen-Zulassungsliste für Streaming-Ziele
type: Documentation
description: Auf dieser Seite finden Sie IP-Bereiche, die Sie Ihrer Zulassungsliste hinzufügen können, um Daten sicher von Experience Platform an Ihren HTTP REST API-Endpunkt, Amazon Kinesis oder Azure Event Hub-Instanz zu exportieren.
exl-id: f41303bd-c886-4c67-9e39-21efc3f5b768
source-git-commit: ca3c9ed87f2365cc1d9e4ef5e4a6145266a11bba
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 9%

---

# IP-Adressen-Zulassungsliste für Streaming-Ziele {#ip-address-allowlist}

>[!IMPORTANT]
>
> * Adobe empfiehlt, diese Seite mit einem Lesezeichen zu versehen und alle drei Monate erneut zu besuchen, um nach den neuesten IP-Adressen zu suchen. Adobe stellt keine Benachrichtigung über neue IP-Bereiche bereit.
> * Die hier dokumentierte Liste der IPs *nicht* gelten für alle Ziele, die Sie mithilfe von [[!DNL Destination SDK]](/help/destinations/destination-sdk/overview.md).

## Übersicht {#overview}

Die hier dokumentierten IP-Bereiche gelten für die folgenden Ziele:

* [HTTP-API-Ziel](./http-destination.md)
* [[!DNL Amazon Kinesis]](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)
* [[!DNL Azure Event Hubs]](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)

Ausgehender Traffic von Experience Platform zu diesen Zielen durchläuft immer die auf dieser Seite aufgelisteten IPs.

Diese Seite enthält IP-Bereiche, die Sie zu Ihrer Zulassungsliste hinzufügen können, um Daten sicher von Experience Platform an Ihren HTTP-Endpunkt zu exportieren. [!DNL Amazon Kinesis]oder [!DNL Azure Event Hubs] -Instanz. Diese Funktion ist besonders nützlich, wenn sich Ihr HTTP-Endpunkt hinter einer Unternehmens-Firewall befindet oder wenn Ihre Unternehmens-Sicherheits- und Compliance-Standards eine Liste von IP-Bereichen erfordern, die auf die Zulassungsliste gesetzt werden müssen.

Sie können Netzwerkzugriffssteuerungen über Ihre Netzwerk-Firewall definieren. Durch Angabe des entsprechenden IP-Bereichs können Sie Traffic für den Datenübertragungsdienst zulassen.

Adobe empfiehlt, dass Sie die folgenden IP-Bereiche zu einer Zulassungsliste hinzufügen, bevor Sie mit den oben genannten Zielen auf dieser Seite arbeiten. Wenn Sie Ihren regionsspezifischen IP-Bereich nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung dieser Streaming-Ziele zu Fehlern oder Leistungseinbußen führen.

## VA7: Kunden in den USA und Amerika {#us-americas}

`20.186.185.239`
`40.70.154.136/29`
`52.254.106.160/28`
`52.254.106.176/28`
`52.254.105.192/28`
`20.186.185.181`
`52.254.107.64/28`
`52.254.107.80/28`
`52.254.106.144/28`
`52.254.106.0/28`
`52.254.107.16/28`
`52.254.107.32/28`
`52.254.106.224/28`
`20.186.185.227`
`52.254.106.192/28`
`52.254.107.128/28`
`52.254.106.208/28`
`52.254.106.240/28`
`52.254.107.0/28`
`52.254.107.144/28`
`20.22.83.112`

## NLD2: EMEA-Kunden {#emea}

`40.74.4.160/28`
`40.74.6.128/28`
`40.74.7.128/28`
`40.74.4.176/28`
`51.144.184.248/29`
`40.74.7.208/28`
`52.142.236.87`
`20.50.23.153`
`20.101.246.9`
`40.74.4.144/28`
`40.74.7.160/28`
`40.74.3.176/28`
`40.74.6.144/28`
`40.74.6.80/28`
`40.74.5.128/28`
`40.74.7.144/28`
`40.74.7.176/28`
`40.74.6.96/28`
`40.74.6.112/28`
`51.105.144.1`
`40.74.7.192/28`
`51.105.144.81`
`51.124.70.4`

## AUS5: APAC-Kunden {#apac}

`20.43.104.80/28`
`20.43.104.16/28`
`20.43.104.128/28`
`20.40.188.166`
`20.40.191.224/28`
`20.43.104.176/28`
`20.43.104.0/28`
`20.43.105.0/28`
`20.43.105.48/28`
`20.40.191.240/28`
`20.43.104.192/28`
`20.40.188.227`
`20.40.188.194`
`20.43.104.144/28`
`20.43.104.160/28`
`20.43.104.96/28`
`20.43.105.32/28`
`20.43.104.112/28`
`20.43.105.16/28`
`20.43.104.48/28`
`20.40.191.96/28`
`20.43.104.32/28`
`20.43.104.64/28`
`20.53.206.128`
`20.227.35.177`

## CAN2: Kanada-Kunden {#can}

`20.104.46.128/28`
`20.104.46.160/28`
`20.104.46.64/28`
`20.104.46.80/28`
`20.116.145.94`
`20.116.147.168`
`20.200.70.192/28`
`20.200.70.208/28`
`20.200.70.224/28`
`20.200.70.240/28`
`20.200.71.0/28`
`20.200.71.112/28`
`20.200.71.128/28`
`20.200.71.144/28`
`20.200.71.16/28`
`20.200.71.160/28`
`20.200.71.176/28`
`20.200.71.32/28`
`20.200.71.48/28`
`20.200.71.64/28`
`20.200.71.80/28`
`20.200.71.96/28`
`20.200.93.180`
`20.200.94.116`
`20.200.94.83`
