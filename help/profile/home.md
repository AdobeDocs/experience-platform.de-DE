---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;unified profile;Unified Profile;unified;Profile;rtcp;XDM graphs
solution: Adobe Experience Platform
title: Übersicht über das Echtzeit-Kundenprofil
topic: guide
description: Das Echtzeit-Kundenprofil ist ein allgemeiner Suchentitäten-Speicher, in dem Informationen aus verschiedensten Datenquellen des Unternehmens zusammengeführt und zum Abruf verfügbar gemacht werden. Diese Daten werden in Form von individuellen Kundenprofilen sowie zugehörigen im Zeitverlauf erfassten, so genannten Zeitreihen-Ereignissen aufbereitet, die es Marketing-Experten ermöglichen, über verschiedenste Kanäle hinweg koordinierte, konsistente und relevante Erlebnisse für ihre Zielgruppen umzusetzen.
translation-type: tm+mt
source-git-commit: 5dd07bf9afe96be3a4c3f4a4d4e3b23aef4fde70
workflow-type: tm+mt
source-wordcount: '1649'
ht-degree: 51%

---


# [!DNL Real-time Customer Profile]Übersicht

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Kunden, unabhängig davon, wo und wann diese mit Ihrer Marke interagieren. With [!DNL Real-time Customer Profile], you can see a holistic view of each individual customer that combines data from multiple channels, including online, offline, CRM, and third party data. [!DNL Profile] ermöglicht es Ihnen, Ihre unterschiedlichen Kundendaten zu einer einheitlichen Ansicht zusammenzuführen, die Ihnen einen umsetzbaren Zeitstempel für jede Kundeninteraktion bietet. Diese Übersicht hilft Ihnen, die Rolle und Verwendung von [!DNL Real-time Customer Profile] in zu verstehen [!DNL Experience Platform].


## [!DNL Profile] in Experience Platform

Die nachfolgende Abbildung zeigt die Zusammenhänge zwischen dem Echtzeit-Kundenprofil und anderen Services in Experience Platform:

![Adobe Experience Platform-Dienste.](images/profile-overview/profile-in-platform.png)

## Profildaten

[!DNL Real-time Customer Profile] ist ein generischer Lookup-Entitätsspeicher, der Daten aus verschiedenen Unternehmensdaten zusammenführt und dann Zugriff auf diese Daten in Form von individuellen Profilen und zugehörigen Zeitreihen-Ereignissen bietet. die es Marketing-Experten ermöglichen, über verschiedenste Kanäle hinweg koordinierte, konsistente und relevante Erlebnisse für ihre Zielgruppen umzusetzen.

### Profil-Guardraht

Experience Platform bietet eine Reihe von Garantieleistungen, mit denen Sie vermeiden können, [Experience Data Model-(XDM-)Schema](../xdm/home.md) zu erstellen, die vom Echtzeit-Customer-Profil nicht unterstützt werden können. Dies umfasst weiche Beschränkungen, die zu Leistungsbeeinträchtigungen führen, sowie harte Beschränkungen, die zu Fehlern und Systembrüchen führen. Weitere Informationen, einschließlich einer Liste von Richtlinien und Beispielanwendungsfällen, finden Sie in der [Profil Guardrails](guardrails.md) Dokumentation.

### Profil Store

Although [!DNL Real-time Customer Profile] processes ingested data and uses Adobe Experience Platform [!DNL Identity Service] to merge related data through identity mapping, it maintains its own data in the [!DNL Profile] store. In other words, the [!DNL Profile] store is separate from [!DNL Catalog] data ([!DNL Data Lake]) and [!DNL Identity Service] data (identity graph).

### Daten aufzeichnen

Ein Profil ist eine auf sogenannten Datensatzdaten basierende Darstellung eines Subjekts, einer Organisation oder einer Einzelperson. So kann etwa ein Produktprofil eine SKU und eine Beschreibung enthalten, während in einem Personenprofil Informationen wie Vorname, Nachname und E-Mail-Adresse erfasst sind. Using [!DNL Experience Platform], you can customize profiles to use types of data relevant to your business. The standard [!DNL Experience Data Model] (XDM) [!DNL Individual Profile] class is the preferred class upon which to build a schema when describing customer record data, and supplies the data integral to many interactions between Platform services. For more information on working with schemas in [!DNL Experience Platform], please begin by reading the [XDM System overview](../xdm/home.md).

### Zeitreihen-Ereignisse

Zeitreihendaten liefern eine Momentaufnahme des Systems zu dem Zeitpunkt, an dem ein Subjekt direkt oder indirekt eine Aktion ausgeführt hat, sowie Daten mit Details zu dem Ereignis selbst. Zeitreihendaten werden im Schema anhand der Standardklasse XDM ExperienceEvent dargestellt. Sie beschreiben Ereignisse wie etwa das Hinzufügen eines Artikels zu einem Warenkorb, das Klicken auf einen Link, das Abspielen eines Videos usw. Auf Grundlage von Zeitreihendaten können Segmentierungsregeln eingerichtet werden. Die einzelnen Ereignisse sind dabei im Kontext eines Profils abrufbar.

