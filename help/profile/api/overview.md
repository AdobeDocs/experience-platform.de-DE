---
keywords: Experience Platform; Profil; Echtzeit-Kundenprofil; Fehlerbehebung; API; einheitliches Profil; Einheitliches Profil; einheitliches Profil; Profil; rtcp; Profil aktivieren; Profil aktivieren; Profil aktivieren
title: Handbuch zur Echtzeit-Kundenprofil-API
description: Die Echtzeit-Kundenprofil-API ermöglicht es Entwicklern, Profildaten zu untersuchen und mit ihnen zu arbeiten, einschließlich Anzeigen von Profilen, Erstellen und Aktualisieren von Zusammenführungsrichtlinien, Exportieren oder Beispielprofildaten und Löschen von Profildaten, die nicht mehr benötigt werden oder fehlerhaft hinzugefügt wurden. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: 4c544170636040b8ab58780022a4c357cfa447de
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 23%

---

# [!DNL Real-time Customer Profile]-API-Handbuch

[!DNL Real-time Customer Profile] ermöglicht es Ihnen, eine ganzheitliche Sicht auf Ihre einzelnen Kunden in Adobe Experience Platform zu erhalten. [!DNL Profile] ermöglicht es Ihnen, verschiedene Kundendaten aus verschiedenen Kanälen wie Online-, Offline-, CRM- und Drittanbieterdaten in einer einheitlichen Ansicht zu bündeln, die eine ausführbare, mit Zeitstempel versehene Übersicht über jede Kundeninteraktion bietet.

Die [!DNL Real-time Customer Profile]-API enthält mehrere Endpunkte, wie unten dargestellt. Weitere Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie in den einzelnen Endpunkthandbüchern sowie in den [Ersten Schritten](getting-started.md).

