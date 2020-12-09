---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;unified profile;Unified Profile;unified;Profile;rtcp;XDM graphs
title: Übersicht über das Echtzeit-Kundenprofil
topic: guide
description: Das Echtzeit-Kundenprofil ist ein allgemeiner Suchentitäten-Speicher, in dem Informationen aus verschiedensten Datenquellen des Unternehmens zusammengeführt und zum Abruf verfügbar gemacht werden. Diese Daten werden in Form von individuellen Kundenprofilen sowie zugehörigen im Zeitverlauf erfassten, so genannten Zeitreihen-Ereignissen aufbereitet, die es Marketing-Experten ermöglichen, über verschiedenste Kanäle hinweg koordinierte, konsistente und relevante Erlebnisse für ihre Zielgruppen umzusetzen.
translation-type: tm+mt
source-git-commit: b8d6bd5caf6c6f4d1da218b6ca12cec154d64412
workflow-type: tm+mt
source-wordcount: '1844'
ht-degree: 42%

---


# [!DNL Real-time Customer Profile]Übersicht

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Kunden, unabhängig davon, wo und wann diese mit Ihrer Marke interagieren. With [!DNL Real-time Customer Profile], you can see a holistic view of each individual customer that combines data from multiple channels, including online, offline, CRM, and third party data. [!DNL Profile] ermöglicht es Ihnen, Ihre unterschiedlichen Kundendaten zu einer einheitlichen Ansicht zusammenzuführen, die Ihnen einen umsetzbaren Zeitstempel für jede Kundeninteraktion bietet. Diese Übersicht hilft Ihnen, die Rolle und Verwendung von [!DNL Real-time Customer Profile] in zu verstehen [!DNL Experience Platform].

## [!DNL Profile] in Experience Platform

Die nachfolgende Abbildung zeigt die Zusammenhänge zwischen dem Echtzeit-Kundenprofil und anderen Services in Experience Platform:

![Adobe Experience Platform-Dienste.](images/profile-overview/profile-in-platform.png)

### Profil-Datenspeicher

Although [!DNL Real-time Customer Profile] processes ingested data and uses Adobe Experience Platform [!DNL Identity Service] to merge related data through identity mapping, it maintains its own data in the [!DNL Profile] store. Der [!DNL Profile] Store ist von den [!DNL Catalog] Daten im Identitätsdiagramm [!DNL Data Lake] und den [!DNL Identity Service] Daten im Identitätsdiagramm getrennt.

Der Profil-Store verwendet eine Microsoft Azurblase Cosmos DB-Infrastruktur und der Platform Data Lake verwendet Microsoft Azurblase Data Lake Datenspeicherung.

### Profil-Guardraht

Experience Platform bietet eine Reihe von Garantieleistungen, mit denen Sie vermeiden können, [Experience Data Model-(XDM-)Schema](../xdm/home.md) zu erstellen, die vom Echtzeit-Customer-Profil nicht unterstützt werden können. Dies umfasst weiche Beschränkungen, die zu Leistungsbeeinträchtigungen führen, sowie harte Beschränkungen, die zu Fehlern und Systembrüchen führen. Weitere Informationen, einschließlich einer Liste von Richtlinien und Beispielanwendungsfällen, finden Sie in der [Profil Guardrails](guardrails.md) Dokumentation.

## Profile verstehen

[!DNL Real-time Customer Profile] führt Daten aus verschiedenen Unternehmenssystemen zusammen und ermöglicht dann den Zugriff auf diese Daten in Form von Profilen mit zugehörigen Zeitreihen-Ereignissen. die es Marketing-Experten ermöglichen, über verschiedenste Kanäle hinweg koordinierte, konsistente und relevante Erlebnisse für ihre Zielgruppen umzusetzen. In den folgenden Abschnitten werden einige der Kernkonzepte hervorgehoben, die Sie verstehen müssen, um Profile innerhalb der Plattform effektiv zu erstellen und zu verwalten.

### Fragmente im Profil im Vergleich zu zusammengeführten Profilen {#profile-fragments-vs-merged-profiles}

