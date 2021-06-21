---
keywords: Experience Platform; Profil; Echtzeit-Kundenprofil; Fehlerbehebung; Limits; Richtlinien; Grenze; Entität; primäre Entität; Dimensionentität;
title: Limits für Echtzeit-Kundenprofildaten
solution: Experience Platform
product: experience platform
type: Documentation
description: Adobe Experience Platform bietet eine Reihe von Limits, mit denen Sie verhindern können, dass Datenmodelle erstellt werden, die vom Echtzeit-Kundenprofil nicht unterstützt werden. In diesem Dokument werden Best Practices und Einschränkungen beschrieben, die bei der Modellierung von Profildaten beachtet werden müssen.
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
source-git-commit: 441c2978b90a4703874787b3ed8b94c4a7779aa8
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 4%

---

# Limits für [!DNL Real-time Customer Profile]-Daten

[!DNL Real-time Customer Profile] bietet individuelle Profile, mit denen Sie personalisierte kanalübergreifende Erlebnisse auf der Grundlage von Verhaltenseinblicken und Kundenattributen bereitstellen können. Um dieses Targeting zu erreichen, verwenden [!DNL Profile] und die Segmentierungs-Engine in Adobe Experience Platform ein stark denormalisiertes Hybrid-Datenmodell, das einen neuen Ansatz zur Entwicklung von Kundenprofilen bietet. Durch die Verwendung dieses hybriden Datenmodells ist es wichtig, dass die erfassten Daten korrekt modelliert werden. Während der [!DNL Profile]-Datenspeicher, in dem Profildaten verwaltet werden, kein relativer Speicher ist, ermöglicht [!DNL Profile] die Integration mit kleinen Dimensionentitäten, um Segmente auf vereinfachte und intuitive Weise zu erstellen. Diese Integration wird als Segmentierung mit mehreren Entitäten bezeichnet.

Adobe Experience Platform bietet eine Reihe von Limits, mit denen Sie verhindern können, dass Datenmodelle erstellt werden, die [!DNL Real-time Customer Profile] nicht unterstützen kann. In diesem Dokument werden diese Limits, Best Practices und Einschränkungen bei der Verwendung von Profildaten für die Segmentierung erläutert.

>[!NOTE]
>
>Die in diesem Dokument dargelegten Limits und Limits werden ständig verbessert. Prüfen Sie regelmäßig nach Updates.

## Erste Schritte

Es wird empfohlen, die folgende Dokumentation zu Experience Platform-Diensten zu lesen, bevor Sie versuchen, Datenmodelle zur Verwendung in [!DNL Real-time Customer Profile] zu erstellen. Die Arbeit mit Datenmodellen und den in diesem Dokument beschriebenen Limits erfordern ein Verständnis der verschiedenen Experience Platform-Dienste, die mit der Verwaltung von [!DNL Real-time Customer Profile]-Entitäten verbunden sind:

* [[!DNL Real-time Customer Profile]](home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [Adobe Experience Platform Identity-Dienst](../identity-service/home.md): Unterstützt die Erstellung einer &quot;einheitlichen Ansicht des Kunden&quot;, indem Identitäten aus unterschiedlichen Datenquellen bei der Erfassung in überbrückt  [!DNL Platform]werden.
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Das standardisierte Framework, mit dem Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../xdm/schema/composition.md): Eine Einführung in Schemas und Datenmodellierung in Experience Platform.
* [Adobe Experience Platform Segmentation Service](../segmentation/home.md): Die Segmentierungsmaschine, die in [!DNL Platform] verwendet wird, um Zielgruppensegmente aus Ihren Kundenprofilen basierend auf Kundenverhalten und -attributen zu erstellen.
   * [Segmentierung mehrerer Entitäten](../segmentation/multi-entity-segmentation.md): Eine Anleitung zum Erstellen von Segmenten, die Dimensionentitäten mit Profildaten integrieren.

## Entitätstypen

Das Store-Datenmodell [!DNL Profile] besteht aus zwei Kernentitätstypen:

