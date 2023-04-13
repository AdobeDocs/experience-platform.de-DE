---
keywords: Experience Platform; Profil; Echtzeit-Kundenprofil; Fehlerbehebung; API; einheitliches Profil; Einheitliches Profil; einheitliches Profil; Profil; rtcp; Profil aktivieren; Profil aktivieren; Profil aktivieren
title: Handbuch zur Echtzeit-Kundenprofil-API
description: Die Echtzeit-Kundenprofil-API ermöglicht es Entwicklern, Profildaten zu untersuchen und mit ihnen zu arbeiten, einschließlich Anzeigen von Profilen, Erstellen und Aktualisieren von Zusammenführungsrichtlinien, Exportieren oder Beispielprofildaten und Löschen von Profildaten, die nicht mehr benötigt werden oder fehlerhaft hinzugefügt wurden. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: 8f61840ad60b7d24c980b218b6f742485f5ebfdd
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 24%

---

# [!DNL Real-Time Customer Profile]-API-Handbuch

[!DNL Real-Time Customer Profile] ermöglicht es Ihnen, eine ganzheitliche Sicht auf Ihre einzelnen Kunden in Adobe Experience Platform zu erhalten. [!DNL Profile] ermöglicht es Ihnen, verschiedene Kundendaten aus verschiedenen Kanälen wie Online-, Offline-, CRM- und Drittanbieterdaten in einer einheitlichen Ansicht zu bündeln, die eine ausführbare, mit Zeitstempel versehene Übersicht über jede Kundeninteraktion bietet.

Die [!DNL Real-Time Customer Profile] Die API enthält mehrere Endpunkte, wie unten beschrieben. Weitere Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie in den einzelnen Endpunkthandbüchern sowie in den [Ersten Schritten](getting-started.md).

