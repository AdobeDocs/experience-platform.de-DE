---
keywords: profile; Echtzeit-Kundenprofil; Fehlerbehebung; Limits; Richtlinien; Grenze; Entität; primäre Entität; Dimensionentität; RTCDP; CDP; B2B Edition; Real-time Customer Data Platform; Echtzeit-Kundendatenplattform; Echtzeit-Kundendatenplattform; b2b; cdp;
title: Standardmäßige Limits für Real-time Customer Data Platform B2B Edition
type: Documentation
description: 'Adobe Experience Platform verwendet ein stark denormalisiertes Hybrid-Datenmodell, das sich vom herkömmlichen relationalen Datenmodell unterscheidet. Dieses Dokument enthält standardmäßige Verwendungs- und Ratenbeschränkungen, mit denen Sie Ihre Daten für eine optimale Systemleistung mit Real-time Customer Data Platform B2B Edition modellieren können. '
source-git-commit: 7b9b01657ab2a682b900a8c55a201f9864e4428b
workflow-type: tm+mt
source-wordcount: '1601'
ht-degree: 1%

---


# Standardmäßige Limits für Real-time Customer Data Platform B2B Edition

>[!NOTE]
>
>Die in diesem Dokument beschriebenen Einschränkungen stellen die von Real-time Customer Data Platform B2B Edition aktivierten Änderungen dar. Für eine vollständige Liste der Standardbeschränkungen für die Echtzeit-Kundendatenplattform B2B Edition kombinieren Sie diese Beschränkungen mit den allgemeinen Adobe Experience Platform-Beschränkungen, die im Abschnitt [Limits für die Dokumentation zu Echtzeit-Kundenprofil-Daten](../profile/guardrails.md).

Mit der Real-time Customer Data Platform B2B Edition können Sie personalisierte kanalübergreifende Erlebnisse bereitstellen, die auf verhaltensbezogenen Einblicken und Kundenattributen in Form von Echtzeit-Kundenprofilen und Kontoprofilen basieren. Um diesen neuen Profilansatz zu unterstützen, verwendet Experience Platform ein stark denormalisiertes Hybrid-Datenmodell, das sich vom herkömmlichen relationalen Datenmodell unterscheidet.

Dieses Dokument enthält standardmäßige Verwendungs- und Ratenbeschränkungen, die Ihnen helfen, Ihre Daten für eine optimale Systemleistung zu modellieren. Bei der Überprüfung der folgenden Limits wird davon ausgegangen, dass Sie die Daten korrekt modelliert haben. Wenden Sie sich bei Fragen zum Modellieren Ihrer Daten an Ihren Kundenbetreuer.

>[!INFO]
>
>Die meisten Kunden überschreiten diese Standardbeschränkungen nicht. Wenden Sie sich an Ihren Kundenbetreuer, wenn Sie mehr über benutzerdefinierte Beschränkungen erfahren möchten.

## Begrenzungstypen

In diesem Dokument gibt es zwei Arten von Standardbeschränkungen:

* **Softlimit:** Es ist möglich, über eine weiche Grenze hinauszugehen, jedoch bieten weiche Begrenzungen eine empfohlene Richtlinie für die Systemleistung.

* **Hardlimit:** Eine feste Begrenzung bietet ein absolutes Maximum.

>[!INFO]
>
>Die in diesem Dokument festgelegten Grenzen werden ständig verbessert. Prüfen Sie regelmäßig nach Updates. Wenden Sie sich an Ihren Kundenbetreuer, wenn Sie mehr über benutzerdefinierte Beschränkungen erfahren möchten.

## Datenmodellbeschränkungen