* **Primäre Entität:** Eine primäre Entität oder Profilentität führt Daten zu einer &quot;einzigen Wahrheitsquelle&quot;für eine Person zusammen. Diese einheitlichen Daten werden mithilfe einer so genannten &quot;Vereinigungsansicht&quot;dargestellt. Eine Vereinigungsansicht aggregiert die Felder aller Schemas, die dieselbe Klasse in ein Vereinigungsschema implementieren. Das Vereinigungsschema für [!DNL Real-time Customer Profile] ist ein denormalisiertes Hybrid-Datenmodell, das als Container für alle Profilattribute und Verhaltensereignisse fungiert.

   Zeitunabhängige Attribute, auch &quot;Datensatzdaten&quot;genannt, werden mit [!DNL XDM Individual Profile] modelliert, während Zeitreihendaten, auch &quot;Ereignisdaten&quot;genannt, mit [!DNL XDM ExperienceEvent] modelliert werden. Da Datensatz- und Zeitreihendaten in Adobe Experience Platform erfasst werden, wird es Trigger [!DNL Real-time Customer Profile], Daten zu erfassen, die für ihre Verwendung aktiviert wurden. Je mehr Interaktionen und Details erfasst werden, desto robuster werden einzelne Profile.

   ![](images/guardrails/profile-entity.png)

* **Entität der Dimension:** Ihr Unternehmen kann auch XDM-Klassen definieren, um andere Dinge als Einzelpersonen zu beschreiben, z. B. Geschäfte, Produkte oder Eigenschaften. Diese nicht-[!DNL XDM Individual Profile]-Schemas werden als &quot;Dimensionselemente&quot;bezeichnet und enthalten keine Zeitreihendaten. Dimension-Entitäten stellen Suchdaten bereit, die Segmentdefinitionen mit mehreren Entitäten unterstützen und vereinfachen. Sie müssen klein genug sein, damit die Segmentierungsmaschine den gesamten Datensatz in den Speicher laden kann, um eine optimale Verarbeitung zu gewährleisten (Schnellpoint-Suche).

   ![](images/guardrails/profile-and-dimension-entities.png)

## Profilfragmente

Es gibt mehrere Limits in diesem Dokument, die auf &quot;Profilfragmente&quot;verweisen. Das Echtzeit-Kundenprofil besteht aus mehreren Profilfragmenten. Jedes Fragment stellt die Daten für die Identität aus einem Datensatz dar, in dem es die primäre Identität ist. Das bedeutet, dass ein Fragment eine primäre ID und Ereignisdaten (Zeitreihen) in einem XDM ExperienceEvent-Datensatz enthalten kann oder aus einer primären ID und Datensatzdaten (zeitunabhängige Attribute) in einem Datensatz &quot;XDM Individual Profile&quot;bestehen kann.

## Begrenzungstypen

Bei der Definition Ihres Datenmodells wird empfohlen, sich an die bereitgestellten Limits zu halten, um eine ordnungsgemäße Leistung sicherzustellen und Systemfehler zu vermeiden.

Die in diesem Dokument bereitgestellten Limits umfassen zwei Begrenzungstypen:

* **Softlimit:** Eine weiche Begrenzung bietet ein empfohlenes Maximum für optimale Systemleistung. Es ist möglich, über eine weiche Grenze hinauszugehen, ohne das System zu beschädigen oder Fehlermeldungen zu erhalten. Eine Überschreitung dieser weichen Grenze führt jedoch zu einer Leistungsbeeinträchtigung. Es wird empfohlen, die weiche Grenze einzuhalten, um eine Verringerung der Gesamtleistung zu vermeiden.

* **Hardlimit:** Eine feste Begrenzung bietet ein absolutes Maximum für das System. Wenn Sie eine feste Grenze überschreiten, führt dies zu Fehlern und Störungen, sodass das System nicht wie erwartet funktioniert.

## Limits für Datenmodelle

Die Einhaltung der folgenden Limits wird beim Erstellen eines Datenmodells zur Verwendung mit [!DNL Real-time Customer Profile] empfohlen.

### Limits Primärer Entitäten

