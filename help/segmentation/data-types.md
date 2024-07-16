---
solution: Experience Platform
title: Unterstützte Datentypen im Segmentierungsdienst
description: Alle Experience-Datenmodell (XDM)-Datentypen werden in Adobe Segmentation Service unterstützt. Die Regeln, die eine Segmentdefinition bilden, werden durch die folgenden Datentypen kontextualisiert.
exl-id: 73f932a7-f864-4566-ade7-c148a12dc83c
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 4%

---

# Unterstützte Datentypen im Segmentation Service

Alle Experience-Datenmodell (XDM)-Datentypen werden in Adobe Experience Platform Segmentation Service unterstützt. Die Regeln, die eine Segmentdefinition bilden, werden durch die folgenden Datentypen kontextualisiert.

## Zeichenfolgendaten

Segmentdefinitionen verwenden Zeichenfolgendaten, um nicht numerische Begrenzungen für Zielgruppen zu definieren, z. B. &quot;Ländername&quot;oder &quot;Treueprogramm-Ebene&quot;.

Zeichenfolgendaten werden in Segmentdefinitionen mit logischen, einschließlich-/ausschließenden und Vergleichsanweisungen einbezogen. Nachdem ein Zeichenfolgenattribut zu Ihrer Segmentdefinition hinzugefügt wurde, können Sie string-relevante Anweisungen verwenden, um es mit anderen Zeichenfolgenfeldern zu bewerten.

| Anweisungstyp | Beispiele |
| -------------- | -------- |
| Logisch       | `and`, `or`, `not` |
| Einschließlich/ausschließlich | `include`, `must` `exist`, `exclude`, `must not exist` |
| Vergleich | `equals`, `does not equal`, `contains`, `starts with` |

## Datumsdaten

Mit Datumsdaten können Sie Ihren Segmentdefinitionen zeitbasierten Kontext zuweisen, indem Sie entweder bestimmte Start-/Enddaten verwenden oder datumsrelevante Anweisungen verwenden, wie in der folgenden Tabelle dargestellt. Bei einer Implementierung wird möglicherweise eine Zielgruppe von Kunden erstellt, die seit *diesem Jahr* mit Ihrer Marke interagiert haben und in den letzten Tagen auch *innerhalb von* aktiv waren.

| Beispielfeld | Datumsbezogene Erklärungen | Planung |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`, `yesterday`, `this month`, `this year` | Relevant für den Tag der Erstellung der Segmentdefinition. |
| person.lastPurchase | `in last`, `during`, `before`, `after`, `within` | Relevant innerhalb einer bestimmten Woche/eines bestimmten Monats. |

## Erlebnisereignisse

Als Adobe Experience Platform-Schema zeichnet [!DNL XDM ExperienceEvents] explizite und implizite Kundeninteraktionen mit [!DNL Platform] integrierten Anwendungen auf, einschließlich einer Momentaufnahme des Systems zum Zeitpunkt der Interaktion. [!DNL ExperienceEvents] sind Faktendatensätze. Sie sind daher eine Datenquelle, die Ihnen während der Segmentdefinition zur Verfügung steht.

Wie in der folgenden Tabelle dargestellt, werden Ereignisdaten mithilfe von Keywords gerendert, die dazu beitragen, das Ereignisverhalten zu verfeinern und Ereignisattribute anzugeben.

| Schlüsselwort | Verwenden von  |
| ------- | --- |
| Ein-/Ausschließen | Beschreibt das Verhalten des Ereignisses durch Einbeziehung oder Auslassung von Daten. |
| Any/all | Hilft bei der Bestimmung der Anzahl an qualifizierten Segmentdefinitionen. |
| Schaltfläche &quot;Zeitregel anwenden&quot; | Umfasst Datumsdaten. |
| Gleich, nicht gleich, beginnt mit, beginnt nicht mit, endet mit, endet nicht mit, enthält, enthält nicht, ist nicht vorhanden, existiert nicht | Enthält Zeichenfolgendaten. |

### Zielgruppenfreigabe

Externe Zielgruppen können auch als Komponenten einer neuen Segmentdefinition verwendet werden, indem deren Attributregeln zu den neuen Segmentdefinitionen hinzugefügt werden.

Derzeit wird nur Adobe Audience Manager als externe Zielgruppe unterstützt, wobei in Zukunft zusätzliche Quellen aktiviert werden. Weitere Informationen zur Verwendung von Adobe Audience Manager-Zielgruppen mit Platform finden Sie im Handbuch zur Freigabe von [Zielgruppen in der Adobe Audience Manager-Dokumentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=de).

### Freigabe von Segmentdefinitionen

In Platform erstellte Segmentdefinitionen können in anderen [Adobe Experience Cloud Core Services](https://experienceleague.adobe.com/docs/core-services/interface/experience-cloud.html?lang=de) verwendet werden. Wenden Sie sich zur Aktivierung dieser Funktion an Ihren Lösungsarchitekten oder Ihren Berater.

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
