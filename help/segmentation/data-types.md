---
keywords: Experience Platform;Home;beliebte Themen;Datentyp;Datentypen;Datentypen;Datentyp;Segmentierungsdatentypen;Segmentierung;Segmentierung;Segmentierungsdienst;Segmentierungsdienstdatentypen;
solution: Experience Platform
title: Unterstützte Datentypen im Segmentierungsdienst
topic-legacy: overview
description: Alle XDM-Datentypen (Experience Data Model) werden im Segmentierungsdienst für Adoben unterstützt. Die Regeln, die eine Segmentdefinition bilden, werden durch die folgenden Datentypen kontextualisiert.
exl-id: 73f932a7-f864-4566-ade7-c148a12dc83c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 4%

---

# Unterstützte Datentypen im Segmentierungsdienst

Alle XDM-Datentypen (Experience Data Model) werden im Adobe Experience Platform Segmentation Service unterstützt. Die Regeln, die eine Segmentdefinition bilden, werden durch die folgenden Datentypen kontextualisiert.

## Zeichenfolgendaten

Segmentdefinitionen verwenden Zeichenfolgendaten, um nicht numerische Einschränkungen für Segmentdefinitionen zu definieren, wie z. B. &quot;Ländername&quot;oder &quot;Treuestufe auf Programm-Ebene&quot;.

Stringdaten werden in Segmentdefinitionen mit logischen, einschließlich-/ausschließlichen und Vergleichsanweisungen eingeschlossen. Nachdem Sie Ihrer Segmentdefinition ein Zeichenfolgenattribut hinzugefügt haben, können Sie mit Zeichenfolgen-relevanten Anweisungen das Attribut mit anderen Zeichenfolgenfeldern vergleichen.

| Anweisungstyp | Beispiele |
| -------------- | -------- |
| Logisch       | `and`, `or`, `not` |
| Inklusiv/exklusiv | `include`, `must` `exist`, `exclude`, `must not exist` |
| Vergleich | `equals`, `does not equal`, `contains`, `starts with` |

## Datumsdaten

Mit den Datumsdaten können Sie Ihren Segmentdefinitionen zeitbasierten Kontext zuweisen, entweder durch Verwendung spezifischer Beginn-/Enddaten oder durch Verwendung datumsrelevanter Anweisungen, wie in der unten stehenden Tabelle dargestellt. Eine Implementierung erstellt möglicherweise eine Audience von Kunden, die in diesem Jahr *jederzeit mit Ihrer Marke interagiert haben und in den letzten Tagen ebenfalls aktiv waren.***

| Beispielfeld | Datumsbezogene Aussagen | Zeitleiste |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`,  `yesterday`,  `this month`,  `this year` | Relevant für den Tag, an dem das Segment erstellt wurde. |
| person.lastPurchase | `in last`, `during`, `before`, `after`, `within` | Relevant innerhalb einer beliebigen Woche/eines Monats. |

## Experience Ereignisses

Als Adobe Experience Platform-Schema zeichnen [!DNL XDM ExperienceEvents] explizite und implizite Kundeninteraktionen mit [!DNL Platform]-integrierten Anwendungen auf, einschließlich einer Momentaufnahme des Systems zum Zeitpunkt der Interaktion. [!DNL ExperienceEvents] sind Faktendatensätze. Sie sind daher eine Datenquelle, die Ihnen während der Segmentdefinition zur Verfügung steht.

Wie in der unten stehenden Tabelle dargestellt, werden die Ereignis-Daten mit Suchbegriffen wiedergegeben, die das Verhalten von Ereignissen verfeinern und Ereignis-Attribute angeben.

| Schlüsselwort | Verwenden von  |
| ------- | --- |
| Einbeziehen/Ausschließen | Beschreibt das Verhalten des Ereignisses durch die Aufnahme oder Auslassung von Daten. |
| Beliebig/Alle | Hilft bei der Bestimmung der Anzahl der qualifizierten Segmente. |
| Umschalter &quot;Zeitregel anwenden&quot; | Enthält Datumsdaten. |
| Gleich, ungleich, Beginn mit, nicht Beginn mit, endet mit, endet nicht mit, enthält, enthält nicht enthält, ist vorhanden, nicht vorhanden | Enthält Zeichenfolgendaten. |

### Zielgruppenfreigabe

Externe Audiencen können auch als Komponenten einer neuen Segmentdefinition verwendet werden, wobei ihre Attributregeln dem neuen Segment hinzugefügt werden.

Derzeit wird nur Adobe Audience Manager als externe Audience unterstützt, wobei in Zukunft zusätzliche Quellen aktiviert werden. Weitere Informationen zur Verwendung von Adobe Audience Manager-Audiencen mit Platform finden Sie im Handbuch [Audience Sharing in der Adobe Audience Manager-Dokumentation](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html).

### Segmentfreigabe

In Platform erstellte Segmente können in anderen [Adobe Experience Cloud Core Services](https://docs.adobe.com/content/help/de-DE/core-services/interface/experience-cloud.html) verwendet werden. Um diese Funktion zu aktivieren, müssen Sie sich an Ihren Lösungsarchitekten oder Ihren Berater wenden.

## Sonstige Datentypen

Zusätzlich zu den oben genannten Datentypen umfasst die Liste unterstützter Datentypen auch:

- Uniform Resource Identifier (URI)
- Enum
- Nummer
- Lang
- Ganzzahl
- Kurz
- Byte
- Boolesch
- Array
- Objekt
- Zuordnung
