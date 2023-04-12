---
title: Data Lake Migration zu Gen2
description: Erfahren Sie mehr über die neuen Funktionen, die durch die Migration des Data Lake zu Gen2 in Adobe Experience Platform bereitgestellt werden.
exl-id: 56d9c77a-d7eb-498d-994f-b15d150dedb7
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# Migration zum Adobe Experience Platform Data Lake auf Gen2

Adobe Experience Platform migriert zum Gen2 Data Lake. Dies ist eine neue Generation von Data Lake, der Platform-Benutzern Vorteile wie die Replikation von geografischen Regionen, feinere rollenbasierte Zugriffskontrollen (RBAC) und eine bessere Skalierung bietet.

## BenutzerAuswirkung

Während Adobe den Data Lake von Gen1 zu Gen 2 migriert, können Benutzer **lesen** aus dem Data Lake, aber alle Funktionen, die **schreiben** in den Data Lake aufgenommen werden. Nachfolgend finden Sie eine Liste der betroffenen Funktionen:

- **Quellen**: Daten aus Quellen und verschiedenen Workflows zur Datenerfassung werden verzögert. Benutzer sehen ihre Daten nach Abschluss der Migration.
- **Query Service**: Benutzer können Abfragen durchführen, aber nicht die Ausgabe der Abfrage in einen Datensatz schreiben.
- **Echtzeit-Kundenprofil**: Daten, die über in den Profilspeicher aufgenommen werden **Batch** Die Aufnahme ist während der Migration nicht verfügbar. Daten, die über **Streaming** Die Aufnahme ist während der Migration verfügbar. Darüber hinaus stehen während der Migration keine Profilexporte zur Verfügung.
- **Data Science Workspace**: Schreibvorgänge aus Data Science Workspace schlagen fehl.
- **Segmentierungsdienst**: Aus **Batch** Die Segmentierung kann während der Migration nicht aktiviert werden. Aus **Streaming** Die Segmentierung ist nicht betroffen.
- **Customer Journey Analytics**: Customer Journey Analytics meldet Daten sind möglicherweise veraltet und werden während der Migration nicht aktualisiert, da Batches nicht in den Data Lake aufgenommen werden.

## Kommunikation mit Platform-Benutzern

Adobe wird sich an Systemadministratoren wenden, um die Auswirkungen der Migration ausführlich zu erörtern und die Migrationsdaten und -zeiten für bestimmte Einrichtungen zu bestätigen.