| Guardrail | Limit | Begrenzungstyp | Beschreibung |
| --- | --- | --- | --- |
| Anzahl der empfohlenen Datensätze für den Beitrag zum Vereinigungsschema [!DNL Profile] | 20 | Soft | **Es werden maximal 20  [!DNL Profile]aktivierte Datensätze empfohlen.** Um einen anderen Datensatz für zu aktivieren,  [!DNL Profile]sollte zunächst ein vorhandener Datensatz entfernt oder deaktiviert werden. |
| Anzahl der empfohlenen Beziehungen mit mehreren Entitäten | 5 | Soft | **Es werden maximal 5 Beziehungen mit mehreren Entitäten empfohlen, die zwischen primären Entitäten und Dimensionsentitäten definiert sind.** Zusätzliche Beziehungszuordnungen sollten erst vorgenommen werden, wenn eine vorhandene Beziehung entfernt oder deaktiviert wurde. |
| Maximale JSON-Tiefe für ID-Feld, das in der Beziehung mit mehreren Entitäten verwendet wird | 4 | Soft | **Die empfohlene maximale JSON-Tiefe für ein ID-Feld, das in Beziehungen mit mehreren Entitäten verwendet wird, beträgt 4.** Dies bedeutet, dass in einem hochverschachtelten Schema Felder, die mehr als vier Ebenen tief verschachtelt sind, nicht als ID-Feld in einer Beziehung verwendet werden sollten. |
| Array-Kardinalität in einem Profilfragment | &lt;=500 | Soft | **Die optimale Array-Kardinalität in einem Profilfragment (zeitunabhängige Daten) ist  &lt;>** |
| Array-Kardinalität in ExperienceEvent | &lt;=10 | Soft | **Die optimale Array-Kardinalität in einem ExperienceEvent (Zeitreihendaten) ist  &lt;>** |

### Limits für Entitäten in Dimensionen

| Guardrail | Limit | Begrenzungstyp | Beschreibung |
| --- | --- | --- | --- |
| Keine Zeitreihendaten für Nicht-[!DNL XDM Individual Profile]-Entitäten zulässig | 0 | Hard | **Zeitreihendaten sind für Nicht-[!DNL XDM Individual Profile] Entitäten in Profile Service nicht zulässig.** Wenn ein Datensatz aus Zeitreihen mit einer Nicht-[!DNL XDM Individual Profile] ID verknüpft ist, sollte der Datensatz nicht für aktiviert werden  [!DNL Profile]. |
| Keine verschachtelten Beziehungen | 0 | Soft | **Sie sollten keine Beziehung zwischen zwei Nicht-[!DNL XDM Individual Profile] Schemas erstellen.** Die Möglichkeit, Beziehungen zu erstellen, wird für keine Schemas empfohlen, die nicht Teil des  [!DNL Profile] Vereinigungsschemas sind. |
| Maximale JSON-Tiefe für primäres ID-Feld | 4 | Soft | **Die empfohlene maximale JSON-Tiefe für das primäre ID-Feld beträgt 4.** Das bedeutet, dass Sie in einem hochverschachtelten Schema ein Feld nicht als primäre ID auswählen sollten, wenn es mehr als vier Ebenen tief verschachtelt ist. Ein Feld, das sich auf der vierten verschachtelten Ebene befindet, kann als primäre ID verwendet werden. |

## Limits bei der Datengröße

Die folgenden Limits beziehen sich auf die Datengröße und werden empfohlen, um sicherzustellen, dass Daten wie gewünscht erfasst, gespeichert und abgefragt werden können.

>[!NOTE]
>
>Die Datengröße wird als unkomprimierte Daten in JSON zum Zeitpunkt der Erfassung gemessen.

### Limits Primärer Entitäten

