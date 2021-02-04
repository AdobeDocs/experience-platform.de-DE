---
source-git-commit: b9816767556b9d50cf2ff5268816d1de6b85fc63
workflow-type: tm+mt
translation-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---
# Migration von Adobe Experience Platform Data Lake zu Gen2

Adobe Experience Platform migriert zum Gen2 Data Lake. Dies ist eine neue Generation von Datenseen, die Plattformbenutzern Vorteile wie die Geo-Region-Replikation, feinere rollenbasierte Zugriffskontrollen (RBAC) und eine bessere Skalierung bietet.

## Benutzerwirkung

Während die Adobe den Data Lake von Gen1 zu Gen 2 migriert, können Benutzer **den Data Lake** lesen, aber alle Funktionen, die **schreiben** in den Data Lake eintragen, werden beeinträchtigt. Nachfolgend finden Sie eine Liste der betroffenen Funktionen:

- **Quellen**: Daten aus den Quellen und verschiedene Workflows werden verzögert. Benutzer sehen ihre Daten, sobald die Migration abgeschlossen ist.
- **Abfrage-Dienst**: Die Benutzer können Abfragen durchführen, können aber die Ausgabe der Abfrage nicht in einen Datensatz schreiben.
- **Echtzeit-Profil**: Daten, die durch  **** Stapelverarbeitung in den Profil Store aufgenommen werden, stehen während der Migration nicht zur Verfügung. Daten, die über die **Streaming**-Erfassung erfasst werden, stehen während der Migration zur Verfügung. Außerdem stehen während der Migration keine Profil-Exporte zur Verfügung.
- **Data Science Workspace**: Schreibvorgänge aus Data Science Workspace schlagen fehl.
- **Segmentierungsdienst**: Audiencen aus der  **** Stapelsegmentierung können während der Migration nicht aktiviert werden. Audiencen, die von der **Streaming**-Segmentierung abgeleitet wurden, sind nicht betroffen.
- **Customer Journey Analytics**: Customer Journey Analytics meldet, dass Daten veraltet sind und während der Migration nicht aktualisiert werden, da keine Stapel in den Data Lake aufgenommen werden.

## Kommunikation mit Plattformbenutzern

Adobe wird sich an Systemadministratoren wenden, um die Auswirkungen der Migration ausführlich zu erörtern und die Migrationsdaten und -zeiten für bestimmte IMS-Organisationen zu bestätigen.