Um alle verfügbaren Endpunkte und CRUD-Vorgänge anzuzeigen, besuchen Sie die [Referenz-Swagger zur Echtzeit-Kundenprofil-API](https://www.adobe.com/go/profile-apis-en).

Eine Anleitung zum Arbeiten mit [!DNL Real-Time Customer Profile] Daten in der [!DNL Experience Platform] Benutzeroberfläche, siehe [Profil-Benutzerhandbuch](../ui/user-guide.md).

<!-- ## (Alpha) Computed attributes {#computed-attributes}

>[!IMPORTANT]
>
>Computed attribute functionality is in alpha and is not available to all users. Documentation and functionality are subject to change.

Computed attributes are functions used to aggregate event-level data into profile-level attributes. These functions are automatically computed so that they can be used across segmentation, activation, and personalization.

Each computed attribute contains an expression, or "rule", that evaluates incoming data and stores the resulting value in a profile attribute. These computations help you to easily answer questions related to things like lifetime purchase value, time between purchases, or number of application opens, without requiring you to manually perform complex calculations each time the information is needed. These computed attribute values can then be viewed in a profile, used to create a segment, or accessed through a number of different access patterns.

You can create, view, edit, and delete computed attributes using the `config/computedAttributes` endpoint. To learn how to use computed attributes, refer to the [computed attributes overview](../computed-attributes/overview.md). For API operations, visit the [computed attributes API endpoint guide](../computed-attributes/ca-api.md). -->

## Edge-Projektionen {#edge-projections}

Die Adobe Experience Platform ermöglicht eine Personalisierung von Kundenerlebnissen in Echtzeit, indem sie Daten auf strategisch platzierten Servern („Edge“-Server genannt) leicht zugänglich macht. Die [!DNL Real-Time Customer Profile] API bietet Endpunkte für die Arbeit mit Edges über Komponenten, die als &quot;Projektionen&quot;bezeichnet werden. Dazu gehören Projektionskonfigurationen, um zu ermitteln, welche Daten auf die einzelnen Edge-Server projiziert werden sollen, sowie Projektionsziele, um zu definieren, wohin eine Projektion geleitet werden soll. Ausführliche Informationen zum Arbeiten mit Edge-Projektionen finden Sie im [Handbuch zu Projektionskonfigurationen und Endpunkten](edge-projections.md).

## Entitäten ([!DNL Profile]-Zugriff) {#entities}

Über Adobe Experience Platform können Sie auf [!DNL Real-Time Customer Profile] Daten mithilfe von RESTful-APIs oder der Benutzeroberfläche. Um zu erfahren, wie Sie mithilfe der API auf Entitäten zugreifen, die allgemein als &quot;Profile&quot;bezeichnet werden, führen Sie die Schritte aus, die im Abschnitt [Endpunktleitfaden für Entitäten](entities.md). So greifen Sie auf Profile zu, die [!DNL Platform] Benutzeroberfläche, siehe [Profil-Benutzerhandbuch](../ui/user-guide.md).

## Exportaufträge ([!DNL Profile]-Export) {#profile-export}

[!DNL Real-Time Customer Profile] -Daten können zur weiteren Verarbeitung in einen Datensatz exportiert werden, z. B. zum Exportieren von Zielgruppensegmenten zur Aktivierung oder zum Reporting von Profilattributen. Exportaufträge für Zielgruppensegmente sind Teil der [!DNL Adobe Experience Platform Segmentation Service] API, lesen Sie bitte die [Endpunktleitfaden für Segmentierungs-Exportaufträge](../../profile/api/export-jobs.md) , um mehr zu erfahren. Eine schrittweise Anleitung zum Erstellen und Verwalten von Exportaufträgen für Profilattribute finden Sie unter [Endpunktleitfaden für Exportaufträge](export-jobs.md).

## Zusammenführungsrichtlinien {#merge-policies}

Beim Zusammenführen von Daten aus mehreren Quellen in [!DNL Experience Platform], sind Zusammenführungsrichtlinien Regeln, die [!DNL Platform] verwendet , um zu bestimmen, wie Daten priorisiert werden und welche Daten kombiniert werden, um individuelle Kundenprofile zu erstellen. Verwenden der [!DNL Real-Time Customer Profile] API können Sie neue Zusammenführungsrichtlinien erstellen, vorhandene Richtlinien verwalten und eine standardmäßige Zusammenführungsrichtlinie für Ihre Organisation festlegen. Informationen zum Arbeiten mit Zusammenführungsrichtlinien mithilfe der finden Sie im [API-Endpunkthandbuch für Zusammenführungsrichtlinien](merge-policies.md).

Um mehr über Zusammenführungsrichtlinien und ihre Rolle innerhalb von Platform zu erfahren, lesen Sie zunächst das [Übersicht über Zusammenführungsrichtlinien](../merge-policies/overview.md).

## Musterstatus der Vorschau ([!DNL Profile]-Vorschau) {#profile-preview}

Da Daten in Platform erfasst werden, wird ein Beispielauftrag ausgeführt, um die Profilanzahl und andere datenbezogene Metriken des Echtzeit-Kundenprofils zu aktualisieren. Die Ergebnisse dieses Beispielauftrags können mit dem `/previewsamplestatus` -Endpunkt, Teil der Echtzeit-Kundenprofil-API. Dieser Endpunkt kann auch verwendet werden, um Profilverteilungen nach Datensatz und Identitäts-Namespace aufzulisten und mehrere Berichte zu generieren, um Einblicke in die Zusammensetzung des Profilspeichers Ihres Unternehmens zu erhalten.  Erste Schritte mit der Verwendung von `/profilepreviewstatus` -Endpunkt, siehe [Beispiel-Status-Endpunktleitfaden für die Vorschau](preview-sample-status.md).

## Profilsystemaufträge {#profile-system-jobs}

Profilaktivierte Daten, die in [!DNL Platform] wird im [!DNL Data Lake] sowie [!DNL Real-Time Customer Profile] Datenspeicher. Gelegentlich kann es erforderlich sein, einen Datensatz oder Batch aus der [!DNL Profile] speichern, um Daten zu entfernen, die Sie nicht mehr benötigen oder die fehlerhaft hinzugefügt wurden. Dazu muss die API zum Erstellen einer [!DNL Profile System Job], auch als bezeichnet[!DNL delete request]&quot;, die bei Bedarf geändert, überwacht oder gelöscht werden können. Erfahren Sie, wie Sie Löschanfragen mit der `/system/jobs` -Endpunkt im [!DNL Real-Time Customer Profile] API ausführen, folgen Sie den Schritten, die im Abschnitt [Endleitfaden für Profilsystemaufträge](profile-system-jobs.md).

## Profilattribute aktualisieren {#update-profile}

Gelegentlich kann es erforderlich sein, Daten im Profilspeicher Ihrer Organisation zu aktualisieren. Vielleicht müssen Sie zum Beispiel Datensätze korrigieren oder einen Attributwert ändern. Dies kann durch Batch-Aufnahme erfolgen und erfordert einen profilaktivierten Datensatz, der mit einem Upsert-Tag konfiguriert ist. Weitere Informationen zur Konfiguration eines Datensatzes für Attributaktualisierungen finden Sie im Tutorial zur [Aktivierung eines Datensatzes für Profil und Upsert](../../catalog/datasets/enable-upsert.md).

## Nächste Schritte {#next-steps}

So starten Sie Aufrufe mit dem [!DNL Real-Time Customer Profile] API, lesen Sie die [Erste Schritte](getting-started.md) Wählen Sie dann eine der Endpunktleitfäden aus, um zu erfahren, wie Sie bestimmte [!DNL Profile]-zugehörige Endpunkte. So arbeiten Sie mit [!DNL Profile] Daten, die [!DNL Experience Platform] Benutzeroberfläche, siehe [Benutzerhandbuch zum Echtzeit-Kundenprofil](../ui/user-guide.md).
