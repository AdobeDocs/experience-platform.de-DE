---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: XDM-Schema und -Deskriptoren
topic: tutorial
translation-type: tm+mt
source-git-commit: 5c5f6c4868e195aef76bacc0a1e5df3857647bde
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 19%

---


# Arbeiten mit [!DNL Experience Data Model] (XDM-)Schemas und Beziehungsdeskriptoren

Normung und Interoperabilität sind Schlüsselkonzepte der Adobe Experience Platform. [!DNL Experience Data Model] (XDM), unterstützt von Adobe, ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schema für das Kundenerlebnis-Management zu definieren. Schemas are the standard way of describing data in [!DNL Experience Platform], allowing all data that conforms to schemas to be reusable without conflicts across an organization and even to be sharable between multiple organizations. Weitere Informationen zu XDM-Schemas erhalten Sie im Beginn in der [XDM-Systemübersicht](../xdm/home.md).

## Erstellen eines Schemas mithilfe der Schema Registry

Die Schema Registry stellt eine Benutzeroberfläche und RESTful-API bereit, über die Sie alle Ressourcen in der Schema Library von Adobe Experience Platform anzeigen und verwalten können. The Schema Library contains resources made available to you by Adobe, [!DNL Experience Platform] partners, and vendors whose applications you use, as well as resources that you define and save to the Schema Registry. Um zu erfahren, wie Sie Schemas für Ihr Unternehmen erstellen, befolgen Sie die Lernprogramme zum [Erstellen eines Schemas mit der Schema Registry-API](../xdm/tutorials/create-schema-api.md) oder zum [Erstellen eines Schemas mithilfe der Schema Editor-Benutzeroberfläche](../xdm/tutorials/create-schema-ui.md).

## Definieren einer Beziehung zwischen zwei Schemata

Die Fähigkeit, Beziehungen zwischen Ihren Kunden und ihren Interaktionen mit Ihrer Marke über verschiedene Kanäle hinweg zu verstehen, ist ein wichtiger Bestandteil von Adobe Experience Platform. Defining these relationships within the structure of your [!DNL Experience Data Model] (XDM) schemas allows you to gain complex insights into your customer data. Diese Beziehungsdeskriptoren können mithilfe der Schema Registry API und der Schema Editor-Benutzeroberfläche definiert werden. Weitere Informationen finden Sie in den Übungen zum Definieren von Beziehungen zwischen zwei Schemas [mithilfe der API](../xdm/tutorials/relationship-api.md) oder [mithilfe der Benutzeroberfläche](../xdm/tutorials/relationship-ui.md).

## Erstellen eines Ad-hoc-Schemas

In specific circumstances, it may be necessary to create an [!DNL Experience Data Model] (XDM) schema with fields that are namespaced for usage only by a single dataset. Ein solches Schema wird als Ad-hoc-Schema bezeichnet. Ad-hoc schemas are used in various [data ingestion](../ingestion/home.md) workflows for [!DNL Experience Platform], including ingesting CSV files and creating certain kinds of [source connections](../sources/home.md). Das Erstellen eines Ad-hoc-Schemas erfolgt mit der Schema Registry API und ist für die Verwendung mit anderen [!DNL Experience Platform] Übungen vorgesehen, bei denen im Rahmen des Workflows ein Ad-hoc-Schema erstellt werden muss. Informationen zum Erstellen eines Ad-hoc-Schemas finden Sie im Lernprogramm zum [Erstellen eines Ad-hoc-Schemas mit der API](../xdm/tutorials/ad-hoc.md).

## Nächste Schritte

Nachdem Sie Schema für Ihr Unternehmen definiert haben, können Sie mit der Erstellung von Datensätzen beginnen, in die Daten aufgenommen werden können. Lesen Sie zunächst die folgende Dokumentation:

* [Datensätze – Übersicht](../catalog/datasets/overview.md)
* [Datenaufnahme – Übersicht](../ingestion/home.md)