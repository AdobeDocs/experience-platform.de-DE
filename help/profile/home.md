---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Übersicht über das Echtzeit-Kundenprofil
topic: guide
translation-type: tm+mt
source-git-commit: f910351d49de9c4a18a444b99b7f102f4ce3ed5b
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 46%

---


# [!DNL Real-time Customer Profile]Übersicht

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Kunden, unabhängig davon, wo und wann diese mit Ihrer Marke interagieren. With [!DNL Real-time Customer Profile], you can see a holistic view of each individual customer that combines data from multiple channels, including online, offline, CRM, and third party data. [!DNL Profile] ermöglicht es Ihnen, Ihre unterschiedlichen Kundendaten zu einer einheitlichen Ansicht zusammenzuführen, die Ihnen einen umsetzbaren Zeitstempel für jede Kundeninteraktion bietet. Diese Übersicht hilft Ihnen, die Rolle und Verwendung von [!DNL Real-time Customer Profile] in zu verstehen [!DNL Experience Platform].

## Erläuterungen [!DNL Real-time Customer Profile]

[!DNL Real-time Customer Profile] ist ein generischer Lookup-Entitätsspeicher, der Daten aus verschiedenen Unternehmensdaten zusammenführt und dann Zugriff auf diese Daten in Form von individuellen Profilen und zugehörigen Zeitreihen-Ereignissen bietet. die es Marketing-Experten ermöglichen, über verschiedenste Kanäle hinweg koordinierte, konsistente und relevante Erlebnisse für ihre Zielgruppen umzusetzen.

### [!DNL Profile] Datenspeicher

Although [!DNL Real-time Customer Profile] processes ingested data and uses Adobe Experience Platform [!DNL Identity Service] to merge related data through identity mapping, it maintains its own data in the [!DNL Profile] store. Das heißt, der [!DNL Profile] Speicher ist getrennt von [!DNL Catalog] Daten ([!DNL Data Lake]) und [!DNL Identity Service] Daten (Identitätsdiagramm).

### [!DNL Profile] und [!DNL Platform] Dienstleistungen

The relationship between [!DNL Real-time Customer Profile] and other services within [!DNL Experience Platform] is highlighted in the following diagram:

![Zusammenhänge zwischen dem Profil und anderen Experience Platform-Services.](images/profile-overview/profile-in-platform.png)

### Profile und Datensatzdaten

Ein Profil ist eine auf sogenannten Datensatzdaten basierende Darstellung eines Subjekts, einer Organisation oder einer Einzelperson. So kann etwa ein Produktprofil eine SKU und eine Beschreibung enthalten, während in einem Personenprofil Informationen wie Vorname, Nachname und E-Mail-Adresse erfasst sind. Using [!DNL Experience Platform], you can customize profiles to use types of data relevant to your business. The standard [!DNL Experience Data Model] (XDM) [!DNL Individual Profile] class is the preferred class upon which to build a schema when describing customer record data, and supplies the data integral to many interactions between Platform services. For more information on working with schemas in [!DNL Experience Platform], please begin by reading the [XDM System overview](../xdm/home.md).

### Zeitreihen-Ereignisse

Zeitreihendaten liefern eine Momentaufnahme des Systems zu dem Zeitpunkt, an dem ein Subjekt direkt oder indirekt eine Aktion ausgeführt hat, sowie Daten mit Details zu dem Ereignis selbst. Zeitreihendaten werden im Schema anhand der Standardklasse XDM ExperienceEvent dargestellt. Sie beschreiben Ereignisse wie etwa das Hinzufügen eines Artikels zu einem Warenkorb, das Klicken auf einen Link, das Abspielen eines Videos usw. Auf Grundlage von Zeitreihendaten können Segmentierungsregeln eingerichtet werden. Die einzelnen Ereignisse sind dabei im Kontext eines Profils abrufbar.

### Identitäten

Bei der Kommunikation mit Kunden gilt es, diese in einer auf sie persönlich abgestimmte Weise anzusprechen. Die Umsetzung solcher für Kunden relevanter digitaler Erlebnisse ist jedoch eine Herausforderung. Denn dazu muss nachvollzogen werden, wie die verschiedenen Daten, die sie auf voneinander getrennten digitalen Kanälen wie Tablets, Smartphones und Laptops generieren, zueinander in Zusammenhang stehen. [!DNL Identity Service] ermöglicht es Ihnen, das Gesamtbild Ihres Kunden zusammenzustellen, indem Sie Identitäten aus mehreren Kanälen verknüpfen und ein Identitätsdiagramm für jeden Kunden erstellen, das Ihnen ein besseres Verständnis ermöglicht. Weitere Informationen finden Sie in der [Übersicht über den Identitätsdienst](../identity-service/home.md).

