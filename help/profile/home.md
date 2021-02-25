---
keywords: Experience Platform;Profil;Echtzeit-Profil des Kunden;Fehlerbehebung;API;Einheitliches Profil;Einheitliches Profil;Profil;RTCP;XDM-Diagramme
title: Übersicht über das Echtzeit-Profil von Kunden
topic: guide
description: Das Echtzeit-Kundenprofil ist ein allgemeiner Suchentitäten-Speicher, in dem Informationen aus verschiedensten Datenquellen des Unternehmens zusammengeführt und zum Abruf verfügbar gemacht werden. Diese Daten werden in Form von individuellen Kundenprofilen sowie zugehörigen im Zeitverlauf erfassten, so genannten Zeitreihen-Ereignissen aufbereitet, die es Marketing-Experten ermöglichen, über verschiedenste Kanäle hinweg koordinierte, konsistente und relevante Erlebnisse für ihre Zielgruppen umzusetzen.
translation-type: tm+mt
source-git-commit: 08eff53f107549fab0f167a6c206b632f3c8c183
workflow-type: tm+mt
source-wordcount: '1825'
ht-degree: 39%

---


# [!DNL Real-time Customer Profile]Übersicht

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Kunden, unabhängig davon, wo und wann diese mit Ihrer Marke interagieren. Mit [!DNL Real-time Customer Profile] können Sie eine ganzheitliche Ansicht jedes einzelnen Kunden anzeigen, indem Sie Daten aus mehreren Kanälen, einschließlich Online-, Offline-, CRM- und Drittanbieterdaten, kombinieren. [!DNL Profile] ermöglicht es Ihnen, Ihre Kundendaten in einer einheitlichen Ansicht zusammenzufassen, die Ihnen einen umsetzbaren Zeitstempel für jede Kundeninteraktion bietet. Diese Übersicht hilft Ihnen, die Rolle und Verwendung von [!DNL Real-time Customer Profile] in [!DNL Experience Platform] zu verstehen.

## [!DNL Profile] in Experience Platform

Die nachfolgende Abbildung zeigt die Zusammenhänge zwischen dem Echtzeit-Kundenprofil und anderen Services in Experience Platform:

![](images/profile-overview/profile-in-platform.png)

## Profile verstehen

[!DNL Real-time Customer Profile] führt Daten aus verschiedenen Unternehmenssystemen zusammen und ermöglicht dann den Zugriff auf diese Daten in Form von Profilen mit zugehörigen Zeitreihen-Ereignissen. die es Marketing-Experten ermöglichen, über verschiedenste Kanäle hinweg koordinierte, konsistente und relevante Erlebnisse für ihre Zielgruppen umzusetzen. In den folgenden Abschnitten werden einige der Kernkonzepte hervorgehoben, die Sie verstehen müssen, um Profile innerhalb der Plattform effektiv zu erstellen und zu verwalten.

### Profil-Datenspeicher

Obwohl [!DNL Real-time Customer Profile] erfasste Daten verarbeitet und Adobe Experience Platform [!DNL Identity Service] verwendet, um verwandte Daten mithilfe der Identitätszuordnung zusammenzuführen, werden im [!DNL Profile]-Datenspeicher eigene Daten gespeichert. Der [!DNL Profile]-Speicher ist getrennt von Katalogdaten im Datensee und [!DNL Identity Service] Daten im Identitätsdiagramm.

Der Profil-Store verwendet eine Microsoft Azurblase Cosmos DB-Infrastruktur und der Platform Data Lake verwendet Microsoft Azurblase Data Lake Datenspeicherung.

### Profil-Guardraht

Experience Platform bietet eine Reihe von Garantieleistungen, mit denen Sie vermeiden können, [Erlebnisdatenmodell (XDM)-Schema](../xdm/home.md) zu erstellen, die vom Echtzeit-Kundendienstprogramm nicht unterstützt werden können. Dies umfasst weiche Beschränkungen, die zu Leistungsbeeinträchtigungen führen, sowie harte Beschränkungen, die zu Fehlern und Systembrüchen führen. Weitere Informationen, einschließlich einer Liste von Richtlinien und Beispielanwendungsfällen, finden Sie in der [Profil Guardrails](guardrails.md) Dokumentation.

### (Beta) Profil Dashboard {#profile-dashboard}

>[!IMPORTANT]
>
>Die Dashboard-Funktion befindet sich derzeit in der Beta-Version und steht nicht allen Benutzern zur Verfügung. Die Dokumentation und Funktionalität können sich ändern.

