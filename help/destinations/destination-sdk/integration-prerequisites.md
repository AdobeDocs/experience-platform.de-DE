---
description: Um Destination SDK verwenden zu können, muss ein Partnerunternehmen die in diesem Dokument aufgeführten Voraussetzungen erfüllen.
title: Voraussetzungen für die Integration
exl-id: 031af9f1-ce18-4056-bd53-199ce8b56be5
source-git-commit: d7c9623619e989a59d72aba74903ffc0e64e7d3c
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 1%

---

# Voraussetzungen für die Integration

Um Destination SDK zu verwenden, stellen Sie sicher, dass Sie die in den folgenden Abschnitten aufgelisteten technischen und partnerschaftlichen Voraussetzungen erfüllen.

## Technische/API-Voraussetzungen für Streaming-Ziele {#streaming-prerequisites}

1. Sie verfügen über einen REST-API-Endpunkt, an den Adobe Experience Platform die folgenden Datentypen bereitstellen kann:
   * Segmentzugehörigkeitsinformationen;
   * Profilidentitätsdaten;
   * (Optional) Zusätzliche Attribute für die Profilanreicherung.
2. Ihr REST-API-Endpunkt unterstützt die Authentifizierung von API-Token-Bearer oder das OAuth 2.0-Authentifizierungsprotokoll.
3. (Optional) Sie haben einen API- oder API-Endpunkt zum Erstellen/Aktualisieren/Löschen von Segmenten für die programmatische Metadatenverwaltung.

## Technische Voraussetzungen für Batch-Ziele {#batch-prerequisites}

1. Sie haben einen Zielspeicherort, der auf gehostet wird. [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage], SFTP, [!DNL Google Cloud]oder eine private [!DNL Data Landing Zone], wo Sie Dateien empfangen können, die aus Experience Platform exportiert wurden.
2. Ihre Zielplattform kann Dateien in dem Format erfassen, das über das [Dateiformatierungsoptionen](/help/destinations/destination-sdk/server-and-file-configuration.md#file-configuration) in Destination SDK für Batch-Ziele.
3. (Optional) Sie verfügen über eine API- oder API-Endpunkt zum Erstellen/Abrufen/Aktualisieren/Löschen (CRUD) von Segmenten für die programmgesteuerte Metadatenverwaltung.

## Voraussetzungen für die Partnerschaft {#partnership-prerequisites}

Wenn Sie ein unabhängiger Software-Anbieter (ISV) oder Systemintegrator (SI) sind und Destination SDK verwenden möchten, lesen Sie die Partnerschaftserfordernisse für ISVs und SIs im Abschnitt [Zugriffsabschnitt abrufen](./overview.md#get-access).
