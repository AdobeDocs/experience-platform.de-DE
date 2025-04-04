---
keywords: Experience Platform;Profil;Echtzeit-Kundenprofil;Fehlerbehebung;API;Einheitliches Profil;Einheitliches Profil;Profil;rtcp;Profil aktivieren;Profil aktivieren
title: Handbuch zur Echtzeit-Kundenprofil-API
description: Mit der Echtzeit-Kundenprofil-API können Entwickler Profildaten untersuchen und mit ihnen arbeiten, einschließlich Profilen anzeigen, Zusammenführungsrichtlinien erstellen und aktualisieren, Profildaten exportieren oder als Beispiel verwenden und Profildaten löschen, die nicht mehr erforderlich sind oder irrtümlich hinzugefügt wurden. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
role: Developer
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 19%

---

# [!DNL Real-Time Customer Profile]-API-Handbuch

[!DNL Real-Time Customer Profile] können Sie sich einen ganzheitlichen Überblick über Ihre einzelnen Kunden in Adobe Experience Platform verschaffen. Mit [!DNL Profile] können Sie unterschiedliche Kundendaten aus verschiedenen Kanälen, wie Online-, Offline-, CRM- und Drittanbieterdaten, in einer zentralen Ansicht zusammenführen, die eine aussagekräftige, Darstellung jeder Kundeninteraktion mit Zeitstempel bietet.

Die [!DNL Real-Time Customer Profile]-API umfasst mehrere Endpunkte, die unten beschrieben werden. Weitere Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie in den einzelnen Endpunkthandbüchern sowie in den [Ersten Schritten](getting-started.md).

