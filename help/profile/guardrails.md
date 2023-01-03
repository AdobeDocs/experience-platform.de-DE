---
keywords: Experience Platform;Profil;Echtzeit-Kundenprofil;Fehlerbehebung;Leitlinien;Richtlinien;Limit;Entität;primäre Entität;Dimensionsentität;
title: Standardmäßige Limits für Echtzeit-Kundenprofildaten
solution: Experience Platform
product: experience platform
type: Documentation
description: Adobe Experience Platform verwendet ein stark denormalisiertes Hybrid-Datenmodell, das sich vom herkömmlichen relationalen Datenmodell unterscheidet. Dieses Dokument liefert standardmäßige Verwendungs- und Quotenbegrenzungen zur Hilfe bei der Modellierung Ihrer Profildaten, sodass eine optimale Systemleistung gewährleistet ist.
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1929'
ht-degree: 95%

---

# Standard-Leitlinien für [!DNL Real-Time Customer Profile]-Daten

Mit Adobe Experience Platform können Sie personalisierte kanalübergreifende Erlebnisse bereitstellen, die auf verhaltensbezogenen Einblicken und Kundenattributen in Form von Echtzeit-Kundenprofilen basieren. Um diesen neuen Ansatz bei Profilen zu unterstützen, verwendet Experience Platform ein stark denormalisiertes Hybrid-Datenmodell, das sich vom herkömmlichen relationalen Datenmodell unterscheidet.

Dieses Dokument liefert standardmäßige Verwendungs- und Quotenbegrenzungen zur Hilfe bei der Modellierung Ihrer Profildaten, sodass eine optimale Systemleistung gewährleistet ist. Bei der Überprüfung der folgenden Leitlinien wird davon ausgegangen, dass Sie die Daten korrekt modelliert haben. Wenden Sie sich bei Fragen zum Modellieren Ihrer Daten an Ihren Kundenbetreuer.

>[!NOTE]
>
>Die meisten Kunden überschreiten diese Standardbeschränkungen nicht. Wenden Sie sich an Ihren Kundenbetreuer, wenn Sie mehr über benutzerdefinierte Beschränkungen erfahren möchten.

## Erste Schritte

Die folgenden Experience Platform-Services sind mit der Modellierung von Echtzeit-Kundenprofildaten beteiligt:

* [[!DNL Real-Time Customer Profile]](home.md): Erstellen einheitlicher Verbraucherprofile anhand von Daten aus mehreren Quellen.
* [Identitäten](../identity-service/home.md): Überbrücken von Identitäten aus unterschiedlichen Datenquellen, während sie in Platform aufgenommen werden.
* [Schemata](../xdm/home.md): Experience-Datenmodell-Schemata (XDM) sind das standardisierte Framework, mit dem Platform Kundenerlebnisdaten organisiert.
* [Segmente](../segmentation/home.md): Die Segmentierungs-Engine in Platform wird verwendet, um basierend auf Kundenverhalten und Kundenattributen Segmente aus Ihren Kundenprofilen zu erstellen.

## Arten von Beschränkungen

In diesem Dokument gibt es zwei Arten von Standardbeschränkungen:

* **Weiche Grenze:** Es ist möglich, über eine weiche Grenze hinauszugehen, jedoch bieten weiche Grenzen eine empfohlene Richtlinie für die Systemleistung.

* **Harte Grenze:** Eine harte Grenze bietet ein absolutes Maximum.

>[!NOTE]
>
>Die in diesem Dokument dargelegten Beschränkungen werden ständig verbessert. Achten Sie regelmäßig auf Updates. Wenden Sie sich an Ihren Kundenbetreuer, wenn Sie mehr über benutzerdefinierte Beschränkungen erfahren möchten.

## Datenmodellbeschränkungen

