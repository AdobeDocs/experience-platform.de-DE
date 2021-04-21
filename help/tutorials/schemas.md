---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: XDM-Schema und -Deskriptoren
topic-legacy: tutorial
type: Tutorial
description: Normung und Interoperabilität sind Schlüsselkonzepte für Adobe Experience Platform. Das von Adobe unterstützte Experience-Datenmodell (XDM) ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schemas für das Customer Experience Management zu definieren. Schemas sind die Standardmethode zur Beschreibung von Daten in der Experience Platform, so dass alle Daten, die mit Schemas konform sind, ohne Konflikte innerhalb einer Organisation wiederverwendbar sind und sogar zwischen mehreren Organisationen geteilt werden können.
exl-id: 1cdc45d7-57ca-4a2d-99a4-9a8cd885a511
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 26%

---

# Arbeiten mit [!DNL Experience Data Model] (XDM)-Schemas und Beziehungsdeskriptoren

Normung und Interoperabilität sind Schlüsselkonzepte für Adobe Experience Platform. [!DNL Experience Data Model] (XDM), angetrieben von der Adobe, ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schema für das Kundenerlebnis-Management zu definieren. Schema sind die Standardmethode zum Beschreiben von Daten in [!DNL Experience Platform], sodass alle Daten, die Schemas entsprechen, innerhalb eines Unternehmens ohne Konflikte wiederverwendet werden können und sogar zwischen mehreren Organisationen freigegeben werden können. Um mehr über XDM-Schema zu erfahren, lesen Sie den Beginn [XDM-Systemübersicht](../xdm/home.md).

## Erstellen eines Schemas mithilfe der Schema-Registrierung

Die Schema Registry stellt eine Benutzeroberfläche und RESTful-API bereit, über die Sie alle Ressourcen in der Schema Library von Adobe Experience Platform anzeigen und verwalten können. Die Schema-Bibliothek enthält Ressourcen, die Ihnen nach Adobe, [!DNL Experience Platform] Partnern und Anbietern, deren Anwendungen Sie verwenden, zur Verfügung gestellt werden, sowie Ressourcen, die Sie definieren und in der Schema-Registrierung speichern. Um zu erfahren, wie Sie Schema für Ihr Unternehmen erstellen, befolgen Sie die Lernprogramme zum Erstellen eines Schemas mit der Schema Registry API](../xdm/tutorials/create-schema-api.md) oder [Erstellen eines Schemas mithilfe der Schema Editor-Benutzeroberfläche](../xdm/tutorials/create-schema-ui.md).[

## Definieren einer Beziehung zwischen zwei Schemata

Die Möglichkeit, Beziehungen zwischen Ihren Kunden und deren Interaktionen mit Ihrer Marke kanalübergreifend zu analysieren, ist ein wichtiger Bestandteil von Adobe Experience Platform. Durch die Definition dieser Beziehungen innerhalb der Struktur Ihrer [!DNL Experience Data Model] (XDM) Schema erhalten Sie komplexe Einblicke in Ihre Kundendaten. Diese Beziehungsdeskriptoren können mithilfe der Schema Registry API und der Schema Editor-Benutzeroberfläche definiert werden. Weitere Informationen finden Sie in den Übungen zum Definieren von Beziehungen zwischen zwei Schemas [mithilfe der API](../xdm/tutorials/relationship-api.md) oder [unter Verwendung der Benutzeroberfläche](../xdm/tutorials/relationship-ui.md).

## Erstellen eines Ad-hoc-Schemas

Unter bestimmten Umständen kann es erforderlich sein, ein [!DNL Experience Data Model] (XDM)-Schema mit Feldern zu erstellen, die nur für die Verwendung durch einen einzigen Datensatz benannt werden. Ein solches Schema wird als Ad-hoc-Schema bezeichnet. Ad-hoc-Schema werden in verschiedenen [Datenerfassung](../ingestion/home.md)-Workflows für [!DNL Experience Platform] verwendet, einschließlich der Erfassung von CSV-Dateien und der Erstellung bestimmter [Quellverbindungen](../sources/home.md). Das Erstellen eines Ad-hoc-Schemas erfolgt mithilfe der Schema Registry API und ist für die Verwendung mit anderen [!DNL Experience Platform]-Lehrgängen vorgesehen, bei denen im Rahmen ihres Workflows ein Ad-hoc-Schema erstellt werden muss. Informationen zum Erstellen eines Ad-hoc-Schemas finden Sie im Lernprogramm für [Erstellen eines Ad-hoc-Schemas mit der API](../xdm/tutorials/ad-hoc.md).

## Nächste Schritte

Nachdem Sie Schema für Ihr Unternehmen definiert haben, können Sie mit der Erstellung von Datensätzen beginnen, in die Daten aufgenommen werden können. Lesen Sie zunächst die folgende Dokumentation:

* [Datensätze – Übersicht](../catalog/datasets/overview.md)
* [Datenerfassung – Übersicht](../ingestion/home.md)
