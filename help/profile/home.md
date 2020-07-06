---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Übersicht über das Echtzeit-Kundenprofil
topic: guide
translation-type: tm+mt
source-git-commit: 4d853dfee931789ca1badd410ce0b4b73c8c2803
workflow-type: tm+mt
source-wordcount: '1795'
ht-degree: 2%

---


# Übersicht über das Echtzeit-Kundenprofil

Mit Adobe Experience Platform können Sie koordinierte, konsistente und relevante Erlebnisse für Ihre Kunden fördern, ganz gleich, wo und wann sie mit Ihrer Marke interagieren. Mit Echtzeit-Kundendaten können Sie eine ganzheitliche Ansicht jedes einzelnen Profils anzeigen, die Daten aus mehreren Kanälen, einschließlich Online-, Offline-, CRM- und Drittanbieterdaten, kombiniert. Mit dem Profil können Sie Ihre unterschiedlichen Kundendaten in einer einheitlichen Sicht zusammenfassen, die ein umsetzbares Konto mit Zeitstempel für jede Kundeninteraktion bietet. Diese Übersicht hilft Ihnen, die Rolle und Verwendung von Echtzeit-Kundendaten in der Experience Platform zu verstehen.

## Verstehen des Echtzeit-Profils von Kunden

Real-time Customer Profil ist ein generischer Lookup-Entitätsspeicher, der Daten aus verschiedenen Unternehmensdaten zusammenführt und dann Zugriff auf diese Daten in Form von individuellen Profilen und zugehörigen Zeitreihen-Ereignissen bietet. Diese Funktion ermöglicht es Marketingexperten, koordinierte, konsistente und relevante Erlebnisse mit ihren Audiencen über mehrere Kanal hinweg zu fördern.

### Profil-Datenspeicher

Obwohl Kundendaten in Echtzeit verarbeitet werden und der Identitätsdienst der Adobe Experience Platform verwendet wird, um verwandte Daten mithilfe der Identitätszuordnung zusammenzuführen, verwaltet das Profil seine eigenen Daten im Profil Store. Das heißt, der Profil-Store ist von den Katalogdaten (Data Lake) und den Identitätsdienstdaten (Identitätsdiagramm) getrennt.

### Dienstleistungen von Profil und Platform

Die Beziehung zwischen Echtzeit-Kundenservice und anderen Diensten innerhalb der Experience Platform wird im folgenden Diagramm hervorgehoben:

![Die Beziehung zwischen Profil und anderen Experience Platformen-Services.](images/profile-overview/profile-in-platform.png)

### Profile und Datensatzdaten

Ein Profil ist eine Darstellung eines Subjekts, einer Organisation oder einer Einzelperson, die auch als Datensatzdaten bezeichnet wird. Das Profil eines Produkts kann beispielsweise eine SKU und eine Beschreibung enthalten, während das Profil einer Person Informationen wie Vorname, Nachname und E-Mail-Adresse enthält. Mithilfe der Experience Platform können Sie Profil anpassen, um Datentypen zu verwenden, die für Ihr Unternehmen relevant sind. Die standardmäßige Experience Data Model-(XDM-)Individuelle Profil-Klasse ist die bevorzugte Klasse, auf der ein Schema bei der Beschreibung von Kundendatensätzen erstellt und die Daten bereitgestellt werden, die für viele Interaktionen zwischen Platform-Diensten integriert sind. Weitere Informationen zum Arbeiten mit Schemas in der Experience Platform erhalten Sie zunächst in der [XDM-Systemübersicht](../xdm/home.md).

### Zeitreihen-Ereignisse

Die Zeitreihendaten liefern eine Momentaufnahme des Systems zum Zeitpunkt, zu dem ein Betreff direkt oder indirekt eine Aktion durchführte, sowie Daten, die das Ereignis selbst detailliert beschreiben. Die Zeitreihendaten, die von der XDM ExperienceEvent-Standardklasse vertreten werden, können Ereignis wie zum Beispiel Elemente beschreiben, die einem Einkaufswagen hinzugefügt werden, Links, auf die geklickt wird, und Videos, die angezeigt werden. Zeitreihendaten können verwendet werden, um Segmentierungsregeln zu nutzen, und Ereignis können einzeln im Kontext eines Profils aufgerufen werden.

