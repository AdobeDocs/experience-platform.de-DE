---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Entwicklerhandbuch für die Policy Service-API
topic: developer guide
translation-type: tm+mt
source-git-commit: cb3a17aa08c67c66101cbf3842bf306ebcca0305
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 16%

---


# [!DNL Policy Service] API developer guide

Adobe Experience Platform [!DNL Data Governance] allows you to manage customer data and ensure compliance with regulations, restrictions, and policies applicable to data use. It plays a key role within [!DNL Experience Platform] at various levels, including cataloging, data lineage, data usage labeling, data usage policies, and controlling usage of data for marketing actions.

The [!DNL Policy Service] API provides several endpoints that allow you to programmatically manage data usage labels and policies, as well as evaluate marketing actions for policy violations. These endpoints are outlined below. Please visit the individual endpoint guides for details and refer to the [getting started guide](./getting-started.md) for important information on required headers, reading sample API calls, and more.

Um alle verfügbaren Endpunkte und CRUD-Vorgänge Ansicht, besuchen Sie den [Policy Service API-Swagger](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml).

## Bezeichnungen

Mit Datennutzungsbeschriftungen können Sie Daten anhand der für diese Daten geltenden Nutzungsrichtlinien kategorisieren. Beschriftungen können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Best practices encourage labeling data as soon as it is ingested into [!DNL Experience Platform], or as soon as data becomes available for use in [!DNL Platform]. Sie können Beschriftungen mithilfe des `/labels` Endpunkts erstellen, Ansichten erstellen, bearbeiten und löschen. Weitere Informationen zur Verwendung dieses Endpunkts finden Sie in der [Beschreibungen-Endpunkthandbuch](./labels.md).

## Marketing-Aktionen

Marketingaktionen (auch als Marketing-Nutzungsszenarien bezeichnet) im Kontext des [!DNL Data Governance] Frameworks sind Aktionen, die ein [!DNL Experience Platform] Datenkonsument durchführen kann und für die Ihr Unternehmen die Datenverwendung einschränken möchte. For detailed information on working with marketing actions, see the [marketing actions endpoint guide](./marketing-actions.md).

## Richtlinien

Data usage policies are rules that describe the kinds of marketing actions that you are allowed to, or restricted from, performing on data within [!DNL Experience Platform]. Eine Richtlinie wird wie folgt definiert:

1. Eine bestimmte Marketingaktion
1. Die Datenverwendungs-Beschriftungen, die für diese Aktion eingeschränkt sind, gegen

To learn how to manage policies in the API, see the [policies endpoint guide](./policies.md)

## Auswertung

Once data usage labels have been applied to [!DNL Platform] datasets, and data usage policies have been defined for marketing actions against those labels, Data Governance capabilities allow you to enforce those policies and prevent data operations that constitute policy violations.

The [!DNL Policy Service] API provides endpoints that allow you to test marketing actions against datasets or arbitrary combinations of data usage labels in order to check if any policy violations occur. Je nach API-Antwort können Sie dann Protokolle in Ihrer Erlebnisanwendung einrichten, um die Einhaltung von Datennutzungsrichtlinien richtig durchzusetzen. See the [evaluation endpoints guide](./evaluation.md) for more information.

## Nächste Schritte

Um mit dem Aufrufen der [!DNL Policy Service] API zu beginnen, lesen Sie die [Erste Schritte-Anleitung](./getting-started.md) und wählen Sie dann eine der Endpunktanleitungen, um zu erfahren, wie Sie bestimmte Endpunkte verwenden. Informationen zum Arbeiten mit Beschriftungen und Richtlinien mithilfe der [!DNL Experience Platform] Benutzeroberfläche finden Sie im Benutzerhandbuch für [Beschriftungen](../labels/user-guide.md) bzw. im [Richtlinien-Benutzerhandbuch](../policies/user-guide.md).