Um alle verfügbaren Endpunkte und CRUD-Vorgänge anzuzeigen, besuchen Sie den [Echtzeit-Kundenprofil-API-Referenz-Swagger](https://www.adobe.com/go/profile-apis-en).

Eine Anleitung zum Arbeiten mit [!DNL Real-Time Customer Profile] in der [!DNL Experience Platform]-Benutzeroberfläche finden Sie im [Benutzerhandbuch für Profile](../ui/user-guide.md).

## Berechnete Attribute {#computed-attributes}

Berechnete Attribute sind Funktionen, mit denen Daten auf Ereignisebene in Attribute auf Profilebene aggregiert werden. Diese Funktionen werden automatisch berechnet, damit sie für die Segmentierung, Aktivierung und Personalisierung verwendet werden können.

Jedes berechnete Attribut enthält einen Ausdruck oder eine „Regel“, die eingehende Daten auswertet und den resultierenden Wert in einem Profilattribut speichert. Mit diesen Berechnungen können Sie Fragen im Zusammenhang mit dem Kaufwert über die gesamte Lebensdauer, der Zeit zwischen Käufen oder der Anzahl der Anwendungsöffnungen leicht beantworten, ohne für jede benötigte Information manuell komplexe Berechnungen ausführen zu müssen. Diese berechneten Attributwerte können dann in einem Profil angezeigt, zur Erstellung einer Zielgruppe verwendet oder über verschiedene Zugriffsmuster aufgerufen werden.

Sie können berechnete Attribute mithilfe des `ca/attributes/`-Endpunkts erstellen, anzeigen, bearbeiten und löschen. Informationen zur Verwendung berechneter Attribute finden Sie unter [Berechnete Attribute - Übersicht](../computed-attributes/overview.md). Informationen zu API-Vorgängen finden Sie im [Handbuch zu API-Endpunkten für berechnete Attribute](../computed-attributes/api.md).

## Entitäten ([!DNL Profile]-Zugriff) {#entities}

Über Adobe Experience Platform können Sie mithilfe von RESTful-APIs oder der Benutzeroberfläche auf [!DNL Real-Time Customer Profile] Daten zugreifen. Um mithilfe der API auf Entitäten zuzugreifen, die gemeinhin als „Profile“ bezeichnet werden, führen Sie die Schritte aus, die im [Handbuch für Entitäten-Endpunkte“ beschrieben ](entities.md). Informationen zum Zugriff auf Profile über die [!DNL Experience Platform] Benutzeroberfläche finden Sie im [Benutzerhandbuch für Profile](../ui/user-guide.md).

## Exportaufträge ([!DNL Profile]-Export) {#profile-export}

[!DNL Real-Time Customer Profile] Daten können zur weiteren Verarbeitung in einen Datensatz exportiert werden, z. B. zum Exportieren von Zielgruppen zur Aktivierung oder Profilattributen für das Reporting. Exportvorgänge für Zielgruppen sind Teil der [!DNL Adobe Experience Platform Segmentation Service]-API. Weitere Informationen finden Sie [ Handbuch ](../../profile/api/export-jobs.md) Segmentierungsexportvorgänge . Schrittweise Anweisungen zum Erstellen und Verwalten von Exportvorgängen für Profilattribute finden Sie im [Handbuch zu Exportvorgängen](export-jobs.md).

## Zusammenführungsrichtlinien {#merge-policies}

Beim Zusammenführen von Daten aus mehreren Quellen in [!DNL Experience Platform] dienen Zusammenführungsrichtlinien als jene Regeln, mit denen [!DNL Experience Platform] bestimmt, wie Daten priorisiert werden und welche Daten kombiniert werden sollen, um individuelle Kundenprofile zu erstellen. Mit der [!DNL Real-Time Customer Profile]-API können Sie neue Zusammenführungsrichtlinien erstellen, vorhandene Richtlinien verwalten und eine standardmäßige Zusammenführungsrichtlinie für Ihre Organisation festlegen. Informationen zum Arbeiten mit Zusammenführungsrichtlinien mithilfe der API finden Sie im [Handbuch zu Endpunkten von Zusammenführungsrichtlinien](merge-policies.md).

Um mehr über Zusammenführungsrichtlinien und ihre Rolle in Experience Platform zu erfahren, lesen Sie zunächst die Übersicht über [ Zusammenführungsrichtlinien ](../merge-policies/overview.md).

## Musterstatus der Vorschau ([!DNL Profile]-Vorschau) {#profile-preview}

Bei der Aufnahme von Daten in Experience Platform wird ein Beispielvorgang ausgeführt, um die Profilanzahl und andere Metriken zu aktualisieren, die sich auf Echtzeit-Kundenprofildaten beziehen. Die Ergebnisse dieses Beispielauftrags können mit dem `/previewsamplestatus`-Endpunkt, der Teil der Echtzeit-Kundenprofil-API ist, angezeigt werden. Dieser Endpunkt kann auch verwendet werden, um Profilverteilungen sowohl nach Datensatz als auch nach Identity-Namespace aufzulisten und mehrere Berichte zu generieren, um einen Einblick in die Zusammensetzung des Profilspeichers Ihres Unternehmens zu erhalten.  Informationen zu den ersten Schritten mit dem `/profilepreviewstatus`-Endpunkt finden Sie im [Handbuch zum Vorschaubeispielstatus-Endpunkt](preview-sample-status.md).

## Profilsystemaufträge {#profile-system-jobs}

Profilaktivierte Daten, die in [!DNL Experience Platform] aufgenommen werden, werden sowohl im [!DNL Data Lake] als auch im [!DNL Real-Time Customer Profile] gespeichert. Gelegentlich kann es erforderlich sein, mit einem Datensatz verknüpfte Profildaten aus dem Profilspeicher zu löschen, um nicht mehr benötigte oder irrtümlich hinzugefügte Daten zu entfernen. Dazu muss mithilfe der -API ein [!DNL Profile System Job] erstellt werden, das auch als &quot;[!DNL delete request]&quot; bezeichnet wird und bei Bedarf geändert, überwacht oder gelöscht werden kann. Um zu erfahren, wie Sie mit Löschanfragen unter Verwendung des `/system/jobs`-Endpunkts in der [!DNL Real-Time Customer Profile]-API arbeiten, folgen Sie den Schritten, die im [Handbuch zum Vorgangs-Endpunkt von Profile System](profile-system-jobs.md) beschrieben sind.

## Aktualisieren von Profilattributen {#update-profile}

Gelegentlich kann es erforderlich sein, Daten im Profilspeicher Ihrer Organisation zu aktualisieren. Vielleicht müssen Sie zum Beispiel Datensätze korrigieren oder einen Attributwert ändern. Dies kann durch Batch-Aufnahme erfolgen und erfordert einen profilaktivierten Datensatz, der mit einem Upsert-Tag konfiguriert ist. Weitere Informationen zur Konfiguration eines Datensatzes für Attributaktualisierungen finden Sie im Tutorial zur [Aktivierung eines Datensatzes für Profil und Upsert](../../catalog/datasets/enable-upsert.md).

## Nächste Schritte {#next-steps}

Um mit Aufrufen mit der [!DNL Real-Time Customer Profile]-API zu beginnen, lesen Sie [Erste Schritte](getting-started.md) und wählen Sie dann eines der Endpunkthandbücher aus, um zu erfahren, wie Sie bestimmte [!DNL Profile] Endpunkte verwenden. Informationen zum Arbeiten mit [!DNL Profile] Daten über die [!DNL Experience Platform]-Benutzeroberfläche finden [ im Benutzerhandbuch zum Echtzeit-Kundenprofil](../ui/user-guide.md).