### Segmentierung

Adobe Experience Platform [!DNL Segmentation Service] produces the audiences needed to power experiences for your individual customers. Wird ein solches Zielgruppensegment erstellt, wird dessen Segment-ID zur Liste der Segmentmitglieder für alle qualifizierten Profile hinzugefügt. Segment rules are built and applied to [!DNL Real-time Customer Profile] data using RESTful APIs and the Segment Builder user interface. Gehen Sie zum Einstieg in die Segmentierung zunächst die [Übersicht über den Segmentierungsdienst](../segmentation/home.md) durch.

### Profilfragmente und Vereinigungsschemas {#profile-fragments-and-union-schemas}

One of the key features of [!DNL Real-time Customer Profile] is the ability to unify multi-channel data. When [!DNL Real-time Customer Profile] is used to access an entity, it can supply you with a merged view of all profile fragments for that entity across datasets, referred to as the union view and made possible through what is known as a union schema. [!DNL Real-time Customer Profile] Daten werden über mehrere Quellen hinweg zusammengeführt, wenn auf eine Entität oder ein Profil mit ihrer ID zugegriffen oder als Segment exportiert wird. Weitere Informationen zum Zugriff auf Profil und Vereinigungen-Ansichten mithilfe der [!DNL Real-time Customer Profile] API finden Sie im [Entitäts-Endpunkthandbuch](api/entities.md).

### Zusammenführungsrichtlinien

When bringing data together from multiple sources and combining it in order to see a complete view of each of your individual customers, merge policies are the rules that [!DNL Platform] uses to determine how data will be prioritized and what data will be combined to create that unified view. Mithilfe von RESTful-APIs oder der Benutzeroberfläche können Sie neue Zusammenführungsrichtlinien erstellen, bestehende Richtlinien verwalten und eine für Ihr Unternehmen als Standard verwendete Zusammenführungsrichtlinie einrichten. Weitere Informationen zum Arbeiten mit Zusammenführungsrichtlinien mithilfe der [!DNL Real-time Customer Profile] API finden Sie im Handbuch [Zusammenführungsrichtlinien](api/merge-policies.md). To work with merge policies using the [!DNL Experience Platform] UI, refer to the [merge policies user guide](ui/merge-policies.md).

### (Alpha) Konfigurieren von berechneten Attributen

>[!IMPORTANT]
>Die nachfolgend beschriebene Funktion für berechnete Attribute befindet sich in der Alpha-Phase. Dokumentation und Funktionalität können sich ändern.

Berechnete Attribute ermöglichen es, den Wert eines Feldes über andere Werte, Berechnungen und Ausdrücke automatisch zu ermitteln. Berechnete Attribute werden auf Profilebene ausgeführt, mit ihnen können also Werte über alle Datensätze und Ereignisse aggregiert werden. Dazu beinhaltet jedes berechnete Attribut einen Ausdruck bzw. eine „Regel“, nach der eingehende Daten ausgewertet werden und das Ergebnis in einem Profilattribut oder Ereignis festgehalten wird. Diese Berechnungen liefern Aufschluss über Metriken wie Kundenlebenszeitwert, Zeit zwischen Käufen oder der Anzahl der geöffneten Anwendungen, ohne dafür jedes Mal, wenn entsprechende Informationen benötigt werden, komplexe Berechnungen durchführen zu müssen. Weitere Informationen zu berechneten Attributen und eine schrittweise Anleitung zum Arbeiten mit diesen Attributen mithilfe der [!DNL Real-time Customer Profile] API finden Sie in der Anleitung zum Endpunkt [berechneter Attribute](api/computed-attributes.md). Dieses Handbuch hilft Ihnen, die Rolle, die berechnete Attribute innerhalb der Adobe Experience Platform spielen, besser zu verstehen. Es enthält Beispiel-API-Aufrufe zur Durchführung grundlegender CRUD-Vorgänge.

## Echtzeitkomponenten

This section introduces the components that allow [!DNL Real-time Customer Profile] to update and monitor record and time series data in real-time.

### Streaming-Aufnahme und Streaming-Segmentierung

