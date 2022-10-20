---
keywords: Experience Platform; Profil; Echtzeit-Kundenprofil; Fehlerbehebung; Limits; Richtlinien; Grenze; Entität; primäre Entität; Dimensionentität;
title: Standardmäßige Limits für Echtzeit-Kundenprofildaten
solution: Experience Platform
product: experience platform
type: Documentation
description: Adobe Experience Platform verwendet ein stark denormalisiertes Hybrid-Datenmodell, das sich vom herkömmlichen relationalen Datenmodell unterscheidet. Dieses Dokument liefert standardmäßige Verwendungs- und Quotenbegrenzungen zur Hilfe bei der Modellierung Ihrer Profildaten, sodass Sie eine optimale Systemleistung gewährleisten können.
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
source-git-commit: d6100f58b8ffd6251c3a58576a41dbfb75c3bb0c
workflow-type: tm+mt
source-wordcount: '1902'
ht-degree: 49%

---

# Standardmäßige Limits für [!DNL Real-time Customer Profile] data

Mit Adobe Experience Platform können Sie personalisierte kanalübergreifende Erlebnisse auf der Grundlage von Verhaltenseinblicken und Kundenattributen in Form von Echtzeit-Kundenprofilen bereitstellen. Um diesen neuen Ansatz bei Profilen zu unterstützen, verwendet Experience Platform ein stark denormalisiertes Hybrid-Datenmodell, das sich vom herkömmlichen relationalen Datenmodell unterscheidet.

Dieses Dokument liefert standardmäßige Verwendungs- und Quotenbegrenzungen zur Hilfe bei der Modellierung Ihrer Profildaten, sodass Sie eine optimale Systemleistung gewährleisten können. Bei der Überprüfung der folgenden Leitlinien wird davon ausgegangen, dass Sie die Daten korrekt modelliert haben. Wenden Sie sich bei Fragen zum Modellieren Ihrer Daten an Ihren Kundenbetreuer.

>[!NOTE]
>
>Die meisten Kunden überschreiten diese Standardbeschränkungen nicht. Wenden Sie sich an Ihren Kundenbetreuer, wenn Sie mehr über benutzerdefinierte Beschränkungen erfahren möchten.

## Erste Schritte

Die folgenden Experience Platform-Services sind mit der Modellierung von Echtzeit-Kundenprofildaten beteiligt:

* [[!DNL Real-time Customer Profile]](home.md): Erstellen Sie einheitliche Verbraucherprofile anhand von Daten aus mehreren Quellen.
* [Identitäten](../identity-service/home.md): Bridge-Identitäten aus unterschiedlichen Datenquellen, während sie in Platform erfasst werden.
* [Schemas](../xdm/home.md): Experience-Datenmodell (XDM)-Schemas sind das standardisierte Framework, mit dem Platform Kundenerlebnisdaten organisiert.
* [Segmente](../segmentation/home.md): Die Segmentierungs-Engine in Platform wird verwendet, um basierend auf dem Kundenverhalten und den Kundenattributen Segmente aus Ihren Kundenprofilen zu erstellen.

## Arten von Beschränkungen

In diesem Dokument gibt es zwei Arten von Standardbeschränkungen:

* **Weiche Grenze:** Es ist möglich, über eine weiche Grenze hinauszugehen, jedoch bieten weiche Grenzen eine empfohlene Richtlinie für die Systemleistung.

* **Harte Grenze:** Eine harte Grenze bietet ein absolutes Maximum.

>[!NOTE]
>
>Die in diesem Dokument dargelegten Beschränkungen werden ständig verbessert. Achten Sie regelmäßig auf Updates. Wenden Sie sich an Ihren Kundenbetreuer, wenn Sie mehr über benutzerdefinierte Beschränkungen erfahren möchten.

## Datenmodellbeschränkungen

