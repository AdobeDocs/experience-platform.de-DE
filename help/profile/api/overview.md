---
keywords: Experience Platform; Profil; Echtzeit-Kundenprofil; Fehlerbehebung; API; einheitliches Profil; einheitliches Profil; einheitliches Profil; Profil; rtcp; Profil aktivieren; Profil aktivieren
title: Handbuch zur Echtzeit-Kundenprofil-API
description: Die Echtzeit-Kundenprofil-API ermöglicht es Entwicklern, Profildaten zu untersuchen und mit ihnen zu arbeiten, einschließlich Anzeigen von Profilen, Erstellen und Aktualisieren von Zusammenführungsrichtlinien, Exportieren oder Beispielprofildaten und Löschen von Profildaten, die nicht mehr benötigt werden oder fehlerhaft hinzugefügt wurden. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
role: Developer
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 19%

---

# [!DNL Real-Time Customer Profile]-API-Handbuch

[!DNL Real-Time Customer Profile] ermöglicht es Ihnen, eine ganzheitliche Sicht auf Ihre einzelnen Kunden in Adobe Experience Platform zu erhalten. [!DNL Profile] ermöglicht es Ihnen, verschiedene Kundendaten aus verschiedenen Kanälen wie Online-, Offline-, CRM- und Drittanbieterdaten in einer einheitlichen Ansicht zu bündeln, die eine ausführbare, mit Zeitstempel versehene Übersicht über jede Kundeninteraktion bietet.

Die [!DNL Real-Time Customer Profile] Die API enthält mehrere Endpunkte, wie unten beschrieben. Weitere Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie in den einzelnen Endpunkthandbüchern sowie in den [Ersten Schritten](getting-started.md).