### Identitäten

Jedes Unternehmen möchte mit seinen Kunden in einer Art und Weise kommunizieren, die sich persönlich anfühlt. Eine der Herausforderungen bei der Bereitstellung relevanter digitaler Erlebnisse für die Kunden besteht jedoch darin, zu verstehen, wie die Daten, die nicht miteinander verbunden sind, miteinander verknüpft werden können. Diese Daten werden häufig über verschiedene digitale Kanal wie Tablets, Mobiltelefone und Laptops verteilt. Mit dem Identitätsdienst können Sie das Gesamtbild Ihres Kunden zusammenstellen, indem Sie Identitäten aus mehreren Kanälen verknüpfen und für jeden Kunden ein Identitätsdiagramm erstellen, das Ihnen ein besseres Verständnis ermöglicht. Weitere Informationen finden Sie in der Übersicht über den [Identitätsdienst](../identity-service/home.md) .

### Segmentierung

Der Segmentierungsdienst für Adobe Experience Platformen stellt die Audiencen bereit, die erforderlich sind, um Erlebnisse für Ihre individuellen Kunden bereitzustellen. Wenn ein Segmentsegment erstellt wird, wird die ID dieses Segments zur Liste der Segmentmitgliedschaften für alle qualifizierten Profil hinzugefügt. Segmentregeln werden mithilfe von RESTful-APIs und der Segmentaufbau-Benutzeroberfläche erstellt und auf Echtzeitdaten von Kunden-Profilen angewendet. Um mehr über die Segmentierung zu erfahren, lesen Sie zunächst die Übersicht über den [Segmentierungsdienst](../segmentation/home.md).

### Profil-Fragmente und Vereinigung-Schemas {#profile-fragments-and-union-schemas}

Eines der Hauptmerkmale von Echtzeit-Kundendaten-Profil ist die Fähigkeit, Daten mit mehreren Kanälen zu vereinen. Wenn Kundendaten in Echtzeit für den Zugriff auf eine Entität verwendet werden, können Sie eine zusammengeführte Ansicht aller Profil-Fragmente für diese Entität über Datensätze hinweg bereitstellen, die als Ansicht der Vereinigung bezeichnet und über ein so genanntes Vereinigung-Schema ermöglicht werden. Echtzeit-Kundendaten werden über mehrere Profil hinweg zusammengeführt, wenn eine Entität oder ein Profil durch ihre ID aufgerufen oder als Segment exportiert wird. Weitere Informationen zum Zugriff auf Profil und Vereinigungen-Ansichten mithilfe der Echtzeit-Client-Profil-API finden Sie im [Entitäts-Endpunkthandbuch](api/entities.md).

### Zusammenführungsrichtlinien

Wenn Daten aus mehreren Quellen zusammengeführt und kombiniert werden, um eine vollständige Ansicht der einzelnen Kunden zu erhalten, gelten für die Zusammenführung der Richtlinien, die Platform verwendet, um zu bestimmen, wie die Daten priorisiert werden und welche Daten kombiniert werden, um eine einheitliche Ansicht zu schaffen. Mit RESTful-APIs oder der Benutzeroberfläche können Sie neue Zusammenführungsrichtlinien erstellen, vorhandene Richtlinien verwalten und eine standardmäßige Zusammenführungsrichtlinie für Ihr Unternehmen festlegen. Weitere Informationen zum Arbeiten mit Zusammenführungsrichtlinien mit der Echtzeit-Profil-API finden Sie im Endpunkthandbuch [zu](api/merge-policies.md)Zusammenführungsrichtlinien. Informationen zum Arbeiten mit Zusammenführungsrichtlinien mithilfe der Benutzeroberfläche &quot;Experience Platform&quot;finden Sie im Benutzerhandbuch [zu Zusammenführungsrichtlinien](ui/merge-policies.md).

### (Alpha) Konfigurieren von berechneten Attributen

>[!IMPORTANT]
>Die in diesem Dokument beschriebene Funktion für berechnete Attribute ist alphanumerisch. Dokumentation und Funktionalität können sich ändern.

