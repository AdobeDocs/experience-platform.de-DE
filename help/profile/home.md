---
keywords: Experience Platform;Profil;Echtzeit-Kundenprofil;Fehlerbehebung;API;Einheitliches Profil;Einheitliches Profil;Profil;RTCP;XDM-Diagramme
title: Übersicht zum Echtzeit-Kundenprofil
description: Das Echtzeit-Kundenprofil führt Daten aus verschiedenen Quellen zusammen und bietet Zugriff auf diese Daten in Form von individuellen Kundenprofilen und zugehörigen Zeitreihenereignissen. die es Marketing-Experten ermöglichen, über verschiedenste Kanäle hinweg koordinierte, konsistente und relevante Erlebnisse für ihre Zielgruppen umzusetzen.
exl-id: c93d8d78-b215-4559-a806-f019c602c4d2
source-git-commit: 8f61840ad60b7d24c980b218b6f742485f5ebfdd
workflow-type: ht
source-wordcount: '1991'
ht-degree: 100%

---

# [!DNL Real-Time Customer Profile] – Übersicht

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Ihre Kundinnen und Kunden, unabhängig davon, wo und wann sie mit Ihrer Marke interagieren. Das [!DNL Real-Time Customer Profile] ermöglicht Ihnen eine ganzheitliche Sicht auf jeden einzelnen Kunden, indem es Daten aus Online- und Offline-Kanälen ebenso wie aus CRMs und Drittanbieter-Datenquellen sowie anderen Kanälen miteinander kombiniert. Mit dem [!DNL Profile] können Sie Ihre unterschiedlichen Kundendaten in einer zentralen Ansicht zusammenführen, die eine aussagekräftige, Darstellung jeder Kundeninteraktion mit Zeitstempel bietet. Diese Übersicht hilft Ihnen, die Rolle und Verwendung des [!DNL Real-Time Customer Profile] in [!DNL Experience Platform] zu verstehen.

## [!DNL Profile] in Experience Platform

Das nachfolgende Diagramm zeigt die Zusammenhänge zwischen dem Echtzeit-Kundenprofil und anderen Services in Experience Platform:

![Die Beziehung zwischen Echtzeit-Kundenprofil und anderen Services in Adobe Experience Platform. Dieses Diagramm zeigt, dass das Profil eine der Kernkomponenten von Adobe Experience Platform ist.](images/profile-overview/profile-in-platform.png)

## Profile verstehen

[!DNL Real-Time Customer Profile] führt Daten aus verschiedenen Unternehmenssystemen zusammen und ermöglicht dann den Zugriff auf diese Daten in Form von Profilen mit zugehörigen Zeitreihen-Ereignissen. die es Marketing-Experten ermöglichen, über verschiedenste Kanäle hinweg koordinierte, konsistente und relevante Erlebnisse für ihre Zielgruppen umzusetzen. In den folgenden Abschnitten werden einige der Kernkonzepte hervorgehoben, die Sie verstehen müssen, um Profile innerhalb von Platform effektiv zu erstellen und zu verwalten.

### Entitätskomposition des Profils

Ein Echtzeit-Kundenprofil besteht aus einer Hauptentität, der sogenannten **primären Entität**, und verschiedenen unterstützenden Entitäten. Im Kontext von Experience Platform ist die primäre Entität normalerweise eine **Profilentität**, die aus Eigenschaften, Verhaltensweisen und Segmentzugehörigkeiten einer einzelnen Person besteht. Andere Entitäten ermöglichen es der Segmentierungs-Engine, Daten außerhalb der primären Entität des Profils zu verwenden, und umfassen Folgendes:

- **Dimensionsentität**: Die Entität, die zur Vereinfachung des Datenmodellierungsprozesses für Informationen verwendet wird, die über Ereignisse oder Profildatensätze hinweg freigegeben werden. Dies wird auch als Lookup-Entität oder Klassifizierungsentität bezeichnet.
- **B2B-Entität**: Entitäten, die die Beziehung des Profils zu B2B-Konten und Opportunities beschreiben.

![Ein Diagramm, das die Zusammensetzung der Profilentität erklärt.](./images/profile-overview/profile-entity-composition.png)

