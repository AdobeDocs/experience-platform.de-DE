---
title: Data-Lake-Migration auf Gen2
description: Erfahren Sie mehr über die neuen Funktionen, die durch die Migration des Data Lake zu Gen2 in Adobe Experience Platform bereitgestellt werden.
exl-id: 56d9c77a-d7eb-498d-994f-b15d150dedb7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# Adobe Experience Platform Data Lake-Migration auf Gen2

Adobe Experience Platform migriert zum Data Lake Gen2. Dies ist eine neue Generation des Data Lake, der Experience Platform-Anwendern Vorteile bietet, wie z. B. Replikation in der geografischen Region, feinere rollenbasierte Zugriffssteuerungen (RBAC) und bessere Skalierung.

## Auswirkungen auf den Benutzer

Während Adobe den Data Lake von Gen1 auf Gen2 migriert, können Benutzende vom Data Lake **lesen**, aber alle Funktionen, die in **Data Lake** schreiben), sind betroffen. Im Folgenden finden Sie eine Liste der betroffenen Funktionen:

- **Quellen**: Das Eintreffen von Daten aus den Quellen und verschiedenen Workflows zur Datenaufnahme wird verzögert. Benutzer sehen ihre Daten, sobald die Migration abgeschlossen ist.
- **Abfrage-Service**: Benutzende können Abfragen durchführen, aber nicht die Ausgabe der Abfrage in einen Datensatz schreiben.
- **Echtzeit-Kundenprofil**: Daten, die über eine **Batch-Aufnahme** in den Profilspeicher aufgenommen werden, sind während der Migration nicht verfügbar. Daten, die über die **Streaming**-Aufnahme aufgenommen werden, sind jedoch während der Migration verfügbar. Darüber hinaus sind während der Migration keine Profilexporte verfügbar.
- **Data Science Workspace**: Schreibvorgänge aus Data Science Workspace schlagen fehl.
- **Segmentierungs** Service: Zielgruppen, die aus der **Batch**-Segmentierung abgeleitet wurden, können während der Migration nicht aktiviert werden. Zielgruppen, die aus **Streaming**-Segmentierung abgeleitet wurden, sind davon nicht betroffen.
- **Customer Journey Analytics**: Customer Journey Analytics meldet, dass die Daten möglicherweise veraltet sind und während der Migration nicht aktualisiert werden, da Batches nicht in den Data Lake aufgenommen werden.

## Kommunikation mit Experience Platform-Benutzenden

Adobe wird sich mit Systemadministratoren in Verbindung setzen, um die Auswirkungen der Migration im Detail zu besprechen und die Migrationsdaten und -zeiten für bestimmte Organisationen zu bestätigen.
