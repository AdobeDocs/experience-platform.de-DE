---
keywords: Profil;Echtzeit-Kundenprofil;Fehlerbehebung;Leitplanken;Richtlinien;Limit;Entität;primäre Entität;Dimensionsentität;RTCDP;CDP;B2B edition;Real-Time Customer Data Platform;Real-time Customer Data Platform;Real-time CDP;B2B;CDP;
title: Standard-Leitplanken für Real-Time Customer Data Platform B2B edition
type: Documentation
description: Adobe Experience Platform verwendet ein stark denormalisiertes Hybrid-Datenmodell, das sich vom herkömmlichen relationalen Datenmodell unterscheidet. Dieses Dokument enthält standardmäßige Verwendungs- und Ratenbeschränkungen, mit denen Sie Ihre Daten für eine optimale Systemleistung mit Adobe Real-Time Customer Data Platform B2B edition modellieren können.
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
feature: Guardrails, B2B
exl-id: 8eff8c3f-a250-4aec-92a1-719ce4281272
source-git-commit: bc399f3af0524232671af780ea1380f1a71a5b7e
workflow-type: tm+mt
source-wordcount: '1817'
ht-degree: 46%

---

# Standard-Leitplanken für Real-Time Customer Data Platform B2B edition

>[!NOTE]
>
>Die in diesem Dokument beschriebenen Einschränkungen stellen die von Real-Time Customer Data Platform B2B edition aktivierten Änderungen dar. Um eine vollständige Liste der standardmäßigen Beschränkungen für Real-Time CDP B2B edition zu erhalten, kombinieren Sie diese Beschränkungen mit den allgemeinen Beschränkungen für Adobe Experience Platform[ die in der Dokumentation zu Leitplanken für Echtzeit-Kundenprofildaten beschrieben ](../profile/guardrails.md).

Mit Real-Time Customer Data Platform B2B edition können Sie personalisierte kanalübergreifende Erlebnisse bereitstellen, die auf verhaltensbezogenen Insights und Kundenattributen in Form von Echtzeit-Kundenprofilen und Account-Profilen basieren. Um diesen neuen Ansatz bei Profilen zu unterstützen, verwendet Experience Platform ein stark denormalisiertes Hybrid-Datenmodell, das sich vom herkömmlichen relationalen Datenmodell unterscheidet.