>[!IMPORTANT]
>
>Da dimensionale und B2B-Entitäten nur außerhalb der primären Entität existieren, werden diese nur für die Stapelsegmentierung verwendet.

Dimensionale und B2B-Entitäten werden über **Schemabeziehungen** mit der primären Entität verknüpft. Weiterführende Informationen finden Sie in der folgenden Dokumentation:

- [Erstellen einer Eins-zu-eins-Schema-Beziehung für Lookup-Entitäten](../xdm/tutorials/relationship-ui.md)
- [Erstellen einer Viele-zu-eins-Schemabeziehung für B2B-Entitäten](../xdm/tutorials/relationship-b2b.md)

### Profil-Datenspeicher

Das [!DNL Real-Time Customer Profile] verarbeitet zwar aufgenommene Daten und führt mithilfe des [!DNL Identity Service] von Adobe Experience Platform zugehörige Daten via Identitätszuordnung zusammen, unterhält aber zugleich auch eigene Daten in seinem [!DNL Profile]-Datenspeicher. Der [!DNL Profile]-Speicher ist getrennt von Katalogdaten im Data Lake und von [!DNL Identity Service]-Daten im Identitätsdiagramm.

Der Profil-Store verwendet eine Microsoft Azure Cosmos DB-Infrastruktur und der Platform Data Lake verwendet Microsoft Azure Data Lake-Datenspeicherung.

### Leitplanken für Profile

Experience Platform bietet eine Reihe von Schutzmaßnahmen, mit denen Sie vermeiden können, [Experience-Datenmodell(XDM)-Schemata](../xdm/home.md) zu erstellen, die vom Echtzeit-Kundenprofil nicht unterstützt werden können. Dies umfasst weiche Beschränkungen, die zu Leistungsbeeinträchtigungen führen, sowie harte Beschränkungen, die zu Fehlern und Systembrüchen führen. Weitere Informationen, einschließlich einer Liste von Richtlinien und Beispielanwendungsfällen, finden Sie in der Dokumentation zu [Profilleitplanken](guardrails.md).

### Profil-Dashboard {#profile-dashboard}

Die Benutzeroberfläche von Experience Platform bietet ein Dashboard, mit dem Sie wichtige Informationen zu Ihren Echtzeit-Kundenprofildaten anzeigen können, indem sie in einem täglichen Schnappschuss erfasst werden. Weitere Informationen zum Zugriff auf und zum Arbeiten mit dem [!DNL Profile]-Dashboard in der Benutzeroberfläche sowie detaillierte Informationen zu den im Dashboard angezeigten Metriken finden Sie im Handbuch [Handbuch für die Benutzeroberfläche des Profil-Dashboards](ui/profile-dashboard.md).

### Profilfragmente im Vergleich zu zusammengeführten Profilen {#profile-fragments-vs-merged-profiles}

Jedes einzelne Kundenprofil besteht aus mehreren Profilfragmenten, die zu einer einzigen Ansicht dieses Kunden zusammengefügt wurden. Wenn ein Kunde beispielsweise über mehrere Kanäle mit Ihrer Marke interagiert, verfügt Ihr Unternehmen über mehrere Profilfragmente, die sich auf diesen einzelnen Kunden beziehen und in mehreren Datensätzen enthalten sind. Wenn diese Fragmente in Platform aufgenommen werden, werden sie zusammengeführt, sodass ein zentrales Profil für diesen Kunden entsteht.

