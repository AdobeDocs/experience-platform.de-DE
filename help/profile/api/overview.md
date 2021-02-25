---
keywords: Experience Platform;Profil;Echtzeit-Profil des Kunden;Fehlerbehebung;API;Einheitliches Profil;Einheitliches Profil;Profil;RTCP;Profil aktivieren;Profil aktivieren
title: Handbuch zur Echtzeit-Client-Profil-API
topic: guide
description: Mit der Echtzeit-Client-Profil-API können Entwickler Profil-Daten, einschließlich Ansicht-Profilen, prüfen und bearbeiten, Zusammenführungsrichtlinien erstellen und aktualisieren, Profil- oder Musterdaten exportieren und löschen sowie Profil-Daten löschen, die nicht mehr benötigt werden oder fehlerhaft hinzugefügt wurden. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
translation-type: tm+mt
source-git-commit: 24a5af0440f58b4e1db639ec971c4e1611f107d8
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 13%

---


# [!DNL Real-time Customer Profile] API-Handbuch

[!DNL Real-time Customer Profile] ermöglicht es Ihnen, eine ganzheitliche Ansicht Ihrer einzelnen Kunden in Adobe Experience Platform zu sehen. [!DNL Profile] ermöglicht Ihnen die Konsolidierung unterschiedlicher Kundendaten aus mehreren Kanälen, z. B. Online-, Offline-, CRM- und Drittanbieterdaten, in einer einheitlichen Ansicht, die ein umsetzbares Zeitstempelkonto für jede Kundeninteraktion bietet.

Die [!DNL Real-time Customer Profile]-API enthält mehrere Endpunkte, wie nachfolgend beschrieben. Weitere Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie in den einzelnen Endpunkthandbüchern.[](getting-started.md)

Um alle verfügbaren Endpunkte und CRUD-Vorgänge Ansicht, besuchen Sie den [Referenz-Swagger ](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml) für das Profil in Echtzeit.

Eine Anleitung zum Arbeiten mit [!DNL Real-time Customer Profile]-Daten in der [!DNL Experience Platform]-Benutzeroberfläche finden Sie im [Profil-Benutzerhandbuch](../ui/user-guide.md).

## (Alpha) Berechnete Attribute {#computed-attributes}

>[!IMPORTANT]
>
>Die Funktion für berechnete Attribute ist alphanumerisch und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalität können sich ändern.

Berechnete Attribute sind Funktionen, mit denen Daten auf Ereignis-Ebene in Attribute auf Profil-Ebene Aggregat werden. Diese Funktionen werden automatisch berechnet, sodass sie für die Segmentierung, Aktivierung und Personalisierung verwendet werden können.

Jedes berechnete Attribut enthält einen Ausdruck, oder &quot;Regel&quot;, der eingehende Daten auswertet und den sich ergebenden Wert in einem Profil-Attribut speichert. Mit diesen Berechnungen können Sie Fragen im Zusammenhang mit dem Kaufwert über die gesamte Lebensdauer, der Zeit zwischen Käufen oder der Anzahl der Anwendungsöffnungen leicht beantworten, ohne für jede benötigte Information manuell komplexe Berechnungen ausführen zu müssen. Diese berechneten Attributwerte können dann in einem Profil angezeigt, zum Erstellen eines Segments verwendet oder über verschiedene Zugriffsmuster aufgerufen werden.

Sie können berechnete Attribute mit dem Endpunkt `config/computedAttributes` erstellen, Ansicht, bearbeiten und löschen. Informationen zur Verwendung berechneter Attribute finden Sie im Abschnitt [Übersicht über berechnete Attribute](../computed-attributes/overview.md). Für API-Vorgänge besuchen Sie das [Handbuch für die API-Endpunkte für berechnete Attribute](../computed-attributes/ca-api.md).

## Edge-Projektionen {#edge-projections}

Die Adobe Experience Platform ermöglicht eine Personalisierung von Kundenerlebnissen in Echtzeit, indem sie Daten auf strategisch platzierten Servern („Edge“-Server genannt) leicht zugänglich macht. Die [!DNL Real-time Customer Profile]-API stellt Endpunkte für die Arbeit mit Kanten über Komponenten bereit, die als &quot;Projektionen&quot;bezeichnet werden. Dazu gehören Projektionskonfigurationen, um zu ermitteln, welche Daten auf die einzelnen Edge-Server projiziert werden sollen, sowie Projektionsziele, um zu definieren, wohin eine Projektion geleitet werden soll. Ausführliche Informationen zum Arbeiten mit Kantenprojektionen finden Sie im Handbuch [Projektionskonfigurationen und Zielendpunkte](edge-projections.md).

## Entitäten ([!DNL Profile]-Zugriff) {#entities}

