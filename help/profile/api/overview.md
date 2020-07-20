---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Entwicklerhandbuch für die Echtzeit-Kundenprofil-API
topic: guide
translation-type: tm+mt
source-git-commit: 57ef7df4b9323b58a90660d515ade61a3974779f
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 27%

---


# [!DNL Real-time Customer Profile] API-Entwicklerleitfaden

[!DNL Real-time Customer Profile] ermöglicht es Ihnen, eine ganzheitliche Ansicht jedes einzelnen Kunden innerhalb der Adobe Experience Platform zu sehen. [!DNL Profile] ermöglicht Ihnen die Konsolidierung unterschiedlicher Kundendaten aus mehreren Kanälen, z. B. Online-, Offline-, CRM- und Drittanbieterdaten, in einer einheitlichen Ansicht, die ein umsetzbares Zeitstempelkonto für jede Kundeninteraktion bietet.

Die [!DNL Real-time Customer Profile] API enthält mehrere Endpunkte, die nachfolgend beschrieben werden. Weitere Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie in den einzelnen Endpunkthandbüchern. Weitere Informationen finden Sie im Handbuch [Erste Schritte](getting-started.md) .

Informationen zur Ansicht aller verfügbaren Endpunkte und CRUD-Vorgänge finden Sie im [Echtzeit-Client-Profil-API-Referenzswagger](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

## (Alpha) Berechnete Attribute {#computed-attributes}

>[!IMPORTANT]
>
>Die Funktion für berechnete Attribute ist alphanumerisch und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalität können sich ändern.

Berechnete Attribute ermöglichen es, den Wert eines Feldes über andere Werte, Berechnungen und Ausdrücke automatisch zu ermitteln. Berechnete Attribute werden auf Profilebene ausgeführt, mit ihnen können also Werte über alle Datensätze und Ereignisse aggregiert werden. Dazu beinhaltet jedes berechnete Attribut einen Ausdruck bzw. eine „Regel“, nach der eingehende Daten ausgewertet werden und das Ergebnis in einem Profilattribut oder Ereignis festgehalten wird. Diese Berechnungen liefern Aufschluss über Metriken wie Kundenlebenszeitwert, Zeit zwischen Käufen oder der Anzahl der geöffneten Anwendungen, ohne dafür jedes Mal, wenn entsprechende Informationen benötigt werden, komplexe Berechnungen durchführen zu müssen. You can create, view, edit, and delete computed attributes using the `config/computedAttributes` endpoint. Informationen zur Verwendung dieses Endpunkts finden Sie im Handbuch [zum Endpunkt berechneter Attribute](computed-attributes.md).

## Edge-Projektionen {#edge-projections}

Die Adobe Experience Platform ermöglicht eine Personalisierung von Kundenerlebnissen in Echtzeit, indem sie Daten auf strategisch platzierten Servern („Edge“-Server genannt) leicht zugänglich macht. The [!DNL Real-time Customer Profile] API provides endpoints for working with edges through components called &quot;projections.&quot; Dazu gehören Projektionskonfigurationen, um zu ermitteln, welche Daten auf die einzelnen Edge-Server projiziert werden sollen, sowie Projektionsziele, um zu definieren, wohin eine Projektion geleitet werden soll. Detaillierte Informationen zum Arbeiten mit Kantenprojektionen finden Sie im Handbuch [Projektionskonfigurationen und Zielendpunkte](edge-projections.md).

## Entitäten ([!DNL Profile] Zugriff) {#entities}

Through Adobe Experience Platform you can access [!DNL Real-time Customer Profile] data using RESTful APIs or the user interface. To learn how to access entities, more commonly known as &quot;profiles&quot;, using the API, follow the steps outlined in the [entities endpoint guide](entities.md). Informationen zum Zugriff auf Profil über die [!DNL Platform] Benutzeroberfläche finden Sie im [Profil-Benutzerhandbuch](../ui/user-guide.md).

## Exportaufträge ([!DNL Profile] Export) {#profile-export}

[!DNL Real-time Customer Profile] Daten können zur weiteren Verarbeitung in einen Datensatz exportiert werden, z. B. zum Exportieren von Segmenten zur Audience für Aktivierungen oder Profil für Berichte. Exportaufträge für Segmentsegmente sind Teil der [!DNL Adobe Experience Platform Segmentation Service] API. Weitere Informationen finden Sie im Handbuch [Segmentierungsexportaufträge](../../profile/api/export-jobs.md) . Eine schrittweise Anleitung zum Erstellen und Verwalten von Exportaufträgen für Profil-Attribute finden Sie im Endpunkthandbuch [zu Exportaufträgen](export-jobs.md).

## Zusammenführungsrichtlinien {#merge-policies}

When bringing data from multiple sources together in [!DNL Experience Platform], merge policies are the rules that [!DNL Platform] uses to determine how data will be prioritized and what data will be combined to create individual customer profiles. Using the [!DNL Real-time Customer Profile] API, you can create new merge policies, manage existing policies, and set a default merge policy for your organization. To learn more about working with merge policies using the API, please visit the [merge policies endpoint guide](merge-policies.md).

For a guide to working with merge policies using the [!DNL Platform] UI, please see the [Merge Policies user guide](../ui/merge-policies.md).

## Profilsystemaufträge {#profile-system-jobs}

Daten, die in [!DNL Platform] aufgenommen werden, werden im [!DNL Data Lake] sowie im [!DNL Real-time Customer Profile] Datenspeicher gespeichert. Occasionally it may be necessary to delete a dataset or batch from the [!DNL Profile] store in order to remove data that you no longer require or that was added in error. This requires using the API to create a [!DNL Profile System Job], known as a &quot;[!DNL delete request]&quot;, that can also be, modified, monitored, or deleted if required. To learn how to work with delete requests using the `/system/jobs` endpoint in the [!DNL Real-time Customer Profile] API, follow the steps outlined in the [profile system jobs endpoint guide](profile-system-jobs.md).

## Nächste Schritte {#next-steps}

Um mit dem Aufrufen der [!DNL Real-time Customer Profile] API zu beginnen, lesen Sie die [Erste Schritte-Anleitung](getting-started.md) und wählen Sie dann eine der Endpunktanleitungen, um zu erfahren, wie Sie bestimmte [!DNL Profile]Endpunkte verwenden. To learn more about working with [!DNL Profile] data using the [!DNL Platform] UI, see the [Real-time Customer Profile user guide](../ui/user-guide.md).