>[!IMPORTANT]
>
>Überprüfen Sie zusätzlich zu dieser Seite mit Leitplanken Ihre Lizenzberechtigungen in Ihrem Kundenauftrag und [ entsprechenden ](https://helpx.adobe.com/de/legal/product-descriptions.html)Produktbeschreibung) die tatsächlichen Nutzungsbeschränkungen.

Dieses Dokument enthält standardmäßige Verwendungs- und Ratenbeschränkungen, die Ihnen helfen, Ihre Daten für eine optimale System-Performance zu modellieren. Bei der Überprüfung der folgenden Leitplanken wird davon ausgegangen, dass Sie die Daten korrekt modelliert haben. Wenden Sie sich bei Fragen zum Modellieren Ihrer Daten an Ihren Kundenbetreuer.

>[!INFO]
>
>Die meisten Kunden überschreiten diese Standardbeschränkungen nicht. Wenden Sie sich an Ihren Kundenbetreuer, wenn Sie mehr über benutzerdefinierte Beschränkungen erfahren möchten.

## Arten von Beschränkungen

In diesem Dokument gibt es zwei Arten von Standardbeschränkungen:

| Art der Leitplanke | Beschreibung |
| -------------- | ----------- |
| **Leistungs-Schutzmaßnahme (weiches Limit)** | Die Leistung betreffende Leitplanken sind Nutzungsbeschränkungen, die sich auf den Umfang Ihrer Anwendungsfälle beziehen. Beim Überschreiten der Leistungsleitplanken kann es zu Leistungseinbußen und Latenzzeiten kommen. Adobe ist für eine solche Leistungsbeeinträchtigung nicht verantwortlich. Kunden, die ständig eine Leistungsschutzmaßnahme überschreiten, können sich dafür entscheiden, zusätzliche Kapazität zu lizenzieren, um eine Leistungsbeeinträchtigung zu vermeiden. |
| **Vom System erzwungene Leitplanken (feste Grenze)** | Systemerzwungene Leitplanken werden von der Real-Time CDP-Benutzeroberfläche oder -API erzwungen. Dies sind Beschränkungen, die Sie nicht überschreiten können, da die Benutzeroberfläche und die API Sie daran hindern oder einen Fehler zurückgeben. |

>[!INFO]
>
>Die in diesem Dokument dargelegten Beschränkungen werden ständig verbessert. Achten Sie regelmäßig auf Updates. Wenden Sie sich an Ihren Kundenbetreuer, wenn Sie mehr über benutzerdefinierte Beschränkungen erfahren möchten.

## Datenmodellbeschränkungen

Die folgenden Leitplanken bieten empfohlene Beschränkungen bei der Modellierung von Echtzeit-Kundenprofildaten. Weitere Informationen zu primären Entitäten und Dimensionsentitäten finden Sie im Abschnitt zu [Entitätstypen](#entity-types) in der Anlage.

### Leitplanken für primäre Entitäten

>[!NOTE]
>
>Die in diesem Abschnitt beschriebenen Datenmodellbeschränkungen stellen die Änderungen dar, die von Real-Time Customer Data Platform B2B edition aktiviert werden. Um eine vollständige Liste der standardmäßigen Beschränkungen für Real-Time CDP B2B edition zu erhalten, kombinieren Sie diese Beschränkungen mit den allgemeinen Beschränkungen für Adobe Experience Platform[ die in der Dokumentation zu Leitplanken für Echtzeit-Kundenprofildaten beschrieben ](../profile/guardrails.md).

| Leitplanke | Limit | Art von Limit | Beschreibung |
| --------- | ----- | ---------- | ----------- |
| Real-Time CDP B2B edition Standard-XDM-Klassendatensätze | 60 | Leistungs-Schutzmaßnahme | Es werden maximal 60 Datensätze empfohlen, die die standardmäßigen Experience-Datenmodell (XDM)-Klassen nutzen, die von Real-Time CDP B2B edition bereitgestellt werden. Eine vollständige Liste der Standard-XDM-Klassen für B2B-Anwendungsfälle finden Sie im Abschnitt [Schemata in der Dokumentation zu Real-Time CDP B2B edition](schemas/b2b.md). <br/><br/>*Hinweis: Aufgrund der Beschaffenheit des denormalisierten Hybrid-Datenmodells von Experience Platform überschreiten die meisten Kunden diese Grenze nicht. Wenden Sie sich an Ihren Kundenbetreuer, wenn Sie Fragen zur Datenmodellierung haben oder mehr über benutzerdefinierte Limits erfahren möchten.* |
| Anzahl der Identitäten eines einzelnen Kontos in einem Identitätsdiagramm | 50 | Leistungs-Schutzmaßnahme | Die maximale Anzahl von Identitäten in einem Identitätsdiagramm für ein einzelnes Konto ist 50. Alle Profile mit mehr als 50 Identitäten sind von der Segmentierung, dem Export und der Suche ausgeschlossen. |
| Alte Beziehungen mit mehreren Entitäten | 20 | Leistungs-Schutzmaßnahme | Es werden maximal 20 Beziehungen mit mehreren Entitäten empfohlen, die in primären Entitäten oder Dimensionsentitäten definiert sind. Zusätzliche Beziehungszuordnungen sollten erst vorgenommen werden, wenn eine vorhandene Beziehung entfernt oder deaktiviert wurde. |
| Viele-zu-eins-Beziehungen pro XDM-Klasse | 2 | Leistungs-Schutzmaßnahme | Es wird empfohlen, pro XDM-Klasse maximal zwei Viele-zu-eins-Beziehungen zu definieren. Zusätzliche Beziehungen sollten erst dann hergestellt werden, wenn eine vorhandene Beziehung entfernt oder deaktiviert wurde. Anweisungen zum Erstellen einer Beziehung zwischen zwei Schemata finden Sie im Tutorial zum [Erstellen von B2B-Schemabeziehungen](../xdm/tutorials/relationship-b2b.md). |

### Leitplanken für Dimensionsentitäten

>[!NOTE]
>
>Die in diesem Abschnitt beschriebenen Datenmodellbeschränkungen stellen die Änderungen dar, die von Real-Time Customer Data Platform B2B edition aktiviert werden. Um eine vollständige Liste der standardmäßigen Beschränkungen für Real-Time CDP B2B edition zu erhalten, kombinieren Sie diese Beschränkungen mit den allgemeinen Beschränkungen für Adobe Experience Platform[ die in der Dokumentation zu Leitplanken für Echtzeit-Kundenprofildaten beschrieben ](../profile/guardrails.md).

| Leitplanke | Limit | Art von Limit | Beschreibung |
| --------- | ----- | ---------- | ----------- |
| Keine verschachtelten Legacy-Beziehungen | 0 | Leistungs-Schutzmaßnahme | Sie sollten keine Beziehung zwischen zwei Nicht-[!DNL XDM Individual Profile]-Schemata erstellen. Das Erstellen von **wird** allen Schemata empfohlen, die nicht Teil des [!DNL Profile]-Vereinigungsschemas sind. |
| Nur B2B-Objekte können Teil von Viele-zu-eins-Beziehungen sein | 0 | Vom System erzwungene Leitplanken | Das System unterstützt nur Viele-zu-Eins-Beziehung zwischen B2B-Objekten. Weiterführende Informationen zu Viele-zu-Eins-Beziehungen finden Sie im Tutorial zum [Definieren von B2B-Schemabeziehungen](../xdm/tutorials/relationship-b2b.md). |
| Maximale Tiefe verschachtelter Beziehungen zwischen B2B-Objekten | 3 | Vom System erzwungene Leitplanken | Die maximale Tiefe verschachtelter Beziehungen zwischen B2B-Objekten beträgt 3. Das bedeutet, dass Sie in einem hochverschachtelten Schema keine Beziehung zwischen B2B-Objekten haben sollten, die mehr als drei Ebenen tief verschachtelt sind. |
| Einzelnes Schema für jede Dimensionseinheit | 1 | Vom System erzwungene Leitplanken | Jede Dimensionsentität muss über ein einzelnes Schema verfügen. Der Versuch, Dimensionsentitäten zu verwenden, die aus mehr als einem Schema erstellt wurden, kann sich auf die Segmentierungsergebnisse auswirken. Für verschiedene Dimensionsentitäten werden separate Schemata erwartet. |

## Datengrößenbeschränkungen

Die folgenden Leitplanken beziehen sich auf die Datengröße und bieten empfohlene Grenzwerte für Daten, die wie vorgesehen aufgenommen, gespeichert und abgefragt werden können. Weitere Informationen zu primären Entitäten und Dimensionsentitäten finden Sie im Abschnitt zu [Entitätstypen](#entity-types) in der Anlage.

>[!INFO]
>
>Die Datengröße wird an den unkomprimierten Daten in JSON zum Zeitpunkt der Aufnahme gemessen.

### Leitplanken für primäre Entitäten

>[!NOTE]
>
>Die in diesem Abschnitt beschriebenen Datengrößenbeschränkungen stellen die von Real-Time Customer Data Platform B2B edition aktivierten Änderungen dar. Um eine vollständige Liste der standardmäßigen Beschränkungen für Real-Time CDP B2B edition zu erhalten, kombinieren Sie diese Beschränkungen mit den allgemeinen Beschränkungen für Adobe Experience Platform[ die in der Dokumentation zu Leitplanken für Echtzeit-Kundenprofildaten beschrieben ](../profile/guardrails.md).

| Leitplanke | Limit | Art von Limit | Beschreibung |
| --------- | ----- | ---------- | ----------- |
| Batches, die pro XDM-Klasse pro Tag aufgenommen werden | 45 | Leistungs-Schutzmaßnahme | Die Gesamtanzahl der täglich pro XDM-Klasse aufgenommenen Batches sollte 45 nicht überschreiten. Die Aufnahme zusätzlicher Batches kann die optimale Performance verringern. |

### Leitplanken für Dimensionsentitäten

>[!NOTE]
>
>Die in diesem Abschnitt beschriebenen Datengrößenbeschränkungen stellen die von Real-Time Customer Data Platform B2B edition aktivierten Änderungen dar. Um eine vollständige Liste der standardmäßigen Beschränkungen für Real-Time CDP B2B edition zu erhalten, kombinieren Sie diese Beschränkungen mit den allgemeinen Beschränkungen für Adobe Experience Platform[ die in der Dokumentation zu Leitplanken für Echtzeit-Kundenprofildaten beschrieben ](../profile/guardrails.md).

| Leitplanke | Limit | Art von Limit | Beschreibung |
| --------- | ----- | ---------- | ----------- |
| Gesamtgröße für alle dimensionalen Entitäten | 5 GB | Leistungs-Schutzmaßnahme | Die empfohlene Gesamtgröße für alle dimensionalen Entitäten beträgt 5 GB. Die Aufnahme großer Dimensionsentitäten kann die System-Performance beeinträchtigen. Es wird beispielsweise nicht empfohlen, einen 10 GB großen Produktkatalog als Dimensionsentität zu laden. |
| Datensätze pro Dimensionsentitätsschema | 5 | Leistungs-Schutzmaßnahme | Es wird empfohlen, maximal 5 Datensätze mit jedem Dimensionsschema zu verknüpfen. Wenn Sie beispielsweise ein Schema für „Produkte“ erstellen und fünf beitragende Datensätze hinzufügen, sollten Sie keinen sechsten Datensatz erstellen, der mit dem Produktschema verknüpft ist. |
| Dimensionsentitäts-Batches, die pro Tag aufgenommen werden | 4 pro Entität | Leistungs-Schutzmaßnahme | Die empfohlene maximale Anzahl von Dimensionsentitäts-Batches, die pro Tag aufgenommen werden, beträgt 4 pro Entität. Sie können beispielsweise Aktualisierungen an einem Produktkatalog bis zu 4-mal täglich aufnehmen. Die Aufnahme zusätzlicher Dimensionsentitäts-Batches für dieselbe Entität kann sich auf die System-Performance auswirken. |

## Leitplanken für die Segmentierung

Die in diesem Abschnitt beschriebenen Leitplanken beziehen sich auf die Anzahl und Art der Zielgruppen, die ein Unternehmen in Experience Platform erstellen kann, sowie auf die Zuordnung und Aktivierung von Zielgruppen zu Zielen.

>[!NOTE]
>
>Die in diesem Abschnitt beschriebenen Segmentierungsbeschränkungen stellen die von Real-Time Customer Data Platform B2B edition aktivierten Änderungen dar. Um eine vollständige Liste der standardmäßigen Beschränkungen für Real-Time CDP B2B edition zu erhalten, kombinieren Sie diese Beschränkungen mit den allgemeinen Beschränkungen für Adobe Experience Platform[ die in der Dokumentation zu Leitplanken für Echtzeit-Kundenprofildaten beschrieben ](../profile/guardrails.md).

| Leitplanke | Limit | Art von Limit | Beschreibung |
| --------- | ----- | ---------- | ----------- |
| Segmentdefinitionen pro B2B-Sandbox | 400 | Leistungs-Schutzmaßnahme | Eine Organisation kann insgesamt über mehr als 400 Segmentdefinitionen verfügen, sofern in jeder einzelnen B2B-Sandbox weniger als 400 Segmentdefinitionen vorhanden sind. Der Versuch, zusätzliche Segmentdefinitionen zu erstellen, kann sich negativ auf die Systemleistung auswirken. |

## Nächste Schritte

Die in diesem Dokument beschriebenen Einschränkungen stellen die von Real-Time Customer Data Platform B2B edition aktivierten Änderungen dar. Um eine vollständige Liste der standardmäßigen Beschränkungen für Real-Time CDP B2B edition zu erhalten, kombinieren Sie diese Beschränkungen mit den allgemeinen Beschränkungen für Adobe Experience Platform[ die in der Dokumentation zu Leitplanken für Echtzeit-Kundenprofildaten beschrieben ](../profile/guardrails.md).

## Anhang

Dieser Abschnitt enthält zusätzliche Details zu den Limits in diesem Dokument.

### Entitätstypen

Das [!DNL Profile] besteht aus zwei Kernentitätstypen: [primäre Entitäten](#primary-entity) und [Dimensionsentitäten](#dimension-entity).

#### Primäre Entität

Eine primäre Entität oder Profilentität führt Daten zu einer „Single Source of Truth“ für einen Kontakt zusammen. Diese einheitlichen Daten werden mithilfe einer so genannten „einheitlichen Ansicht“ dargestellt. Eine einheitliche Ansicht aggregiert die Felder aller Schemata, die dieselbe Klasse implementieren, in ein einziges einheitliches Schema. Das einheitliche Schema für [!DNL Real-Time Customer Profile] ist ein denormalisiertes Hybrid-Datenmodell, das als Container für alle Profilattribute und Verhaltensereignisse fungiert.

Zeitunabhängige Attribute, auch „Datensatzdaten “genannt, werden mithilfe von [!DNL XDM Individual Profile] modelliert, während die auch als „Ereignisdaten“ bezeichneten Zeitreihendaten mit [!DNL XDM ExperienceEvent] modelliert werden. Wenn Datensatz- und Zeitreihendaten in Adobe Experience Platform aufgenommen werden, dient dies als Trigger für [!DNL Real-Time Customer Profile], um mit der Aufnahme von Daten zu beginnen, die für diese Verwendung aktiviert wurden. Je mehr Interaktionen und Details erfasst werden, desto zuverlässiger werden die einzelnen Profile.

![Eine Infografik, die die Unterschiede zwischen Datensatzdaten und Zeitreihendaten aufzeigt.](../profile/images/guardrails/profile-entity.png)

#### Dimension-Entität

Während der Profildatenspeicher, in dem Profildaten verwaltet werden, kein relativer Speicher ist, ermöglicht das Profil die Integration mit kleinen Dimensionsentitäten, um Zielgruppen auf vereinfachte und intuitive Weise zu erstellen. Diese Integration wird als [Segmentierung mehrerer Entitäten“ ](../segmentation/tutorials/multi-entity-segmentation.md).

Ihr Unternehmen kann auch XDM-Klassen definieren, um abgesehen von Einzelpersonen auch andere Dinge zu beschreiben, z. B. Geschäfte, Produkte oder Eigenschaften. Diese nicht [!DNL XDM Individual Profile] Schemata werden als „Dimensionsentitäten“ (auch als „Lookup-Entitäten“ bezeichnet) bezeichnet und enthalten keine Zeitreihendaten. Schemata, die Dimensionsentitäten darstellen, werden durch die Verwendung von [Schemabeziehungen) mit Profilentitäten ](../xdm/tutorials/relationship-ui.md).

Dimensionsentitäten stellen Suchdaten bereit, die Segmentdefinitionen mit mehreren Entitäten unterstützen und vereinfachen. Sie müssen klein genug sein, damit die Segmentierungsmaschine den gesamten Datensatz in den Speicher laden kann, um eine optimale Verarbeitung zu gewährleisten (schnelle Punktsuche).

![Eine Infografik, die zeigt, dass eine Profilentität aus Dimensionsentitäten besteht.](../profile/images/guardrails/profile-and-dimension-entities.png)
