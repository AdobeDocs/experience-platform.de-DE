---
keywords: IP-Adresse, IP-Bereich, Zulassungsliste-Ziele, Zulassungsliste auf die Zulassungsliste setzte, Streaming-Ziele
title: IP-Adressen-Zulassungsliste für Streaming-Ziele
type: Documentation
description: Auf dieser Seite finden Sie IP-Bereiche, die Sie Ihrer Zulassungsliste hinzufügen können, um Daten aus Experience Platform sicher in Ihren HTTP-REST-API-Endpunkt, Amazon Kinesis oder Ihre Azure Event Hubs-Instanz zu exportieren.
exl-id: f41303bd-c886-4c67-9e39-21efc3f5b768
source-git-commit: 5c67466f5321038e75d22e216a8be2e745adac49
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 8%

---

# IP-Adressen-Zulassungsliste für Streaming-Ziele {#ip-address-allowlist}

>[!IMPORTANT]
>
> * Adobe empfiehlt, ein Lesezeichen für diese Seite zu erstellen und sie alle drei Monate erneut aufzurufen, um nach den neuesten IP-Adressen zu suchen. Adobe bietet keine Benachrichtigung über neue IP-Bereiche.
> * Die Liste der hier dokumentierten IPs *gilt nicht* für Ziele, die Sie mit [[!DNL Destination SDK]](/help/destinations/destination-sdk/overview.md) erstellen.

## Überblick {#overview}

Die hier dokumentierten IP-Bereiche gelten für die folgenden Ziele:

* [HTTP-API-Ziel](./http-destination.md)
* [[!DNL Amazon Kinesis]](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)
* [[!DNL Azure Event Hubs]](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)

Der von Experience Platform an diese Ziele ausgehende Traffic durchläuft immer die auf dieser Seite aufgelisteten IPs.

Auf dieser Seite finden Sie IP-Bereiche, die Sie Ihrer Zulassungsliste hinzufügen können, um Daten aus Experience Platform sicher in Ihren HTTP-Endpunkt, Ihre [!DNL Amazon Kinesis] oder Ihre [!DNL Azure Event Hubs]-Instanz zu exportieren. Diese Funktion ist besonders nützlich, wenn sich Ihr HTTP-Endpunkt hinter einer Unternehmens-Firewall befindet oder wenn Ihre Sicherheits- und Compliance-Standards des Unternehmens eine Liste von IP-Bereichen erfordern, die auf die Zulassungsliste gesetzt werden müssen.

Sie können Netzwerkzugriffssteuerungen über Ihre Netzwerk-Firewall definieren. Durch Angabe des entsprechenden IP-Bereichs können Sie Traffic für den Datenübertragungs-Service zulassen.

Adobe auf die Zulassungsliste setzen empfiehlt, die folgenden IP-Bereiche zu einer -Seite hinzuzufügen, bevor Sie mit den oben genannten Zielen auf dieser Seite arbeiten. Wenn Sie Ihren regionsspezifischen IP-Bereich nicht zu Ihrer Zulassungsliste hinzufügen, kann dies zu Fehlern oder Leistungseinbußen bei der Verwendung dieser Streaming-Ziele führen.

## VA7: Kunden aus den USA und Amerika {#us-americas}

* `4.152.211.251`
* `20.22.83.112`
* `20.186.185.181`
* `20.186.185.227`
* `20.186.185.239`
* `40.70.154.136/29`
* `52.254.105.192/28`
* `52.254.106.0/28`
* `52.254.106.144/28`
* `52.254.106.160/28`
* `52.254.106.176/28`
* `52.254.106.192/28`
* `52.254.106.208/28`
* `52.254.106.224/28`
* `52.254.106.240/28`
* `52.254.107.0/28`
* `52.254.107.16/28`
* `52.254.107.32/28`
* `52.254.107.64/28`
* `52.254.107.80/28`
* `52.254.107.128/28`
* `52.254.107.144/28`

## VA6: Kunden aus den USA und Amerika, die mit AWS arbeiten {#aws}

Der folgende IP-Bereich gilt für Experience Platform-Kunden, die mit Amazon Web Services (AWS) arbeiten. Weitere Informationen dazu finden Sie in der Übersicht [ Experience Platform Multi-Cloud .](../../../landing/multi-cloud.md)

