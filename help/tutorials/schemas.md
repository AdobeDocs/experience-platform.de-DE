---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: XDM-Schema und -Deskriptoren
topic: tutorial
translation-type: tm+mt
source-git-commit: 2f0f155beacbc6a4ba2892ae211a9c0305e969ac
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---


# Arbeiten mit Experience Data Model-(XDM-)Schemas und Beziehungsdeskriptoren

Standardisierung und Interoperabilität sind Schlüsselkonzepte der Adobe Experience Platform. Das von Adobe unterstützte Experience Data Model (XDM) ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schema für das Kundenerlebnis-Management zu definieren. Schema sind die Standardmethode zum Beschreiben von Daten in Experience Platform, sodass alle Daten, die Schemas entsprechen, innerhalb eines Unternehmens problemlos wiederverwendet werden können und sogar für mehrere Unternehmen freigegeben werden können. Weitere Informationen zu XDM-Schemas erhalten Sie im Beginn in der [XDM-Systemübersicht](../xdm/home.md).

## Erstellen eines Schemas mithilfe der Schema-Registrierung

Die Schema Registry stellt eine Benutzeroberfläche und RESTful-API bereit, über die Sie alle Ressourcen in der Adobe Experience Platform Schema Library Ansicht und verwalten können. Die Schema-Bibliothek enthält Ressourcen, die Ihnen von Adobe, Experience Platform-Partnern und Anbietern, deren Anwendungen Sie verwenden, zur Verfügung gestellt werden, sowie Ressourcen, die Sie definieren und in der Schema-Registrierung speichern. Um zu erfahren, wie Sie Schemas für Ihr Unternehmen erstellen, befolgen Sie die Lernprogramme zum [Erstellen eines Schemas mit der Schema Registry-API](../xdm/tutorials/create-schema-api.md) oder zum [Erstellen eines Schemas mithilfe der Schema Editor-Benutzeroberfläche](../xdm/tutorials/create-schema-ui.md).

## Definieren einer Beziehung zwischen zwei Schemas

Die Fähigkeit, die Beziehungen zwischen Ihren Kunden und ihre Interaktionen mit Ihrer Marke über verschiedene Kanal hinweg zu verstehen, ist ein wichtiger Bestandteil der Adobe Experience Platform. Die Definition dieser Beziehungen innerhalb der Struktur Ihrer Experience Data Model (XDM)-Schema ermöglicht Ihnen, komplexe Einblicke in Ihre Kundendaten zu erhalten. Diese Beziehungsdeskriptoren können mithilfe der Schema Registry API und der Schema Editor-Benutzeroberfläche definiert werden. Weitere Informationen finden Sie in den Übungen zum Definieren von Beziehungen zwischen zwei Schemas [mithilfe der API](../xdm/tutorials/relationship-api.md) oder [mithilfe der Benutzeroberfläche](../xdm/tutorials/relationship-ui.md).

## Erstellen eines Ad-hoc-Schemas

Unter bestimmten Umständen kann es erforderlich sein, ein XDM-Schema (Experience Data Model) mit Feldern zu erstellen, die nur für die Verwendung durch einen einzigen Datensatz benannt werden. Dies wird als Ad-hoc-Schema bezeichnet. Ad-hoc-Schema werden in verschiedenen [Datenerfassungs](../ingestion/home.md) -Workflows für Experience Platform verwendet, einschließlich der Erfassung von CSV-Dateien und der Erstellung bestimmter Arten von [Quellverbindungen](../sources/home.md). Das Erstellen eines Ad-hoc-Schemas erfolgt mithilfe der Schema Registry API und ist für die Verwendung mit anderen Experience Platform-Lehrgängen vorgesehen, bei denen im Rahmen ihres Workflows ein Ad-hoc-Schema erstellt werden muss. Informationen zum Erstellen eines Ad-hoc-Schemas finden Sie im Lernprogramm zum [Erstellen eines Ad-hoc-Schemas mit der API](../xdm/tutorials/ad-hoc.md).

## Nächste Schritte

Nachdem Sie Schema für Ihr Unternehmen definiert haben, können Sie mit der Erstellung von Datensätzen beginnen, in die Daten aufgenommen werden können. Lesen Sie zunächst die folgende Dokumentation:

* [Übersicht über Datasets](../catalog/datasets/overview.md)
* [Dateneinbindung - Übersicht](../ingestion/home.md)