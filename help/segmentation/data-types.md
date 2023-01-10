---
keywords: Experience Platform; Startseite; beliebte Themen; Datentyp; Datentypen; Datentypen; Datentypen; Datentyp; Segmentierungsdatentypen; Segmentierung; Segmentierung; Segmentierungsdienst; Datentypen des Segmentierungsdienstes; Segmentierungsdienst
solution: Experience Platform
title: Unterstützte Datentypen im Segmentierungsdienst
description: Alle Experience-Datenmodell (XDM)-Datentypen werden in Adobe Segmentation Service unterstützt. Die Regeln, die eine Segmentdefinition bilden, werden durch die folgenden Datentypen kontextualisiert.
exl-id: 73f932a7-f864-4566-ade7-c148a12dc83c
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 6%

---

# Unterstützte Datentypen im Segmentation Service

Alle Experience-Datenmodell (XDM)-Datentypen werden in Adobe Experience Platform Segmentation Service unterstützt. Die Regeln, die eine Segmentdefinition bilden, werden durch die folgenden Datentypen kontextualisiert.

## Zeichenfolgendaten

Segmentdefinitionen verwenden Zeichenfolgendaten, um nicht numerische Begrenzungen für Segmentzielgruppen zu definieren, z. B. &quot;Ländername&quot;oder &quot;Treueprogramm-Ebene&quot;.

Zeichenfolgendaten werden in Segmentdefinitionen mit logischen, einschließlich-/ausschließenden und Vergleichsanweisungen einbezogen. Nachdem ein Zeichenfolgenattribut zu Ihrer Segmentdefinition hinzugefügt wurde, können Sie string-relevante Anweisungen verwenden, um es mit anderen Zeichenfolgenfeldern zu bewerten.

| Anweisungstyp | Beispiele |
| -------------- | -------- |
| Logisch       | `and`, `or`, `not` |
| Einschließlich/exklusiv | `include`, `must` `exist`, `exclude`, `must not exist` |
| Vergleich | `equals`, `does not equal`, `contains`, `starts with` |

## Datumsdaten

Mit Datumsdaten können Sie Ihren Segmentdefinitionen zeitbasierten Kontext zuweisen, indem Sie entweder bestimmte Start-/Enddaten verwenden oder datumsrelevante Anweisungen verwenden, wie in der folgenden Tabelle dargestellt. Eine Implementierung erstellt möglicherweise eine Zielgruppe von Kunden, die jederzeit mit Ihrer Marke interagiert haben *dieses Jahr* und auch aktiv war *Innerhalb* die letzten Tage.

| Beispielfeld | Datumsbezogene Erklärungen | Zeitleiste |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`, `yesterday`, `this month`, `this year` | Relevant für den Tag, an dem das Segment erstellt wurde. |
| person.lastPurchase | `in last`, `during`, `before`, `after`, `within` | Relevant innerhalb einer bestimmten Woche/eines bestimmten Monats. |

## Erlebnisereignisse

Als Adobe Experience Platform-Schema [!DNL XDM ExperienceEvents] explizite und implizite Kundeninteraktionen mit [!DNL Platform]-integrierte Anwendungen, einschließlich einer Momentaufnahme des Systems zum Zeitpunkt der Interaktion. [!DNL ExperienceEvents] sind Faktendatensätze. Sie sind daher eine Datenquelle, die Ihnen während der Segmentdefinition zur Verfügung steht.

Wie in der folgenden Tabelle dargestellt, werden Ereignisdaten mithilfe von Keywords gerendert, die dazu beitragen, das Ereignisverhalten zu verfeinern und Ereignisattribute anzugeben.

| Schlüsselwort | Verwenden von  |
| ------- | --- |
| Ein-/Ausschließen | Beschreibt das Verhalten des Ereignisses durch Einbeziehung oder Auslassung von Daten. |
| Any/all | Hilft bei der Bestimmung der Anzahl qualifizierter Segmente. |
| Schaltfläche &quot;Zeitregel anwenden&quot; | Umfasst Datumsdaten. |
| Gleich, nicht gleich, beginnt mit, beginnt nicht mit, endet mit, endet nicht mit, enthält, enthält nicht, ist nicht vorhanden, existiert nicht | Enthält Zeichenfolgendaten. |

### Zielgruppenfreigabe

Externe Zielgruppen können auch als Komponenten einer neuen Segmentdefinition verwendet werden, indem deren Attributregeln zum neuen Segment hinzugefügt werden.

Derzeit wird nur Adobe Audience Manager als externe Zielgruppe unterstützt, wobei in Zukunft zusätzliche Quellen aktiviert werden. Weitere Informationen zur Verwendung von Adobe Audience Manager-Zielgruppen mit Platform finden Sie im [Handbuch zur Zielgruppenfreigabe in der Adobe Audience Manager-Dokumentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=de).

### Segmentfreigabe

In Platform erstellte Segmente können innerhalb anderer [Hauptdienste von Adobe Experience Cloud](https://experienceleague.adobe.com/docs/core-services/interface/experience-cloud.html?lang=de). Um diese Funktion zu aktivieren, müssen Sie sich an Ihren Lösungsarchitekten oder Ihren Berater wenden.

## Andere Datentypen

Zusätzlich zu den oben genannten Datentypen umfasst die Liste der unterstützten Datentypen auch:

- Uniform resource identifier (URI)
- Enum
- Zahl
- Lang
- Ganzzahl
- Kurz
- Byte
- Boolesch
- Array
- Objekt
- Zuordnung