* `3.209.222.108`
* `3.211.230.204`
* `35.169.227.49`
* `66.117.18.133`
* `66.117.18.134`
* `66.117.18.135`

## NLD2: EMEA-Kunden {#emea}

* `20.50.23.153`
* `20.101.246.9`
* `40.74.3.176/28`
* `40.74.4.144/28`
* `40.74.4.160/28`
* `40.74.4.176/28`
* `40.74.5.128/28`
* `40.74.6.80/28`
* `40.74.6.96/28`
* `40.74.6.112/28`
* `40.74.6.128/28`
* `40.74.6.144/28`
* `40.74.7.128/28`
* `40.74.7.144/28`
* `40.74.7.160/28`
* `40.74.7.176/28`
* `40.74.7.192/28`
* `40.74.7.208/28`
* `51.105.144.1`
* `51.105.144.81`
* `51.124.70.4`
* `51.144.184.248/29`
* `52.142.236.87`
* `108.141.12.47`

## AUS5: APAC-Kunden {#apac}

* `20.40.188.166`
* `20.40.188.194`
* `20.40.188.227`
* `20.40.191.96/28`
* `20.40.191.224/28`
* `20.40.191.240/28`
* `20.43.104.0/28`
* `20.43.104.16/28`
* `20.43.104.32/28`
* `20.43.104.48/28`
* `20.43.104.64/28`
* `20.43.104.80/28`
* `20.43.104.96/28`
* `20.43.104.112/28`
* `20.43.104.128/28`
* `20.43.104.144/28`
* `20.43.104.160/28`
* `20.43.104.176/28`
* `20.43.104.192/28`
* `20.43.105.0/28`
* `20.43.105.16/28`
* `20.43.105.32/28`
* `20.43.105.48/28`
* `20.227.35.177`
* `20.53.206.128`

## CAN2: Kanada-Kunden {#can}

* `20.104.46.64/28`
* `20.104.46.80/28`
* `20.104.46.128/28`
* `20.104.46.160/28`
* `20.116.145.94`
* `20.116.147.168`
* `20.200.70.192/28`
* `20.200.70.208/28`
* `20.200.70.224/28`
* `20.200.70.240/28`
* `20.200.71.0/28`
* `20.200.71.16/28`
* `20.200.71.32/28`
* `20.200.71.48/28`
* `20.200.71.64/28`
* `20.200.71.80/28`
* `20.200.71.96/28`
* `20.200.71.112/28`
* `20.200.71.128/28`
* `20.200.71.144/28`
* `20.200.71.160/28`
* `20.200.71.176/28`
* `20.200.93.180`
* `20.200.94.83`
* `20.200.94.116`

## GBR9: Großbritannien-Kunden {#gbr}

* `20.26.64.112/28`
* `20.26.64.208/28`
* `20.26.64.240/28`
* `20.26.65.0/28`
* `20.26.128.247`
* `20.26.130.226`
* `20.26.131.71`
* `20.108.119.100`
* `20.108.202.84`
* `20.254.1.128/28`
* `20.254.2.32/28`
* `20.254.2.128/28`
* `20.254.2.208/28`
* `20.254.3.32/28`
* `20.254.3.48/28`
* `20.254.3.112/28`
* `20.254.3.144/28`
* `20.254.3.176/28`
* `20.254.3.192/28`
* `20.254.3.240/28`
* `20.254.4.0/28`
* `20.254.4.16/28`
* `20.254.4.32/28`
* `20.254.4.64/28`
* `20.254.4.96/28`

## IND2: Indien-Kunden {#india}

* `4.188.4.11`
* `4.188.4.99`
* `4.188.4.138`
* `4.188.4.154`
* `4.188.4.167`
* `4.213.40.145`
* `4.224.74.0/28`
* `4.224.74.64/28`
* `4.224.74.80/28`
* `4.224.74.96/28`
* `20.244.74.112/28`
* `20.244.77.0/28`
* `20.244.77.16/28`
* `20.244.77.160/28`
* `20.244.77.208/28`
* `20.244.78.0/28`
* `20.244.78.208/28`
* `20.244.79.0/28`
* `20.244.79.16/28`
* `20.244.79.48/28`
* `20.244.79.80/28`
* `20.244.79.128/28`
* `20.244.79.144/28`
* `20.244.79.192/28`
* `20.244.79.208/28`
* `20.244.79.224/28`
