---
keywords: Experience Platform;Profil;Echtzeit-Profil des Kunden;Fehlerbehebung;API;Profil aktivieren;Profil aktivieren
title: Daten Hinzufügen Echtzeit-Profil des Kunden
topic-legacy: tutorial
type: Tutorial
description: In diesem Tutorial werden die Schritte beschrieben, die zum Hinzufügen von Daten zum Echtzeit-Kundenprofil erforderlich sind.
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 50%

---

# Daten Hinzufügen [!DNL Real-time Customer Profile]

In diesem Lernprogramm werden die Schritte beschrieben, die zum Hinzufügen von Daten zu [!DNL Real-time Customer Profile] erforderlich sind.

## Schema für [!DNL Real-time Customer Profile] aktivieren

Daten, die in [!DNL Experience Platform] für die Verwendung von [!DNL Real-time Customer Profile] aufgenommen werden, müssen einem [!DNL Experience Data Model] (XDM)-Schema entsprechen, das für [!DNL Profile] aktiviert ist. Damit ein Schema zum Profil aktiviert werden kann, muss es entweder die [!DNL XDM Individual Profile]- oder [!DNL XDM ExperienceEvent]-Klasse implementieren.

Sie können ein Schema zur Verwendung in [!DNL Real-time Customer Profile] mithilfe der [!DNL Schema Registry]-API oder der [!DNL Schema Editor]-Benutzeroberfläche aktivieren. Beginnen Sie zunächst mit den Tutorials zum [Erstellen eines Schemas mit APIs](../../xdm/tutorials/create-schema-api.md) oder zum [Erstellen eines Schemas mithilfe der Schema-Editor-UI](../../xdm/tutorials/create-schema-ui.md).

## Hinzufügen von Daten mithilfe der Batch-Erfassung

Alle Daten, die mit der Stapelverarbeitung zu [!DNL Platform] hochgeladen wurden, werden in einzelne Datensätze hochgeladen. Bevor diese Daten von [!DNL Real-time Customer Profile] verwendet werden können, muss der betreffende Datensatz spezifisch konfiguriert werden. Vollständige Anweisungen finden Sie im Tutorial zum [Konfigurieren eines Datensatzes für den Profile und Identity Service](dataset-configuration.md).

Nachdem der Datensatz konfiguriert wurde, können Sie Daten in den Datensatz eingeben. Detaillierte Anweisungen zum Hochladen von Dateien in verschiedenen Formaten finden Sie im [Entwicklerhandbuch zur Batch-Erfassung](../../ingestion/batch-ingestion/api-overview.md).

## Hinzufügen von Daten mithilfe der Streaming-Erfassung

Alle Stream-erfassten Daten, die mit einem [!DNL Profile]-aktivierten XDM-Schema konform sind, werden automatisch den entsprechenden Datensatz in [!DNL Real-time Customer Profile] hinzufügen oder überschreiben. Wenn mehr als eine Identität im Datensatz bereitgestellt wird oder Zeitreihendaten verwendet werden, werden diese Identitäten im Identitätsdiagramm ohne zusätzliche Konfiguration zugeordnet. Weitere Informationen hierzu finden Sie im [Entwicklerhandbuch zur Streaming-Erfassung](../../ingestion/tutorials/streaming-record-data.md).

## Überprüfen Sie, ob der Upload erfolgreich war

Beim erstmaligen Hochladen von Daten in einen neuen Datensatz oder im Rahmen eines Prozesses mit einer neuen ETL oder Datenquelle wird empfohlen, die Daten sorgfältig zu überprüfen, um sicherzustellen, dass sie korrekt hochgeladen wurden.

Mit der Zugriffs-API [!DNL Real-time Customer Profile] können Sie Stapeldaten abrufen, während sie in ein Dataset geladen werden. Wenn Sie keine der erwarteten Entitäten abrufen können, ist Ihr Datensatz möglicherweise nicht für [!DNL Profile] aktiviert. Nachdem Sie bestätigt haben, dass Ihr Datensatz aktiviert wurde, stellen Sie sicher, dass Ihr Quelldatenformat und Ihre Identifikatoren Ihre Erwartungen unterstützen.

Detaillierte Anweisungen zum Zugriff auf Entitäten mit der [!DNL Real-time Customer Profile]-API finden Sie im [Entitäts-Endpunkthandbuch](../api/entities.md), auch als &quot;API[!DNL Profile Access]&quot;bezeichnet.