Berechnete Attribute ermöglichen es Ihnen, den Feldwert anhand anderer Werte, Berechnungen und Ausdruck automatisch zu berechnen. Berechnete Attribute werden auf Profil-Ebene ausgeführt, d. h., Sie können Werte über alle Datensätze und Ereignis hinweg Aggregat haben. Jedes berechnete Attribut enthält einen Ausdruck, oder &quot;Regel&quot;, der eingehende Daten auswertet und den sich ergebenden Wert in einem Profil-Attribut oder in einem Ereignis speichert. Diese Berechnungen helfen Ihnen, Fragen im Zusammenhang mit dem Kaufwert über die gesamte Lebensdauer, der Zeit zwischen Käufen oder der Anzahl der Anwendungen einfach zu beantworten, ohne dass Sie bei jeder erforderlichen Information manuell komplexe Berechnungen durchführen müssen. Weitere Informationen zu berechneten Attributen und eine schrittweise Anleitung zum Arbeiten mit diesen Attributen mithilfe der Echtzeit-Kunden-Profil-API finden Sie in der Endpunktanleitung zu [berechneten Attributen](api/computed-attributes.md). Dieses Handbuch hilft Ihnen, die Rolle, die berechnete Attribute innerhalb der Adobe Experience Platform spielen, besser zu verstehen. Es enthält Beispiel-API-Aufrufe zur Durchführung grundlegender CRUD-Vorgänge.

## Echtzeitkomponenten

In diesem Abschnitt werden die Komponenten vorgestellt, mit denen Echtzeit-Kundendaten in Echtzeit aktualisiert und überwacht werden können.

### Streaming-Erfassung und Streaming-Segmentierung

Die Echtzeiteingabe wird durch einen Prozess ermöglicht, der als Streaming-Erfassung bezeichnet wird. Während Profil- und Zeitreihendaten erfasst werden, entscheidet sich das Echtzeit-Profil automatisch, diese Daten über einen laufenden Prozess namens Streaming-Segmentierung einzubeziehen oder auszuschließen, bevor sie mit vorhandenen Daten zusammengeführt und die Vereinigung-Ansicht aktualisiert wird. Infolgedessen können Sie sofort Berechnungen durchführen und Entscheidungen treffen, um Kunden bei der Interaktion mit Ihrer Marke erweiterte, individualisierte Erlebnisse bereitzustellen. Während der Erfassung werden die Daten auch überprüft, um sicherzustellen, dass sie ordnungsgemäß erfasst werden und dem Schema entsprechen, auf dem der Datensatz basiert. Für weitere Informationen darüber, was während der Erfassung validiert wird, lesen Sie bitte zunächst die Qualitätsübersicht [zur](../ingestion/quality/overview.md)Datenerfassung.

### Edge-Projektionskonfigurationen und -ziele

Um koordinierte, konsistente und personalisierte Erlebnisse für Ihre Kunden über mehrere Kanal hinweg in Echtzeit zu ermöglichen, müssen die richtigen Daten jederzeit verfügbar sein und im Zuge von Änderungen kontinuierlich aktualisiert werden. Adobe Experience Platform ermöglicht diesen Echtzeitzugriff auf Daten durch die Verwendung von so genannten Rändern. Ein Edge ist ein geografisch platzierter Server, der Daten speichert und für Anwendungen leicht zugänglich macht. Adobe-Anwendungen wie Adobe Target und Adobe Campaign verwenden beispielsweise Kanten, um personalisierte Kundenerlebnisse in Echtzeit bereitzustellen. Die Daten werden durch eine Projektion an eine Kante geleitet, wobei ein Projektionsziel die Kante definiert, an die die Daten gesendet werden, und eine Projektionskonfiguration, die die spezifischen Informationen definiert, die an der Kante zur Verfügung gestellt werden. Weitere Informationen und die Arbeit mit Projektionen mithilfe der Echtzeit-Customer Profil API finden Sie im Handbuch [Edge-Projektions-Endpunkte](api/edge-projections.md).

## Daten Hinzufügen Echtzeit-Profil

Die Platform kann so konfiguriert werden, dass Daten zu Datensatz und Zeitreihen an Profil gesendet werden. Dies unterstützt Echtzeit-Streaming-Erfassung und Stapelverarbeitung. Weitere Informationen finden Sie in der Übung, in der das [Hinzufügen von Daten zum Echtzeit-Kundenkonto](tutorials/add-profile-data.md)beschrieben wird.

