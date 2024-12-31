---
description: Um Destination SDK verwenden zu können, muss eine Partnerfirma die in diesem Dokument aufgeführten Voraussetzungen erfüllen.
title: Voraussetzungen für die Integration
exl-id: 031af9f1-ce18-4056-bd53-199ce8b56be5
source-git-commit: c1ba465a8a866bd8bdc9a2b294ec5d894db81e11
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 2%

---

# Voraussetzungen für die Integration

Um Destination SDK zu verwenden, stellen Sie sicher, dass Sie die in den folgenden Abschnitten aufgeführten technischen Voraussetzungen und Partnerschaftserfordernisse erfüllen.

## Technische/API-Voraussetzungen für Streaming-Ziele {#streaming-prerequisites}

1. Sie verfügen über einen REST-API-Endpunkt für Adobe Experience Platform, um die folgenden Datentypen für bereitzustellen:
   * Informationen zur Zielgruppenzugehörigkeit;
   * Informationen zur Profilidentität;
   * (Optional) Zusätzliche Attribute für die Profilanreicherung.
2. Ihr REST-API-Endpunkt unterstützt grundlegende Protokolle, Bearer-Token oder die OAuth 2.0-Authentifizierungsprotokolle.
3. (Optional) Sie haben eine API zum Erstellen/Aktualisieren/Löschen oder einen API-Endpunkt für die programmgesteuerte Metadatenverwaltung.

## Technische Voraussetzungen für Batch-Ziele {#batch-prerequisites}

1. Sie haben einen Zielspeicherort, der auf [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage], [!DNL SFTP], [!DNL Google Cloud] oder einem privaten [!DNL Data Landing Zone] gehostet wird, wo Sie Dateien empfangen können, die aus Experience Platform exportiert wurden.
2. Destination SDK Ihre Zielplattform kann Dateien in dem Format aufnehmen, das über die [Dateiformatierungsoptionen“ in der ](functionality/destination-server/file-formatting.md) für Batch-Ziele konfiguriert wurde.
3. (Optional) Sie haben eine Zielgruppen-API ([!DNL CRUD]) oder einen API-Endpunkt zum Erstellen/Abrufen/Aktualisieren/Löschen für die programmgesteuerte Metadatenverwaltung.

## Voraussetzungen für die Partnerschaft {#partnership-prerequisites}

Wenn Sie ein unabhängiger Software-Anbieter (ISV) oder Systemintegrator (SI) sind, der Destination SDK verwenden möchte, lesen Sie die Partnerschaftsanforderungen für ISVs und SIs im Abschnitt [Zugriff erhalten](overview.md#get-access).