Die folgenden Limits bieten empfohlene Einschränkungen bei der Modellierung von Echtzeit-Kundenprofildaten. Weitere Informationen zu primären Entitäten und Dimensionsentitäten finden Sie im Abschnitt zu [Entitätstypen](#entity-types) in der Anlage.

### Leitlinien für primäre Entitäten

| Beschränkung | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| XDM Individual Profile-Klassendatensätze | 20 | Weich | Es werden maximal 20 Datensätze empfohlen, die die XDM Individual Profile-Klasse nutzen. |
| XDM ExperienceEvent-Klassendatensätze | 20 | Weich | Es werden maximal 20 Datensätze empfohlen, die die XDM ExperienceEvent-Klasse nutzen. |
| Für Profil aktivierte Adobe Analytics Report Suite-Datensätze | 1 | Soft | Es sollte maximal ein (1) Analytics Report Suite-Datensatz für Profil aktiviert werden. Der Versuch, mehrere Analytics Report Suite-Datensätze für Profil zu aktivieren, kann unbeabsichtigte Auswirkungen auf die Datenqualität haben. Weitere Informationen finden Sie im Abschnitt zu [Adobe Analytics-Datensätzen](#aa-datasets) im Anhang. |
| Beziehungen mit mehreren Entitäten | 5 | Soft | Es werden maximal 5 Beziehungen mit mehreren Entitäten empfohlen, die in primären Entitäten oder Dimensionsentitäten definiert sind. Zusätzliche Beziehungszuordnungen sollten erst vorgenommen werden, wenn eine vorhandene Beziehung entfernt oder deaktiviert wurde. |
| JSON-Tiefe für ein ID-Feld, das in Beziehungen mit mehreren Entitäten verwendet wird | 4 | Soft | Die empfohlene maximale JSON-Tiefe für ein ID-Feld, das in Beziehungen mit mehreren Entitäten verwendet wird, ist 4. Dies bedeutet, dass in einem stark verschachtelten Schema Felder, die mehr als vier Ebenen tief verschachtelt sind, nicht als ID-Felder in einer Beziehung verwendet werden sollten. |
| Array-Kardinalität in einem Profilfragment | &lt;=500 | Soft | Die optimale Array-Kardinalität in einem Profilfragment (zeitunabhängige Daten) ist &lt;=500. |
| Array-Kardinalität in ExperienceEvent | &lt;=10 | Soft | Die optimale Array-Kardinalität in ExperienceEvent (Zeitreihendaten) ist &lt;=10. |
| Identitätsanzahl im Identitätsdiagramm eines einzelnen Profils | 50 | Hard | **Die maximale Anzahl von Identitäten in einem Identitätsdiagramm für ein einzelnes Profil ist 50.** Alle Profile mit mehr als 50 Identitäten sind von der Segmentierung, dem Export und der Suche ausgeschlossen. |

{style=&quot;table-layout:auto&quot;}

### Leitlinien für Dimensionsentitäten

| Beschränkung | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| Keine Zeitreihendaten zulässig für Nicht-[!DNL XDM Individual Profile]-Entitäten | 0 | Hart | **Zeitreihendaten sind für Nicht-[!DNL XDM Individual Profile]-Entitäten im Profil-Service nicht zulässig.** Wenn ein Zeitreihen-Datensatz mit einer Nicht-[!DNL XDM Individual Profile]-ID verknüpft ist, sollte der Datensatz nicht für [!DNL Profile] aktiviert sein. |
| Keine verschachtelten Beziehungen | 0 | Weich | Sie sollten keine Beziehung zwischen zwei Nicht-[!DNL XDM Individual Profile]-Schemas erstellen. Die Möglichkeit, Beziehungen zu erstellen, wird für keine Schemas empfohlen, die nicht Teil des einheitlichen [!DNL Profile]-Schemas sind. |
| JSON-Tiefe für primäres ID-Feld | 4 | Soft | Die empfohlene maximale JSON-Tiefe für das primäre ID-Feld ist 4. Das bedeutet, dass Sie in einem stark verschachtelten Schema kein Feld als primäre ID auswählen sollten, wenn es mehr als vier Ebenen tief verschachtelt ist. Ein Feld, das sich auf der vierten verschachtelten Ebene befindet, kann als primäre ID verwendet werden. |

{style=&quot;table-layout:auto&quot;}

## Datengrößenbeschränkungen

In den folgenden Leitlinien erhalten Sie Informationen zur Datengröße und zu empfohlenen Beschränkungen für Daten, um eine problemlose Aufnahme, Speicherung und Abfrage zu gewährleisten. Weitere Informationen zu primären Entitäten und Dimensionsentitäten finden Sie im Abschnitt zu [Entitätstypen](#entity-types) in der Anlage.

>[!NOTE]
>
>Die Datengröße wird an den unkomprimierten Daten in JSON zum Zeitpunkt der Aufnahme gemessen.

### Leitlinien für primäre Entitäten

| Beschränkung | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| Maximale ExperienceEvent-Größe | 10 KB | Hard | **Die maximale Größe eines Ereignisses ist 10 KB.** Die Aufnahme wird fortgesetzt, jedoch werden alle Ereignisse, die größer als 10 KB sind, entfernt. |
| Maximale Größe von Profildatensätzen | 100 KB | Hard | **Die maximale Größe eines einzelnen Profildatensatzes ist 100 MB.** Die Aufnahme wird fortgesetzt, jedoch werden Profildatensätze, die größer als 100 KB sind, entfernt. |
| Maximale Größe von Profilfragmenten | 50 MB | Hard | **Die maximale Größe eines einzelnen Profldatensatzes ist 50 MB.** Die Segmentierung, der Export und die Suche können bei [Profilfragmenten](#profile-fragments), die größer als 50 MB sind, fehlschlagen. |
| Maximale Größe gespeicherter Profile | 50 MB | Soft | **Die maximale Größe eines gespeicherten Profils ist 50 MB.** Das Hinzufügen neuer [Profilfragmente](#profile-fragments) in einem Profil, das größer als 50 MB ist, wirkt sich negativ auf die Systemleistung aus. Beispielsweise könnte ein Profil ein einzelnes Fragment mit 50 MB enthalten oder mehrere Fragmente aus mehreren Datensätzen mit einer kombinierten Gesamtgröße von 50 MB. Der Versuch, ein Profil mit einem einzelnen Fragment, das größer als 50 MB ist, oder mit mehreren Fragmenten mit einer kombinierten Größe von mehr als 50 MB zu speichern, wirkt sich negativ auf die Systemleistung aus. |
| Anzahl der täglich aufgenommenen Profil- oder ExperienceEvent-Batches | 90 | Soft | **Die maximale Anzahl von Profil- oder ExperienceEvent-Batches, die pro Tag aufgenommen werden, beträgt 90.** Das bedeutet, dass die Gesamtanzahl der pro Tag aufgenommenen Profil- und ExperienceEvent-Batches 90 nicht überschreiten darf. Das Aufnehmen zusätzlicher Batches beeinträchtigt die Systemleistung. |

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
| Segmente pro Sandbox | 4.000 | Soft | Eine Organisation kann insgesamt über mehr als 4000 Segmente verfügen, sofern in jeder einzelnen Sandbox weniger als 4000 Segmente vorhanden sind. Der Versuch, zusätzliche Segmente zu erstellen, kann sich auf die Systemleistung auswirken. |
| Edge-Segmente pro Sandbox | 150 | Soft | Eine Organisation kann insgesamt über mehr als 150 Edge-Segmente verfügen, sofern in jeder einzelnen Sandbox weniger als 150 Edge-Segmente vorhanden sind. Der Versuch, zusätzliche Edge-Segmente zu erstellen, kann sich negativ auf die Systemleistung auswirken. |
| Streaming-Segmente pro Sandbox | 500 | Soft | Eine Organisation kann insgesamt über mehr als 500 Streaming-Segmente verfügen, sofern in jeder einzelnen Sandbox weniger als 500 Streaming-Segmente vorhanden sind. Der Versuch, zusätzliche Streaming-Segmente zu erstellen, kann sich negativ auf die Systemleistung auswirken. |
| Batch-Segmente pro Sandbox | 4.000 | Soft | Eine Organisation kann insgesamt über mehr als 4000 Batch-Segmente verfügen, sofern in jeder einzelnen Sandbox weniger als 4000 Batch-Segmente vorhanden sind. Der Versuch, zusätzliche Batch-Segmente zu erstellen, kann sich negativ auf die Systemleistung auswirken. |

{style=&quot;table-layout:auto&quot;}

## Anhang

Dieser Abschnitt enthält zusätzliche Details zu den Limits in diesem Dokument.

### Entitätstypen

Das [!DNL Profile]-Datenspeichermodell besteht aus zwei Kernentitätstypen:

* **Primäre Entität:** Eine primäre Entität oder Profilentität führt Daten zu einer „Single Source of Truth“ für einen Kontakt zusammen. Diese einheitlichen Daten werden mithilfe einer so genannten „einheitlichen Ansicht“ dargestellt. Eine einheitliche Ansicht aggregiert die Felder aller Schemas, die dieselbe Klasse implementieren, in ein einziges einheitliches Schema. Das einheitliche Schema für [!DNL Real-Time Customer Profile] ist ein denormalisiertes Hybrid-Datenmodell, das als Container für alle Profilattribute und Verhaltensereignisse fungiert.

   Zeitunabhängige Attribute, auch „Datensatzdaten “genannt, werden mithilfe von [!DNL XDM Individual Profile] modelliert, während die auch als „Ereignisdaten“ bezeichneten Zeitreihendaten mit [!DNL XDM ExperienceEvent] modelliert werden. Wenn Datensatz- und Zeitreihendaten in Adobe Experience Platform aufgenommen werden, dient dies als Trigger für [!DNL Real-Time Customer Profile], um mit der Aufnahme von Daten zu beginnen, die für diese Verwendung aktiviert wurden. Je mehr Interaktionen und Details erfasst werden, desto zuverlässiger werden die einzelnen Profile.

   ![Eine Infografik, in der die Unterschiede zwischen Datensatzdaten und Zeitreihendaten erläutert werden.](images/guardrails/profile-entity.png)

* **Dimensionsentität:** Während der Profildatenspeicher, in dem Profildaten verwaltet werden, kein relativer Speicher ist, ermöglicht das Profil die Integration mit kleinen Dimensionsentitäten, um Segmente auf vereinfachte und intuitive Weise zu erstellen. Diese Integration wird als [Segmentierung mehrerer Entitäten](../segmentation/multi-entity-segmentation.md) bezeichnet. Ihr Unternehmen kann auch XDM-Klassen definieren, um abgesehen von Einzelpersonen auch andere Dinge zu beschreiben, z. B. Geschäfte, Produkte oder Eigenschaften. Diese Nicht-[!DNL XDM Individual Profile]-Schemas werden als „Dimensionsentitäten“ bezeichnet und enthalten keine Zeitreihendaten. Dimensionsentitäten stellen Suchdaten bereit, die Segmentdefinitionen mit mehreren Entitäten unterstützen und vereinfachen. Sie müssen klein genug sein, damit die Segmentierungsmaschine den gesamten Datensatz in den Speicher laden kann, um eine optimale Verarbeitung zu gewährleisten (schnelle Punktsuche).

   ![Eine Infografik, die anzeigt, dass eine Profilentität aus Dimensionentitäten besteht.](images/guardrails/profile-and-dimension-entities.png)

### Profilfragmente

In diesem Dokument gibt es mehrere Leitlinien, die auf „Profilfragmente“ verweisen. In der Experience Platform werden mehrere Profilfragmente zusammengeführt, um das Echtzeit-Kundenprofil zu bilden. Jedes Fragment stellt eine eindeutige primäre Identität und den entsprechenden Datensatz oder vollständigen Satz von Ereignisdaten für diese ID in einem bestimmten Datensatz dar. Weitere Informationen zu Profilfragmenten finden Sie in der [Profilübersicht](home.md#profile-fragments-vs-merged-profiles).

### Zusammenführungsrichtlinien {#merge-policies}

Beim Zusammenführen von Daten aus mehreren Quellen dienen als Zusammenführungsrichtlinien die Regeln, mit denen Platform bestimmt, wie Daten priorisiert werden und welche Daten kombiniert werden sollen, um eine einheitliche Ansicht zu schaffen. Wenn ein Kunde beispielsweise über mehrere Kanäle mit Ihrer Marke interagiert, verfügt Ihre Organisation über mehrere Profilfragmente, die sich auf diesen einzelnen Kunden beziehen und in mehreren Datensätzen enthalten sind. Wenn diese Fragmente in Platform aufgenommen werden, werden sie zusammengeführt, sodass ein zentrales Profil für diesen Kunden entsteht. Wenn die Daten aus mehreren Quellen in Konflikt stehen, bestimmt die Zusammenführungsrichtlinie, welche Informationen in das Profil für die Person aufgenommen werden sollen. Pro Organisation sind maximal fünf (5) Zusammenführungsrichtlinien zulässig. Weitere Informationen zu Zusammenführungsrichtlinien finden Sie in der [Übersicht über Zusammenführungsrichtlinien](merge-policies/overview.md).

### Adobe Analytics Report Suite-Datensätze in Platform {#aa-datasets}

Für Profil können mehrere Report Suites aktiviert werden, solange alle Datenkonflikte gelöst sind. Mit der Funktionalität zur Datenvorbereitung können Sie Datenkonflikte zwischen eVars, Listen und Eigenschaften beheben. Weitere Informationen zur Verwendung der Funktionalität zur Datenvorbereitung finden Sie im [Handbuch zur Adobe Analytics Connector-Benutzeroberfläche](../sources/tutorials/ui/create/adobe-applications/analytics.md).