| Guardrail | Limit | Begrenzungstyp | Beschreibung |
| --- | --- | --- | --- |
| Maximale ExperienceEvent-Größe | 10 KB | Hard | **Die maximale Größe eines Ereignisses beträgt 10 KB.** Die Aufnahme wird fortgesetzt, jedoch werden alle Ereignisse, die größer als 10 KB sind, gelöscht. |
| Maximale Profildatensatzgröße | 100 KB | Hard | **Die maximale Größe eines Profildatensatzes beträgt 100 KB.** Die Aufnahme wird fortgesetzt, Profildatensätze, die größer als 100 KB sind, werden jedoch gelöscht. |
| Maximale Größe von Profilfragmenten | 50 MB | Hard | **Die maximale Größe eines Profilfragments beträgt 50 MB.** Die Segmentierung, der Export und die Suche können bei allen  [Profilfragmenten, die größer als 50 MB ](#profile-fragments) sind, fehlschlagen. |
| Maximale Profilspeichergröße | 50 MB | Soft | **Die maximale Größe eines gespeicherten Profils beträgt 50 MB.** Das Hinzufügen neuer  [Profilfragmente zu ](#profile-fragments) einem Profil, das größer als 50 MB ist, wirkt sich auf die Systemleistung aus. |
| Anzahl der täglich erfassten Profil- oder ExperienceEvent-Batches | 90 | Soft | **Die maximale Anzahl von Profil- oder ExperienceEvent-Batches, die pro Tag erfasst werden, beträgt 90.** Das bedeutet, dass die Gesamtanzahl der täglich erfassten Profil- und ExperienceEvent-Batches 90 nicht überschreiten darf. Die Aufnahme zusätzlicher Batches wirkt sich auf die Systemleistung aus. |

### Limits für Entitäten in Dimensionen

| Guardrail | Limit | Begrenzungstyp | Beschreibung |
| --- | --- | --- | --- |
| Maximale Gesamtgröße für alle dimensionalen Entitäten | 5 GB | Soft | **Die maximal empfohlene Gesamtgröße für alle dimensionalen Entitäten beträgt 5 GB.** Die Erfassung großer Dimensionselemente führt zu einer verminderten Systemleistung. Es wird beispielsweise nicht empfohlen, einen 10 GB großen Produktkatalog als Dimensionentität zu laden. |
| Datensätze pro dimensionales Entitätsschema | 5 | Soft | **Es werden maximal 5 Datensätze empfohlen, die mit jedem Dimensionsschema verknüpft sind.** Wenn Sie beispielsweise ein Schema für &quot;Produkte&quot;erstellen und fünf beitragende Datensätze hinzufügen, sollten Sie keinen sechsten Datensatz erstellen, der mit dem Produktschema verknüpft ist. |
| Anzahl der pro Tag erfassten Dimensionentitäts-Batches | 4 pro Unternehmen | Soft | **Die maximale Anzahl von Dimensionentitäts-Batches, die pro Tag erfasst werden, beträgt 4 pro Entität.** Sie können beispielsweise Aktualisierungen an einem Produktkatalog bis zu 4-mal täglich erfassen. Die Aufnahme zusätzlicher Dimensionentitäts-Batches für dieselbe Entität wirkt sich auf die Systemleistung aus. |

## Limits bei der Segmentierung

Die in diesem Abschnitt beschriebenen Limits beziehen sich auf die Anzahl und Art der Segmente, die ein Unternehmen in Experience Platform erstellen kann, sowie auf die Zuordnung und Aktivierung von Segmenten zu Zielen.

| Guardrail | Limit | Begrenzungstyp | Beschreibung |
| --- | --- | --- | --- |
| Maximale Segmentanzahl pro Sandbox | 10 K | Soft | **Die maximale Anzahl von Segmenten, die ein Unternehmen erstellen kann, beträgt 10.000 pro Sandbox.** Eine Organisation kann insgesamt über mehr als 10.000 Segmente verfügen, sofern in jeder einzelnen Sandbox weniger als 10.000 Segmente vorhanden sind. Der Versuch, zusätzliche Segmente zu erstellen, führt zu einer Beeinträchtigung der Systemleistung. |
| Maximale Anzahl von Streaming-Segmenten pro Sandbox | 500 | Soft | **Die maximale Anzahl von Streaming-Segmenten, die ein Unternehmen erstellen kann, beträgt 500 pro Sandbox.** Eine Organisation kann über mehr als 500 Streaming-Segmente verfügen, sofern in jeder einzelnen Sandbox weniger als 500 Streaming-Segmente vorhanden sind. Der Versuch, zusätzliche Streaming-Segmente zu erstellen, führt zu einer Beeinträchtigung der Systemleistung. |
| Maximale Anzahl an Batch-Segmenten pro Sandbox | 10 K | Soft | **Die maximale Anzahl von Batch-Segmenten, die ein Unternehmen erstellen kann, beträgt 10.000 pro Sandbox.** Eine Organisation kann insgesamt über mehr als 10.000 Batch-Segmente verfügen, sofern in jeder einzelnen Sandbox weniger als 10.000 Batch-Segmente vorhanden sind. Der Versuch, zusätzliche Batch-Segmente zu erstellen, führt zu einer Beeinträchtigung der Systemleistung. |
