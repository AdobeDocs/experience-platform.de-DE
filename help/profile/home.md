---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Übersicht über das Echtzeit-Kundenprofil
topic: guide
translation-type: tm+mt
source-git-commit: d349ffab7c0de72d38b5195585c14a4a8f80e37c
workflow-type: tm+mt
source-wordcount: '1636'
ht-degree: 3%

---


# Übersicht über das Echtzeit-Kundenprofil

Mit der Adobe Experience Platform können Sie koordinierte, konsistente und relevante Erlebnisse für Ihre Kunden bereitstellen, unabhängig davon, wo und wann sie mit Ihrer Marke interagieren. Mit Echtzeit-Kundendaten können Sie eine ganzheitliche Ansicht jedes einzelnen Profils anzeigen, die Daten aus mehreren Kanälen, einschließlich Online-, Offline-, CRM- und Drittanbieterdaten, kombiniert. Mit dem Profil können Sie Ihre unterschiedlichen Kundendaten in einer einheitlichen Sicht zusammenfassen, die ein umsetzbares Konto mit Zeitstempel für jede Kundeninteraktion bietet. Diese Übersicht hilft Ihnen, die Rolle und Verwendung von Echtzeit-Kundendaten in Experience Platform zu verstehen.

## Verstehen des Echtzeit-Profils von Kunden

Real-time Customer Profil ist ein generischer Lookup-Entitätsspeicher, der Daten aus verschiedenen Unternehmensdaten zusammenführt und dann Zugriff auf diese Daten in Form von individuellen Profilen und zugehörigen Zeitreihen-Ereignissen bietet. Diese Funktion ermöglicht es Marketingexperten, koordinierte, konsistente und relevante Erlebnisse mit ihren Audiencen über mehrere Kanal hinweg zu fördern.

### Profil-Datenspeicher

Obwohl Kundendaten in Echtzeit verarbeitet werden und der Adobe Experience Platform Identity Service zum Zusammenführen verwandter Daten über die Identitätszuordnung verwendet wird, verwaltet das Profil seine eigenen Daten im Profil Store. Das heißt, der Profil-Store ist von den Katalogdaten (Data Lake) und den Identitätsdienstdaten (Identitätsdiagramm) getrennt.

### Profil- und Plattformdienste

Die Beziehung zwischen dem Echtzeit-Kundendienst und anderen Diensten in Experience Platform wird in der folgenden Abbildung hervorgehoben:

![Die Beziehung zwischen Profil und anderen Experience Platform-Diensten.](images/profile-overview/profile-in-platform.png)

### Profile und Datensatzdaten

Ein Profil ist eine Darstellung eines Subjekts, einer Organisation oder einer Einzelperson, die auch als Datensatzdaten bezeichnet wird. Das Profil eines Produkts kann beispielsweise eine SKU und eine Beschreibung enthalten, während das Profil einer Person Informationen wie Vorname, Nachname und E-Mail-Adresse enthält. Mithilfe der Experience Platform können Sie Profil so anpassen, dass für Ihr Unternehmen relevante Datentypen verwendet werden. Die standardmäßige Experience Data Model-(XDM-)Individuelle Profil-Klasse ist die bevorzugte Klasse, auf der ein Schema bei der Beschreibung von Kundendatensätzen erstellt und die Daten bereitgestellt werden, die für viele Interaktionen zwischen Plattformdiensten unentbehrlich sind. Weitere Informationen zum Arbeiten mit Schemas in Experience Platform erhalten Sie zunächst in der [XDM-Systemübersicht](../xdm/home.md).

### Zeitreihen-Ereignisse