Über Adobe Experience Platform können Sie mit RESTful-APIs oder der Benutzeroberfläche auf [!DNL Real-time Customer Profile]-Daten zugreifen. Um zu erfahren, wie Sie mithilfe der API auf Entitäten zugreifen können, die allgemein als &quot;Profil&quot;bezeichnet werden, führen Sie die Schritte aus, die im [entity endpoint guide](entities.md) beschrieben werden. Informationen zum Zugriff auf Profil mit der [!DNL Platform]-Benutzeroberfläche finden Sie im [Profil-Benutzerhandbuch](../ui/user-guide.md).

## Exportaufträge ([!DNL Profile] export) {#profile-export}

[!DNL Real-time Customer Profile] Daten können zur weiteren Verarbeitung in einen Datensatz exportiert werden, z. B. zum Exportieren von Segmenten zur Audience für Aktivierungen oder Profil für Berichte. Exportaufträge für Segmentsegmente sind Teil der API. Lesen Sie hierzu bitte das [Handbuch [!DNL Adobe Experience Platform Segmentation Service] zu Exportaufträgen für Segmentierungen](../../profile/api/export-jobs.md), um mehr zu erfahren. Eine schrittweise Anleitung zum Erstellen und Verwalten von Exportaufträgen für Profil-Attribute finden Sie im [Endpunkt-Handbuch für Exportaufträge](export-jobs.md).

## Zusammenführungsrichtlinien {#merge-policies}

Beim Zusammenführen von Daten aus mehreren Quellen in [!DNL Experience Platform] sind Zusammenführungsrichtlinien die Regeln, mit denen [!DNL Platform] bestimmt wird, wie Daten priorisiert werden und welche Daten kombiniert werden, um individuelle Profil zu erstellen. Mit der API [!DNL Real-time Customer Profile] können Sie neue Zusammenführungsrichtlinien erstellen, vorhandene Richtlinien verwalten und eine standardmäßige Zusammenführungsrichtlinie für Ihr Unternehmen festlegen. Weitere Informationen zum Arbeiten mit Zusammenführungsrichtlinien mithilfe der API finden Sie im [Endpunktleitfaden ](merge-policies.md) für Zusammenführungsrichtlinien.

Eine Anleitung zum Arbeiten mit Zusammenführungsrichtlinien mithilfe der [!DNL Platform]-Benutzeroberfläche finden Sie im Benutzerhandbuch [Richtlinien zusammenführen](../ui/merge-policies.md).

## Musterstatus der Vorschau ([!DNL Profile] Vorschau) {#profile-preview}

Da für Profil aktivierte Daten in die Experience Platform aufgenommen werden, werden sie im Profil-Datenspeicher gespeichert. Wenn die Anzahl der Datensätze im Profil-Store zunimmt oder sinkt, wird ein Musterauftrag ausgeführt, der Informationen darüber enthält, wie viele Profil-Fragmente und zusammengeführte Profil sich im Datenspeicher befinden. Mithilfe der Profil-API können Sie das neueste erfolgreiche Beispiel sowie die Verteilung von Listen-Profilen nach Datensatz und Identitäts-Namensraum Vorschau werden. Informationen zum Einstieg in die Verwendung des Endpunkts `/profilepreviewstatus` finden Sie im Abschnitt [Vorschau sample status endpoint guide](preview-sample-status.md).

## Profilsystemaufträge {#profile-system-jobs}

Profil-aktivierte Daten, die in [!DNL Platform] eingeschlossen werden, werden im [!DNL Data Lake] sowie im [!DNL Real-time Customer Profile]-Datenspeicher gespeichert. Gelegentlich kann es erforderlich sein, einen Datensatz oder Stapel aus dem [!DNL Profile]-Speicher zu löschen, um Daten zu entfernen, die Sie nicht mehr benötigen oder die zu Fehlern hinzugefügt wurden. Dies erfordert die Verwendung der API zum Erstellen eines [!DNL Profile System Job], auch als &quot;[!DNL delete request]&quot;bezeichnet, das bei Bedarf geändert, überwacht oder gelöscht werden kann. Um zu erfahren, wie Sie mit dem `/system/jobs`-Endpunkt in der [!DNL Real-time Customer Profile]-API arbeiten, führen Sie die Schritte aus, die im [Profil-Endpunkt für Systemaufträge](profile-system-jobs.md) beschrieben werden.

## Nächste Schritte {#next-steps}

Um mit dem Aufrufen der API zu beginnen, lesen Sie das Handbuch [Erste Schritte](getting-started.md) und wählen Sie dann eine der Endpunktleitfäden aus, um zu erfahren, wie bestimmte [!DNL Profile]-bezogene Endpunkte verwendet werden. [!DNL Real-time Customer Profile] Informationen zum Arbeiten mit [!DNL Profile]-Daten mithilfe der [!DNL Experience Platform]-Benutzeroberfläche finden Sie im [Benutzerleitfaden für Kunden-Profil in Echtzeit](../ui/user-guide.md).