Um alle verfügbaren Endpunkte und CRUD-Vorgänge anzuzeigen, besuchen Sie die [Referenz-Swagger zur Echtzeit-Kundenprofil-API](https://www.adobe.com/go/profile-apis-en).

Eine Anleitung zum Arbeiten mit [!DNL Real-Time Customer Profile] Daten in der [!DNL Experience Platform] Benutzeroberfläche, siehe [Profil-Benutzerhandbuch](../ui/user-guide.md).

## [!BADGE Beta]{type=informative} Berechnete Attribute {#computed-attributes}

>[!IMPORTANT]
>
Die Funktion für berechnete Attribute befindet sich in der Beta-Phase und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalität können sich ändern.

Berechnete Attribute sind Funktionen, mit denen Daten auf Ereignisebene in Attribute auf Profilebene aggregiert werden. Diese Funktionen werden automatisch berechnet, sodass sie für die Segmentierung, Aktivierung und Personalisierung verwendet werden können.

Jedes berechnete Attribut enthält einen Ausdruck oder eine &quot;Regel&quot;, der/die eingehende Daten auswertet und den resultierenden Wert in einem Profilattribut speichert. Mit diesen Berechnungen können Sie Fragen im Zusammenhang mit dem Kaufwert über die gesamte Lebensdauer, der Zeit zwischen Käufen oder der Anzahl der Anwendungsöffnungen leicht beantworten, ohne für jede benötigte Information manuell komplexe Berechnungen ausführen zu müssen. Diese berechneten Attributwerte können dann in einem Profil angezeigt, zum Erstellen einer Zielgruppe verwendet oder über verschiedene Zugriffsmuster aufgerufen werden.

Sie können berechnete Attribute mithilfe der Variablen `ca/attributes/` -Endpunkt. Informationen zur Verwendung berechneter Attribute finden Sie im Abschnitt [Übersicht über berechnete Attribute](../computed-attributes/overview.md). Besuchen Sie für API-Vorgänge den Abschnitt [Handbuch zum API-Endpunkt für berechnete Attribute](../computed-attributes/api.md).

## Entitäten ([!DNL Profile]-Zugriff) {#entities}

Über Adobe Experience Platform können Sie auf [!DNL Real-Time Customer Profile] Daten mithilfe von RESTful-APIs oder der Benutzeroberfläche. Um zu erfahren, wie Sie mithilfe der API auf Entitäten zugreifen, die allgemein als &quot;Profile&quot;bezeichnet werden, führen Sie die Schritte aus, die im Abschnitt [Endpunktleitfaden für Entitäten](entities.md). So greifen Sie auf Profile zu, die [!DNL Platform] Benutzeroberfläche, siehe [Profil-Benutzerhandbuch](../ui/user-guide.md).

## Exportaufträge ([!DNL Profile]-Export) {#profile-export}

[!DNL Real-Time Customer Profile] -Daten können zur weiteren Verarbeitung in einen Datensatz exportiert werden, z. B. zum Exportieren von Zielgruppen zur Aktivierung oder zum Reporting von Profilattributen. Exportaufträge für Zielgruppen sind Teil der [!DNL Adobe Experience Platform Segmentation Service] API, lesen Sie bitte die [Endpunktleitfaden für Segmentierungs-Exportaufträge](../../profile/api/export-jobs.md) , um mehr zu erfahren. Eine schrittweise Anleitung zum Erstellen und Verwalten von Exportaufträgen für Profilattribute finden Sie unter [Endpunktleitfaden für Exportaufträge](export-jobs.md).

## Zusammenführungsrichtlinien {#merge-policies}

Beim Zusammenführen von Daten aus mehreren Quellen in [!DNL Experience Platform], sind Zusammenführungsrichtlinien Regeln, die [!DNL Platform] verwendet , um zu bestimmen, wie Daten priorisiert werden und welche Daten kombiniert werden, um individuelle Kundenprofile zu erstellen. Verwenden der [!DNL Real-Time Customer Profile] API können Sie neue Zusammenführungsrichtlinien erstellen, vorhandene Richtlinien verwalten und eine standardmäßige Zusammenführungsrichtlinie für Ihre Organisation festlegen. Um mit Zusammenführungsrichtlinien mithilfe der API zu arbeiten, besuchen Sie die [Endleitfaden für Zusammenführungsrichtlinien](merge-policies.md).

Um mehr über Zusammenführungsrichtlinien und ihre Rolle innerhalb von Platform zu erfahren, lesen Sie zunächst das [Übersicht über Zusammenführungsrichtlinien](../merge-policies/overview.md).

## Musterstatus der Vorschau ([!DNL Profile]-Vorschau) {#profile-preview}

Da Daten in Platform erfasst werden, wird ein Beispielauftrag ausgeführt, um die Profilanzahl und andere datenbezogene Metriken des Echtzeit-Kundenprofils zu aktualisieren. Die Ergebnisse dieses Beispielauftrags können mit dem `/previewsamplestatus` -Endpunkt, Teil der Echtzeit-Kundenprofil-API. Dieser Endpunkt kann auch verwendet werden, um Profilverteilungen nach Datensatz und Identitäts-Namespace aufzulisten und mehrere Berichte zu generieren, um Einblicke in die Zusammensetzung des Profilspeichers Ihres Unternehmens zu erhalten.  Erste Schritte mit der Verwendung von `/profilepreviewstatus` -Endpunkt, siehe [Beispiel-Status-Endpunktleitfaden für die Vorschau](preview-sample-status.md).

## Profilsystemaufträge {#profile-system-jobs}

Profilaktivierte Daten, die in [!DNL Platform] wird im [!DNL Data Lake] sowie [!DNL Real-Time Customer Profile] Datenspeicher. Gelegentlich kann es erforderlich sein, mit einem Datensatz verknüpfte Profildaten aus dem Profilspeicher zu löschen, um nicht mehr benötigte oder fehlerhaft hinzugefügte Daten zu entfernen. Dies erfordert die Verwendung der API zum Erstellen einer [!DNL Profile System Job], auch als bezeichnet[!DNL delete request]&quot;, die bei Bedarf geändert, überwacht oder gelöscht werden können. Erfahren Sie, wie Sie Löschanfragen mit der `/system/jobs` -Endpunkt im [!DNL Real-Time Customer Profile] API ausführen, folgen Sie den Schritten, die im Abschnitt [Endleitfaden für Profilsystemaufträge](profile-system-jobs.md).

## Profilattribute aktualisieren {#update-profile}

Gelegentlich kann es erforderlich sein, Daten im Profilspeicher Ihres Unternehmens zu aktualisieren. Vielleicht müssen Sie zum Beispiel Datensätze korrigieren oder einen Attributwert ändern. Dies kann durch Batch-Aufnahme erfolgen und erfordert einen profilaktivierten Datensatz, der mit einem Upsert-Tag konfiguriert ist. Weitere Informationen zur Konfiguration eines Datensatzes für Attributaktualisierungen finden Sie im Tutorial zur [Aktivierung eines Datensatzes für Profil und Upsert](../../catalog/datasets/enable-upsert.md).

## Nächste Schritte {#next-steps}

So starten Sie Aufrufe mit dem [!DNL Real-Time Customer Profile] API, lesen Sie die [Erste Schritte](getting-started.md) Wählen Sie dann eine der Endpunktleitfäden aus, um zu erfahren, wie Sie bestimmte [!DNL Profile]-zugehörige Endpunkte. Arbeiten mit [!DNL Profile] Daten, die [!DNL Experience Platform] Benutzeroberfläche, siehe [Benutzerhandbuch zum Echtzeit-Kundenprofil](../ui/user-guide.md).