Um alle verfügbaren Endpunkte und CRUD-Vorgänge anzuzeigen, besuchen Sie den [Real-time Customer Profile API Reference Swagger](https://www.adobe.com/go/profile-apis-en).

Eine Anleitung zum Arbeiten mit [!DNL Real-time Customer Profile]-Daten in der [!DNL Experience Platform]-Benutzeroberfläche finden Sie im [Profil-Benutzerhandbuch](../ui/user-guide.md).

## (Alpha) Berechnete Attribute {#computed-attributes}

>[!IMPORTANT]
>
>Die Funktion für berechnete Attribute ist alphanumerisch und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalität können sich ändern.

Berechnete Attribute sind Funktionen, mit denen Daten auf Ereignisebene in Attribute auf Profilebene aggregiert werden. Diese Funktionen werden automatisch berechnet, sodass sie für die Segmentierung, Aktivierung und Personalisierung verwendet werden können.

Jedes berechnete Attribut enthält einen Ausdruck oder eine &quot;Regel&quot;, der/die eingehende Daten auswertet und den resultierenden Wert in einem Profilattribut speichert. Mit diesen Berechnungen können Sie Fragen im Zusammenhang mit dem Kaufwert über die gesamte Lebensdauer, der Zeit zwischen Käufen oder der Anzahl der Anwendungsöffnungen leicht beantworten, ohne für jede benötigte Information manuell komplexe Berechnungen ausführen zu müssen. Diese berechneten Attributwerte können dann in einem Profil angezeigt, zum Erstellen eines Segments verwendet oder über verschiedene Zugriffsmuster aufgerufen werden.

Mithilfe des Endpunkts `config/computedAttributes` können Sie berechnete Attribute erstellen, anzeigen, bearbeiten und löschen. Informationen zur Verwendung berechneter Attribute finden Sie in der [Übersicht über berechnete Attribute](../computed-attributes/overview.md). Besuchen Sie für API-Vorgänge das [Handbuch zum API-Endpunkt für berechnete Attribute](../computed-attributes/ca-api.md).

## Edge-Projektionen {#edge-projections}

Die Adobe Experience Platform ermöglicht eine Personalisierung von Kundenerlebnissen in Echtzeit, indem sie Daten auf strategisch platzierten Servern („Edge“-Server genannt) leicht zugänglich macht. Die [!DNL Real-time Customer Profile]-API bietet Endpunkte zum Arbeiten mit Edges über Komponenten, die als &quot;Projektionen&quot;bezeichnet werden. Dazu gehören Projektionskonfigurationen, um zu ermitteln, welche Daten auf die einzelnen Edge-Server projiziert werden sollen, sowie Projektionsziele, um zu definieren, wohin eine Projektion geleitet werden soll. Ausführliche Informationen zum Arbeiten mit Edge-Projektionen finden Sie im Handbuch [Projektionskonfigurationen und Endpunkte ](edge-projections.md).

## Entitäten ([!DNL Profile]-Zugriff) {#entities}

Über Adobe Experience Platform können Sie mithilfe von RESTful-APIs oder der Benutzeroberfläche auf [!DNL Real-time Customer Profile] Daten zugreifen. Um zu erfahren, wie Sie mithilfe der API auf Entitäten zugreifen können, die allgemein als &quot;Profile&quot;bezeichnet werden, führen Sie die Schritte aus, die im [Endpoint-Handbuch für Entitäten](entities.md) beschrieben sind. Informationen zum Zugriff auf Profile mithilfe der [!DNL Platform]-Benutzeroberfläche finden Sie im [Profil-Benutzerhandbuch](../ui/user-guide.md).

## Exportaufträge ([!DNL Profile]-Export) {#profile-export}

[!DNL Real-time Customer Profile] -Daten können zur weiteren Verarbeitung in einen Datensatz exportiert werden, z. B. zum Exportieren von Zielgruppensegmenten zur Aktivierung oder zum Reporting von Profilattributen. Exportaufträge für Zielgruppensegmente sind Teil der [!DNL Adobe Experience Platform Segmentation Service]-API. Weitere Informationen finden Sie im [Endpoint-Handbuch für Segmentierungsexportaufträge](../../profile/api/export-jobs.md). Eine schrittweise Anleitung zum Erstellen und Verwalten von Exportaufträgen für Profilattribute finden Sie im [Endpunkt für Exportaufträge](export-jobs.md).

## Zusammenführungsrichtlinien {#merge-policies}

Beim Zusammenführen von Daten aus mehreren Quellen in [!DNL Experience Platform] dienen Zusammenführungsrichtlinien als jene Regeln, mit denen [!DNL Platform] bestimmt, wie Daten priorisiert werden und welche Daten kombiniert werden, um individuelle Kundenprofile zu erstellen. Mit der API [!DNL Real-time Customer Profile] können Sie neue Zusammenführungsrichtlinien erstellen, vorhandene Richtlinien verwalten und eine standardmäßige Zusammenführungsrichtlinie für Ihre Organisation festlegen. Informationen zum Arbeiten mit Zusammenführungsrichtlinien mithilfe der finden Sie im [API-Endpunkthandbuch für Zusammenführungsrichtlinien](merge-policies.md).

Um mehr über Zusammenführungsrichtlinien und ihre Rolle in Platform zu erfahren, lesen Sie zunächst den [Überblick über Zusammenführungsrichtlinien](../merge-policies/overview.md).

## Musterstatus der Vorschau ([!DNL Profile]-Vorschau) {#profile-preview}

Da für Profil aktivierte Daten in Experience Platform erfasst werden, werden sie im Profildatenspeicher gespeichert. Da die Anzahl der Datensätze im Profilspeicher zunimmt oder sinkt, wird ein Beispielauftrag ausgeführt, der Informationen darüber enthält, wie viele Profilfragmente und zusammengeführte Profile sich im Datenspeicher befinden. Mithilfe der Profil-API können Sie eine Vorschau des neuesten erfolgreichen Beispiels anzeigen sowie die Profilverteilung nach Datensatz und Identitäts-Namespace auflisten. Informationen zum Einstieg in die Verwendung des Endpunkts `/profilepreviewstatus` finden Sie im [Handbuch zum Beispiel-Status-Endpunkt für die Vorschau](preview-sample-status.md).

## Profilsystemaufträge {#profile-system-jobs}

Profilaktivierte Daten, die in [!DNL Platform] erfasst werden, werden im [!DNL Data Lake] sowie im [!DNL Real-time Customer Profile]-Datenspeicher gespeichert. Gelegentlich kann es erforderlich sein, einen Datensatz oder Batch aus dem [!DNL Profile]-Speicher zu löschen, um nicht mehr benötigte oder fehlerhaft hinzugefügte Daten zu entfernen. Dies erfordert die Verwendung der API zum Erstellen eines [!DNL Profile System Job], auch als &quot;[!DNL delete request]&quot;bezeichnet, das bei Bedarf geändert, überwacht oder gelöscht werden kann. Um zu erfahren, wie Sie Löschanfragen mithilfe des Endpunkts `/system/jobs` in der API [!DNL Real-time Customer Profile] verwenden, führen Sie die Schritte aus, die im Endpunkt [Profilsystemaufträge](profile-system-jobs.md) beschrieben sind.

## Nächste Schritte {#next-steps}

Um Aufrufe mit der [!DNL Real-time Customer Profile]-API zu tätigen, lesen Sie das [Erste Schritte-Handbuch](getting-started.md) und wählen Sie dann eine der Endpunkthandbücher aus, um zu erfahren, wie Sie bestimmte [!DNL Profile]-bezogene Endpunkte verwenden. Informationen zum Arbeiten mit [!DNL Profile]-Daten mithilfe der [!DNL Experience Platform]-Benutzeroberfläche finden Sie im [Benutzerhandbuch zum Echtzeit-Kundenprofil](../ui/user-guide.md).