Die folgenden Limits bieten empfohlene Einschränkungen bei der Modellierung von Echtzeit-Kundenprofildaten. Weitere Informationen zu primären Entitäten und Dimensionentitäten finden Sie im Abschnitt zu [Entitätstypen](#entity-types) in der Anlage.

### Limits Primärer Entitäten

>[!NOTE]
>
>Die in diesem Abschnitt beschriebenen Datenmodellbeschränkungen stellen die von Real-time Customer Data Platform B2B Edition aktivierten Änderungen dar. Für eine vollständige Liste der Standardbeschränkungen für die Echtzeit-Kundendatenplattform B2B Edition kombinieren Sie diese Beschränkungen mit den allgemeinen Adobe Experience Platform-Beschränkungen, die im Abschnitt [Limits für die Dokumentation zu Echtzeit-Kundenprofil-Daten](../profile/guardrails.md).

| Guardrail | Limit | Begrenzungstyp | Beschreibung |
| --- | --- | --- | --- |
| Standard-XDM-Klassendatensätze der Echtzeit-CDP B2B Edition | 60 | Soft | Es wird empfohlen, maximal 60 Datensätze zu verwenden, die die standardmäßigen Experience-Datenmodell (XDM)-Klassen nutzen, die von der Echtzeit-Kundendatenplattform B2B Edition bereitgestellt werden. Eine vollständige Liste der Standard-XDM-Klassen für B2B-Anwendungsfälle finden Sie im Abschnitt [Schemas in der Dokumentation zur Echtzeit-Kundendatenplattform B2B Edition](schemas/b2b.md). <br/><br/>*Hinweis: Aufgrund der Natur des denormalisierten Hybrid-Datenmodells von Experience Platform überschreiten die meisten Kunden diese Grenze nicht. Wenden Sie sich an Ihren Kundenbetreuer, wenn Sie Fragen zur Datenmodellierung haben oder mehr über benutzerdefinierte Beschränkungen erfahren möchten.* |
| Alte Beziehungen mit mehreren Entitäten | 20 | Soft | Es werden maximal 20 Beziehungen mit mehreren Entitäten empfohlen, die zwischen primären Entitäten und Dimensionsentitäten definiert sind. Zusätzliche Beziehungszuordnungen sollten erst vorgenommen werden, wenn eine vorhandene Beziehung entfernt oder deaktiviert wurde. |
| Viele-zu-eins-Beziehungen pro XDM-Klasse | 2 | Soft | Es werden maximal zwei n:n-Beziehungen empfohlen, die pro XDM-Klasse definiert sind. Zusätzliche Beziehungen sollten erst dann hergestellt werden, wenn eine vorhandene Beziehung entfernt oder deaktiviert wurde. Anweisungen zum Erstellen einer Beziehung zwischen zwei Schemas finden Sie im Tutorial zu [Erstellen von B2B-Schemabeziehungen](../xdm/tutorials/relationship-b2b.md). |

### Limits für Entitäten in Dimensionen

>[!NOTE]
>
>Die in diesem Abschnitt beschriebenen Datenmodellbeschränkungen stellen die von Real-time Customer Data Platform B2B Edition aktivierten Änderungen dar. Für eine vollständige Liste der Standardbeschränkungen für die Echtzeit-Kundendatenplattform B2B Edition kombinieren Sie diese Beschränkungen mit den allgemeinen Adobe Experience Platform-Beschränkungen, die im Abschnitt [Limits für die Dokumentation zu Echtzeit-Kundenprofil-Daten](../profile/guardrails.md).

| Guardrail | Limit | Begrenzungstyp | Beschreibung |
| --- | --- | --- | --- |
| Keine verschachtelten Legacy-Beziehungen | 0 | Soft | Sie sollten keine Beziehung zwischen zwei Nicht-[!DNL XDM Individual Profile] Schemas. Die Möglichkeit, Beziehungen zu erstellen, wird für keine Schemas empfohlen, die nicht Teil der [!DNL Profile] Vereinigungsschema. |
| Nur B2B-Objekte können an vielen zu 1 Beziehungen teilnehmen | 0 | Hard | Das System unterstützt nur eine n:n-Beziehung zwischen B2B-Objekten. Weiterführende Informationen zu einer Vielzahl von Beziehungen finden Sie im Tutorial zu [Erstellen von B2B-Schemabeziehungen](../xdm/tutorials/relationship-b2b.md). |
| Maximale Tiefe verschachtelter Beziehungen zwischen B2B-Objekten | 3 | Hard | Die maximale Tiefe verschachtelter Beziehungen zwischen B2B-Objekten beträgt 3. Das bedeutet, dass Sie in einem hochverschachtelten Schema keine Beziehung zwischen B2B-Objekten haben sollten, die mehr als drei Ebenen tief verschachtelt sind. |

## Datengrößenbeschränkungen

Die folgenden Limits beziehen sich auf die Datengröße und bieten empfohlene Beschränkungen für Daten, die erfasst, gespeichert und wie gewünscht abgefragt werden können. Weitere Informationen zu primären Entitäten und Dimensionentitäten finden Sie im Abschnitt zu [Entitätstypen](#entity-types) in der Anlage.

>[!INFO]
>
>Die Datengröße wird als unkomprimierte Daten in JSON zum Zeitpunkt der Erfassung gemessen.

### Limits Primärer Entitäten

>[!NOTE]
>
>Die in diesem Abschnitt beschriebenen Datengrößenbeschränkungen stellen die von Real-time Customer Data Platform B2B Edition aktivierten Änderungen dar. Für eine vollständige Liste der Standardbeschränkungen für die Echtzeit-Kundendatenplattform B2B Edition kombinieren Sie diese Beschränkungen mit den allgemeinen Adobe Experience Platform-Beschränkungen, die im Abschnitt [Limits für die Dokumentation zu Echtzeit-Kundenprofil-Daten](../profile/guardrails.md).

| Guardrail | Limit | Begrenzungstyp | Beschreibung |
| --- | --- | --- | --- |
| Batches, die pro XDM-Klasse pro Tag erfasst werden | 45 | Soft | Die Gesamtanzahl der täglich pro XDM-Klasse erfassten Batches sollte 45 nicht überschreiten. Die Erfassung zusätzlicher Batches kann eine optimale Leistung verhindern. |

### Limits für Entitäten in Dimensionen

>[!NOTE]
>
>Die in diesem Abschnitt beschriebenen Datengrößenbeschränkungen stellen die von Real-time Customer Data Platform B2B Edition aktivierten Änderungen dar. Für eine vollständige Liste der Standardbeschränkungen für die Echtzeit-Kundendatenplattform B2B Edition kombinieren Sie diese Beschränkungen mit den allgemeinen Adobe Experience Platform-Beschränkungen, die im Abschnitt [Limits für die Dokumentation zu Echtzeit-Kundenprofil-Daten](../profile/guardrails.md).

| Guardrail | Limit | Begrenzungstyp | Beschreibung |
| --- | --- | --- | --- |
| Gesamtgröße für alle dimensionalen Entitäten | 5 GB | Soft | Die empfohlene Gesamtgröße für alle dimensionalen Entitäten beträgt 5 GB. Die Erfassung großer Dimensionselemente kann die Systemleistung beeinträchtigen. Es wird beispielsweise nicht empfohlen, einen 10 GB großen Produktkatalog als Dimensionentität zu laden. |
| Datensätze pro dimensionales Entitätsschema | 5 | Soft | Es werden maximal 5 Datensätze empfohlen, die mit jedem Dimensionsschema verknüpft sind. Wenn Sie beispielsweise ein Schema für &quot;Produkte&quot;erstellen und fünf beitragende Datensätze hinzufügen, sollten Sie keinen sechsten Datensatz erstellen, der mit dem Produktschema verknüpft ist. |
| Dimension Entitäts-Batches, die pro Tag erfasst werden | 4 pro Unternehmen | Soft | Die empfohlene maximale Anzahl von Dimensionentitäts-Batches, die pro Tag erfasst werden, beträgt 4 pro Entität. Sie können beispielsweise Aktualisierungen an einem Produktkatalog bis zu 4-mal täglich erfassen. Die Aufnahme zusätzlicher Dimensionentitäts-Batches für dieselbe Entität kann sich auf die Systemleistung auswirken. |

## Limits bei der Segmentierung

Die in diesem Abschnitt beschriebenen Limits beziehen sich auf die Anzahl und Art der Segmente, die ein Unternehmen in Experience Platform erstellen kann, sowie auf die Zuordnung und Aktivierung von Segmenten zu Zielen.

>[!NOTE]
>
>Die in diesem Abschnitt beschriebenen Segmentierungsbeschränkungen stellen die von Real-time Customer Data Platform B2B Edition aktivierten Änderungen dar. Für eine vollständige Liste der Standardbeschränkungen für die Echtzeit-Kundendatenplattform B2B Edition kombinieren Sie diese Beschränkungen mit den allgemeinen Adobe Experience Platform-Beschränkungen, die im Abschnitt [Limits für die Dokumentation zu Echtzeit-Kundenprofil-Daten](../profile/guardrails.md).

| Guardrail | Limit | Begrenzungstyp | Beschreibung |
| --- | --- | --- | --- |
| Segmente pro B2B-Sandbox | 400 | Soft | Eine Organisation kann insgesamt über mehr als 400 Segmente verfügen, sofern in jeder einzelnen B2B-Sandbox weniger als 400 Segmente vorhanden sind. Der Versuch, zusätzliche Segmente zu erstellen, kann sich auf die Systemleistung auswirken. |

## Nächste Schritte

Die in diesem Dokument beschriebenen Einschränkungen stellen die von Real-time Customer Data Platform B2B Edition aktivierten Änderungen dar. Für eine vollständige Liste der Standardbeschränkungen für die Echtzeit-Kundendatenplattform B2B Edition kombinieren Sie diese Beschränkungen mit den allgemeinen Adobe Experience Platform-Beschränkungen, die im Abschnitt [Limits für die Dokumentation zu Echtzeit-Kundenprofil-Daten](../profile/guardrails.md).

## Anhang

Dieser Abschnitt enthält zusätzliche Details zu den Beschränkungen in diesem Dokument.

### Entitätstypen

Die [!DNL Profile] Store-Datenmodell besteht aus zwei Kernentitätstypen:

* **Primäre Entität:** Eine primäre Entität oder Profilentität führt Daten zu einer &quot;einzigen Quelle der Wahrheit&quot;für eine Person zusammen. Diese einheitlichen Daten werden mithilfe einer so genannten &quot;Vereinigungsansicht&quot;dargestellt. Eine Vereinigungsansicht aggregiert die Felder aller Schemas, die dieselbe Klasse in ein Vereinigungsschema implementieren. Das Vereinigungsschema für [!DNL Real-time Customer Profile] ist ein denormalisiertes Hybrid-Datenmodell, das als Container für alle Profilattribute und Verhaltensereignisse fungiert.

   Zeitunabhängige Attribute, auch &quot;Datensatzdaten&quot;genannt, werden mithilfe von Modellen modelliert [!DNL XDM Individual Profile], während Zeitreihendaten, auch als &quot;Ereignisdaten&quot;bezeichnet, modelliert werden mit [!DNL XDM ExperienceEvent]. Während Datensatz- und Zeitreihendaten in Adobe Experience Platform erfasst werden, werden sie in Trigger [!DNL Real-time Customer Profile] , um mit der Aufnahme von Daten zu beginnen, die für ihre Verwendung aktiviert wurden. Je mehr Interaktionen und Details erfasst werden, desto robuster werden einzelne Profile.

   ![](../profile/images/guardrails/profile-entity.png)

* **Entität der Dimension:** Während der Profildatenspeicher, in dem Profildaten verwaltet werden, kein relativer Speicher ist, ermöglicht das Profil die Integration mit kleinen Dimensionselementen, um Segmente auf vereinfachte und intuitive Weise zu erstellen. Diese Integration wird als [Segmentierung mehrerer Entitäten](../segmentation/multi-entity-segmentation.md). Ihr Unternehmen kann auch XDM-Klassen definieren, um andere Dinge als Einzelpersonen zu beschreiben, z. B. Geschäfte, Produkte oder Eigenschaften. Diese Nicht-[!DNL XDM Individual Profile] Schemas werden als &quot;Dimensionselemente&quot;bezeichnet und enthalten keine Zeitreihendaten. Dimension-Entitäten stellen Suchdaten bereit, die Segmentdefinitionen mit mehreren Entitäten unterstützen und vereinfachen. Sie müssen klein genug sein, damit die Segmentierungsmaschine den gesamten Datensatz in den Speicher laden kann, um eine optimale Verarbeitung zu gewährleisten (Schnellpoint-Suche).

   ![](../profile/images/guardrails/profile-and-dimension-entities.png)