Die Zeitreihendaten liefern eine Momentaufnahme des Systems zum Zeitpunkt, zu dem ein Betreff direkt oder indirekt eine Aktion durchführte, sowie Daten, die das Ereignis selbst detailliert beschreiben. Die Zeitreihendaten, die von der XDM ExperienceEvent-Standardklasse vertreten werden, können Ereignis wie zum Beispiel Elemente beschreiben, die einem Einkaufswagen hinzugefügt werden, Links, auf die geklickt wird, und Videos, die angezeigt werden. Zeitreihendaten können verwendet werden, um Segmentierungsregeln zu nutzen, und Ereignis können einzeln im Kontext eines Profils aufgerufen werden.

### Identitäten

Jedes Unternehmen möchte mit seinen Kunden in einer Art und Weise kommunizieren, die sich persönlich anfühlt. Eine der Herausforderungen bei der Bereitstellung relevanter digitaler Erlebnisse für die Kunden besteht jedoch darin, zu verstehen, wie die Daten, die nicht miteinander verbunden sind, miteinander verknüpft werden können. Diese Daten werden häufig über verschiedene digitale Kanal wie Tablets, Mobiltelefone und Laptops verteilt. Mit dem Identitätsdienst können Sie das Gesamtbild Ihres Kunden zusammenstellen, indem Sie Identitäten aus mehreren Kanälen verknüpfen und für jeden Kunden ein Identitätsdiagramm erstellen, das Ihnen ein besseres Verständnis ermöglicht. Weitere Informationen finden Sie in der Übersicht über den [Identitätsdienst](../identity-service/home.md) .

### Segmentierung

Der Segmentierungsdienst für Adobe Experience Platform stellt die Audiencen bereit, die erforderlich sind, um Erlebnisse für Ihre individuellen Kunden bereitzustellen. Wenn ein Segmentsegment erstellt wird, wird die ID dieses Segments zur Liste der Segmentmitgliedschaften für alle qualifizierten Profil hinzugefügt. Segmentregeln werden mithilfe von RESTful-APIs und der Segmentaufbau-Benutzeroberfläche erstellt und auf Echtzeitdaten von Kunden-Profilen angewendet. Um mehr über die Segmentierung zu erfahren, lesen Sie zunächst die Übersicht über den [Segmentierungsdienst](../segmentation/home.md).

### Profil-Fragmente und Vereinigung-Schemas {#profile-fragments-and-union-schemas}

Eines der Hauptmerkmale von Echtzeit-Kundendaten-Profil ist die Fähigkeit, Daten mit mehreren Kanälen zu vereinen. Wenn Kundendaten in Echtzeit für den Zugriff auf eine Entität verwendet werden, können Sie eine zusammengeführte Ansicht aller Profil-Fragmente für diese Entität über Datensätze hinweg bereitstellen, die als Ansicht der Vereinigung bezeichnet und über ein so genanntes Vereinigung-Schema ermöglicht werden. Echtzeit-Kundendaten werden über mehrere Profil hinweg zusammengeführt, wenn eine Entität oder ein Profil durch ihre ID aufgerufen oder als Segment exportiert wird. Weitere Informationen zum Zugriff auf Profil und Vereinigungen-Ansichten finden Sie im Unterleitfaden für Kunden-Profil-API-Entwickler in Echtzeit zu [Entitäten, auch als &quot;Profil-Zugriff&quot;](api/entities.md)bezeichnet.

### Zusammenführungsrichtlinien

Wenn Daten aus mehreren Quellen zusammengeführt und kombiniert werden, um eine vollständige Ansicht der einzelnen Kunden zu erhalten, gelten für die Zusammenführung der Richtlinien, die Plattform verwendet, um zu bestimmen, wie die Daten priorisiert werden und welche Daten kombiniert werden, um eine einheitliche Ansicht zu schaffen. Mit RESTful-APIs oder der Benutzeroberfläche können Sie neue Zusammenführungsrichtlinien erstellen, vorhandene Richtlinien verwalten und eine standardmäßige Zusammenführungsrichtlinie für Ihr Unternehmen festlegen. Weitere Informationen zum Arbeiten mit Zusammenführungsrichtlinien mithilfe von APIs finden Sie im [Leitfaden](api/merge-policies.md) zu Zusammenführungsrichtlinien für Kunden-Profil-API in Echtzeit oder im Benutzerhandbuch [zu](ui/merge-policies.md) Zusammenführungsrichtlinien für die Verwendung von Zusammenführungsrichtlinien mithilfe der Plattform-Benutzeroberfläche.

