---
keywords: Experience Platform;Profil;Echtzeit-Profil von Kunden;Fehlerbehebung;Guardrails;Guidelines;limit;entity;primary entity;dimension entity;
title: Leitlinien für Daten zum Echtzeit-Profil von Kunden
solution: Experience Platform
product: experience platform
topic-legacy: guide
type: Documentation
description: Adobe Experience Platform bietet eine Reihe von Garantieleistungen, mit denen Sie vermeiden können, Datenmodelle zu erstellen, die vom Echtzeit-Profil nicht unterstützt werden können. In diesem Dokument werden Best Practices und Einschränkungen erläutert, die bei der Modellierung von Profil-Daten zu beachten sind.
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1456'
ht-degree: 2%

---

# Grundlagen für [!DNL Real-time Customer Profile]-Daten

[!DNL Real-time Customer Profile] stellt individuelle Profil bereit, mit denen Sie personalisierte Erlebnisse für Kanal auf der Grundlage von Einblicken in das Verhalten und Kundenattributen bereitstellen können. Um dieses Targeting zu erreichen, verwenden [!DNL Profile] und die Segmentierungsmaschine in Adobe Experience Platform ein stark denormalisiertes Hybrid-Datenmodell, das einen neuen Ansatz zur Entwicklung von Profilen von Kunden Angebot. Die Verwendung dieses Hybrid-Datenmodells macht es äußerst wichtig, dass die erfassten Daten korrekt modelliert werden. Während der [!DNL Profile]-Datenspeicher zur Verwaltung von Profil-Daten kein relativer Speicher ist, ermöglicht [!DNL Profile] die Integration mit kleinen Dimensionentitäten, um Segmente auf vereinfachte und intuitive Weise zu erstellen. Diese Integration wird als Segmentierung mehrerer Entitäten bezeichnet.

Adobe Experience Platform bietet eine Reihe von Garantieleistungen, um zu vermeiden, dass Datenmodelle erstellt werden, die von [!DNL Real-time Customer Profile] nicht unterstützt werden. In diesem Dokument werden diese Garantien sowie Best Practices und Einschränkungen bei der Verwendung von Profil-Daten für die Segmentierung erläutert.

>[!NOTE]
>
>Die in diesem Dokument dargelegten Garantien und Grenzen werden ständig verbessert. Schauen Sie regelmäßig nach Updates.

## Erste Schritte

Es wird empfohlen, die folgende Dokumentation zu Experience Platform Services zu lesen, bevor Sie versuchen, Datenmodelle für die Verwendung in [!DNL Real-time Customer Profile] zu erstellen. Die Arbeit mit Datenmodellen und den in diesem Dokument beschriebenen Garantien erfordern ein Verständnis der verschiedenen Experience Platform-Services, die mit der Verwaltung von [!DNL Real-time Customer Profile]-Entitäten verbunden sind:

* [[!DNL Real-time Customer Profile]](home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [Adobe Experience Platform-Identitätsdienst](../identity-service/home.md): Unterstützt die Erstellung einer &quot;einzigen Ansicht des Kunden&quot;, indem Identitäten aus unterschiedlichen Datenquellen bei der Erfassung überbrückt werden  [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Das standardisierte Framework, mit dem Plattform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Zusammensetzung](../xdm/schema/composition.md) des Schemas: Einführung in Schema und Datenmodellierung in der Experience Platform.
* [Adobe Experience Platform-Segmentierungsdienst](../segmentation/home.md): Die Segmentierungsmaschine, die  [!DNL Platform] verwendet wird, um Audiencen-Segmente aus Ihren Profilen basierend auf Kundenverhalten und -attributen zu erstellen.
   * [Segmentierung](../segmentation/multi-entity-segmentation.md) mehrerer Entitäten: Eine Anleitung zum Erstellen von Segmenten, die Dimensionselemente mit Profil-Daten integrieren.

## Entitätstypen

Das Datenmodell [!DNL Profile] zum Speichern besteht aus zwei Kern-Entitätstypen:

* **Primär entity:** Eine primäre Entität oder Profil-Entität führt Daten zu einer &quot;einzigen Wahrheitsquelle&quot;für eine Einzelperson zusammen. Diese vereinheitlichten Daten werden mithilfe einer so genannten &quot;Vereinigung-Ansicht&quot;dargestellt. Eine Vereinigung-Ansicht Aggregat die Felder aller Schema, die dieselbe Klasse implementieren, in einem einzigen Vereinigung-Schema. Das Vereinigung-Schema für [!DNL Real-time Customer Profile] ist ein denormalisiertes Hybrid-Datenmodell, das als Container für alle Profil- und Verhaltensattribute fungiert.

   Zeitunabhängige Attribute, auch als &quot;Datensatzdaten&quot;bezeichnet, werden mit [!DNL XDM Individual Profile] modelliert, während Zeitreihendaten, auch als &quot;Ereignis-Daten&quot;bezeichnet, mit [!DNL XDM ExperienceEvent] modelliert werden. Da Daten zu Datensatz und Zeitreihen in Adobe Experience Platform erfasst werden, beginnen die Trigger [!DNL Real-time Customer Profile] mit der Erfassung von Daten, die für ihre Verwendung aktiviert wurden. Je mehr Interaktionen und Details einbezogen werden, desto robuster werden die einzelnen Profil.

   ![](images/guardrails/profile-entity.png)

* **Entität der Dimension:** Ihr Unternehmen kann auch XDM-Klassen definieren, um andere Dinge als Einzelpersonen zu beschreiben, wie z. B. Geschäfte, Produkte oder Eigenschaften. Diese nicht-[!DNL XDM Individual Profile]-Schema werden als &quot;Dimensionselemente&quot;bezeichnet und enthalten keine Zeitreihendaten. Dimensionen-Entitäten bieten Nachschlagedaten, die die Segmentdefinitionen mehrerer Entitäten erleichtern und vereinfachen, und müssen klein genug sein, damit die Segmentierungsmaschine den gesamten Datensatz zur optimalen Verarbeitung in den Speicher laden kann (schnelle Nachschlagevorgänge).

   ![](images/guardrails/profile-and-dimension-entities.png)

## Arten begrenzen

Bei der Definition Ihres Datenmodells wird empfohlen, sich an den angegebenen Garantieleistungen zu halten, um eine ordnungsgemäße Leistung sicherzustellen und Systemfehler zu vermeiden. Die in diesem Dokument vorgesehenen Garantien umfassen zwei Arten von Beschränkungen:

* **Weicher Grenzwert:** Eine weiche Grenze bietet ein empfohlenes Maximum für eine optimale Systemleistung. Es ist möglich, über eine weiche Grenze hinauszugehen, ohne das System zu beschädigen oder Fehlermeldungen zu erhalten, allerdings führt ein Überschreiten einer weichen Grenze zu einer Leistungsbeeinträchtigung. Es wird empfohlen, die weiche Grenze einzuhalten, um eine Verringerung der Gesamtleistung zu vermeiden.

* **Hard limit:** Eine feste Grenze bietet ein absolutes Maximum für das System. Wenn Sie eine feste Grenze überschreiten, werden Unterbrechungen und Fehler auftreten, wodurch das System nicht wie erwartet funktioniert.

## Datenmodellgarantien

Es wird empfohlen, beim Erstellen eines Datenmodells zur Verwendung mit [!DNL Real-time Customer Profile] die folgenden Garantien einzuhalten.

### Primär Entitätsgarantien

| Guardrail | Maximal | Typ begrenzen | Beschreibung |
| --- | --- | --- | --- |
| Anzahl der empfohlenen Datensätze als Beitrag zum Schema [!DNL Profile]-Vereinigung | 20 | Soft | **Es werden maximal 20  [!DNL Profile]aktivierte Datensätze empfohlen.** Um einen anderen Datensatz zu aktivieren,  [!DNL Profile]sollte zunächst ein vorhandener Datensatz entfernt oder deaktiviert werden. |
| Anzahl der empfohlenen Beziehungen mit mehreren Entitäten | 5 | Weich | **Es wird empfohlen, maximal 5 Beziehungen mit mehreren Entitäten zu definieren, die zwischen primären Entitäten und Dimensionselementen definiert sind.** Zusätzliche Beziehungszuordnungen sollten erst dann vorgenommen werden, wenn eine bestehende Beziehung entfernt oder deaktiviert wurde. |
| Maximale JSON-Tiefe für ID-Feld, das in einer Beziehung mit mehreren Entitäten verwendet wird | 4 | Weich | **Die empfohlene maximale JSON-Tiefe für ein ID-Feld, das in Beziehungen mit mehreren Entitäten verwendet wird, ist 4.** Dies bedeutet, dass in einem hochverschachtelten Schema Felder, die mehr als vier Ebenen tief verschachtelt sind, nicht als ID-Feld in einer Beziehung verwendet werden sollten. |
| Array-Kardinalität in einem Profil-Fragment | &lt;=500 | Weich | **Die optimale Array-Kardinalität in einem Profil-Fragment (zeitunabhängige Daten) ist  &lt;>** |
| Array-Kardinalität in ExperienceEvent | &lt;=10 | Weich | **Die optimale Array-Kardinalität in einem ExperienceEvent (Zeitreihendaten) ist  &lt;>** |

### Garantieleistungen für Dimensionen

| Guardrail | Maximal | Typ begrenzen | Beschreibung |
| --- | --- | --- | --- |
| Keine Zeitreihendaten zulässig für Nicht-[!DNL XDM Individual Profile]-Entitäten | 0 | Hard | **Zeitreihendaten sind für Nicht-[!DNL XDM Individual Profile] Entitäten im Profil Service nicht zulässig.** Wenn ein Dataset einer Zeitreihe mit einer Nicht-[!DNL XDM Individual Profile] ID verknüpft ist, sollte der Datensatz nicht aktiviert werden  [!DNL Profile]. |
| Keine verschachtelten Beziehungen | 0 | Weich | **Sie sollten keine Beziehung zwischen zwei Nicht-[!DNL XDM Individual Profile] Schemas herstellen.** Die Möglichkeit, Beziehungen zu erstellen, wird nicht für Schema empfohlen, die nicht Teil des Schemas  [!DNL Profile] Vereinigung sind. |
| Maximale JSON-Tiefe für primäres ID-Feld | 4 | Weich | **Die empfohlene maximale JSON-Tiefe für das primäre ID-Feld ist 4.** Das bedeutet, dass Sie in einem hochverschachtelten Schema kein Feld als primäre ID auswählen sollten, wenn es mehr als vier Ebenen tief verschachtelt ist. Ein Feld, das sich auf der vierten verschachtelten Ebene befindet, kann als primäre ID verwendet werden. |

## Datengröße

Die folgenden Garantien beziehen sich auf die Datengröße und werden empfohlen, um sicherzustellen, dass Daten wie gewünscht erfasst, gespeichert und abgefragt werden können.

>[!NOTE]
>
>Die Datengröße wird als unkomprimierte Daten in JSON zum Zeitpunkt der Erfassung gemessen.

### Primär Entitätsgarantien

| Guardrail | Maximal | Typ begrenzen | Beschreibung |
| --- | --- | --- | --- |
| Maximale Größe pro Profil | 10 KB | Weich | **Die empfohlene Maximalgröße für ein Profil-Fragment beträgt 10 KB.** Die Erfassung größerer Profil-Fragmente wirkt sich auf die Systemleistung aus. Das Laden eines umfangreichen CRM-Datensatzes mit einer Größe von 50 kB, in dem einige Profil-Fragmente enthalten sind, führt beispielsweise zu einer Beeinträchtigung der Systemleistung. |
| Absolute Maximalgröße pro Profil-Fragment | 1 MB | hart | **Die absolute Maximalgröße eines Profil-Fragments beträgt 1 MB.** Die Auslastung schlägt fehl, wenn versucht wird, ein Profil-Fragment hochzuladen, das größer als 1 MB ist. |

### Garantieleistungen für Dimensionen

| Guardrail | Maximal | Typ begrenzen | Beschreibung |
| --- | --- | --- | --- |
| Maximale Gesamtgröße für alle dimensionalen Entitäten | 5 GB | Weich | **Die maximal empfohlene Gesamtgröße für alle dimensionalen Entitäten beträgt 5 GB.** Die Erfassung von Entitäten mit großer Dimension führt zu einer Beeinträchtigung der Systemleistung. Beispielsweise wird der Versuch, einen 10-GB-Produktkatalog als Dimensionentität zu laden, nicht empfohlen. |
| Datenbestände pro dimensionales Entitäts-Schema | 5 | Weich | **Es werden maximal 5 Datensätze empfohlen, die mit jedem dimensionalen Entitäts-Schema verknüpft sind.** Wenn Sie beispielsweise ein Schema für &quot;products&quot;erstellen und fünf beitragende Datensätze hinzufügen, sollten Sie keinen sechsten Datensatz erstellen, der mit dem Schema &quot;products&quot;verknüpft ist. |

## Segmentierungsgarantien

Die in diesem Abschnitt erläuterten Leitlinien beziehen sich auf die Anzahl und Art der Segmente, die ein Unternehmen innerhalb der Experience Platform erstellen kann, sowie auf die Zuordnung und Aktivierung von Segmenten zu Zielen.

| Guardrail | Maximal | Typ begrenzen | Beschreibung |
| --- | --- | --- | --- |
| Maximale Anzahl von Segmenten pro Sandbox | 10 K | Weich | **Die maximale Anzahl von Segmenten, die ein Unternehmen erstellen kann, beträgt 10 KB pro Sandbox.** Eine Organisation kann insgesamt mehr als 10.000 Segmente haben, solange in jeder einzelnen Sandbox weniger als 10.000 Segmente vorhanden sind. Der Versuch, weitere Segmente zu erstellen, führt zu einer Beeinträchtigung der Systemleistung. |
| Maximale Anzahl Streaming-Segmente pro Sandbox | 500 | Weich | **Die maximale Anzahl von Streaming-Segmenten, die ein Unternehmen erstellen kann, beträgt 500 pro Sandbox.** Eine Organisation kann insgesamt über 500 Streaming-Segmente verfügen, sofern in jeder einzelnen Sandbox weniger als 500 Streaming-Segmente vorhanden sind. Der Versuch, zusätzliche Streaming-Segmente zu erstellen, führt zu einer Beeinträchtigung der Systemleistung. |
| Maximale Anzahl an Stapelsegmenten pro Sandbox | 10 K | Weich | **Die maximale Anzahl von Stapelsegmenten, die ein Unternehmen erstellen kann, beträgt 10 KB pro Sandbox.** Ein Unternehmen kann insgesamt mehr als 10.000 Stapelsegmente haben, solange in jeder einzelnen Sandbox weniger als 10.000 Stapelsegmente vorhanden sind. Der Versuch, zusätzliche Stapelsegmente zu erstellen, führt zu einer Beeinträchtigung der Systemleistung. |
