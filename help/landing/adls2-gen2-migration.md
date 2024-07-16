---
title: Data Lake Migration zu Gen2
description: Erfahren Sie mehr über die neuen Funktionen, die durch die Migration des Data Lake zu Gen2 in Adobe Experience Platform bereitgestellt werden.
exl-id: 56d9c77a-d7eb-498d-994f-b15d150dedb7
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Migration zum Adobe Experience Platform Data Lake auf Gen2

Adobe Experience Platform migriert zum Gen2 Data Lake. Dies ist eine neue Generation von Data Lake, der Platform-Benutzern Vorteile wie die Replikation von geografischen Regionen, feinere rollenbasierte Zugriffskontrollen (RBAC) und eine bessere Skalierung bietet.

## BenutzerAuswirkung

Während Adobe den Data Lake von Gen1 zu Gen 2 migriert, können Benutzer **lesen** vom Data Lake aus, aber alle Funktionen, die **write** in den Data Lake eintragen, sind betroffen. Nachfolgend finden Sie eine Liste der betroffenen Funktionen:

- **Quellen**: Daten aus Quellen und verschiedene Datenerfassungs-Workflows werden verzögert. Benutzer sehen ihre Daten nach Abschluss der Migration.
- **Abfragedienst**: Benutzer können Abfragen durchführen, aber die Ausgabe der Abfrage nicht in einen Datensatz schreiben.
- **Echtzeit-Kundenprofil**: Daten, die über die Aufnahme von **batch** in den Profilspeicher aufgenommen werden, stehen während der Migration nicht zur Verfügung. Daten, die über die Aufnahme von **Streaming** erfasst werden, stehen während der Migration jedoch zur Verfügung. Darüber hinaus stehen während der Migration keine Profilexporte zur Verfügung.
- **Data Science Workspace**: Schreibvorgänge aus Data Science Workspace schlagen fehl.
- **Segmentierungsdienst**: Zielgruppen, die aus der **Batch**-Segmentierung abgeleitet wurden, können während der Migration nicht aktiviert werden. Von der **Streaming**-Segmentierung abgeleitete Zielgruppen sind nicht betroffen.
- **Customer Journey Analytics**: Customer Journey Analytics meldet Daten möglicherweise veraltet und wird während der Migration nicht aktualisiert, da Batches nicht in den Data Lake aufgenommen werden.

## Kommunikation mit Platform-Benutzern

Adobe wird sich an die Systemadministratoren wenden, um die Auswirkungen der Migration ausführlich zu erörtern und die Migrationsdaten und -zeiten für bestimmte Organisationen zu bestätigen.
