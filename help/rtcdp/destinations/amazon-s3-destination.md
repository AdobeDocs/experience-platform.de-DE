---
title: Amazon S3-Ziel
seo-title: Amazon S3-Ziel
description: Erstellen Sie eine aktive ausgehende Verbindung zu Ihrem Amazon Web Services (AWS) S3-Speicher, um in regelmäßigen Abständen tabulatorgetrennte oder CSV-Datendateien aus Adobe Experience Platform in Ihre eigenen S3-Buckets zu exportieren.
seo-description: Erstellen Sie eine aktive ausgehende Verbindung zu Ihrem Amazon Web Services (AWS) S3-Speicher, um in regelmäßigen Abständen tabulatorgetrennte oder CSV-Datendateien aus Adobe Experience Platform in Ihre eigenen S3-Buckets zu exportieren.
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 51%

---


# [!DNL Amazon S3] Ziel

## Übersicht

Create a live outbound connection to your [!DNL Amazon Web Services] (AWS) S3 storage to periodically export tab-delimited or CSV data files from Adobe Experience Platform into your own S3 buckets.

## Ziel verbinden {#connect-destination}

See [Cloud storage destinations workflow ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)for instructions on how to connect to your cloud storage destinations, including [!DNL Amazon S3].

For [!DNL Amazon S3] destinations, enter the following information in the create destination workflow:

* **[!DNL Amazon S3]Zugriffsschlüssel und[!DNL Amazon S3]geheimer Schlüssel **: Generieren Sie in[!DNL Amazon S3]diesem Fall einen Zugriffsschlüssel - ein Schlüssel-Paar für den geheimen Zugriff, um Adobe CDP-Zugriff auf Ihr[!DNL Amazon S3]Konto zu gewähren.



>[!IMPORTANT]
>
>Die Adobe-Echtzeit-CDP benötigt `write`-Berechtigungen für das Bucket-Objekt, für das die Exportdateien bereitgestellt werden.