Die folgenden Leitlinien bieten empfohlene Beschränkungen bei der Modellierung von Echtzeit-Kundenprofildaten. Weitere Informationen zu primären Entitäten und Dimensionsentitäten finden Sie im Abschnitt zu [Entitätstypen](#entity-types) in der Anlage.

### Leitlinien für primäre Entitäten

| Beschränkung | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| Klassendatensätze von XDM Individual Profile | 20 | Weich | Es werden maximal 20 Datensätze empfohlen, die die Klasse &quot;XDM Individual Profile&quot;nutzen. |
| XDM ExperienceEvent-Klassendatensätze | 20 | Weich | Es werden maximal 20 Datensätze empfohlen, die die XDM ExperienceEvent-Klasse nutzen. |
| Für Profil aktivierte Adobe Analytics Report Suite-Datensätze | 1 | Soft | Es sollte maximal ein (1) Analytics Report Suite-Datensatz für Profil aktiviert werden. Der Versuch, mehrere Analytics Report Suite-Datensätze für Profile zu aktivieren, kann unbeabsichtigte Auswirkungen auf die Datenqualität haben. Weitere Informationen finden Sie im Abschnitt zu [Adobe Analytics-Datensätze](#aa-datasets) in der Anlage. |
| Beziehungen mit mehreren Entitäten | 5 | Weich | Es werden maximal 5 Beziehungen mit mehreren Entitäten empfohlen, die in primären Entitäten oder Dimensionsentitäten definiert sind. Zusätzliche Beziehungszuordnungen sollten erst vorgenommen werden, wenn eine vorhandene Beziehung entfernt oder deaktiviert wurde. |
| JSON-Tiefe für ID-Feld, das in der Beziehung mit mehreren Entitäten verwendet wird | 4 | Soft | Die empfohlene maximale JSON-Tiefe für ein ID-Feld, das in Beziehungen mit mehreren Entitäten verwendet wird, beträgt 4. Dies bedeutet, dass in einem hochverschachtelten Schema Felder, die mehr als vier Ebenen tief verschachtelt sind, nicht als ID-Feld in einer Beziehung verwendet werden sollten. |
| Array-Kardinalität in einem Profilfragment | &lt;=500 | Soft | Die optimale Array-Kardinalität in einem Profilfragment (zeitunabhängige Daten) ist &lt;=500. |
| Array-Kardinalität in ExperienceEvent | &lt;=10 | Soft | Die optimale Array-Kardinalität in einem ExperienceEvent (Zeitreihendaten) ist &lt;=10. |
| Identitätsanzahl für jedes Profil - Identitätsdiagramm | 50 | Hard | **Die maximale Anzahl von Identitäten in einem Identitätsdiagramm für ein einzelnes Profil beträgt 50.** Alle Profile mit mehr als 50 Identitäten werden von der Segmentierung, dem Export und der Suche ausgeschlossen. |

{style=&quot;table-layout:auto&quot;}

### Leitlinien für Dimensionsentitäten

| Beschränkung | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| Keine Zeitreihendaten zulässig für Nicht-Zeitreihen[!DNL XDM Individual Profile] entity | 0 | Hart | **Zeitreihendaten sind für Nicht-Analytics nicht zulässig.[!DNL XDM Individual Profile] Entitäten in Profil Service.** Wenn ein Datensatz aus Zeitreihen mit einem Nicht-Segment verknüpft ist[!DNL XDM Individual Profile] ID, sollte der Datensatz nicht für [!DNL Profile]. |
| Keine verschachtelten Beziehungen | 0 | Weich | Sie sollten keine Beziehung zwischen zwei Nicht-[!DNL XDM Individual Profile]-Schemas erstellen. Die Möglichkeit, Beziehungen zu erstellen, wird für keine Schemas empfohlen, die nicht Teil des einheitlichen [!DNL Profile]-Schemas sind. |
| JSON-Tiefe für primäres ID-Feld | 4 | Soft | Die empfohlene maximale JSON-Tiefe für das primäre ID-Feld beträgt 4. Das bedeutet, dass Sie in einem hochverschachtelten Schema ein Feld nicht als primäre ID auswählen sollten, wenn es mehr als vier Ebenen tief verschachtelt ist. Ein Feld, das sich auf der vierten verschachtelten Ebene befindet, kann als primäre ID verwendet werden. |

{style=&quot;table-layout:auto&quot;}

## Datengrößenbeschränkungen

In den folgenden Leitlinien erhalten Sie Informationen zur Datengröße und zu empfohlenen Beschränkungen für Daten, um eine problemlose Aufnahme, Speicherung und Abfrage zu gewährleisten. Weitere Informationen zu primären Entitäten und Dimensionsentitäten finden Sie im Abschnitt zu [Entitätstypen](#entity-types) in der Anlage.

>[!NOTE]
>
>Die Datengröße wird an den unkomprimierten Daten in JSON zum Zeitpunkt der Aufnahme gemessen.

### Leitlinien für primäre Entitäten

| Beschränkung | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| Maximale ExperienceEvent-Größe | 10 KB | Hard | **Die maximale Größe eines Ereignisses beträgt 10 KB.** Die Aufnahme wird fortgesetzt, jedoch werden alle Ereignisse, die größer als 10 KB sind, gelöscht. |
| Maximale Profildatensatzgröße | 100 KB | Hard | **Die maximale Größe eines Profildatensatzes beträgt 100 KB.** Die Aufnahme wird fortgesetzt, Profildatensätze, die größer als 100 KB sind, werden jedoch gelöscht. |
| Maximale Größe von Profilfragmenten | 50 MB | Hard | **Die maximale Größe eines einzelnen Profilfragments beträgt 50 MB.** Die Segmentierung, der Export und die Suche können bei allen [Profilfragment](#profile-fragments) größer als 50 MB ist. |
| Maximale Profilspeichergröße | 50 MB | Soft | **Die maximale Größe eines gespeicherten Profils beträgt 50 MB.** Hinzufügen neuer [Profilfragmente](#profile-fragments) in ein Profil, das größer als 50 MB ist, wirkt sich auf die Systemleistung aus. Beispielsweise könnte ein Profil ein einzelnes Fragment mit 50 MB enthalten oder mehrere Fragmente aus mehreren Datensätzen mit einer kombinierten Gesamtgröße von 50 MB enthalten. Der Versuch, ein Profil mit einem einzelnen Fragment, das größer als 50 MB ist, oder mehreren Fragmenten mit einer Gesamtgröße von mehr als 50 MB zu speichern, wirkt sich auf die Systemleistung aus. |
| Anzahl der täglich erfassten Profil- oder ExperienceEvent-Batches | 90 | Soft | **Die maximale Anzahl von Profil- oder ExperienceEvent-Batches, die pro Tag erfasst werden, beträgt 90.** Das bedeutet, dass die Gesamtanzahl der täglich erfassten Profil- und ExperienceEvent-Batches 90 nicht überschreiten darf. Die Erfassung zusätzlicher Batches wirkt sich auf die Systemleistung aus. |

{style=&quot;table-layout:auto&quot;}

### Leitlinien für Dimensionsentitäten

| Beschränkung | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| Gesamtgröße für alle dimensionalen Entitäten | 5 GB | Weich | Die empfohlene Gesamtgröße für alle dimensionalen Entitäten beträgt 5 GB. Die Aufnahme großer Dimensionsentitäten kann die Systemleistung beeinträchtigen. Es wird beispielsweise nicht empfohlen, einen 10 GB großen Produktkatalog als Dimensionsentität zu laden. |
| Datensätze pro Dimensionsentitätsschema | 5 | Weich | Es wird empfohlen, maximal 5 Datensätze mit jedem Dimensionsschema zu verknüpfen. Wenn Sie beispielsweise ein Schema für „Produkte“ erstellen und fünf beitragende Datensätze hinzufügen, sollten Sie keinen sechsten Datensatz erstellen, der mit dem Produktschema verknüpft ist. |
| Dimensionsentitäts-Batches, die pro Tag aufgenommen werden | 4 pro Entität | Weich | Die empfohlene maximale Anzahl von Dimensionsentitäts-Batches, die pro Tag aufgenommen werden, beträgt 4 pro Entität. Sie können beispielsweise Aktualisierungen an einem Produktkatalog bis zu 4-mal täglich aufnehmen. Die Aufnahme zusätzlicher Dimensionsentitäts-Batches für dieselbe Entität kann sich auf die Systemleistung auswirken. |

{style=&quot;table-layout:auto&quot;}

## Leitlinien für die Segmentierung

Die in diesem Abschnitt beschriebenen Leitlinien beziehen sich auf die Anzahl und Beschaffenheit der Segmente, die ein Unternehmen in Experience Platform erstellen kann, sowie auf die Zuordnung von Segmenten zu Zielen bzw. ihre Aktivierung für Ziele.

| Beschränkung | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| Segmente pro Sandbox | 4000 | Soft | Eine Organisation kann insgesamt über mehr als 4000 Segmente verfügen, sofern in jeder einzelnen Sandbox weniger als 4000 Segmente vorhanden sind. Der Versuch, zusätzliche Segmente zu erstellen, kann sich auf die Systemleistung auswirken. |
| Edge-Segmente pro Sandbox | 150 | Soft | Eine Organisation kann insgesamt über mehr als 150 Edge-Segmente verfügen, sofern in jeder einzelnen Sandbox weniger als 150 Edge-Segmente vorhanden sind. Der Versuch, zusätzliche Edge-Segmente zu erstellen, kann die Systemleistung beeinträchtigen. |
| Streaming-Segmente pro Sandbox | 500 | Soft | Eine Organisation kann über mehr als 500 Streaming-Segmente verfügen, sofern in jeder einzelnen Sandbox weniger als 500 Streaming-Segmente vorhanden sind. Der Versuch, zusätzliche Streaming-Segmente zu erstellen, kann die Systemleistung beeinträchtigen. |
| Batch-Segmente pro Sandbox | 4000 | Soft | Eine Organisation kann insgesamt über mehr als 4.000 Batch-Segmente verfügen, sofern in jeder einzelnen Sandbox weniger als 4.000 Batch-Segmente vorhanden sind. Der Versuch, zusätzliche Batch-Segmente zu erstellen, kann die Systemleistung beeinträchtigen. |

{style=&quot;table-layout:auto&quot;}

## Anhang

Dieser Abschnitt enthält zusätzliche Details zu den Limits in diesem Dokument.

### Entitätstypen

Das [!DNL Profile]-Datenspeichermodell besteht aus zwei Kernentitätstypen:

* **Primäre Entität:** Eine primäre Entität oder Profilentität führt Daten zu einer „Single Source of Truth“ für einen Kontakt zusammen. Diese einheitlichen Daten werden mithilfe einer so genannten „einheitlichen Ansicht“ dargestellt. Eine einheitliche Ansicht aggregiert die Felder aller Schemas, die dieselbe Klasse implementieren, in ein einziges einheitliches Schema. Das einheitliche Schema für [!DNL Real-time Customer Profile] ist ein denormalisiertes Hybrid-Datenmodell, das als Container für alle Profilattribute und Verhaltensereignisse fungiert.

   Zeitunabhängige Attribute, auch „Datensatzdaten “genannt, werden mithilfe von [!DNL XDM Individual Profile] modelliert, während die auch als „Ereignisdaten“ bezeichneten Zeitreihendaten mit [!DNL XDM ExperienceEvent] modelliert werden. Wenn Datensatz- und Zeitreihendaten in Adobe Experience Platform aufgenommen werden, dient dies als Trigger für [!DNL Real-time Customer Profile], um mit der Aufnahme von Daten zu beginnen, die für diese Verwendung aktiviert wurden. Je mehr Interaktionen und Details erfasst werden, desto zuverlässiger werden die einzelnen Profile.

   ![](images/guardrails/profile-entity.png)

* **Dimensionsentität:** Während der Profildatenspeicher, in dem Profildaten verwaltet werden, kein relativer Speicher ist, ermöglicht das Profil die Integration mit kleinen Dimensionsentitäten, um Segmente auf vereinfachte und intuitive Weise zu erstellen. Diese Integration wird als [Segmentierung mehrerer Entitäten](../segmentation/multi-entity-segmentation.md) bezeichnet. Ihr Unternehmen kann auch XDM-Klassen definieren, um abgesehen von Einzelpersonen auch andere Dinge zu beschreiben, z. B. Geschäfte, Produkte oder Eigenschaften. Diese Nicht-[!DNL XDM Individual Profile]-Schemas werden als „Dimensionsentitäten“ bezeichnet und enthalten keine Zeitreihendaten. Dimensionsentitäten stellen Suchdaten bereit, die Segmentdefinitionen mit mehreren Entitäten unterstützen und vereinfachen. Sie müssen klein genug sein, damit die Segmentierungsmaschine den gesamten Datensatz in den Speicher laden kann, um eine optimale Verarbeitung zu gewährleisten (schnelle Punktsuche).

   ![](images/guardrails/profile-and-dimension-entities.png)

### Profilfragmente

In diesem Dokument gibt es mehrere Limits, die auf &quot;Profilfragmente&quot;verweisen. In Experience Platform werden mehrere Profilfragmente zusammengeführt, um das Echtzeit-Kundenprofil zu bilden. Jedes Fragment stellt eine eindeutige primäre Identität und die entsprechenden Datensatz- oder Ereignisdaten für diese ID in einem bestimmten Datensatz dar. Weiterführende Informationen zu Profilfragmenten finden Sie im Abschnitt [Profilübersicht](home.md#profile-fragments-vs-merged-profiles).

### Zusammenführungsrichtlinien {#merge-policies}

Beim Zusammenführen von Daten aus mehreren Quellen dienen Zusammenführungsrichtlinien als jene Regeln, mit denen Platform bestimmt, wie Daten priorisiert werden und welche Daten kombiniert werden, um eine einheitliche Ansicht zu schaffen. Wenn ein Kunde beispielsweise über mehrere Kanäle mit Ihrer Marke interagiert, verfügt Ihr Unternehmen über mehrere Profilfragmente, die sich auf diesen einzelnen Kunden beziehen und in mehreren Datensätzen enthalten sind. Wenn diese Fragmente in Platform aufgenommen werden, werden sie zusammengeführt, sodass ein zentrales Profil für diesen Kunden entsteht. Wenn die Daten aus mehreren Quellen in Konflikt stehen, bestimmt die Zusammenführungsrichtlinie, welche Informationen in das Profil für die Person aufgenommen werden sollen. Pro Organisation sind maximal fünf (5) Zusammenführungsrichtlinien zulässig. Weitere Informationen zu Zusammenführungsrichtlinien finden Sie im Abschnitt [Übersicht über Zusammenführungsrichtlinien](merge-policies/overview.md).

### Adobe Analytics Report Suite-Datensätze in Platform {#aa-datasets}

Für Profile können mehrere Report Suites aktiviert werden, solange alle Datenkonflikte gelöst sind. Mit der Datenvorbereitung können Sie Datenkonflikte zwischen eVars, Listen und Props beheben. Weitere Informationen zur Verwendung der Funktion &quot;Datenvorbereitung&quot;finden Sie in der [Handbuch zur Benutzeroberfläche von Adobe Analytics Connector](../sources/tutorials/ui/create/adobe-applications/analytics.md).