### Identitäten

Bei der Kommunikation mit Kunden gilt es, diese in einer auf sie persönlich abgestimmte Weise anzusprechen. Die Umsetzung solcher für Kunden relevanter digitaler Erlebnisse ist jedoch eine Herausforderung. Denn dazu muss nachvollzogen werden, wie die verschiedenen Daten, die sie auf voneinander getrennten digitalen Kanälen wie Tablets, Smartphones und Laptops generieren, zueinander in Zusammenhang stehen. [!DNL Identity Service] liefert Ihnen ein vollständiges Bild Ihrer Kunden. Denn dieser führt die Identitäten aus verschiedenen Kanälen in einem für jeden Kunden individuellen Identitätsdiagramm zusammen, über das Sie ein klareres Verständnis jedes Einzelnen gewinnen. Weitere Informationen finden Sie in der [Identity Service – Übersicht](../identity-service/home.md).

### Segmentierung

Adobe Experience Platform [!DNL Segmentation Service] produces the audiences needed to power experiences for your individual customers. Wird ein solches Zielgruppensegment erstellt, wird dessen Segment-ID zur Liste der Segmentmitglieder für alle qualifizierten Profile hinzugefügt. Segment rules are built and applied to [!DNL Real-time Customer Profile] data using RESTful APIs and the Segment Builder user interface. Um mehr über die Segmentierung zu erfahren, lesen Sie zunächst die [Segmentation Service – Übersicht](../segmentation/home.md).

### Profilfragmente und Vereinigungsschemas {#profile-fragments-and-union-schemas}

One of the key features of [!DNL Real-time Customer Profile] is the ability to unify multi-channel data. When [!DNL Real-time Customer Profile] is used to access an entity, it can supply you with a merged view of all profile fragments for that entity across datasets, referred to as the union view and made possible through what is known as a union schema. [!DNL Real-time Customer Profile] Daten werden über mehrere Quellen hinweg zusammengeführt, wenn auf eine Entität oder ein Profil mit ihrer ID zugegriffen oder als Segment exportiert wird. Weitere Informationen zum Zugriff auf Profil und Vereinigungen-Ansichten mithilfe der [!DNL Real-time Customer Profile] API finden Sie im [Entitäts-Endpunkthandbuch](api/entities.md).

### Zusammenführungsrichtlinien

When bringing data together from multiple sources and combining it in order to see a complete view of each of your individual customers, merge policies are the rules that [!DNL Platform] uses to determine how data will be prioritized and what data will be combined to create that unified view. Über die RESTful APIs oder die Benutzeroberfläche können Sie neue Zusammenführungsrichtlinien erstellen, vorhandene Richtlinien verwalten und eine standardmäßige Zusammenführungsrichtlinie für Ihr Unternehmen einrichten. Weitere Informationen zum Arbeiten mit Zusammenführungsrichtlinien mithilfe der [!DNL Real-time Customer Profile] API finden Sie im Handbuch [Zusammenführungsrichtlinien](api/merge-policies.md). To work with merge policies using the [!DNL Experience Platform] UI, refer to the [merge policies user guide](ui/merge-policies.md).

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

[!DNL Platform] kann so konfiguriert werden, dass Ihre Daten zu Datensatz und Zeitreihen an gesendet werden. Dies unterstützt die Echtzeit-Streaming-Erfassung und Batch-Erfassung. [!DNL Profile] Weitere Informationen dazu, wie Sie dem Echtzeit-Kundenprofil Daten hinzufügen, finden Sie in [diesem Tutorial](tutorials/add-profile-data.md).

>[!NOTE]
>
>Daten, die über Adoben gesammelt werden, einschließlich [!DNL Analytics Cloud], [!DNL Marketing Cloud]und [!DNL Advertising Cloud], fließen in [!DNL Experience Platform] und werden in [!DNL Profile]erfasst.

### [!DNL Profile] Erfassungsmetriken

Observability Insights ermöglicht die Ermittlung von Schlüsselmetriken in Adobe Experience Platform. In addition to [!DNL Platform] usage statistics and performance indicators for various [!DNL Platform] functionalities, there are specific [!DNL Profile]-related metrics that allow you to gain insight into incoming request rates, successful ingestion rates, ingested record sizes, and more. To learn more, begin by reading the [Observability Insights overview](../observability/home.md), and for a complete list of [!DNL Profile] metrics, see the documentation on [available metrics](../observability/metrics.md).

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

To learn more about [!DNL Real-time Customer Profile], please continue reading the documentation and supplement your learning by watching the video below or exploring other [Experience Platform video tutorials](https://docs.adobe.com/content/help/en/platform-learn/tutorials/overview.html).

>[!WARNING]
>
>Die im folgenden Video dargestellte [!DNL Platform] Benutzeroberfläche ist veraltet. Die neuesten Screenshots und Funktionen der Benutzeroberfläche finden Sie im Benutzerhandbuch [zum](ui/user-guide.md) Echtzeit-Profil.

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12)