---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tutorials zum Echtzeit-Kundenprofil
topic: tutorial
translation-type: tm+mt
source-git-commit: 5c5f6c4868e195aef76bacc0a1e5df3857647bde
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 47%

---


# Konfigurieren [!DNL Real-time Customer Profile] und [!DNL Identity Service]

In order to configure [!DNL Real-time Customer Profile] for your organization, you are required to complete multiple separate workflows. In diesem Dokument werden die erforderlichen Schritte beschrieben und Links zu Tutorials für die einzelnen Workflows bereitgestellt. To learn more about [!DNL Real-time Customer Profile], begin by reading the [Profile overview](../profile/home.md).

## Schema für [!DNL Profile] und [!DNL Identity]

Before data can be ingested into Adobe Experience Platform and used in the creation of [!DNL Real-time Customer Profiles], a schema must be created to provide the structure for the data that will be ingested and that schema must be enabled for use in [!DNL Profile] and Adobe Experience Platform [!DNL Identity Service]. For step-by-step instructions on creating a schema that is enabled for both [!DNL Profile] and [!DNL Identity Service], please refer to the tutorials for [creating a schema using the Schema Registry API](../xdm/tutorials/create-schema-api.md) or [creating a schema using the Schema Builder UI](../xdm/tutorials/create-schema-ui.md).

## Konfigurieren eines Datensatzes für [!DNL Profile] und [!DNL Identity]

To begin ingesting data into [!DNL Profile], you must have a dataset that has been properly configured for use with [!DNL Real-time Customer Profile] and [!DNL Identity Service]. Befolgen Sie zunächst das [Tutorial zum Konfigurieren eines Datensatzes für Profil und Identität](../profile/tutorials/dataset-configuration.md).

## Konfigurieren von Zusammenführungsrichtlinien

Mit Adobe Experience Platform können Sie Daten aus verschiedenen Quellen zusammenführen und kombinieren, damit Sie sich einen kompletten Überblick über einzelne Kunden verschaffen können. When bringing this data together, merge policies are the rules that [!DNL Platform] uses to determine how data will be prioritized and what data will be combined to create that unified view. Mithilfe von RESTful-APIs oder der Benutzeroberfläche können Sie neue Zusammenführungsrichtlinien erstellen, bestehende Richtlinien verwalten und eine für Ihr Unternehmen als Standard verwendete Zusammenführungsrichtlinie einrichten. To work with merge policies in the [!DNL Platform] UI, visit the [merge policies user guide](../profile/ui/merge-policies.md). Informationen zum Arbeiten mit Zusammenführungsrichtlinien mithilfe der Real-time Customer Profile-API finden Sie im [Entwicklerhandbuch für Zusammenführungsrichtlinien](../profile/api/merge-policies.md).

## Konfigurieren von Kantenprojektionen

Um koordinierte, konsistente und personalisierte Erlebnisse für Ihre Kunden über mehrere Kanal hinweg in Echtzeit zu ermöglichen, müssen die richtigen Daten jederzeit verfügbar sein und bei Änderungen kontinuierlich aktualisiert werden. Adobe [!DNL Experience Platform] enables this real-time access to data through the use of what are known as edges. Eine Kante ist ein geografisch platzierter Server, der Daten speichert und für Anwendungen leicht zugänglich macht. Die Daten werden durch eine Projektion an eine Kante geleitet, wobei ein Projektionsziel die Kante definiert, an die die Daten gesendet werden, und eine Projektionskonfiguration die spezifischen Informationen definiert, die an der Kante zur Verfügung gestellt werden. For more information and to begin working with edges, refer to the [!DNL Real-time Customer Profile] API [sub-guide on edge projections](../profile/api/edge-projections.md).

## Nächste Schritte

Once you have configured [!DNL Real-time Customer Profile] for your organization, you can begin adding data to individual customer profiles and creating audience segments based on specific customer attributes. Erste Schritte finden Sie in den folgenden Tutorials:

* [Hinzufügen von Daten zum Echtzeit-Kundenprofil](../profile/tutorials/add-profile-data.md)
* [Erstellen eines Segments](../segmentation/tutorials/create-a-segment.md)