>[!NHinweis]
>Daten, die über Adobe-Lösungen erfasst werden, einschließlich Analytics Cloud, Marketing Cloud und Advertising Cloud, fließen in die Experience Platform und werden in Profil erfasst.

### Profil-Erfassungsmetriken

Mithilfe von &quot;Observability Insights&quot;können Sie wichtige Metriken in der Adobe Experience Platform verfügbar machen. Zusätzlich zu den Nutzungsstatistiken und Leistungsindikatoren für verschiedene Funktionen der Platform gibt es spezifische Profil-bezogene Metriken, mit denen Sie Einblicke in eingehende Anforderungsraten, erfolgreiche Erfassungsraten, erfasste Datensatzgrößen und mehr gewinnen können. Weitere Informationen finden Sie in der Übersicht über die [Beobachtungseinblicke](../observability/home.md). Eine vollständige Liste der Profil-Metriken finden Sie in der Dokumentation zu den [verfügbaren Metriken](../observability/metrics.md).

## Datenverwaltung und Datenschutz

Die Datenverwaltung ist eine Reihe von Strategien und Technologien, mit denen Kundendaten verwaltet und die Einhaltung von Vorschriften, Einschränkungen und Richtlinien für die Datenverwendung sichergestellt werden.

Im Hinblick auf den Zugriff auf Daten spielt die Datenverwaltung auf verschiedenen Ebenen eine Schlüsselrolle in der Experience Platform:
* Beschriftung der Datenverwendung
* Datenschutzrichtlinien
* Zugriffskontrolle über Daten zu Marketingaktionen

Die Datenverwaltung wird an verschiedenen Punkten verwaltet. Dazu gehört die Entscheidung, welche Daten in die Platform eingebunden werden und welche Daten nach der Erfassung für eine bestimmte Marketingaktion verfügbar sind. Weitere Informationen finden Sie in der Übersicht über die [Datenverwaltung](../data-governance/home.md).

### Bearbeitung von Ausschluss- und Datenschutzanfragen

Mit der Experience Platform können Ihre Kunden Abmeldeanfragen im Zusammenhang mit der Nutzung und Datenspeicherung ihrer Daten innerhalb des Echtzeit-Profils senden. Weitere Informationen zur Bearbeitung von Opt-out-Anfragen finden Sie in der Dokumentation zur [Berücksichtigung von Opt-out-Anfragen](../segmentation/honoring-opt-outs.md).

## Profil-Leitlinien

Die Experience Platform hat eine Reihe von Leitlinien zu beachten, um Profil effektiv zu nutzen.

| Abschnitt | Grenze |
| ------- | -------- |
| Profil Vereinigung Schema | Maximal **20** Datensätze können zum Schema der Profil-Vereinigung beitragen. |
| Beziehungen zwischen mehreren Entitäten | Es können maximal **5** Beziehungen mit mehreren Entitäten erstellt werden. |
| JSON-Tiefe für mehrere Entitäten | Die maximale JSON-Tiefe beträgt **4**. |
| Zeitreihendaten | Zeitreihendaten sind im Profil für Nicht-Personen-Entitäten **nicht** zulässig. |
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
>Eine Nicht-Person-Entität bezieht sich auf jede XDM-Klasse, die **nicht** zum Profil gehört.

## Nächste Schritte und zusätzliche Ressourcen

Um mehr über Echtzeit-Kundensupport zu erfahren, lesen Sie bitte die Dokumentation weiter und ergänzen Sie Ihre Kenntnisse, indem Sie sich das unten stehende Video ansehen oder andere [Experience Platform-Videolehrgänge](https://docs.adobe.com/content/help/en/platform-learn/tutorials/overview.html)erkunden.

>[!WARNING]
>Die Benutzeroberfläche der Platform, die im folgenden Video gezeigt wird, ist veraltet. Die neuesten Screenshots und Funktionen der Benutzeroberfläche finden Sie im Benutzerhandbuch [zum](ui/user-guide.md) Echtzeit-Profil.

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12)