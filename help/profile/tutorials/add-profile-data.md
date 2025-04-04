---
keywords: Experience Platform;Profil;Echtzeit-Kundenprofil;Fehlerbehebung;API;Profil aktivieren;Profil aktivieren
title: Hinzufügen von Daten zum Echtzeit-Kundenprofil
type: Tutorial
description: In diesem Tutorial werden die Schritte beschrieben, die zum Hinzufügen von Daten zum Echtzeit-Kundenprofil erforderlich sind.
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 59%

---


# Hinzufügen von Daten zu [!DNL Real-Time Customer Profile]

In diesem Tutorial werden die Schritte beschrieben, die zum Hinzufügen von Daten zu [!DNL Real-Time Customer Profile] erforderlich sind.

## Aktivieren eines Schemas für [!DNL Real-Time Customer Profile]

Daten, die in [!DNL Experience Platform] zur Verwendung durch [!DNL Real-Time Customer Profile] aufgenommen werden, müssen einem [!DNL Experience Data Model] (XDM)-Schema entsprechen, das für die [!DNL Profile] aktiviert ist. Damit ein Schema für das Profil aktiviert werden kann, muss es entweder die Klasse [!DNL XDM Individual Profile] oder [!DNL XDM ExperienceEvent] implementieren.

Sie können ein Schema zur Verwendung in [!DNL Real-Time Customer Profile] mithilfe der [!DNL Schema Registry]-API oder der [!DNL Schema Editor]-Benutzeroberfläche aktivieren. Beginnen Sie zunächst mit den Tutorials zum [Erstellen eines Schemas mit APIs](../../xdm/tutorials/create-schema-api.md) oder zum [Erstellen eines Schemas mithilfe der Schema-Editor-UI](../../xdm/tutorials/create-schema-ui.md).

## Hinzufügen von Daten mithilfe der Batch-Erfassung

Alle Daten, die mithilfe der Batch-Aufnahme in [!DNL Experience Platform] hochgeladen wurden, werden in die einzelnen Datensätze hochgeladen. Bevor diese Daten von [!DNL Real-Time Customer Profile] verwendet werden können, muss der betreffende Datensatz speziell konfiguriert werden. Vollständige Anweisungen finden Sie im Tutorial zum [Konfigurieren eines Datensatzes für den Profile und Identity Service](dataset-configuration.md).

Nachdem der Datensatz konfiguriert wurde, können Sie Daten in den Datensatz eingeben. Detaillierte Anweisungen zum Hochladen von Dateien in verschiedenen Formaten finden Sie im [Entwicklerhandbuch zur Batch-Erfassung](../../ingestion/batch-ingestion/api-overview.md).

## Hinzufügen von Daten mithilfe der Streaming-Erfassung

Alle im Stream aufgenommenen Daten, die mit einem [!DNL Profile] XDM-Schema konform sind, fügen automatisch den entsprechenden Datensatz in [!DNL Real-Time Customer Profile] hinzu oder überschreiben ihn. Wenn mehr als eine Identität im Datensatz bereitgestellt wird oder Zeitreihendaten verwendet werden, werden diese Identitäten im Identitätsdiagramm ohne zusätzliche Konfiguration zugeordnet. Weitere Informationen hierzu finden Sie im [Entwicklerhandbuch zur Streaming-Erfassung](../../ingestion/tutorials/streaming-record-data.md).

## Überprüfen Sie, ob der Upload erfolgreich war

Beim erstmaligen Hochladen von Daten in einen neuen Datensatz oder im Rahmen eines Prozesses mit einer neuen ETL oder Datenquelle wird empfohlen, die Daten sorgfältig zu überprüfen, um sicherzustellen, dass sie korrekt hochgeladen wurden.

Mit der Zugriffs-API des [!DNL Real-Time Customer Profile] können Sie Batch-Daten abrufen, sobald sie in einen Datensatz geladen werden. Wenn Sie keine der erwarteten Entitäten abrufen können, ist Ihr Datensatz möglicherweise nicht für [!DNL Profile] aktiviert. Nachdem Sie bestätigt haben, dass Ihr Datensatz aktiviert wurde, stellen Sie sicher, dass Ihr Quelldatenformat und Ihre Identifikatoren Ihre Erwartungen unterstützen.

Ausführliche Anweisungen für den Zugriff auf Entitäten mithilfe der [!DNL Real-Time Customer Profile]-API finden Sie im [Handbuch für Entitäten-](../api/entities.md), auch bekannt als &quot;[!DNL Profile Access]-API“.

## Aktualisieren der Profilspeicherdaten

Gelegentlich kann es erforderlich sein, Daten im Profilspeicher Ihrer Organisation zu aktualisieren. Vielleicht müssen Sie zum Beispiel Datensätze korrigieren oder einen Attributwert ändern. Dies kann durch Batch-Aufnahme erfolgen und erfordert einen profilaktivierten Datensatz, der mit einem Upsert-Tag konfiguriert ist. Weitere Informationen zur Konfiguration eines Datensatzes für Attributaktualisierungen finden Sie im Tutorial zur [Aktivierung eines Datensatzes für Profil und Upsert](../../catalog/datasets/enable-upsert.md).