## (Alpha) Konfigurieren von berechneten Attributen

>[!IMPORTANT]
>Die in diesem Dokument beschriebene Funktion für berechnete Attribute ist alphanumerisch. Dokumentation und Funktionalität können sich ändern.

Berechnete Attribute ermöglichen es Ihnen, den Feldwert anhand anderer Werte, Berechnungen und Ausdruck automatisch zu berechnen. Berechnete Attribute werden auf Profil-Ebene ausgeführt, d. h., Sie können Werte über alle Datensätze und Ereignis hinweg Aggregat haben. Jedes berechnete Attribut enthält einen Ausdruck, oder &quot;Regel&quot;, der eingehende Daten auswertet und den sich ergebenden Wert in einem Profil-Attribut oder in einem Ereignis speichert. Diese Berechnungen helfen Ihnen, Fragen im Zusammenhang mit dem Kaufwert über die gesamte Lebensdauer, der Zeit zwischen Käufen oder der Anzahl der Anwendungen einfach zu beantworten, ohne dass Sie bei jeder erforderlichen Information manuell komplexe Berechnungen durchführen müssen. Weitere Informationen zu berechneten Attributen und eine schrittweise Anleitung zum Arbeiten mit diesen Attributen finden Sie im [Unterhandbuch zur Echtzeit-Client-Profil-API zu berechneten Attributen](api/computed-attributes.md). Dieses Handbuch hilft Ihnen, die Rolle von berechneten Attributen in Adobe Experience Platform besser zu verstehen. Es enthält Beispiel-API-Aufrufe für grundlegende CRUD-Vorgänge mit der Echtzeit-Client-Profil-API.

## Echtzeitkomponenten

In diesem Abschnitt werden die Komponenten vorgestellt, mit denen Echtzeit-Kundendaten in Echtzeit aktualisiert und überwacht werden können.

### Streaming-Erfassung und Streaming-Segmentierung

Die Echtzeiteingabe wird durch einen Prozess ermöglicht, der als Streaming-Erfassung bezeichnet wird. Während Profil- und Zeitreihendaten erfasst werden, entscheidet sich das Echtzeit-Profil automatisch, diese Daten über einen laufenden Prozess namens Streaming-Segmentierung einzubeziehen oder auszuschließen, bevor sie mit vorhandenen Daten zusammengeführt und die Vereinigung-Ansicht aktualisiert wird. Dadurch können Sie sofort Berechnungen durchführen und Entscheidungen treffen, um Kunden bei der Interaktion mit Ihrer Marke erweiterte, individualisierte Erlebnisse bereitzustellen. Während der Erfassung werden die Daten auch überprüft, um sicherzustellen, dass sie ordnungsgemäß erfasst werden und dem Schema entsprechen, auf dem der Datensatz basiert. Für weitere Informationen darüber, was während der Erfassung validiert wird, lesen Sie bitte zunächst den Überblick über die [Datenerhebungsqualität](../ingestion/quality/overview.md).

### Edge-Prognosen

Um koordinierte, konsistente und personalisierte Erlebnisse für Ihre Kunden über mehrere Kanal hinweg in Echtzeit zu ermöglichen, müssen die richtigen Daten jederzeit verfügbar sein und im Zuge von Änderungen kontinuierlich aktualisiert werden. Adobe Experience Platform ermöglicht diesen Echtzeitzugriff auf Daten durch die Verwendung von so genannten Kanten. Ein Edge ist ein geografisch platzierter Server, der Daten speichert und für Anwendungen leicht zugänglich macht. Adobe-Anwendungen wie Adobe Zielgruppe und Adobe Campaign verwenden beispielsweise Kanten, um personalisierte Kundenerlebnisse in Echtzeit bereitzustellen. Die Daten werden durch eine Projektion an eine Kante geleitet, wobei ein Projektionsziel die Kante definiert, an die die Daten gesendet werden, und eine Projektionskonfiguration, die die spezifischen Informationen definiert, die an der Kante zur Verfügung gestellt werden. Weitere Informationen und die Arbeit mit Kanten und Projektionen finden Sie im [Unterleitfaden](api/edge-projections.md)zur Echtzeit-Client-Profil-API für Edge-Projektionen.

