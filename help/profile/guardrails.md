---
title: Standardmäßige Leitplanken für Echtzeit-Kundenprofildaten und Segmentierung
solution: Experience Platform
product: experience platform
type: Documentation
description: Erfahren Sie mehr über Leistung und systemerzwungene Schutzmechanismen für Profildaten und die Segmentierung, um eine optimale Nutzung der Funktionalität von Real-Time CDP sicherzustellen.
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
source-git-commit: f5ae9170b312d9f24c863a14b8cc2310fcaf1cb2
workflow-type: tm+mt
source-wordcount: '2668'
ht-degree: 51%

---

# Standard-Leitplanken für [!DNL Real-Time Customer Profile] und Segmentierung

Mit Adobe Experience Platform können Sie personalisierte kanalübergreifende Erlebnisse bereitstellen, die auf verhaltensbezogenen Insights und Kundenattributen in Form von Echtzeit-Kundenprofilen basieren. Um diesen neuen Ansatz bei Profilen zu unterstützen, verwendet Experience Platform ein stark denormalisiertes Hybrid-Datenmodell, das sich vom herkömmlichen relationalen Datenmodell unterscheidet.

>[!IMPORTANT]
>
>Überprüfen Sie zusätzlich zu dieser Seite mit Leitplanken Ihre Lizenzberechtigungen in Ihrem Kundenauftrag und [&#x200B; entsprechenden &#x200B;](https://helpx.adobe.com/de/legal/product-descriptions.html)Produktbeschreibung) die tatsächlichen Nutzungsbeschränkungen.
>
>Alternativ können Sie den [Capacity-Service](../landing/license-usage-and-guardrails/capacity.md) verwenden, um Ihren Streaming-Durchsatz und andere Parameter in Experience Platform zu überwachen und festzulegen.

Dieses Dokument liefert standardmäßige Verwendungs- und Quotenbegrenzungen zur Hilfe bei der Modellierung Ihrer Profildaten, sodass eine optimale System-Performance gewährleistet ist. Bei der Überprüfung der folgenden Leitplanken wird davon ausgegangen, dass Sie die Daten korrekt modelliert haben. Wenden Sie sich bei Fragen zum Modellieren Ihrer Daten an Ihren Kundenbetreuer.

>[!NOTE]
>
>Die meisten Kunden überschreiten diese Standardbeschränkungen nicht. Wenden Sie sich an Ihren Kundenbetreuer, wenn Sie mehr über benutzerdefinierte Beschränkungen erfahren möchten.

## Erste Schritte

Die folgenden Experience Platform-Services sind an der Modellierung von Echtzeit-Kundenprofildaten beteiligt:

* [[!DNL Real-Time Customer Profile]](home.md): Erstellen einheitlicher Verbraucherprofile anhand von Daten aus mehreren Quellen.
* [Identitäten](../identity-service/home.md): Bridge-Identitäten aus unterschiedlichen Datenquellen bei der Aufnahme in Experience Platform.
* [Schemata](../xdm/home.md): Experience-Datenmodell-Schemata (XDM) sind das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
* [Zielgruppen](../segmentation/home.md): Die Segmentierungs-Engine in Experience Platform wird verwendet, um Zielgruppen aus Ihren Kundenprofilen basierend auf Kundenverhalten und -attributen zu erstellen.

## Arten von Beschränkungen

In diesem Dokument gibt es zwei Arten von Standardbeschränkungen:

| Art der Leitplanke | Beschreibung |
| -------------- | ----------- |
| **Leistungs-Schutzmaßnahme (weiches Limit)** | Die Leistung betreffende Leitplanken sind Nutzungsbeschränkungen, die sich auf den Umfang Ihrer Anwendungsfälle beziehen. Beim Überschreiten der Leistungsleitplanken kann es zu Leistungseinbußen und Latenzzeiten kommen. Adobe ist für eine solche Leistungsbeeinträchtigung nicht verantwortlich. Kunden, die ständig eine Leistungsschutzmaßnahme überschreiten, können sich dafür entscheiden, zusätzliche Kapazität zu lizenzieren, um eine Leistungsbeeinträchtigung zu vermeiden. |
| **Vom System erzwungene Leitplanken (feste Grenze)** | Systemerzwungene Leitplanken werden von der Real-Time CDP-Benutzeroberfläche oder -API erzwungen. Dies sind Beschränkungen, die Sie nicht überschreiten können, da die Benutzeroberfläche und die API Sie daran hindern oder einen Fehler zurückgeben. |

{style="table-layout:auto"}

>[!NOTE]
>
>Die in diesem Dokument dargelegten Beschränkungen werden ständig verbessert. Achten Sie regelmäßig auf Updates. Wenden Sie sich an Ihren Kundenbetreuer, wenn Sie mehr über benutzerdefinierte Beschränkungen erfahren möchten.

## Datenmodellbeschränkungen

Die folgenden Leitplanken bieten empfohlene Beschränkungen bei der Modellierung von Echtzeit-Kundenprofildaten. Weitere Informationen zu primären Entitäten und Dimensionsentitäten finden Sie im Abschnitt zu [Entitätstypen](#entity-types) in der Anlage.

![Ein Diagramm mit den verschiedenen Leitplanken für Profildaten in Adobe Experience Platform.](./images/guardrails/profile-guardrails.png)

### Leitplanken für primäre Entitäten

| Leitplanke | Limit | Art von Limit | Beschreibung |
| --------- | ----- | ---------- | ----------- |
| XDM Individual Profile-Klassendatensätze | 20 | Leistungs-Schutzmaßnahme | Es werden maximal 20 Datensätze empfohlen, die die XDM Individual Profile-Klasse nutzen. |
| XDM ExperienceEvent-Klassendatensätze | 20 | Leistungs-Schutzmaßnahme | Es werden maximal 20 Datensätze empfohlen, die die XDM ExperienceEvent-Klasse nutzen. |
| Für Profil aktivierte Adobe Analytics Report Suite-Datensätze | 1 | Leistungs-Schutzmaßnahme | Es sollte maximal ein (1) Analytics Report Suite-Datensatz für Profil aktiviert werden. Der Versuch, mehrere Analytics Report Suite-Datensätze für Profil zu aktivieren, kann unbeabsichtigte Auswirkungen auf die Datenqualität haben. Weitere Informationen finden Sie im Abschnitt zu [Adobe Analytics-Datensätzen](#aa-datasets) im Anhang. |
| Beziehungen mit mehreren Entitäten | 5 | Leistungs-Schutzmaßnahme | Es werden maximal 5 Beziehungen mit mehreren Entitäten empfohlen, die in primären Entitäten oder Dimensionsentitäten definiert sind. Zusätzliche Beziehungszuordnungen sollten erst vorgenommen werden, wenn eine vorhandene Beziehung entfernt oder deaktiviert wurde. |
| JSON-Tiefe für ein ID-Feld, das in Beziehungen mit mehreren Entitäten verwendet wird | 4 | Leistungs-Schutzmaßnahme | Die empfohlene maximale JSON-Tiefe für ein ID-Feld, das in Beziehungen mit mehreren Entitäten verwendet wird, ist 4. Dies bedeutet, dass in einem stark verschachtelten Schema Felder, die mehr als vier Ebenen tief verschachtelt sind, nicht als ID-Felder in einer Beziehung verwendet werden sollten. |
| Array-Kardinalität in einem Profilfragment | &lt;=500 | Leistungs-Schutzmaßnahme | Die optimale Array-Kardinalität in einem Profilfragment (zeitunabhängige Daten) ist &lt;=500. |
| Array-Kardinalität in ExperienceEvent | &lt;=10 | Leistungs-Schutzmaßnahme | Die optimale Array-Kardinalität in ExperienceEvent (Zeitreihendaten) ist &lt;=10. |
| Identitätsanzahl im Identitätsdiagramm eines einzelnen Profils | 50 | Vom System erzwungene Leitplanken | **Die maximale Anzahl von Identitäten in einem Identitätsdiagramm für ein einzelnes Profil ist 50.** Alle Profile mit mehr als 50 Identitäten sind von der Segmentierung, dem Export und der Suche ausgeschlossen. Weitere Informationen finden Sie im Handbuch unter [Grundlagen zur Logik beim Löschen von Identitäten](../identity-service/guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated). |

{style="table-layout:auto"}

### Leitplanken für Dimensionsentitäten

| Leitplanke | Limit | Art von Limit | Beschreibung |
| --------- | ----- | ---------- | ----------- |
| Keine Zeitreihendaten zulässig für Nicht-[!DNL XDM Individual Profile]-Entitäten | 0 | Vom System erzwungene Leitplanken | **Zeitreihendaten sind für Nicht-[!DNL XDM Individual Profile]-Entitäten im Profil-Service nicht zulässig.** Wenn ein Zeitreihen-Datensatz mit einer Nicht-[!DNL XDM Individual Profile]-ID verknüpft ist, sollte der Datensatz nicht für [!DNL Profile] aktiviert sein. |
| Keine verschachtelten Beziehungen | 0 | Leistungs-Schutzmaßnahme | Sie sollten keine Beziehung zwischen zwei Nicht-[!DNL XDM Individual Profile]-Schemata erstellen. Die Möglichkeit, Beziehungen zu erstellen, wird für keine Schemata empfohlen, die nicht Teil des einheitlichen [!DNL Profile]-Schemas sind. |
| JSON-Tiefe für primäres ID-Feld | 4 | Leistungs-Schutzmaßnahme | Die empfohlene maximale JSON-Tiefe für das primäre ID-Feld ist 4. Das bedeutet, dass Sie in einem stark verschachtelten Schema kein Feld als primäre ID auswählen sollten, wenn es mehr als vier Ebenen tief verschachtelt ist. Ein Feld, das sich auf der vierten verschachtelten Ebene befindet, kann als primäre ID verwendet werden. |

{style="table-layout:auto"}

## Datengrößenbeschränkungen

Die folgenden Leitplanken beziehen sich auf die Datengröße und bieten empfohlene Grenzwerte für Daten, die wie vorgesehen aufgenommen, gespeichert und abgefragt werden können. Weitere Informationen zu primären Entitäten und Dimensionsentitäten finden Sie im Abschnitt zu [Entitätstypen](#entity-types) in der Anlage.

>[!NOTE]
>
>Die Datengröße wird an den unkomprimierten Daten in JSON zum Zeitpunkt der Aufnahme gemessen.

### Leitplanken für primäre Entitäten

| Leitplanke | Limit | Art von Limit | Beschreibung |
| --------- | ----- | ---------- | ----------- |
| Maximale ExperienceEvent-Größe | 10 KB | Vom System erzwungene Leitplanken | **Die maximale Größe eines Ereignisses ist 10 KB.** Die Aufnahme wird fortgesetzt, jedoch werden alle Ereignisse, die größer als 10 KB sind, entfernt. |
| Maximale Größe von Profildatensätzen | 100 KB | Vom System erzwungene Leitplanken | **Die maximale Größe eines einzelnen Profildatensatzes ist 100 MB.** Die Aufnahme wird fortgesetzt, jedoch werden Profildatensätze, die größer als 100 KB sind, entfernt. |
| Maximale Größe von Profilfragmenten | 50 MB | Vom System erzwungene Leitplanken | **Die maximale Größe eines einzelnen Profldatensatzes ist 50 MB.** Die Segmentierung, der Export und die Suche können bei [Profilfragmenten](#profile-fragments), die größer als 50 MB sind, fehlschlagen. |
| Maximale Größe gespeicherter Profile | 50 MB | Leistungs-Schutzmaßnahme | **Die maximale Größe eines gespeicherten Profils ist 50 MB.** Das Hinzufügen neuer [Profilfragmente](#profile-fragments) in einem Profil, das größer als 50 MB ist, wirkt sich negativ auf die System-Performance aus. Beispielsweise könnte ein Profil ein einzelnes Fragment mit 50 MB enthalten oder mehrere Fragmente aus mehreren Datensätzen mit einer kombinierten Gesamtgröße von 50 MB. Der Versuch, ein Profil mit einem einzelnen Fragment, das größer als 50 MB ist, oder mit mehreren Fragmenten mit einer kombinierten Größe von mehr als 50 MB zu speichern, wirkt sich negativ auf die System-Performance aus. |
| Anzahl der täglich aufgenommenen Profil- oder ExperienceEvent-Batches | 90 | Leistungs-Schutzmaßnahme | **Die maximale Anzahl von Profil- oder ExperienceEvent-Batches, die pro Tag aufgenommen werden, beträgt 90.** Das bedeutet, dass die Gesamtanzahl der pro Tag aufgenommenen Profil- und ExperienceEvent-Batches 90 nicht überschreiten darf. Das Aufnehmen zusätzlicher Batches beeinträchtigt die System-Performance. |
| Anzahl der ExperienceEvents pro Profildatensatz | 5.000 | Leistungs-Schutzmaßnahme | **Die maximale Anzahl von ExperienceEvents pro Profildatensatz ist 5.000.** Profile mit mehr als 5.000 ExperienceEvents verwenden bei Verwendung mit der Segmentierung nur die **neuesten** 5.000 ExperienceEvents. |

{style="table-layout:auto"}

### Leitplanken für Dimensionsentitäten

| Leitplanke | Limit | Art von Limit | Beschreibung |
| --------- | ----- | ---------- | ----------- |
| Gesamtgröße für alle dimensionalen Entitäten | 5 GB | Leistungs-Schutzmaßnahme | Die empfohlene Gesamtgröße für alle dimensionalen Entitäten beträgt 5 GB. Die Aufnahme großer Dimensionsentitäten kann die System-Performance beeinträchtigen. Es wird beispielsweise nicht empfohlen, einen 10 GB großen Produktkatalog als Dimensionsentität zu laden. |
| Datensätze pro Dimensionsentitätsschema | 5 | Leistungs-Schutzmaßnahme | Es wird empfohlen, maximal 5 Datensätze mit jedem Dimensionsschema zu verknüpfen. Wenn Sie beispielsweise ein Schema für „Produkte“ erstellen und fünf beitragende Datensätze hinzufügen, sollten Sie keinen sechsten Datensatz erstellen, der mit dem Produktschema verknüpft ist. |
| Dimensionsentitäts-Batches, die pro Tag aufgenommen werden | 4 pro Entität | Leistungs-Schutzmaßnahme | Die empfohlene maximale Anzahl von Dimensionsentitäts-Batches, die pro Tag aufgenommen werden, beträgt 4 pro Entität. Sie können beispielsweise Aktualisierungen an einem Produktkatalog bis zu 4-mal täglich aufnehmen. Die Aufnahme zusätzlicher Dimensionsentitäts-Batches für dieselbe Entität kann sich auf die System-Performance auswirken. |

{style="table-layout:auto"}

## Leitplanken für die Segmentierung {#segmentation-guardrails}

Die in diesem Abschnitt beschriebenen Leitplanken beziehen sich auf die Anzahl und Art der Zielgruppen, die ein Unternehmen in Experience Platform erstellen kann, sowie auf die Zuordnung und Aktivierung von Zielgruppen zu Zielen.

| Leitplanke | Limit | Art von Limit | Beschreibung |
| --------- | ----- | ---------- | ----------- |
| Zielgruppen pro Sandbox | 4.000 | Leistungs-Schutzmaßnahme | Pro Sandbox können bis zu 4000 **aktive** Zielgruppen verwendet werden. Pro Organisation können mehr als 4.000 Zielgruppen verwendet werden, sofern in jeder (individuellen) Sandbox **4.000** vorhanden sind. Dies umfasst Batch-, Streaming- und Edge-Zielgruppen. Der Versuch, zusätzliche Zielgruppen zu erstellen, kann sich negativ auf die Systemleistung auswirken. Lesen Sie mehr über [Erstellen von Zielgruppen](/help/segmentation/ui/segment-builder.md) mithilfe von Segment Builder. |
| Edge-Zielgruppen pro Sandbox | 150 | Leistungs-Schutzmaßnahme | Pro Sandbox können bis zu 150 **aktive** Edge-Zielgruppen verwendet werden. Pro Organisation können mehr als 150 Edge-Zielgruppen verwendet werden, sofern in jeder (individuellen) Sandbox **150 Edge** Zielgruppen vorhanden sind. Der Versuch, zusätzliche Edge-Zielgruppen zu erstellen, kann sich negativ auf die Systemleistung auswirken. Weitere Informationen zu [Edge-Zielgruppen](/help/segmentation/methods/edge-segmentation.md). |
| Edge-Durchsatz über alle Sandboxes hinweg | 1500 RPS | Leistungs-Schutzmaßnahme | Die Edge-Segmentierung unterstützt einen kombinierten Spitzenwert von 1.500 eingehenden Ereignissen pro Sekunde, die über Ihre Produktions- und Entwicklungs-Sandboxes hinweg in die Adobe Experience Platform Edge Network eintreten. Die Segmentierung in Edge kann bis zu 350 Millisekunden dauern, um ein eingehendes Ereignis zu verarbeiten, nachdem es in die Adobe Experience Platform Edge Network gelangt ist. Weitere Informationen zu [Edge-Zielgruppen](/help/segmentation/methods/edge-segmentation.md). |
| Streaming-Zielgruppen pro Sandbox | 500 | Leistungs-Schutzmaßnahme | Pro Sandbox können bis zu 500 **aktive** Streaming-Zielgruppen verwendet werden. Pro Organisation können mehr als 500 Streaming-Zielgruppen verwendet werden, sofern in jeder **-Sandbox weniger als 500 Streaming** Zielgruppen vorhanden sind. Dies umfasst sowohl Streaming- als auch Edge-Zielgruppen. Der Versuch, zusätzliche Streaming-Zielgruppen zu erstellen, kann sich negativ auf die Systemleistung auswirken. Weitere Informationen über [Streaming-Zielgruppen](/help/segmentation/methods/streaming-segmentation.md). |
| Streaming-Durchsatz über alle Sandboxes hinweg | 1500 RPS | Leistungs-Schutzmaßnahme | Die Streaming-Segmentierung unterstützt einen kombinierten Spitzenwert von 1500 eingehenden Ereignissen pro Sekunde in Ihren Produktions- und Entwicklungs-Sandboxes. Es kann bis zu 5 Minuten dauern, bis ein Profil für die Segmentzugehörigkeit qualifiziert ist. Weitere Informationen über [Streaming-Zielgruppen](/help/segmentation/methods/streaming-segmentation.md). |
| Batch-Zielgruppen pro Sandbox | 4.000 | Leistungs-Schutzmaßnahme | Pro Sandbox können bis zu 4000 **aktive** Batch-Zielgruppen verwendet werden. Pro Organisation können mehr als 4.000 Batch-Zielgruppen verwendet werden, sofern in jeder (individuellen) Sandbox **4.000 Batch** Zielgruppen vorhanden sind. Der Versuch, zusätzliche Batch-Zielgruppen zu erstellen, kann sich negativ auf die Systemleistung auswirken. |
| Konto-Zielgruppen pro Sandbox | 50 | Vom System erzwungene Leitplanken | Sie können in einer Sandbox maximal 50 Konto-Zielgruppen erstellen. Nachdem Sie 50 Zielgruppen in einer Sandbox erreicht haben, wird das Steuerelement **[!UICONTROL Zielgruppe erstellen]** beim Erstellen einer neuen Konto-Zielgruppe deaktiviert. Lesen Sie mehr über [Account-Zielgruppen](/help/segmentation/types/account-audiences.md). |
| Veröffentlichte Kompositionen pro Sandbox | 10 | Leistungs-Schutzmaßnahme | Sie können maximal 10 veröffentlichte Kompositionen in einer Sandbox haben. Weitere Informationen zur [Audience-Komposition“ finden Sie im Handbuch zur Benutzeroberfläche](/help/segmentation/ui/audience-composition.md). **Hinweis**: Mit Federated Audience Komposition erstellte Kompositionen werden **nicht** mit dieser Leitplanke gezählt. |
| Maximale Zielgruppengröße | 30 Prozent | Leistungs-Schutzmaßnahme | Die empfohlene maximale Mitgliedschaft einer Zielgruppe beträgt 30 % der Gesamtzahl der Profile im System. Das Erstellen von Zielgruppen mit mehr als 30 % der Profile als Mitglieder oder mit mehreren großen Zielgruppen ist möglich, wirkt sich jedoch auf die Systemleistung aus. |
| Flexible Auswertungsdurchgänge für Zielgruppen | 50 pro Jahr (Produktions-Sandbox)<br/>100 pro Jahr (Entwicklungs-Sandbox) | Vom System erzwungene Leitplanken | Sie haben pro Jahr maximal 50 flexible Zielgruppenauswertungsdurchgänge pro (Produktions-)**Sandbox**. Sie haben pro Jahr maximal 100 flexible Zielgruppenauswertungsdurchgänge pro Sandbox **Entwicklung**. |
| Flexible Auswertungsdurchgänge für Zielgruppen | 2 pro Tag | Vom System erzwungene Leitplanken | Sie haben maximal 2 Ausführungen pro Tag pro Sandbox. |
| Zielgruppen pro flexibler Ausführung der Zielgruppenevaluierung | 20 | Vom System erzwungene Leitplanken | Pro Ausführung der flexiblen Zielgruppenauswertung können maximal 20 Zielgruppen erstellt werden. |

{style="table-layout:auto"}

## Erwartete Verfügbarkeit

Im folgenden Abschnitt wird die **erwartete** Verfügbarkeit für Zielgruppen und Zusammenführungsrichtlinien in nachgelagerten Services wie Real-Time CDP-Zielen beschrieben:

| Sandbox-Typ | Zeit |
| ------------ | ---- |
| Vorhandene Sandboxes | 1 Stunde |
| Neue Sandboxes | 2 Stunden |
| Neu zurückgesetzte Sandboxes | 2 Stunden |

{style="table-layout:auto"}

## Anhang

Dieser Abschnitt enthält zusätzliche Details zu den Limits in diesem Dokument.

### Entitätstypen

Das [!DNL Profile] besteht aus zwei Kernentitätstypen: [primäre Entitäten](#primary-entity) und [Dimensionsentitäten](#dimension-entity).

#### Primäre Entität

Eine primäre Entität oder Profilentität führt Daten zu einer „Single Source of Truth“ für einen Kontakt zusammen. Diese einheitlichen Daten werden mithilfe einer so genannten „einheitlichen Ansicht“ dargestellt. Eine einheitliche Ansicht aggregiert die Felder aller Schemata, die dieselbe Klasse implementieren, in ein einziges einheitliches Schema. Das einheitliche Schema für [!DNL Real-Time Customer Profile] ist ein denormalisiertes Hybrid-Datenmodell, das als Container für alle Profilattribute und Verhaltensereignisse fungiert.

Zeitunabhängige Attribute, auch „Datensatzdaten “genannt, werden mithilfe von [!DNL XDM Individual Profile] modelliert, während die auch als „Ereignisdaten“ bezeichneten Zeitreihendaten mit [!DNL XDM ExperienceEvent] modelliert werden. Wenn Datensatz- und Zeitreihendaten in Adobe Experience Platform aufgenommen werden, dient dies als Trigger für [!DNL Real-Time Customer Profile], um mit der Aufnahme von Daten zu beginnen, die für diese Verwendung aktiviert wurden. Je mehr Interaktionen und Details erfasst werden, desto zuverlässiger werden die einzelnen Profile.

![Eine Infografik, die die Unterschiede zwischen Datensatzdaten und Zeitreihendaten aufzeigt.](images/guardrails/profile-entity.png)

#### Dimension-Entität

Während der Profildatenspeicher, in dem Profildaten verwaltet werden, kein relativer Speicher ist, ermöglicht das Profil die Integration mit kleinen Dimensionsentitäten, um Zielgruppen auf vereinfachte und intuitive Weise zu erstellen. Diese Integration wird als [Segmentierung mehrerer Entitäten“ &#x200B;](../segmentation/tutorials/multi-entity-segmentation.md).

Ihr Unternehmen kann auch XDM-Klassen definieren, um abgesehen von Einzelpersonen auch andere Dinge zu beschreiben, z. B. Geschäfte, Produkte oder Eigenschaften. Diese Schemata, die mit anderen XDM-Klassen als der Klasse „XDM Individual Profile“ modelliert werden, werden als „Dimensionsentitäten“ (auch „Lookup-Entitäten“ genannt) bezeichnet und enthalten keine Zeitreihendaten. Schemata, die Dimensionsentitäten darstellen, werden durch die Verwendung von [Schemabeziehungen) mit Profilentitäten &#x200B;](../xdm/tutorials/relationship-ui.md).

Dimensionsentitäten stellen Suchdaten bereit, die Segmentdefinitionen mit mehreren Entitäten unterstützen und vereinfachen. Sie müssen klein genug sein, damit die Segmentierungsmaschine den gesamten Datensatz in den Speicher laden kann, um eine optimale Verarbeitung zu gewährleisten (schnelle Punktsuche).

![Eine Infografik, die zeigt, dass eine Profilentität aus Dimensionsentitäten besteht.](images/guardrails/profile-and-dimension-entities.png)

### Profilfragmente

In diesem Dokument gibt es mehrere Leitplanken, die sich auf „Profilfragmente“ beziehen. In Experience Platform werden mehrere Profilfragmente zusammengeführt, um das Echtzeit-Kundenprofil zu bilden. Jedes Fragment stellt eine eindeutige primäre Identität und den entsprechenden Datensatz oder vollständigen Satz von Ereignisdaten für diese ID in einem bestimmten Datensatz dar. Weitere Informationen zu Profilfragmenten finden Sie in der [Profilübersicht](home.md#profile-fragments-vs-merged-profiles).

### Zusammenführungsrichtlinien {#merge-policies}

Beim Zusammenführen von Daten aus mehreren Quellen dienen Zusammenführungsrichtlinien als jene Regeln, mit denen Experience Platform bestimmt, wie Daten priorisiert werden und welche Daten kombiniert werden sollen, um eine Übersicht zu schaffen. Wenn ein Kunde beispielsweise über mehrere Kanäle mit Ihrer Marke interagiert, verfügt Ihre Organisation über mehrere Profilfragmente, die sich auf diesen einzelnen Kunden beziehen und in mehreren Datensätzen enthalten sind. Wenn diese Fragmente in Experience Platform aufgenommen werden, werden sie zusammengeführt, sodass ein einziges Profil für diesen Kunden entsteht. Wenn die Daten aus mehreren Quellen in Konflikt stehen, bestimmt die Zusammenführungsrichtlinie, welche Informationen in das Profil für die Person aufgenommen werden sollen. Pro Sandbox sind maximal fünf (5) Zusammenführungsrichtlinien zulässig, die das `_xdm.context.profile`-Schema verwenden. Weitere Informationen zu Zusammenführungsrichtlinien finden Sie in der [Übersicht über Zusammenführungsrichtlinien](merge-policies/overview.md).

### Adobe Analytics Report Suite-Datensätze in Experience Platform {#aa-datasets}

Für Profil können mehrere Report Suites aktiviert werden, solange alle Datenkonflikte gelöst sind. Mit der Funktionalität zur Datenvorbereitung können Sie Datenkonflikte zwischen eVars, Listen und Eigenschaften beheben. Weitere Informationen zur Verwendung der Funktionalität zur Datenvorbereitung finden Sie im [Handbuch zur Adobe Analytics Connector-Benutzeroberfläche](../sources/tutorials/ui/create/adobe-applications/analytics.md).

## Nächste Schritte

In der folgenden Dokumentation finden Sie weitere Informationen zu anderen Experience Platform-Services-Leitplanken, zu End-to-End-Latenzinformationen und Lizenzinformationen aus Real-Time CDP-Produktbeschreibungsdokumenten:

* [Real-Time CDP-Leitplanken](/help/rtcdp/guardrails/overview.md)
* [End-to-End-Latenzdiagramme](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=de#end-to-end-latency-diagrams) für verschiedene Experience Platform-Services.
* [Real-Time Customer Data Platform (B2C Edition - Prime- und Ultimate-Pakete)](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2P - Prime- und Ultimate-Pakete)](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B - Prime- und Ultimate-Pakete)](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