Der Prozess, Daten in Echtzeit zu erfassen, wird als Streaming-Aufnahme bezeichnet. As profile and time series data is ingested, [!DNL Real-time Customer Profile] automatically decides to include or exclude that data from segments through an ongoing process called streaming segmentation, before merging it with existing data and updating the union view. Das Ergebnis: Berechnungen und Entscheidungen dazu, wie Sie Ihren Kunden herausragende, individuell auf sie abgestimmte Erlebnisse liefern, lassen sich direkt während ihrer Interaktion mit Ihrer Marke anstellen bzw. treffen. Im Verlauf der Datenaufnahme wird außerdem validiert, ob die Daten ordnungsgemäß erfasst werden und dem Schema entsprechen, auf dem der Datensatz basiert. Weitere Informationen dazu, welche Validierungen bei der Datenaufnahme vorgenommen werden, finden Sie in der Übersicht über die Datenaufnahme unter [Datenqualität](../ingestion/quality/overview.md).

### Edge-Projektionskonfigurationen und -ziele

Um koordinierte, konsistente und personalisierte Erlebnisse für Ihre Kunden über mehrere Kanal hinweg in Echtzeit umsetzen zu können, müssen die passenden Daten jederzeit verfügbar sein und im Zuge von Veränderungen laufend aktualisiert werden. Adobe Experience Platform ermöglicht diesen Echtzeitzugriff auf Daten mithilfe sogenannter Edges. Ein Edge ist ein regional aufgestellter Server, der Daten erfasst und direkt für Anwendungen abrufbar macht. Adobe-Anwendungen wie etwa Adobe Target und Adobe Campaign nutzen Edges, um personalisierte Kundenerlebnisse in Echtzeit bereitzustellen. Die Daten werden mittels Projektion an einen Edge übermittelt, wobei ein Projektionsziel den Edge definiert, an den die Daten gesendet werden, und eine Projektionskonfiguration, die die Informationen spezifiziert, die am Edge zur Verfügung gestellt werden. Weitere Informationen und die Arbeit mit Projektionen mithilfe der [!DNL Real-time Customer Profile] API finden Sie im Handbuch [Edge-Projektions-Endpunkte](api/edge-projections.md).

## Daten Hinzufügen [!DNL Real-time Customer Profile]

[!DNL Platform] kann so konfiguriert werden, dass Ihre Daten zu Datensatz und Zeitreihen an gesendet werden. Dies unterstützt die Echtzeit-Streaming-Erfassung und Batch-Erfassung. [!DNL Profile] Weitere Informationen dazu, wie Sie dem Echtzeit-Kundenprofil Daten hinzufügen, finden Sie in [diesem Tutorial](tutorials/add-profile-data.md).

>[!NHinweis]
>Daten, die über Adobe-Lösungen erfasst werden, einschließlich [!DNL Analytics Cloud], [!DNL Marketing Cloud]und [!DNL Advertising Cloud], fließen in [!DNL Experience Platform] die Datenerfassung und werden in diese integriert [!DNL Profile].

### [!DNL Profile] Erfassungsmetriken

Observability Insights ermöglicht die Ermittlung wichtiger Metriken in Adobe Experience Platform. In addition to [!DNL Platform] usage statistics and performance indicators for various [!DNL Platform] functionalities, there are specific [!DNL Profile]-related metrics that allow you to gain insight into incoming request rates, successful ingestion rates, ingested record sizes, and more. To learn more, begin by reading the [Observability Insights overview](../observability/home.md), and for a complete list of [!DNL Profile] metrics, see the documentation on [available metrics](../observability/metrics.md).

## [!DNL Data governance] und [!DNL Privacy]

[!DNL Data governance] umfasst eine Reihe von Strategien und Technologien, mittels derer Kundendaten so verwaltet werden können, dass die Einhaltung gesetzlicher Bestimmungen, Einschränkungen und Richtlinien zu ihrer Nutzung gewährleistet bleibt.

As it relates to accessing data, data governance plays a key role within [!DNL Experience Platform] at various levels:
* Datennutzungsbeschriftungen
* Datenzugriffsrichtlinien
* Kontrollmechanismen für den Datenzugriff für Marketing-Aktivitäten

[!DNL Data governance] an mehreren Stellen verwaltet wird. These include deciding what data is ingested into [!DNL Platform] and what data is accessible after ingestion for a given marketing action. Gehen Sie für weitere Informationen hierzu zunächst die [Übersicht über Data Governance](../data-governance/home.md) durch.

### Umgang mit Opt-out- und Datenschutzanfragen