## Daten Hinzufügen Echtzeit-Profil

Die Plattform kann so konfiguriert werden, dass Ihre Daten zu Datensatz und Zeitreihen an Profil gesendet werden. Dies unterstützt Echtzeit-Streaming-Erfassung und Stapelverarbeitung. Weitere Informationen finden Sie in der Übung, in der das [Hinzufügen von Daten zum Echtzeit-Kundenkonto](tutorials/add-profile-data.md)beschrieben wird.

>[!Note]
>Daten, die mit Adobe-Lösungen wie Analytics Cloud, Marketing Cloud und Advertising Cloud erfasst werden, fließen in die Experience Platform und werden in Profil erfasst.

### Profil-Streaming-Erfassungsmetriken

Mithilfe von &quot;Observability Insights&quot;können Sie wichtige Metriken in Adobe Experience Platform bereitstellen. Zusätzlich zu den Statistiken zur Plattformnutzung und Leistungsindikatoren für verschiedene Plattformfunktionalitäten gibt es spezifische Metriken zum Profil, mit denen Sie Einblicke in eingehende Anforderungsraten, erfolgreiche Erfassungsraten, erfasste Datensatzgrößen und mehr gewinnen können. Weitere Informationen finden Sie in der Übersicht über die [Beobachtungseinblicke](../observability/home.md). Eine vollständige Liste der Profil-Metriken finden Sie in der Dokumentation zu den [verfügbaren Metriken](../observability/metrics.md).

## Datenverwaltung und Datenschutz

Die Datenverwaltung ist eine Reihe von Strategien und Technologien, mit denen Kundendaten verwaltet und die Einhaltung von Vorschriften, Einschränkungen und Richtlinien für die Datenverwendung sichergestellt werden.

Da es sich um den Zugriff auf Daten handelt, spielt die Datenverwaltung auf verschiedenen Ebenen in der Experience Platform eine Schlüsselrolle:
* Beschriftung der Datenverwendung
* Datenschutzrichtlinien
* Zugriffskontrolle über Daten zu Marketingaktionen

Die Datenverwaltung wird an verschiedenen Punkten verwaltet. Dazu gehört die Entscheidung, welche Daten in die Plattform eingebunden werden und welche Daten nach der Erfassung für eine bestimmte Marketingaktion verfügbar sind. Weitere Informationen finden Sie in der Übersicht über die [Datenverwaltung](../data-governance/home.md).

### Bearbeitung von Ausschluss- und Datenschutzanfragen

Mit der Experience Platform können Ihre Kunden Abmeldeanfragen im Zusammenhang mit der Nutzung und Datenspeicherung ihrer Daten innerhalb des Echtzeit-Profils des Kunden senden. Weitere Informationen zur Bearbeitung von Opt-out-Anfragen finden Sie in der Dokumentation zur [Berücksichtigung von Opt-out-Anfragen](../segmentation/honoring-opt-outs.md).

## Nächste Schritte und zusätzliche Ressourcen

Weitere Informationen zum Echtzeit-Profil von Kunden erhalten Sie, wenn Sie die Dokumentation in diesem Handbuch lesen und Ihr Lernen durch das Video unten ergänzen oder andere Videoschulungen zu [Experience Platform erkunden](https://docs.adobe.com/content/help/en/platform-learn/tutorials/overview.html).

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12)