---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Segmentation Service-Datentypen
topic: overview
translation-type: tm+mt
source-git-commit: cb6a2f91eb6c18835bd9542e5b66af4682227491
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 4%

---


# Vom Adobe Experience Platform Segmentation Service unterstützte Datentypen

Alle XDM-Datentypen werden in [!DNL Segmentation Service]unterstützt. Die Regeln, die eine Segmentdefinition bilden, werden durch die folgenden Datentypen kontextualisiert.

## Zeichenfolgendaten

Segmentdefinitionen verwenden Zeichenfolgendaten, um nicht-numerische Beschränkungen für Segmentdefinitionen zu definieren, wie z. B. &quot;Ländername&quot;oder &quot;Treuhandstufe&quot;für Programme.

Stringdaten werden in Segmentdefinitionen mit logischen, einschließlich-/ausschließlichen und Vergleichsanweisungen eingeschlossen. Nachdem Sie Ihrer Segmentdefinition ein Zeichenfolgenattribut hinzugefügt haben, können Sie mit Zeichenfolgen-relevanten Anweisungen das Attribut mit anderen Zeichenfolgenfeldern vergleichen.

| Anweisungstyp | Beispiele |
| -------------- | -------- |
| Logisch | `and`, `or`, `not` |
| Inklusiv/exklusiv | `include`, `must` `exist`, `exclude`, `must not exist` |
| Vergleich | `equals`, `does not equal`, `contains`, `starts with` |

## Datumsdaten

Mit den Datumsdaten können Sie Ihren Segmentdefinitionen zeitbasierten Kontext zuweisen, entweder durch Verwendung spezifischer Beginn-/Enddaten oder durch Verwendung datumsrelevanter Anweisungen, wie in der unten stehenden Tabelle dargestellt. Eine Implementierung könnte eine Audience von Kunden schaffen, die *dieses Jahr* jederzeit mit Ihrer Marke interagiert haben und auch in den letzten Tagen aktiv *gewesen* sind.

| Beispielfeld | Datumsbezogene Aussagen | Timeline |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`, `yesterday`, `this month`, `this year` | Relevant für den Tag, an dem das Segment erstellt wurde. |
| person.lastPurchase | `in last`, `during`, `before`, `after`, `within` | Relevant innerhalb einer beliebigen Woche/eines Monats. |

## Experience Ereignisses

Als Adobe Experience Platform-Schema zeichnet XDM ExperienceEvents explizite und implizite Kundeninteraktionen mit [!DNL Platform]integrierten Anwendungen auf, einschließlich einer Momentaufnahme des Systems zum Zeitpunkt der Interaktion. ExperienceEvents sind Faktendatensätze. Sie sind daher eine Datenquelle, die Ihnen während der Segmentdefinition zur Verfügung steht.

Wie in der unten stehenden Tabelle dargestellt, werden die Ereignis-Daten mit Suchbegriffen wiedergegeben, die das Verhalten von Ereignissen verfeinern und Ereignis-Attribute angeben.

| Schlüsselwort | Verwenden von  |
| ------- | --- |
| Einbeziehen/Ausschließen | Beschreibt das Verhalten des Ereignisses durch die Einbeziehung oder Auslassung von Daten. |
| Beliebig/Alle | Hilft bei der Bestimmung der Anzahl der qualifizierten Segmente. |
| Umschalter &quot;Zeitregel anwenden&quot; | Enthält Datumsdaten. |
| Gleich, ungleich, Beginn mit, nicht Beginn mit, endet mit, endet nicht mit, enthält, enthält nicht enthält, ist vorhanden, nicht vorhanden | Enthält Zeichenfolgendaten. |

## Segmente

Bestehende Segmentdefinitionen können auch als Komponenten einer neuen Segmentdefinition verwendet werden, wobei ihre Attribut- und Ereignis-basierten Regeln dem neuen Segment hinzugefügt werden.

## Audiences

Externe Audiencen können auch als Komponenten einer neuen Segmentdefinition verwendet werden, wobei ihre Attributregeln dem neuen Segment hinzugefügt werden.

Derzeit wird nur Adobe Audience Manager als Audience unterstützt. Weitere Quellen werden in Zukunft aktiviert.

## Sonstige Datentypen

Zusätzlich zu den oben genannten Datentypen umfasst die Liste unterstützter Datentypen auch:

- Uniform Resource Identifier (URI)
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