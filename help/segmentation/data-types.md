---
solution: Experience Platform
title: Unterstützte Datentypen im Segmentierungs-Service
description: Alle Experience-Datenmodell (XDM)-Datentypen werden im Segmentierungs-Service von Adobe unterstützt. Die Regeln, aus denen eine Segmentdefinition besteht, werden durch die folgenden Datentypen kontextualisiert.
exl-id: 73f932a7-f864-4566-ade7-c148a12dc83c
source-git-commit: 0a9028beca36b46d6228c0038366bbac5d32603c
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 4%

---

# Unterstützte Datentypen im Segmentierungs-Service

Alle Experience-Datenmodell (XDM)-Datentypen werden im Segmentierungs-Service von Adobe Experience Platform unterstützt. Die Regeln, aus denen eine Segmentdefinition besteht, werden durch die folgenden Datentypen kontextualisiert.

## Zeichenfolgen-Daten

Segmentdefinitionen verwenden Zeichenfolgendaten, um nicht-numerische Einschränkungen für Zielgruppen zu definieren, z. B. „Ländername“ oder „Treueprogramm-Ebene“.

Zeichenfolgendaten werden mithilfe von logischen, inklusiven/exklusiven und Vergleichsanweisungen in Segmentdefinitionen eingeschlossen. Nachdem ein Zeichenfolgenattribut zu Ihrer Segmentdefinition hinzugefügt wurde, können Sie zeichenfolgenrelevante Anweisungen verwenden, um es mit anderen Zeichenfolgenfeldern zu vergleichen.

| Anweisungstyp | Beispiele |
| -------------- | -------- |
| Logisch       | `and`, `or`, `not` |
| Inklusive/exklusive | `include`, `must` `exist`, `exclude`, `must not exist` |
| Vergleich | `equals`, `does not equal`, `contains`, `starts with` |

## Datumsangaben

Mit Datumsdaten können Sie Ihren Segmentdefinitionen einen zeitbasierten Kontext zuweisen, entweder mithilfe spezifischer Start-/Enddaten oder mithilfe von datumsrelevanten Anweisungen, wie in der folgenden Tabelle dargestellt. Eine Implementierung könnte darin bestehen, eine Zielgruppe von Kunden zu erstellen, die zu irgendeinem Zeitpunkt (*Jahr) mit Ihrer Marke interagiert* und *den* Tagen auch aktiv waren.

| Beispielfeld | Datumsrelevante Aussagen | Timeline |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`, `yesterday`, `this month`, `this year` | Relevant für den Tag der Erstellung der Segmentdefinition. |
| person.lastPurchase | `in last`, `during`, `before`, `after`, `within` | Relevant innerhalb einer bestimmten Woche/eines Monats. |

## Erlebnisereignisse

Als Adobe Experience Platform-Schema erfassen [!DNL XDM ExperienceEvents] explizite und implizite Kundeninteraktionen mit Experience Platform-integrierten Anwendungen, einschließlich einer Momentaufnahme des Systems zum Zeitpunkt der Interaktion. [!DNL ExperienceEvents] sind Faktenaufzeichnungen. Als solche sind sie eine Datenquelle, die Ihnen während der Segmentdefinition zur Verfügung steht.

Wie in der folgenden Tabelle dargestellt, werden Ereignisdaten mit Schlüsselwörtern gerendert, die dabei helfen, das Verhalten von Ereignissen zu verfeinern und Ereignisattribute anzugeben.

| Schlüsselwort | Verwenden von  |
| ------- | --- |
| Ein-/Ausschließen | Beschreibt das Verhalten des Ereignisses durch Einschließen oder Auslassen von Daten. |
| Beliebig/Alle | Hilft bei der Bestimmung der Anzahl der qualifizierten Segmentdefinitionen. |
| Umschalter „Zeitregel anwenden“ | Enthält Datumsdaten. |
| Gleich, nicht gleich, beginnt mit, beginnt nicht mit, endet mit, endet nicht mit, enthält, enthält nicht, existiert, ist nicht vorhanden | Enthält Zeichenfolgendaten. |

### Zielgruppenfreigabe

Externe Zielgruppen können auch als Komponenten einer neuen Segmentdefinition verwendet werden, indem ihre Attributregeln zu den neuen Segmentdefinitionen hinzugefügt werden.

Derzeit wird nur Adobe Audience Manager als externe Zielgruppe unterstützt, wobei in Zukunft zusätzliche Quellen aktiviert werden. Weitere Informationen zur Verwendung von Adobe Audience Manager-Zielgruppen mit Experience Platform finden Sie im [Handbuch zur Zielgruppenfreigabe in der Dokumentation zu Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=de).

### Freigabe der Segmentdefinition

In Experience Platform erstellte Segmentdefinitionen können in anderen [Adobe Experience Cloud Core Services&rbrace; verwendet &#x200B;](https://experienceleague.adobe.com/docs/core-services/interface/experience-cloud.html?lang=de). Um diese Funktion zu aktivieren, müssen Sie sich an Ihren Lösungsarchitekten oder Ihren Berater wenden.

## Andere Datentypen

Zusätzlich zu den oben genannten Datentypen umfasst die Liste der unterstützten Datentypen auch:

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
