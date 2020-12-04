---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
title: Leitlinien für Experience Platformen
topic: guide
translation-type: tm+mt
source-git-commit: 59cf089a8bf7ce44e7a08b0bb1d4562f5d5104db
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 2%

---


# [!DNL Platform] Guardradien für [!DNL Real-time Customer Profile]

[!DNL Real-time Customer Profile] stellt individuelle Profil bereit, mit denen Sie personalisierte Erlebnisse für Kanal auf der Grundlage von Einblicken in das Verhalten und Kundenattributen bereitstellen können. Um dieses Targeting zu erreichen, [!DNL Profile] und die Segmentierungsmaschine in Adobe Experience Platform verwenden ein stark denormalisiertes Hybriddatenmodell, das einen neuen Ansatz zur Entwicklung von Profilen für Kunden Angebot. Die Verwendung dieses Hybrid-Datenmodells macht es äußerst wichtig, dass die erfassten Daten korrekt modelliert werden. Während der [!DNL Profile] Datenspeicher, in dem Profil-Daten gespeichert werden, kein relationaler Speicher ist, [!DNL Profile] ermöglicht er die Integration mit kleinen Dimensionselementen, um Segmente auf vereinfachte und intuitive Weise zu erstellen. Diese Integration wird als Segmentierung mehrerer Entitäten bezeichnet.

Adobe Experience Platform bietet eine Reihe von Garantieleistungen, mit denen Sie vermeiden können, Datenmodelle zu erstellen, die nicht unterstützt werden [!DNL Real-time Customer Profile] können. In diesem Dokument werden die Best Practices und Einschränkungen bei der Verwendung von Dimensionselementen, insbesondere bei der Stapelsegmentierung, erläutert.

>[!NOTE]
>
>Die in diesem Dokument dargelegten Garantien und Grenzen werden ständig verbessert. Schauen Sie regelmäßig nach Updates.

## Erste Schritte

Es wird empfohlen, die folgende Dokumentation zu Experience Platform Services zu lesen, bevor Sie versuchen, Datenmodelle zur Verwendung in [!DNL Real-time Customer Profile]zu erstellen. Die Arbeit mit Datenmodellen und den in diesem Dokument dargelegten Garantien erfordern ein Verständnis der verschiedenen Experience Platformen, die mit der Verwaltung von [!DNL Real-time Customer Profile] Entitäten verbunden sind:

* [[!DNL Real-time Customer Profile]](home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [Adobe Experience Platform-Identitätsdienst](../identity-service/home.md): Unterstützt die Erstellung einer &quot;einzigen Ansicht des Kunden&quot;, indem Identitäten aus unterschiedlichen Datenquellen bei der Erfassung überbrückt werden [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Das standardisierte Framework, mit dem Plattform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Zusammensetzung](../xdm/schema/composition.md)des Schemas: Einführung in Schema und Datenmodellierung in der Experience Platform.
* [Adobe Experience Platform-Segmentierungsdienst](../segmentation/home.md): Die Segmentierungsmaschine, die [!DNL Platform] verwendet wird, um Kundensegmente aus Ihren Profilen basierend auf Kundenverhalten und -attributen zu erstellen.
   * [Segmentierung](../segmentation/multi-entity-segmentation.md)mehrerer Entitäten: Eine Anleitung zum Erstellen von Segmenten, die Dimensionselemente mit Profil-Daten integrieren.

## Entitätstypen

Das [!DNL Profile] Datenspeichermodell besteht aus zwei Kernentitätstypen:

* **Primär:** Eine primäre Entität oder eine Entität eines Profils führt Daten zu einer &quot;einzigen Wahrheitsquelle&quot;für eine Person zusammen. Diese vereinheitlichten Daten werden mithilfe einer so genannten &quot;Vereinigung-Ansicht&quot;dargestellt. Eine Vereinigung-Ansicht Aggregat die Felder aller Schema, die dieselbe Klasse implementieren, in einem einzigen Vereinigung-Schema. Das Vereinigung-Schema für [!DNL Real-time Customer Profile] ist ein denormalisiertes Hybrid-Datenmodell, das als Container für alle Profil- und Verhaltensattribute fungiert.

   Zeitunabhängige Attribute, auch als &quot;Datensatzdaten&quot;bezeichnet, werden modelliert, [!DNL XDM Individual Profile]während Zeitreihendaten, auch als &quot;Ereignis-Daten&quot;bezeichnet, anhand von [!DNL XDM ExperienceEvent]Modellen modelliert werden. Da in Adobe Experience Platform Daten aus Datensatz- und Zeitreihen erfasst werden, werden Daten, die für ihre Verwendung aktiviert wurden, [!DNL Real-time Customer Profile] aufgenommen. Je mehr Interaktionen und Details einbezogen werden, desto robuster werden die einzelnen Profil.

   ![](images/guardrails/profile-entity.png)

* **Dimension:** Ihr Unternehmen kann auch XDM-Klassen definieren, um andere Dinge als Einzelpersonen zu beschreiben, z. B. Geschäfte, Produkte oder Eigenschaften. Diese Nicht-[!DNL XDM Individual Profile] Schema werden als &quot;Dimensionselemente&quot;bezeichnet und enthalten keine Zeitreihendaten. Dimensionen-Entitäten bieten Nachschlagedaten, die die Segmentdefinitionen mehrerer Entitäten erleichtern und vereinfachen, und müssen klein genug sein, damit die Segmentierungsmaschine den gesamten Datensatz zur optimalen Verarbeitung in den Speicher laden kann (schnelle Nachschlagevorgänge).

   ![](images/guardrails/profile-and-dimension-entities.png)

## Arten begrenzen

Bei der Definition Ihres Datenmodells wird empfohlen, sich an den angegebenen Garantieleistungen zu halten, um eine ordnungsgemäße Leistung sicherzustellen und Systemfehler zu vermeiden. Die in diesem Dokument vorgesehenen Garantien umfassen zwei Arten von Beschränkungen:

* **Weicher Grenzwert:** Eine weiche Grenze bietet ein empfohlenes Maximum für eine optimale Systemleistung. Es ist möglich, über eine weiche Grenze hinauszugehen, ohne das System zu beschädigen oder Fehlermeldungen zu erhalten, allerdings führt ein Überschreiten einer weichen Grenze zu einer Leistungsbeeinträchtigung. Es wird empfohlen, die weiche Grenze einzuhalten, um eine Verringerung der Gesamtleistung zu vermeiden.

* **Grenze:** Eine feste Begrenzung bietet ein absolutes Maximum für das System. Wenn Sie eine feste Grenze überschreiten, werden Unterbrechungen und Fehler auftreten, wodurch das System nicht wie erwartet funktioniert.

## Datenmodellgarantien

Es wird empfohlen, beim Erstellen eines Datenmodells für die Verwendung mit den folgenden [!DNL Real-time Customer Profile]Garantien vorzugehen.

### Primär Entitätsgarantien

| Guardrail | Maximal | Typ begrenzen | Beschreibung |
| --- | --- | --- | --- |
| Anzahl der empfohlenen Datensätze als Beitrag zum Schema der [!DNL Profile] Vereinigung | 20 | Soft | **Es werden maximal 20 [!DNL Profile]aktivierte Datensätze empfohlen.** Um einen anderen Datensatz zu aktivieren, [!DNL Profile]sollte zunächst ein vorhandener Datensatz entfernt oder deaktiviert werden. |
| Anzahl der empfohlenen Beziehungen mit mehreren Entitäten | 5 | Soft | **Es wird empfohlen, maximal 5 Beziehungen mit mehreren Entitäten zu definieren, die zwischen primären Entitäten und Dimensionselementen definiert sind.** Zusätzliche Beziehungszuordnungen sollten erst dann vorgenommen werden, wenn eine bestehende Beziehung entfernt oder deaktiviert wurde. |
| Maximale JSON-Tiefe für ID-Feld, das in einer Beziehung mit mehreren Entitäten verwendet wird | 4 | Soft | **Die empfohlene maximale JSON-Tiefe für ein ID-Feld, das in Beziehungen mit mehreren Entitäten verwendet wird, ist 4.** Dies bedeutet, dass in einem hochverschachtelten Schema Felder, die mehr als vier Ebenen tief verschachtelt sind, nicht als ID-Feld in einer Beziehung verwendet werden sollten. |
| Array-Kardinalität in einem Profil-Fragment | &lt;=500 | Soft | **Die optimale Array-Kardinalität in einem Profil-Fragment (zeitunabhängige Daten) ist &lt;=500.** |
| Array-Kardinalität in ExperienceEvent | &lt;=10 | Soft | **Die optimale Array-Kardinalität in einem ExperienceEvent (Zeitreihendaten) ist &lt;=10.** |

### Garantieleistungen für Dimensionen

| Guardrail | Maximal | Typ begrenzen | Beschreibung |
| --- | --- | --- | --- |
| Keine Zeitreihendaten für Nicht-[!DNL XDM Individual Profile] Entitäten zulässig | 0 | Hard | **Zeitreihendaten sind für Nicht-[!DNL XDM Individual Profile] -Entitäten im Profil Service nicht zulässig.** Wenn ein Dataset einer Zeitreihe mit einer Nicht-[!DNL XDM Individual Profile] -ID verknüpft ist, sollte der Datensatz nicht aktiviert werden [!DNL Profile]. |
| Keine verschachtelten Beziehungen | 0 | Soft | **Sie sollten keine Beziehung zwischen zwei Nicht-[!DNL XDM Individual Profile] Schemas herstellen.** Die Möglichkeit, Beziehungen zu erstellen, wird nicht für Schema empfohlen, die nicht Teil des Schemas [!DNL Profile] Vereinigung sind. |
| Maximale JSON-Tiefe für primäres ID-Feld | 4 | Soft | **Die empfohlene maximale JSON-Tiefe für das primäre ID-Feld ist 4.** Das bedeutet, dass Sie in einem hochverschachtelten Schema kein Feld als primäre ID auswählen sollten, wenn es mehr als vier Ebenen tief verschachtelt ist. Ein Feld, das sich auf der vierten verschachtelten Ebene befindet, kann als primäre ID verwendet werden. |

## Datengröße

Die folgenden Garantien beziehen sich auf die Datengröße und werden empfohlen, um sicherzustellen, dass Daten wie gewünscht erfasst, gespeichert und abgefragt werden können.

>[!NOTE]
>
>Die Datengröße wird als unkomprimierte Daten in JSON zum Zeitpunkt der Erfassung gemessen.

### Primär Entitätsgarantien

| Guardrail | Maximal | Typ begrenzen | Beschreibung |
| --- | --- | --- | --- |
| Maximale Größe pro Profil | 10 KB | Soft | **Die empfohlene Maximalgröße für ein Profil-Fragment beträgt 10 KB.** Die Erfassung größerer Profil-Fragmente wirkt sich auf die Systemleistung aus. Das Laden eines umfangreichen CRM-Datensatzes mit einer Größe von 50 kB, in dem einige Profil-Fragmente enthalten sind, führt beispielsweise zu einer Beeinträchtigung der Systemleistung. |
| Absolute Maximalgröße pro Profil-Fragment | 1MB | Hard | **Die absolute Maximalgröße eines Profil-Fragments beträgt 1 MB.** Die Auslastung schlägt fehl, wenn versucht wird, ein Profil-Fragment hochzuladen, das größer als 1 MB ist. |

### Garantieleistungen für Dimensionen

| Guardrail | Maximal | Typ begrenzen | Beschreibung |
| --- | --- | --- | --- |
| Maximale Gesamtgröße für alle dimensionalen Entitäten | 5 GB   | Soft | **Die maximal empfohlene Gesamtgröße für alle dimensionalen Entitäten beträgt 5 GB.** Die Erfassung von Entitäten mit großer Dimension führt zu einer Beeinträchtigung der Systemleistung. Beispielsweise wird der Versuch, einen 10-GB-Produktkatalog als Dimensionentität zu laden, nicht empfohlen. |
| Datenbestände pro dimensionales Entitäts-Schema | 5 | Soft | **Es werden maximal 5 Datensätze empfohlen, die mit jedem dimensionalen Entitäts-Schema verknüpft sind.** Wenn Sie beispielsweise ein Schema für &quot;products&quot;erstellen und fünf beitragende Datensätze hinzufügen, sollten Sie keinen sechsten Datensatz erstellen, der mit dem Schema &quot;products&quot;verknüpft ist. |