Jedes einzelne Profil besteht aus mehreren Profil-Fragmenten, die zu einer einzigen Ansicht des Kunden zusammengeführt wurden. Wenn ein Kunde beispielsweise über mehrere Kanal mit Ihrer Marke interagiert, enthält Ihr Unternehmen mehrere Profil-Fragmente, die sich auf diesen einzelnen Kunden beziehen und in mehreren Datensätzen angezeigt werden. Wenn diese Fragmente in eine Plattform integriert werden, werden sie zusammengeführt, um ein einzelnes Profil für diesen Kunden zu erstellen.

Wenn die Daten aus mehreren Quellen in Konflikt geraten (z. B. ein Fragment als &quot;Einzel&quot;, während die anderen Listen den Kunden als &quot;verheiratet&quot;Liste haben), bestimmt die [Zusammenführungsrichtlinie](#merge-policies) , welche Informationen priorisiert und in das Profil aufgenommen werden sollen. Daher ist die Gesamtanzahl der Fragmente innerhalb der Plattform wahrscheinlich höher als die Gesamtanzahl der zusammengeführten Profile, da jedes Profil aus mehreren Fragmenten besteht.

### Daten aufzeichnen

Ein Profil ist eine Darstellung eines Subjekts, einer Organisation oder einer Einzelperson, die aus vielen Attributen besteht (auch als Datensatzdaten bezeichnet). So kann etwa ein Produktprofil eine SKU und eine Beschreibung enthalten, während in einem Personenprofil Informationen wie Vorname, Nachname und E-Mail-Adresse erfasst sind. Using [!DNL Experience Platform], you can customize profiles to use specific data relevant to your business. The standard [!DNL Experience Data Model] (XDM) class, [!DNL XDM Individual Profile], is the preferred class upon which to build a schema when describing customer record data, and supplies the data integral to many interactions between Platform services. For more information on working with schemas in [!DNL Experience Platform], please begin by reading the [XDM System overview](../xdm/home.md).

### Zeitreihen-Ereignisse

Zeitreihendaten liefern eine Momentaufnahme des Systems zu dem Zeitpunkt, an dem ein Subjekt direkt oder indirekt eine Aktion ausgeführt hat, sowie Daten mit Details zu dem Ereignis selbst. Zeitreihendaten werden im Schema anhand der Standardklasse XDM ExperienceEvent dargestellt. Sie beschreiben Ereignisse wie etwa das Hinzufügen eines Artikels zu einem Warenkorb, das Klicken auf einen Link, das Abspielen eines Videos usw. Auf Grundlage von Zeitreihendaten können Segmentierungsregeln eingerichtet werden. Die einzelnen Ereignisse sind dabei im Kontext eines Profils abrufbar.

### Identitäten

Bei der Kommunikation mit Kunden gilt es, diese in einer auf sie persönlich abgestimmte Weise anzusprechen. Die Umsetzung solcher für Kunden relevanter digitaler Erlebnisse ist jedoch eine Herausforderung. Denn dazu muss nachvollzogen werden, wie die verschiedenen Daten, die sie auf voneinander getrennten digitalen Kanälen wie Tablets, Smartphones und Laptops generieren, zueinander in Zusammenhang stehen. [!DNL Identity Service] ermöglicht es Ihnen, das Gesamtbild Ihres Kunden zusammenzustellen, indem Sie Identitäten aus mehreren Kanälen verknüpfen und ein Identitätsdiagramm für jeden Kunden erstellen. Weitere Informationen finden Sie in der [Identity Service – Übersicht](../identity-service/home.md).

### Zusammenführungsrichtlinien

When bringing data fragments together from multiple sources and combining them in order to see a complete view of each of your individual customers, merge policies are the rules that [!DNL Platform] uses to determine how data will be prioritized and what data will be used to create the customer profile. Wenn Daten aus mehreren Datensätzen miteinander in Konflikt stehen, bestimmt die Richtlinie zum Zusammenführen, wie diese Daten behandelt werden und welcher Wert verwendet werden soll. Über die RESTful APIs oder die Benutzeroberfläche können Sie neue Zusammenführungsrichtlinien erstellen, vorhandene Richtlinien verwalten und eine standardmäßige Zusammenführungsrichtlinie für Ihr Unternehmen einrichten. Weitere Informationen zum Arbeiten mit Zusammenführungsrichtlinien mithilfe der [!DNL Real-time Customer Profile] API finden Sie im Handbuch [Zusammenführungsrichtlinien](api/merge-policies.md). To work with merge policies using the [!DNL Experience Platform] UI, refer to the [merge policies user guide](ui/merge-policies.md).

### Vereinigung Schema {#profile-fragments-and-union-schemas}

One of the key features of [!DNL Real-time Customer Profile] is the ability to unify multi-channel data. When [!DNL Real-time Customer Profile] is used to access an entity, it can supply you with a merged view of all profile fragments for that entity across datasets, referred to as the union view and made possible through what is known as a union schema. [!DNL Real-time Customer Profile] Daten werden über mehrere Quellen hinweg zusammengeführt, wenn auf eine Entität oder ein Profil mit ihrer ID zugegriffen oder als Segment exportiert wird. Weitere Informationen zum Zugriff auf Profil und Vereinigungen-Ansichten mithilfe der [!DNL Real-time Customer Profile] API finden Sie im [Entitäts-Endpunkthandbuch](api/entities.md).

### Segmentierung

Adobe Experience Platform [!DNL Segmentation Service] produces the audiences needed to power experiences for your individual customers. Wird ein solches Zielgruppensegment erstellt, wird dessen Segment-ID zur Liste der Segmentmitglieder für alle qualifizierten Profile hinzugefügt. Segment rules are built and applied to [!DNL Real-time Customer Profile] data using RESTful APIs and the Segment Builder user interface. Um mehr über die Segmentierung zu erfahren, lesen Sie zunächst die [Segmentation Service – Übersicht](../segmentation/home.md).

### (Alpha) Konfigurieren von berechneten Attributen

>[!IMPORTANT]
>
>Die Funktion für berechnete Attribute ist alphanumerisch. Dokumentation und Funktionalität können sich ändern.

Mit berechneten Attributen können Sie den Wert von Feldern anhand anderer Werte, Berechnungen und Ausdrücke automatisch berechnen. Berechnete Attribute agieren auf der Profilebene, d. h., Sie können Werte über alle Datensätze und Ereignisse hinweg aggregieren. Jedes berechnete Attribut enthält einen Ausdruck oder eine „Regel“, der bzw. die eingehende Daten auswertet und den resultierenden Wert in einem Profilattribut oder Ereignis speichert. Mit diesen Berechnungen können Sie Fragen im Zusammenhang mit dem Kaufwert über die gesamte Lebensdauer, der Zeit zwischen Käufen oder der Anzahl der Anwendungsöffnungen leicht beantworten, ohne für jede benötigte Information manuell komplexe Berechnungen ausführen zu müssen. Weitere Informationen zu berechneten Attributen und eine schrittweise Anleitung zum Arbeiten mit diesen Attributen mithilfe der [!DNL Real-time Customer Profile] API finden Sie in der Anleitung zum Endpunkt [berechneter Attribute](api/computed-attributes.md). Dieses Handbuch hilft Ihnen, die Rolle von berechneten Attributen in Adobe Experience Platform besser zu verstehen. Es enthält Beispiel-API-Aufrufe zur Durchführung grundlegender CRUD-Vorgänge.

## Echtzeitkomponenten

This section introduces the components that allow [!DNL Real-time Customer Profile] to update and monitor record and time series data in real-time.

### Streaming-Erfassung und Streaming-Segmentierung

Der Prozess, Daten in Echtzeit zu erfassen, wird als Streaming-Erfassung bezeichnet. As profile and time series data is ingested, [!DNL Real-time Customer Profile] automatically decides to include or exclude that data from segments through an ongoing process called streaming segmentation, before merging it with existing data and updating the union view. Das Ergebnis: Berechnungen und Entscheidungen dazu, wie Sie Ihren Kunden herausragende, individuell auf sie abgestimmte Erlebnisse liefern, lassen sich direkt während ihrer Interaktion mit Ihrer Marke anstellen bzw. treffen. Im Verlauf der Datenaufnahme wird außerdem validiert, ob die Daten ordnungsgemäß erfasst werden und dem Schema entsprechen, auf dem der Datensatz basiert. Weitere Informationen dazu, welche Validierungen bei der Datenaufnahme vorgenommen werden, finden Sie in der Übersicht über die Datenaufnahme unter [Datenqualität](../ingestion/quality/overview.md).

### Edge-Projektionskonfigurationen und -ziele

Um koordinierte, konsistente und personalisierte Erlebnisse für Ihre Kunden über mehrere Kanäle hinweg in Echtzeit umsetzen zu können, müssen die richtigen Daten jederzeit verfügbar sein und bei Änderungen kontinuierlich aktualisiert werden. Adobe Experience Platform ermöglicht diesen Echtzeitzugriff auf Daten mithilfe sogenannter Edges. Ein Edge ist ein regional aufgestellter Server, der Daten erfasst und direkt für Anwendungen abrufbar macht. Adobe-Anwendungen wie etwa Adobe Target und Adobe Campaign nutzen Edges, um personalisierte Kundenerlebnisse in Echtzeit bereitzustellen. Die Daten werden mittels Projektion an einen Edge übermittelt, wobei ein Projektionsziel den Edge definiert, an den die Daten gesendet werden, und eine Projektionskonfiguration, die die Informationen spezifiziert, die am Edge zur Verfügung gestellt werden. Weitere Informationen und die Arbeit mit Projektionen mithilfe der [!DNL Real-time Customer Profile] API finden Sie im Handbuch [Edge-Projektions-Endpunkte](api/edge-projections.md).

## Ingest data into [!DNL Profile]

[!DNL Platform] kann so konfiguriert werden, dass Daten aus Datensatz- und Zeitreihen an gesendet werden, [!DNL Profile]wodurch Echtzeit-Streaming und Stapelverarbeitung unterstützt werden. Weitere Informationen dazu, wie Sie dem Echtzeit-Kundenprofil Daten hinzufügen, finden Sie in [diesem Tutorial](tutorials/add-profile-data.md).

>[!NOTE]
>
>Daten, die über Adoben gesammelt werden, einschließlich [!DNL Analytics Cloud], [!DNL Marketing Cloud]und [!DNL Advertising Cloud], fließen in [!DNL Experience Platform] und werden in [!DNL Profile]erfasst.

### [!DNL Profile] Erfassungsmetriken

Observability Insights ermöglicht die Ermittlung von Schlüsselmetriken in Adobe Experience Platform. In addition to [!DNL Platform] usage statistics and performance indicators for various [!DNL Platform] functionalities, there are specific [!DNL Profile]-related metrics that allow you to gain insight into incoming request rates, successful ingestion rates, ingested record sizes, and more. To learn more, begin by reading the [Observability Insights API overview](../observability/api/overview.md), and for a complete list of [!DNL Profile] metrics, see the documentation on [available metrics](../observability/api/metrics.md#available-metrics).

## [!DNL Data governance] und [!DNL Privacy]

[!DNL Data governance] umfasst eine Reihe von Strategien und Technologien, mittels derer Kundendaten so verwaltet werden können, dass die Einhaltung gesetzlicher Bestimmungen, Einschränkungen und Richtlinien zu ihrer Nutzung gewährleistet bleibt.

As it relates to accessing data, data governance plays a key role within [!DNL Experience Platform] at various levels:
* Datennutzungsbeschriftungen
* Datenzugriffsrichtlinien
* Kontrollmechanismen für den Datenzugriff für Marketing-Aktivitäten

[!DNL Data governance] an mehreren Stellen verwaltet wird. These include deciding what data is ingested into [!DNL Platform] and what data is accessible after ingestion for a given marketing action. Gehen Sie für weitere Informationen hierzu zunächst die [Übersicht über Data Governance](../data-governance/home.md) durch.

### Umgang mit Opt-out- und Datenschutzanfragen

[!DNL Experience Platform] ermöglicht es Ihren Kunden, Abmeldeanfragen im Zusammenhang mit der Nutzung und Datenspeicherung ihrer Daten innerhalb von [!DNL Real-time Customer Profile]zu senden. Weitere Informationen hierzu finden Sie in der Dokumentation zum Thema [Berücksichtigen von Opt-out-Anfragen](../segmentation/honoring-opt-outs.md).

## Nächste Schritte und zusätzliche Ressourcen

Weitere Informationen zum Arbeiten mit [!DNL Real-time Customer Profile]dem [Profil-UI-Handbuch](ui/user-guide.md) oder [API-Entwicklerhandbuch](api/overview.md).

>[!WARNING]
>
>Die Benutzeroberfläche der Experience Platform wird häufig aktualisiert und kann sich seit der Aufzeichnung des Videos geändert haben. Die neuesten Screenshots und Funktionen der Benutzeroberfläche finden Sie im Benutzerhandbuch [zum](ui/user-guide.md) Echtzeit-Profil.

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12)