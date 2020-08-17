---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;enable profile;Enable profile
solution: Adobe Experience Platform
title: Hinzufügen von Daten zum Echtzeit-Kundenprofil
topic: tutorial
description: In diesem Tutorial werden die Schritte beschrieben, die zum Hinzufügen von Daten zum Echtzeit-Kundenprofil erforderlich sind.
translation-type: tm+mt
source-git-commit: bf99b08a1093a815687cc06372407949e170a0b3
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 53%

---


# Daten Hinzufügen [!DNL Real-time Customer Profile]

This tutorial outlines the steps necessary to add data to [!DNL Real-time Customer Profile].

## Schema aktivieren für [!DNL Real-time Customer Profile]

Daten, die [!DNL Experience Platform] zur Verwendung durch [!DNL Real-time Customer Profile] verwendet werden, müssen einem [!DNL Experience Data Model] (XDM-)Schema entsprechen, für das aktiviert wurde [!DNL Profile]. In order for a schema to be enabled for Profile, it must implement either the [!DNL XDM Individual Profile] or [!DNL XDM ExperienceEvent] class.

Sie können ein Schema zur Verwendung [!DNL Real-time Customer Profile] mit der [!DNL Schema Registry] API oder der [!DNL Schema Editor] Benutzeroberfläche aktivieren. Beginnen Sie zunächst mit den Tutorials zum [Erstellen eines Schemas mit APIs](../../xdm/tutorials/create-schema-api.md) oder zum [Erstellen eines Schemas mithilfe der Schema-Editor-UI](../../xdm/tutorials/create-schema-ui.md).

## Hinzufügen von Daten mithilfe der Batch-Erfassung

All data uploaded to [!DNL Platform] using batch ingestion is uploaded to individual datasets. Before this data can be used by [!DNL Real-time Customer Profile], the dataset in question has to be specifically configured. Vollständige Anweisungen finden Sie im Tutorial zum [Konfigurieren eines Datensatzes für den Profile und Identity Service](dataset-configuration.md).

Nachdem der Datensatz konfiguriert wurde, können Sie Daten in den Datensatz eingeben. Detaillierte Anweisungen zum Hochladen von Dateien in verschiedenen Formaten finden Sie im [Entwicklerhandbuch zur Batch-Erfassung](../../ingestion/batch-ingestion/api-overview.md).

## Hinzufügen von Daten mithilfe der Streaming-Erfassung

Any stream-ingested data that is compliant with a [!DNL Profile]-enabled XDM schema will automatically add or overwrite the appropriate record in [!DNL Real-time Customer Profile]. Wenn mehr als eine Identität im Datensatz bereitgestellt wird oder Zeitreihendaten verwendet werden, werden diese Identitäten im Identitätsdiagramm ohne zusätzliche Konfiguration zugeordnet. Weitere Informationen hierzu finden Sie im [Entwicklerhandbuch zur Streaming-Erfassung](../../ingestion/tutorials/streaming-record-data.md).

## Überprüfen Sie, ob der Upload erfolgreich war

Beim erstmaligen Hochladen von Daten in einen neuen Datensatz oder im Rahmen eines Prozesses mit einer neuen ETL oder Datenquelle wird empfohlen, die Daten sorgfältig zu überprüfen, um sicherzustellen, dass sie korrekt hochgeladen wurden.

Using the [!DNL Real-time Customer Profile] Access API, you can retrieve batch data as it gets loaded into a dataset. If you are unable to retrieve any of the entities you expect, your dataset may not be enabled for [!DNL Profile]. Nachdem Sie bestätigt haben, dass Ihr Datensatz aktiviert wurde, stellen Sie sicher, dass Ihr Quelldatenformat und Ihre Identifikatoren Ihre Erwartungen unterstützen.

Detaillierte Anweisungen zum Zugriff auf Entitäten mit der [!DNL Real-time Customer Profile] API finden Sie im [Entitäts-Endpunkthandbuch](../api/entities.md), auch als &quot;[!DNL Profile Access] API&quot;bezeichnet.