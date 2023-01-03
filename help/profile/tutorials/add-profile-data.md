---
keywords: Experience Platform; Profil; Echtzeit-Kundenprofil; Fehlerbehebung; API; Profil aktivieren; Profil aktivieren
title: Hinzufügen von Daten zum Echtzeit-Kundenprofil
topic-legacy: tutorial
type: Tutorial
description: In diesem Tutorial werden die Schritte beschrieben, die zum Hinzufügen von Daten zum Echtzeit-Kundenprofil erforderlich sind.
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 63%

---


# Hinzufügen von Daten zu [!DNL Real-Time Customer Profile]

In diesem Tutorial werden die Schritte beschrieben, die zum Hinzufügen von Daten zu [!DNL Real-Time Customer Profile].

## Aktivieren eines Schemas für [!DNL Real-Time Customer Profile]

Daten, die erfasst werden in [!DNL Experience Platform] zur Verwendung durch [!DNL Real-Time Customer Profile] muss einer [!DNL Experience Data Model] (XDM)-Schema, das für [!DNL Profile]. Damit ein Schema für Profil aktiviert werden kann, muss es entweder das [!DNL XDM Individual Profile] oder [!DNL XDM ExperienceEvent] -Klasse.

Sie können ein Schema zur Verwendung in [!DNL Real-Time Customer Profile] mithilfe der [!DNL Schema Registry] API oder [!DNL Schema Editor] -Benutzeroberfläche. Beginnen Sie zunächst mit den Tutorials zum [Erstellen eines Schemas mit APIs](../../xdm/tutorials/create-schema-api.md) oder zum [Erstellen eines Schemas mithilfe der Schema-Editor-UI](../../xdm/tutorials/create-schema-ui.md).

## Hinzufügen von Daten mithilfe der Batch-Erfassung

Alle Daten, die in hochgeladen wurden [!DNL Platform] Die Batch-Erfassung wird in einzelne Datensätze hochgeladen. Bevor diese Daten verwendet werden können von [!DNL Real-Time Customer Profile], muss der betreffende Datensatz spezifisch konfiguriert werden. Vollständige Anweisungen finden Sie im Tutorial zum [Konfigurieren eines Datensatzes für den Profile und Identity Service](dataset-configuration.md).

Nachdem der Datensatz konfiguriert wurde, können Sie Daten in den Datensatz eingeben. Detaillierte Anweisungen zum Hochladen von Dateien in verschiedenen Formaten finden Sie im [Entwicklerhandbuch zur Batch-Erfassung](../../ingestion/batch-ingestion/api-overview.md).

## Hinzufügen von Daten mithilfe der Streaming-Erfassung

Alle Stream-aufgenommenen Daten, die mit einer [!DNL Profile]-aktiviertes XDM-Schema fügt automatisch den entsprechenden Datensatz in hinzu oder überschreibt ihn. [!DNL Real-Time Customer Profile]. Wenn mehr als eine Identität im Datensatz bereitgestellt wird oder Zeitreihendaten verwendet werden, werden diese Identitäten im Identitätsdiagramm ohne zusätzliche Konfiguration zugeordnet. Weitere Informationen hierzu finden Sie im [Entwicklerhandbuch zur Streaming-Erfassung](../../ingestion/tutorials/streaming-record-data.md).

## Überprüfen Sie, ob der Upload erfolgreich war

Beim erstmaligen Hochladen von Daten in einen neuen Datensatz oder im Rahmen eines Prozesses mit einer neuen ETL oder Datenquelle wird empfohlen, die Daten sorgfältig zu überprüfen, um sicherzustellen, dass sie korrekt hochgeladen wurden.

Mit der Zugriffs-API des [!DNL Real-Time Customer Profile] können Sie Batch-Daten abrufen, sobald sie in einen Datensatz geladen werden. Wenn Sie keine der erwarteten Entitäten abrufen können, ist Ihr Datensatz möglicherweise nicht für [!DNL Profile] aktiviert. Nachdem Sie bestätigt haben, dass Ihr Datensatz aktiviert wurde, stellen Sie sicher, dass Ihr Quelldatenformat und Ihre Identifikatoren Ihre Erwartungen unterstützen.

Detaillierte Anweisungen zum Zugriff auf Entitäten mithilfe des [!DNL Real-Time Customer Profile] API, siehe [Endpunktleitfaden für Entitäten](../api/entities.md), auch als bezeichnet[!DNL Profile Access] API&quot;.

## Aktualisieren von Profilspeicherdaten

Gelegentlich kann es erforderlich sein, Daten im Profilspeicher Ihrer Organisation zu aktualisieren. Vielleicht müssen Sie zum Beispiel Datensätze korrigieren oder einen Attributwert ändern. Dies kann durch Batch-Aufnahme erfolgen und erfordert einen profilaktivierten Datensatz, der mit einem Upsert-Tag konfiguriert ist. Weitere Informationen zur Konfiguration eines Datensatzes für Attributaktualisierungen finden Sie im Tutorial zur [Aktivierung eines Datensatzes für Profil und Upsert](../../catalog/datasets/enable-upsert.md).