Mit anderen Worten: Profilfragmente stellen eine eindeutige primäre Identität und die entsprechenden [Datensätze](#record-data) oder [Ereignisdaten](#time-series-events) für diese ID in einem bestimmten Datensatz dar.

Wenn die Daten aus mehreren Datensätzen in Konflikt stehen (z. B. listet ein Fragment den Kunden als „ledig“ auf, während ein anderes den Kunden als „verheiratet“ auflistet), bestimmt die [Zusammenführungsrichtlinie](#merge-policies), welche Informationen priorisiert und in das Profil für die Einzelperson aufgenommen werden sollen. Da jedes Profil im Allgemeinen aus mehreren Fragmenten aus mehreren Datensätzen besteht, ist die Gesamtanzahl der Fragmente innerhalb von Platform wahrscheinlich höher als die Gesamtanzahl der zusammengeführten Profile.

### Daten aufzeichnen {#record-data}

Ein Profil ist eine Darstellung eines Subjekts, einer Organisation oder einer Einzelperson, die aus vielen Attributen besteht (auch als Datensatzdaten bezeichnet). So kann etwa ein Produktprofil eine SKU und eine Beschreibung enthalten, während in einem Personenprofil Informationen wie Vorname, Nachname und E-Mail-Adresse erfasst sind. Mit [!DNL Experience Platform] können Sie Profile so anpassen, dass die für Ihr Unternehmen relevanten Daten verwendet werden. Die standardmäßige Klasse, das [!DNL Experience Data Model] (XDM), [!DNL XDM Individual Profile], ist die bevorzugte Klasse für die Erstellung eines Schemas zur Beschreibung von Kundendatensatzdaten und liefert eine Vielzahl von für die Interaktionen zwischen Platform-Services essentiellen Daten. Lesen Sie zum Einstieg in die Arbeit mit Schemas in [!DNL Experience Platform] zunächst die [Übersicht über das XDM-System](../xdm/home.md) durch.

### Zeitreihen-Ereignisse {#time-series-events}

Zeitreihendaten liefern eine Momentaufnahme des Systems zu dem Zeitpunkt, an dem ein Subjekt direkt oder indirekt eine Aktion ausgeführt hat, sowie Daten mit Details zu dem Ereignis selbst. Zeitreihendaten werden im Schema anhand der Standardklasse XDM ExperienceEvent dargestellt. Sie beschreiben Ereignisse wie etwa das Hinzufügen eines Artikels zu einem Warenkorb, das Klicken auf einen Link, das Abspielen eines Videos usw. Auf Grundlage von Zeitreihendaten können Segmentierungsregeln eingerichtet werden. Die einzelnen Ereignisse sind dabei im Kontext eines Profils abrufbar.

### Identitäten

Bei der Kommunikation mit Kunden gilt es, diese in einer auf sie persönlich abgestimmte Weise anzusprechen. Die Umsetzung solcher für Kunden relevanter digitaler Erlebnisse ist jedoch eine Herausforderung. Denn dazu muss nachvollzogen werden, wie die verschiedenen Daten, die sie auf voneinander getrennten digitalen Kanälen wie Tablets, Smartphones und Laptops generieren, zueinander in Zusammenhang stehen. [!DNL Identity Service] ermöglicht es Ihnen, das Gesamtbild Ihres Kunden zusammenzusetzen, indem Sie Identitäten aus mehreren Kanälen verknüpfen und ein Identitätsdiagramm für jeden Kunden erstellen. Weitere Informationen finden Sie in der [Identity Service – Übersicht](../identity-service/home.md).

### Zusammenführungsrichtlinien

Um ein umfassendes Bild jedes Ihrer Kunden zu zeichnen, werden Daten aus verschiedenen Quellen zusammengeführt und kombiniert. Zusammenführungsrichtlinien stellen dabei die Regeln, nach denen [!DNL Platform] bestimmt, wie Daten priorisiert und welche Daten zur Erstellung dieser zentralen Sicht verwendet werden.

Wenn Daten aus mehreren Datensätzen miteinander in Konflikt stehen, bestimmt die Zusammenführungsrichtlinie, wie diese Daten behandelt werden und welcher Wert verwendet werden soll. Über die RESTful APIs oder die Benutzeroberfläche können Sie neue Zusammenführungsrichtlinien erstellen, vorhandene Richtlinien verwalten und eine standardmäßige Zusammenführungsrichtlinie für Ihr Unternehmen einrichten.

Um mehr über Zusammenführungsrichtlinien und ihre Rolle in der Experience Platform zu erfahren, lesen Sie zunächst die [Übersicht über Zusammenführungsrichtlinien](merge-policies/overview.md).

### Vereinigungsschemas {#profile-fragments-and-union-schemas}

Eines der wichtigsten Merkmale des [!DNL Real-Time Customer Profile] ist seine Fähigkeit, Daten aus verschiedenen Kanälen zusammenzuführen. Wird über das [!DNL Real-Time Customer Profile] auf eine Entität zugegriffen, kann es eine datensatzübergreifende Sicht aller Profilfragmente für die entsprechende Entität liefern, die als „Vereinigungsansicht“ bezeichnet und über ein sogenanntes Vereinigungsschema umgesetzt wird.

Weitere Informationen zu Vereinigungsschemas, einschließlich dem Zugriff auf Vereinigungsschemas in der Benutzeroberfläche, finden Sie im [Handbuch zur Benutzeroberfläche der Vereinigungsschemas](ui/union-schema.md).

<!-- ### (Alpha) Computed attributes

>[!IMPORTANT]
>
>Computed attribute functionality is in alpha. The documentation and functionality are subject to change.

Computed attributes are functions used to aggregate event-level data into profile-level attributes. These functions are automatically computed so that they can be used across segmentation, activation, and personalization. These computations help you to easily answer questions related to things like lifetime purchase value, time between purchases, or number of application opens, without requiring you to manually perform complex calculations each time the information is needed. For more information on computed attributes, including understanding the role computed attributes play within Adobe Experience Platform, please begin by reading the [computed attributes overview](computed-attributes/overview.md). -->

## Profile und Segmente

Der [!DNL Segmentation Service] von Adobe Experience Platform liefert die Zielgruppen, die für die Bereitstellung von Erlebnissen für Ihre individuellen Kunden benötigt werden. Wird ein solches Zielgruppensegment erstellt, wird dessen Segment-ID zur Liste der Segmentmitglieder für alle qualifizierten Profile hinzugefügt. Segmentregeln werden mithilfe von RESTful-APIs und der Benutzeroberfläche von Segment Builder erstellt und auf die Daten des [!DNL Real-Time Customer Profile] angewendet. Um mehr über die Segmentierung zu erfahren, lesen Sie zunächst die [Segmentation Service – Übersicht](../segmentation/home.md).

### Streaming-Erfassung und Streaming-Segmentierung

Der Prozess, Daten in Echtzeit zu erfassen, wird als Streaming-Erfassung bezeichnet. Bevor aufgenommene Profil- und Zeitreihendaten mit bestehenden Daten zusammengeführt werden und die Vereinigungsansicht aktualisiert wird, bestimmt das [!DNL Real-Time Customer Profile] anhand der sogenannten Streaming-Segmentierung durchgehend automatisch, ob die neuen Daten in den Segmenten eingeschlossen oder von ihnen ausgeschlossen werden. Das Ergebnis: Berechnungen und Entscheidungen dazu, wie Sie Ihren Kunden herausragende, individuell auf sie abgestimmte Erlebnisse liefern, lassen sich direkt während ihrer Interaktion mit Ihrer Marke anstellen bzw. treffen. Im Verlauf der Datenaufnahme wird außerdem validiert, ob die Daten ordnungsgemäß erfasst werden und dem Schema entsprechen, auf dem der Datensatz basiert. Weitere Informationen dazu, welche Validierungen bei der Datenaufnahme vorgenommen werden, finden Sie in der Übersicht über die Datenaufnahme unter [Datenqualität](../ingestion/quality/overview.md).

## Edge-Projektionen

Um koordinierte, konsistente und personalisierte Erlebnisse für Ihre Kunden über mehrere Kanäle hinweg in Echtzeit bieten zu können, müssen die richtigen Daten jederzeit verfügbar sein und bei Änderungen kontinuierlich aktualisiert werden. Adobe Experience Platform ermöglicht diesen Echtzeitzugriff auf Daten mithilfe sogenannter Edges. Ein Edge ist ein regional aufgestellter Server, der Daten erfasst und direkt für Anwendungen abrufbar macht. Adobe-Programme wie etwa Adobe Target und Adobe Campaign nutzen beispielsweise Edges, um personalisierte Kundenerlebnisse in Echtzeit bereitzustellen. Die Daten werden mittels Projektion an einen Edge übermittelt, wobei ein Projektionsziel den Edge definiert, an den die Daten gesendet werden, und eine Projektionskonfiguration, die die Informationen spezifiziert, die am Edge zur Verfügung gestellt werden. Weitere Informationen und die Arbeit mit Projektionen mithilfe der [!DNL Real-Time Customer Profile]-API finden Sie im [Handbuch zu den Endpunkten für die Edge-Projektion](api/edge-projections.md).

## Aufnehmen von Daten in [!DNL Profile]

[!DNL Platform] kann so konfiguriert werden, dass Ihre Datensatz- und Zeitreihendaten an das [!DNL Profile] gesendet werden, und unterstützt die Aufnahme im Echtzeit-Streaming sowie per Batch. Weiterführende Informationen dazu, wie Sie [dem Echtzeit-Kundenprofil Daten hinzufügen](tutorials/add-profile-data.md), finden Sie im entsprechenden Tutorial.

>[!NOTE]
>
>Daten, die über Adobe-Lösungen wie [!DNL Analytics Cloud], [!DNL Marketing Cloud] und [!DNL Advertising Cloud] erfasst werden, fließen in [!DNL Experience Platform] und werden in [!DNL Profile] aufgenommen.

### Metriken zur Aufnahme von Profilen

Observability Insights ermöglicht die Ermittlung von Schlüsselmetriken in Adobe Experience Platform. Zusätzlich zu den in verfügbaren Nutzungsstatistiken und Leistungsindikatoren von [!DNL Experience Platform] für verschiedene [!DNL Platform]-Funktionalitäten können Sie verschiedene auf das Profil bezogene Metriken ermitteln, die Ihnen Aufschluss über die Rate eingehender Anfragen, erfolgreicher Datenaufnahmen, Größen der aufgenommenen Datensätze und mehr geben. Um mehr zu erfahren, lesen Sie zunächst die [Übersicht über die Observability Insights-API](../observability/api/overview.md). Eine vollständige Liste der Echtzeit-Kundenprofil-Metriken finden Sie in der Dokumentation zu [verfügbaren Metriken](../observability/api/metrics.md#available-metrics).

## Aktualisieren von Profilspeicherdaten

Gelegentlich kann es erforderlich sein, Daten im Profilspeicher Ihrer Organisation zu aktualisieren. Vielleicht müssen Sie zum Beispiel Datensätze korrigieren oder einen Attributwert ändern. Dies kann durch Batch-Aufnahme erfolgen und erfordert einen profilaktivierten Datensatz, der mit einem Upsert-Tag konfiguriert ist. Weitere Informationen zur Konfiguration eines Datensatzes für Attributaktualisierungen finden Sie im Tutorial zur [Aktivierung eines Datensatzes für Profil und Upsert](../catalog/datasets/enable-upsert.md).

## Data Governance und [!DNL Privacy]

Data Governance umfasst eine Reihe von Strategien und Technologien, mittels derer Kundendaten so verwaltet werden können, dass die Einhaltung gesetzlicher Bestimmungen, Einschränkungen und Richtlinien zur Nutzung dieser Daten gewährleistet bleibt.

Da es um Datenzugriff geht, nimmt die Data Governance in [!DNL Experience Platform] eine zentrale Rolle ein, und zwar auf verschiedenen Ebenen:

- Datennutzungsbeschriftungen
- Datenzugriffsrichtlinien
- Zugangssteuerung für Marketing-Aktivitäten

Die Umsetzung von Data Governance erfolgt an mehreren Stellen. So wird etwa bestimmt, welche Daten in [!DNL Platform] aufgenommen werden und auf welche Daten nach ihrer Aufnahme für eine bestimmte Marketing-Aktivität zugegriffen werden kann. Gehen Sie für weitere Informationen hierzu zunächst die [Übersicht über Data Governance](../data-governance/home.md) durch.

### Umgang mit Opt-out- und Datenschutzanfragen

[!DNL Experience Platform] bietet Funktionalitäten für das Einsenden von Ausstiegsanfragen durch Ihre Kunden bezüglich der Nutzung und Speicherung ihrer Daten im [!DNL Real-Time Customer Profile]. Weitere Informationen hierzu finden Sie in der Dokumentation zum Thema [Berücksichtigen von Opt-out-Anfragen](../segmentation/consents.md).

## Nächste Schritte und zusätzliche Ressourcen

Um mehr über die Verwendung von Echtzeit-Kundenprofildaten mithilfe der Benutzeroberfläche von Experience Platform oder der Profil-API zu erfahren, lesen Sie zunächst das [Handbuch zur Profil-Benutzeroberfläche](ui/user-guide.md) beziehungsweise das [API-Entwicklerhandbuch](api/overview.md).
