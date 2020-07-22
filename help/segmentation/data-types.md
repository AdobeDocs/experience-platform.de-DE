---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Segmentation Service-Datentypen
topic: overview
translation-type: tm+mt
source-git-commit: 96b6f820e5d372446c4927e7719aedadb2b11bc9
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 5%

---


# Von der Adobe Experience Platform [!DNL Segmentation Service] unterstützte Datentypen

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

Zeichnen Sie als Adobe Experience Platform-Schema explizite und implizite Kundeninteraktionen mit [!DNL XDM ExperienceEvents] [!DNL Platform]integrierten Anwendungen auf, einschließlich einer Momentaufnahme des Systems zum Zeitpunkt der Interaktion. [!DNL ExperienceEvents] sind Faktendatensätze. Sie sind daher eine Datenquelle, die Ihnen während der Segmentdefinition zur Verfügung steht.

Wie in der unten stehenden Tabelle dargestellt, werden die Ereignis-Daten mit Suchbegriffen wiedergegeben, die das Verhalten von Ereignissen verfeinern und Ereignis-Attribute angeben.

| Schlüsselwort | Verwenden von  |
| ------- | --- |
| Einbeziehen/Ausschließen | Beschreibt das Verhalten des Ereignisses durch die Einbeziehung oder Auslassung von Daten. |
| Beliebig/Alle | Hilft bei der Bestimmung der Anzahl der qualifizierten Segmente. |
| Umschalter &quot;Zeitregel anwenden&quot; | Enthält Datumsdaten. |
| Gleich, ungleich, Beginn mit, nicht Beginn mit, endet mit, endet nicht mit, enthält, enthält nicht enthält, ist vorhanden, nicht vorhanden | Enthält Zeichenfolgendaten. |

### Zielgruppenfreigabe

Externe Audiencen können auch als Komponenten einer neuen Segmentdefinition verwendet werden, wobei ihre Attributregeln dem neuen Segment hinzugefügt werden.

Derzeit wird nur Adobe Audience Manager als externe Audience unterstützt, wobei in Zukunft zusätzliche Quellen aktiviert werden. Weitere Informationen zur Verwendung von Adobe Audience Manager-Audiencen mit Platform finden Sie im Handbuch zur Freigabe von [Audiencen in der Dokumentation](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)des Adobe Audience Managers.

### Segmentfreigabe

In der Plattform erstellte Segmente können in anderen [Adobe Experience Cloud-Hauptdiensten](https://docs.adobe.com/content/help/de-DE/core-services/interface/experience-cloud.html)verwendet werden. Um diese Funktion zu aktivieren, müssen Sie sich an Ihren Lösungsarchitekten oder Ihren Berater wenden.

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