Die Benutzeroberfläche der Experience Platform bietet ein Dashboard, mit dem Sie wichtige Informationen zu Ihren Echtzeit-Kundendaten, wie sie in einem täglichen Schnappschuss erfasst werden, Ansichten vornehmen können. Weitere Informationen zum Zugriff auf und zum Arbeiten mit dem [!DNL Profile]-Dashboard in der Benutzeroberfläche sowie detaillierte Informationen zu den im Dashboard angezeigten Metriken finden Sie im Handbuch [Profil Dashboard UI guide](ui/profile-dashboard.md).

### Fragmente im Profil im Vergleich zu zusammengeführten Profilen {#profile-fragments-vs-merged-profiles}

Jedes einzelne Profil besteht aus mehreren Profil-Fragmenten, die zu einer einzigen Ansicht des Kunden zusammengeführt wurden. Wenn ein Kunde beispielsweise über mehrere Kanal mit Ihrer Marke interagiert, enthält Ihr Unternehmen mehrere Profil-Fragmente, die sich auf diesen einzelnen Kunden beziehen und in mehreren Datensätzen angezeigt werden. Wenn diese Fragmente in eine Plattform integriert werden, werden sie zusammengeführt, um ein einzelnes Profil für diesen Kunden zu erstellen.

Wenn die Daten aus mehreren Quellen in Konflikt geraten (z. B. ein Fragment als &quot;Einzel&quot;, während die anderen Listen als &quot;verheiratet&quot;Liste werden), bestimmt die [Zusammenführungsrichtlinie](#merge-policies), welche Informationen priorisiert und in das Profil für die Einzelperson aufgenommen werden sollen. Daher ist die Gesamtanzahl der Fragmente innerhalb der Plattform wahrscheinlich höher als die Gesamtanzahl der zusammengeführten Profile, da jedes Profil aus mehreren Fragmenten besteht.

### Daten aufzeichnen

Ein Profil ist eine Darstellung eines Subjekts, einer Organisation oder einer Einzelperson, die aus vielen Attributen besteht (auch als Datensatzdaten bezeichnet). So kann etwa ein Produktprofil eine SKU und eine Beschreibung enthalten, während in einem Personenprofil Informationen wie Vorname, Nachname und E-Mail-Adresse erfasst sind. Mithilfe von [!DNL Experience Platform] können Sie Profil anpassen, um bestimmte Daten zu verwenden, die für Ihr Unternehmen relevant sind. Die Standard-Klasse [!DNL Experience Data Model] (XDM), [!DNL XDM Individual Profile], ist die bevorzugte Klasse, auf der ein Schema bei der Beschreibung von Kundendatensätzen erstellt werden sollte, und stellt die Datenintegralität zu vielen Interaktionen zwischen Plattformdiensten bereit. Weitere Informationen zum Arbeiten mit Schemas in [!DNL Experience Platform] finden Sie im [XDM-Systemüberblick](../xdm/home.md).

### Zeitreihen-Ereignisse

Zeitreihendaten liefern eine Momentaufnahme des Systems zu dem Zeitpunkt, an dem ein Subjekt direkt oder indirekt eine Aktion ausgeführt hat, sowie Daten mit Details zu dem Ereignis selbst. Zeitreihendaten werden im Schema anhand der Standardklasse XDM ExperienceEvent dargestellt. Sie beschreiben Ereignisse wie etwa das Hinzufügen eines Artikels zu einem Warenkorb, das Klicken auf einen Link, das Abspielen eines Videos usw. Auf Grundlage von Zeitreihendaten können Segmentierungsregeln eingerichtet werden. Die einzelnen Ereignisse sind dabei im Kontext eines Profils abrufbar.

### Identitäten

Bei der Kommunikation mit Kunden gilt es, diese in einer auf sie persönlich abgestimmte Weise anzusprechen. Die Umsetzung solcher für Kunden relevanter digitaler Erlebnisse ist jedoch eine Herausforderung. Denn dazu muss nachvollzogen werden, wie die verschiedenen Daten, die sie auf voneinander getrennten digitalen Kanälen wie Tablets, Smartphones und Laptops generieren, zueinander in Zusammenhang stehen. [!DNL Identity Service] ermöglicht es Ihnen, das Gesamtbild Ihres Kunden zusammenzustellen, indem Sie Identitäten aus mehreren Kanälen verknüpfen und ein Identitätsdiagramm für jeden Kunden erstellen. Weitere Informationen finden Sie in der [Identity Service – Übersicht](../identity-service/home.md).

### Zusammenführungsrichtlinien

Wenn Sie Datenfragmente aus mehreren Quellen zusammenführen und sie kombinieren, um eine vollständige Ansicht der einzelnen Kunden zu erhalten, sind Zusammenführungsrichtlinien die Regeln, mit denen [!DNL Platform] bestimmt wird, wie die Daten priorisiert werden und welche Daten zur Erstellung des Profils verwendet werden. Wenn Daten aus mehreren Datensätzen miteinander in Konflikt stehen, bestimmt die Richtlinie zum Zusammenführen, wie diese Daten behandelt werden und welcher Wert verwendet werden soll. Über die RESTful APIs oder die Benutzeroberfläche können Sie neue Zusammenführungsrichtlinien erstellen, vorhandene Richtlinien verwalten und eine standardmäßige Zusammenführungsrichtlinie für Ihr Unternehmen einrichten.

Weitere Informationen zum Arbeiten mit Zusammenführungsrichtlinien mithilfe der API finden Sie im Endpunktleitfaden [Zusammenführungsrichtlinien](api/merge-policies.md). [!DNL Real-time Customer Profile] Informationen zum Arbeiten mit Zusammenführungsrichtlinien mithilfe der [!DNL Experience Platform]-Benutzeroberfläche finden Sie im Handbuch [Zusammenführungsrichtlinien ](ui/merge-policies.md).

### Vereinigung Schema {#profile-fragments-and-union-schemas}

Eines der Hauptmerkmale von [!DNL Real-time Customer Profile] ist die Fähigkeit, Daten mit mehreren Kanälen zu vereinen. Wenn [!DNL Real-time Customer Profile] für den Zugriff auf eine Entität verwendet wird, können Sie eine zusammengeführte Ansicht aller Profil-Fragmente für diese Entität über Datensätze hinweg bereitstellen, die als &quot;Vereinigung-Ansicht&quot;bezeichnet und über das so genannte Vereinigung-Schema ermöglicht werden.

Weitere Informationen zu Schemas in der Vereinigung, einschließlich dem Zugriff auf Vereinigung-Schema in der Benutzeroberfläche, finden Sie im Handbuch [Vereinigung Schema UI guide](ui/union-schema.md).

### (Alpha) Berechnete Attribute

>[!IMPORTANT]
>
>Die Funktion für berechnete Attribute ist alphanumerisch. Die Dokumentation und Funktionalität können sich ändern.

Berechnete Attribute sind Funktionen, mit denen Daten auf Ereignis-Ebene in Attribute auf Profil-Ebene Aggregat werden. Diese Funktionen werden automatisch berechnet, sodass sie für die Segmentierung, Aktivierung und Personalisierung verwendet werden können. Mit diesen Berechnungen können Sie Fragen im Zusammenhang mit dem Kaufwert über die gesamte Lebensdauer, der Zeit zwischen Käufen oder der Anzahl der Anwendungsöffnungen leicht beantworten, ohne für jede benötigte Information manuell komplexe Berechnungen ausführen zu müssen. Weitere Informationen zu berechneten Attributen, einschließlich eines Verständnisses der Rolle, die berechnete Attribute innerhalb von Adobe Experience Platform spielen, erhalten Sie zunächst unter [Übersicht über berechnete Attribute](computed-attributes/overview.md).

## Profil und Segmente

Adobe Experience Platform [!DNL Segmentation Service] stellt die Audiencen bereit, die erforderlich sind, um Erlebnisse für Ihre individuellen Kunden bereitzustellen. Wird ein solches Zielgruppensegment erstellt, wird dessen Segment-ID zur Liste der Segmentmitglieder für alle qualifizierten Profile hinzugefügt. Segmentregeln werden mithilfe RESTful-APIs und der Segment Builder-Benutzeroberfläche erstellt und auf [!DNL Real-time Customer Profile]-Daten angewendet. Um mehr über die Segmentierung zu erfahren, lesen Sie zunächst die [Segmentation Service – Übersicht](../segmentation/home.md).

### Streaming-Erfassung und Streaming-Segmentierung

Der Prozess, Daten in Echtzeit zu erfassen, wird als Streaming-Erfassung bezeichnet. Bei der Erfassung von Profil- und Zeitreihendaten entscheidet [!DNL Real-time Customer Profile] automatisch, diese Daten über einen laufenden Prozess namens Streaming-Segmentierung einzubeziehen oder auszuschließen, bevor sie mit vorhandenen Daten zusammengeführt und die Ansicht der Vereinigung aktualisiert werden. Das Ergebnis: Berechnungen und Entscheidungen dazu, wie Sie Ihren Kunden herausragende, individuell auf sie abgestimmte Erlebnisse liefern, lassen sich direkt während ihrer Interaktion mit Ihrer Marke anstellen bzw. treffen. Im Verlauf der Datenaufnahme wird außerdem validiert, ob die Daten ordnungsgemäß erfasst werden und dem Schema entsprechen, auf dem der Datensatz basiert. Weitere Informationen dazu, welche Validierungen bei der Datenaufnahme vorgenommen werden, finden Sie in der Übersicht über die Datenaufnahme unter [Datenqualität](../ingestion/quality/overview.md).

## Edge-Projektionen

Um koordinierte, konsistente und personalisierte Erlebnisse für Ihre Kunden über mehrere Kanäle hinweg in Echtzeit umsetzen zu können, müssen die richtigen Daten jederzeit verfügbar sein und bei Änderungen kontinuierlich aktualisiert werden. Adobe Experience Platform ermöglicht diesen Echtzeitzugriff auf Daten mithilfe sogenannter Edges. Ein Edge ist ein regional aufgestellter Server, der Daten erfasst und direkt für Anwendungen abrufbar macht. Adobe-Anwendungen wie etwa Adobe Target und Adobe Campaign nutzen Edges, um personalisierte Kundenerlebnisse in Echtzeit bereitzustellen. Die Daten werden mittels Projektion an einen Edge übermittelt, wobei ein Projektionsziel den Edge definiert, an den die Daten gesendet werden, und eine Projektionskonfiguration, die die Informationen spezifiziert, die am Edge zur Verfügung gestellt werden. Weitere Informationen und die Arbeit mit Projektionen mithilfe der [!DNL Real-time Customer Profile]-API finden Sie im Handbuch [Endpunkte für die Edge-Projektion](api/edge-projections.md).

## Daten in [!DNL Profile] einfügen

[!DNL Platform] kann so konfiguriert werden, dass Daten aus Datensatz- und Zeitreihen an gesendet werden,  [!DNL Profile]wodurch Echtzeit-Streaming und Stapelverarbeitung unterstützt werden. Weitere Informationen dazu, wie Sie dem Echtzeit-Kundenprofil Daten hinzufügen, finden Sie in [diesem Tutorial](tutorials/add-profile-data.md).

>[!NOTE]
>
>Daten, die über Adoben-Lösungen wie [!DNL Analytics Cloud], [!DNL Marketing Cloud] und [!DNL Advertising Cloud] erfasst werden, fließen in [!DNL Experience Platform] und werden in [!DNL Profile] eingeschlossen.

### Profil-Erfassungsmetriken

Observability Insights ermöglicht die Ermittlung von Schlüsselmetriken in Adobe Experience Platform. Zusätzlich zu den [!DNL Experience Platform]-Nutzungsstatistiken und Leistungsindikatoren für verschiedene [!DNL Platform]-Funktionen gibt es spezielle Profil-bezogene Metriken, mit denen Sie Einblicke in eingehende Anforderungsraten, erfolgreiche Erfassungsraten, erfasste Datensatzgrößen und mehr gewinnen können. Weitere Informationen finden Sie in der [Übersicht über die Beobachtungs-Insight-API](../observability/api/overview.md). Eine vollständige Liste der Echtzeit-Kundenmetriken finden Sie in der Dokumentation zu [verfügbaren Metriken](../observability/api/metrics.md#available-metrics).

## [!DNL Data governance] und [!DNL Privacy]

[!DNL Data governance] umfasst eine Reihe von Strategien und Technologien, mittels derer Kundendaten so verwaltet werden können, dass die Einhaltung gesetzlicher Bestimmungen, Einschränkungen und Richtlinien zu ihrer Nutzung gewährleistet bleibt.

Im Hinblick auf den Zugriff auf Daten spielt die Datenverwaltung auf verschiedenen Ebenen eine Schlüsselrolle innerhalb von [!DNL Experience Platform]:
* Datennutzungsbeschriftungen
* Datenzugriffsrichtlinien
* Kontrollmechanismen für den Datenzugriff für Marketing-Aktivitäten

[!DNL Data governance] an mehreren Stellen verwaltet wird. Dazu gehört die Entscheidung, welche Daten nach der Erfassung für eine bestimmte Marketingaktion in [!DNL Platform] eingegeben werden und welche Daten verfügbar sind. Gehen Sie für weitere Informationen hierzu zunächst die [Übersicht über Data Governance](../data-governance/home.md) durch.

### Umgang mit Opt-out- und Datenschutzanfragen

[!DNL Experience Platform] ermöglicht es Ihren Kunden, Abmeldeanfragen im Zusammenhang mit der Nutzung und Datenspeicherung ihrer Daten innerhalb von  [!DNL Real-time Customer Profile]zu senden. Weitere Informationen hierzu finden Sie in der Dokumentation zum Thema [Berücksichtigen von Opt-out-Anfragen](../segmentation/honoring-opt-outs.md).

## Nächste Schritte und zusätzliche Ressourcen

Um mehr über die Verwendung von [!DNL Real-time Customer Profile]-Daten mithilfe der Benutzeroberfläche der Experience Platform oder der Profil-API zu erfahren, lesen Sie zunächst das [Profil-UI-Handbuch](ui/user-guide.md) bzw. das [API-Entwicklerhandbuch](api/overview.md).