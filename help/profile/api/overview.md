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

[!DNL Real-Time Customer Profile] ermöglicht es Ihnen, eine ganzheitliche Sicht Ihrer einzelnen Kunden in Adobe Experience Platform zu erhalten. Mit [!DNL Profile] können Sie unterschiedliche Kundendaten aus verschiedenen Kanälen, z. B. Online-, Offline-, CRM- und Drittanbieter-Daten, in einer einheitlichen Ansicht zusammenfassen, die ein umsetzbares, mit Zeitstempel versehenes Konto für jede Kundeninteraktion bietet.

Die [!DNL Real-Time Customer Profile] -API enthält mehrere Endpunkte, wie unten dargestellt. Weitere Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie in den einzelnen Endpunkthandbüchern sowie in den [Ersten Schritten](getting-started.md).

Um alle verfügbaren Endpunkte und CRUD-Vorgänge anzuzeigen, besuchen Sie den [Real-Time Customer Profile API Reference Swagger](https://www.adobe.com/go/profile-apis-en).

Eine Anleitung zum Arbeiten mit [!DNL Real-Time Customer Profile] -Daten in der Benutzeroberfläche von [!DNL Experience Platform] finden Sie im [Profil-Benutzerhandbuch](../ui/user-guide.md).

## [!BADGE Beta]{type=informative} Berechnete Attribute {#computed-attributes}

>[!IMPORTANT]
>
Die Funktion für berechnete Attribute befindet sich in der Beta-Phase und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalität können sich ändern.

Berechnete Attribute sind Funktionen, mit denen Daten auf Ereignisebene in Attribute auf Profilebene aggregiert werden. Diese Funktionen werden automatisch berechnet, sodass sie für die Segmentierung, Aktivierung und Personalisierung verwendet werden können.

Jedes berechnete Attribut enthält einen Ausdruck oder eine &quot;Regel&quot;, der/die eingehende Daten auswertet und den resultierenden Wert in einem Profilattribut speichert. Mit diesen Berechnungen können Sie Fragen im Zusammenhang mit dem Kaufwert über die gesamte Lebensdauer, der Zeit zwischen Käufen oder der Anzahl der Anwendungsöffnungen leicht beantworten, ohne für jede benötigte Information manuell komplexe Berechnungen ausführen zu müssen. Diese berechneten Attributwerte können dann in einem Profil angezeigt, zum Erstellen einer Zielgruppe verwendet oder über verschiedene Zugriffsmuster aufgerufen werden.

Sie können berechnete Attribute mit dem `ca/attributes/` -Endpunkt erstellen, anzeigen, bearbeiten und löschen. Informationen zur Verwendung berechneter Attribute finden Sie in der [Übersicht über berechnete Attribute](../computed-attributes/overview.md). Besuchen Sie für API-Vorgänge das Handbuch [API-Endpunkt für berechnete Attribute](../computed-attributes/api.md).

## Entitäten ([!DNL Profile]-Zugriff) {#entities}

Über Adobe Experience Platform können Sie mithilfe von RESTful-APIs oder der Benutzeroberfläche auf [!DNL Real-Time Customer Profile] -Daten zugreifen. Um zu erfahren, wie Sie mithilfe der API auf Entitäten zugreifen können, die allgemein als &quot;Profile&quot;bezeichnet werden, führen Sie die Schritte aus, die im [Endpunkthandbuch für Entitäten](entities.md) beschrieben sind. Informationen zum Zugriff auf Profile über die Benutzeroberfläche von [!DNL Platform] finden Sie im [Profil-Benutzerhandbuch](../ui/user-guide.md).

## Exportaufträge ([!DNL Profile]-Export) {#profile-export}

[!DNL Real-Time Customer Profile] -Daten können zur weiteren Verarbeitung in einen Datensatz exportiert werden, z. B. zum Exportieren von Zielgruppen zur Aktivierung oder zum Exportieren von Profilattributen für die Berichterstellung. Exportaufträge für Zielgruppen sind Teil der [!DNL Adobe Experience Platform Segmentation Service] -API. Weiterführende Informationen dazu finden Sie im Endpunktleitfaden [Segmentierungsexport-Aufträge . ](../../profile/api/export-jobs.md) Eine schrittweise Anleitung zum Erstellen und Verwalten von Exportaufträgen für Profilattribute finden Sie im [Endpunkthandbuch zu Exportaufträgen](export-jobs.md).

## Zusammenführungsrichtlinien {#merge-policies}

Beim Zusammenführen von Daten aus mehreren Quellen in [!DNL Experience Platform] dienen Zusammenführungsrichtlinien als jene Regeln, mit denen [!DNL Platform] bestimmt, wie Daten priorisiert werden und welche Daten kombiniert werden, um individuelle Kundenprofile zu erstellen. Mit der API [!DNL Real-Time Customer Profile] können Sie neue Zusammenführungsrichtlinien erstellen, vorhandene Richtlinien verwalten und eine standardmäßige Zusammenführungsrichtlinie für Ihre Organisation festlegen. Informationen zum Arbeiten mit Zusammenführungsrichtlinien mithilfe der API finden Sie im [Endpunkthandbuch zu Zusammenführungsrichtlinien](merge-policies.md).

Um mehr über Zusammenführungsrichtlinien und ihre Rolle in Platform zu erfahren, lesen Sie zunächst die [Übersicht über Zusammenführungsrichtlinien](../merge-policies/overview.md).

## Musterstatus der Vorschau ([!DNL Profile]-Vorschau) {#profile-preview}

Da Daten in Platform erfasst werden, wird ein Beispielauftrag ausgeführt, um die Profilanzahl und andere datenbezogene Metriken des Echtzeit-Kundenprofils zu aktualisieren. Die Ergebnisse dieses Beispielauftrags können mit dem `/previewsamplestatus` -Endpunkt angezeigt werden, der Teil der Echtzeit-Kundenprofil-API ist. Dieser Endpunkt kann auch verwendet werden, um Profilverteilungen nach Datensatz und Identitäts-Namespace aufzulisten und mehrere Berichte zu generieren, um Einblicke in die Zusammensetzung des Profilspeichers Ihres Unternehmens zu erhalten.  Informationen zum Einstieg in die Verwendung des Endpunkts `/profilepreviewstatus` finden Sie im Handbuch [Vorschaustatus-Endpunkt-Handbuch](preview-sample-status.md) .

## Profilsystemaufträge {#profile-system-jobs}

Profilaktivierte Daten, die in [!DNL Platform] erfasst werden, werden sowohl im [!DNL Data Lake] als auch im [!DNL Real-Time Customer Profile] -Datenspeicher gespeichert. Gelegentlich kann es erforderlich sein, mit einem Datensatz verknüpfte Profildaten aus dem Profilspeicher zu löschen, um nicht mehr benötigte oder fehlerhaft hinzugefügte Daten zu entfernen. Dazu muss die API zum Erstellen eines [!DNL Profile System Job] (auch als &quot;[!DNL delete request]&quot; bezeichnet) verwendet werden, der bei Bedarf geändert, überwacht oder gelöscht werden kann. Um zu erfahren, wie Sie mit Löschanfragen mithilfe des Endpunkts `/system/jobs` in der API [!DNL Real-Time Customer Profile] arbeiten, führen Sie die Schritte aus, die im Endpunkthandbuch für Profilsystemaufträge](profile-system-jobs.md) beschrieben sind.[

## Profilattribute aktualisieren {#update-profile}

Gelegentlich kann es erforderlich sein, Daten im Profilspeicher Ihres Unternehmens zu aktualisieren. Vielleicht müssen Sie zum Beispiel Datensätze korrigieren oder einen Attributwert ändern. Dies kann durch Batch-Aufnahme erfolgen und erfordert einen profilaktivierten Datensatz, der mit einem Upsert-Tag konfiguriert ist. Weitere Informationen zur Konfiguration eines Datensatzes für Attributaktualisierungen finden Sie im Tutorial zur [Aktivierung eines Datensatzes für Profil und Upsert](../../catalog/datasets/enable-upsert.md).

## Nächste Schritte {#next-steps}

Um Aufrufe mit der API [!DNL Real-Time Customer Profile] durchzuführen, lesen Sie das Handbuch [Erste Schritte](getting-started.md) und wählen Sie dann eine der Endpunkthandbücher aus, um zu erfahren, wie Sie bestimmte Endpunkte mit [!DNL Profile] verwenden. Informationen zum Arbeiten mit [!DNL Profile] -Daten mithilfe der [!DNL Experience Platform] -Benutzeroberfläche finden Sie im [Benutzerhandbuch zum Echtzeit-Kundenprofil](../ui/user-guide.md).