[!DNL Experience Platform] ermöglicht es Ihren Kunden, Abmeldeanfragen im Zusammenhang mit der Nutzung und Datenspeicherung ihrer Daten innerhalb von [!DNL Real-time Customer Profile]zu senden. Weitere Informationen hierzu finden Sie in der Dokumentation zum Thema [Berücksichtigen von Opt-out-Anfragen](../segmentation/honoring-opt-outs.md).

## [!DNL Profile] Richtlinien

[!DNL Experience Platform] hat eine Reihe von Leitlinien zu befolgen, um wirksam zu nutzen [!DNL Profile].

| Abschnitt | Grenze |
| ------- | -------- |
| [!DNL Profile] Vereinigung Schema | Maximal **20** Datensätze können zum Schema der [!DNL Profile] Vereinigung beitragen. |
| Beziehungen zwischen mehreren Entitäten | Es können maximal **5** Beziehungen mit mehreren Entitäten erstellt werden. |
| JSON-Tiefe für mehrere Entitäten | Die maximale JSON-Tiefe beträgt **4**. |
| Zeitreihendaten | Zeitreihendaten sind **nicht** in [!DNL Profile] für Nicht-Personen-Entitäten zulässig. |
| Beziehungen zu Nichtpersonen im Schema | Nicht-menschliche Schema-Beziehungen sind **nicht** zulässig. |
| Profil-Fragment | Die empfohlene Maximalgröße für ein Profil-Fragment ist **10 kB**.<br><br> Die absolute Maximalgröße eines Profil-Fragments ist **1 MB**. |
| Nicht-personenbezogene Entität | Die maximale Gesamtgröße für eine einzelne Nicht-Person-Entität beträgt **200 MB**. |
| Datensätze pro Nicht-Person-Entität | Eine Nicht-Person-Entität kann maximal **1** Datensatz zugeordnet werden. |

<!--
| Section | Boundary | Enforcement |
| ------- | -------- | ----------- |
| Profile union schema | A maximum of **20** datasets can contribute to the Profile union schema. | A message stating you've reached the maximum number of datasets appears. You must either disable or clean up other obsolete datasets in order to create a new dataset. |
| Multi-entity relationships | A maximum of **5** multi-entity relationship can be created. | A message stating all available mappings have been used appears when the fifth relationship is mapped. An error message letting you know you have exceeded the number of available mappings appears when attempting to map a sixth relationship. | 
| JSON depth for multi-entity association | The maximum JSON depth is **4**. | When trying to use the relationship selector with a field that is more than four levels deep, an error message appears, stating it is ineligible for multi-entity association. |
| Time series data | Time-series data is **not** permitted in Profile for non-people entities. | A message stating that this data cannot be enabled for Profile because it is of an unsupported type appears. |
| Non-people schema relationships | Non-people schema relationships are **not** permitted. | Relationships between two non-people schemas cannot be created. The relationships checkbox will be disabled. |
| Profile fragment | The recommended maximum size of a profile fragment is **10kB**.<br><br> The absolute maximum size of a profile fragment is **1MB**. | If you upload a fragment that is larger than 10kB, a warning appears, stating that performance may be degraded since the fragment exceeds the recommended maximum working size.<br><br> If you upload a fragment that is larger than 1MB, ingestion will fail, and an alert letting you know that records have failed will be sent. |
| Non-person entity | The maximum total size for a single non-person entity is **200MB**. | If you load an object as a non-person entity that is larger than 200MB, an alert will appear, stating that the entity has exceeded the maximum allowable size and will not be useable for segmentation. |
| Datasets per non-person entity | A maximum of **1** dataset can be associated to a non-person entity. | If you try to create a second dataset that is associated to the same non-person entity, an error appears, stating that only one dataset can be active per non-person entity. |

--->

>[!NOTE]
>
>
>Eine Nicht-Person-Entität bezieht sich auf jede XDM-Klasse, die **nicht** Teil von ist [!DNL Profile].

## Nächste Schritte und zusätzliche Ressourcen

To learn more about [!DNL Real-time Customer Profile], please continue reading the documentation and supplement your learning by watching the video below or exploring other [Experience Platform video tutorials](https://docs.adobe.com/content/help/de-DE/platform-learn/tutorials/overview.html).

>[!WARNING]
>Die im folgenden Video dargestellte [!DNL Platform] Benutzeroberfläche ist veraltet. Die neuesten Screenshots und Funktionen der Benutzeroberfläche finden Sie im Benutzerhandbuch [zum](ui/user-guide.md) Echtzeit-Profil.

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12)