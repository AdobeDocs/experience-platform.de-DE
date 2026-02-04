---
title: Zielgruppen-Validierung
description: Erfahren Sie, wie Experience Platform Ihre Zielgruppen validiert, um sicherzustellen, dass sie nachgelagert eine gute Leistung erbringen.
source-git-commit: 52439e55d3c48631488b17b6b04256bcbbe37bcb
workflow-type: tm+mt
source-wordcount: '1630'
ht-degree: 1%

---


# Zielgruppen-Validierung

Beim Schreiben einer Zielgruppendefinition in Adobe Experience Platform bietet die Zielgruppenvalidierung integrierte Validierungen und Leitplanken, um sicherzustellen, dass Ihre Zielgruppen nicht nur präzise, sondern auch stabil und skalierbar sind.

Durch die Befolgung der Best Practices für die Zielgruppendefinition können Sie sicherstellen, dass Ihre Zielgruppen schneller ausgewertet werden, Ihre Logik auch dann effizient bleibt, wenn Ihre Zielgruppengröße zunimmt, und das Risiko von Auswertungsfehlern in Zeiten hohen Traffics reduzieren. Optimierte Zielgruppen verbessern auch die Aktivierungsgeschwindigkeit für Ziele, reduzieren die Echtzeit-Personalisierungslatenz und sorgen für die allgemeine Sandbox-Stabilität.

Experience Platform führt diese Validierungen beim Aufbau Ihrer Audience in Segment Builder in Echtzeit aus. Wenn Sie Ereignisse oder Attribute hinzufügen, die die Validierungsschwellen überschreiten, erhalten Sie in der Benutzeroberfläche von Segment Builder sofortiges Feedback.

## Validierungstypen {#validation-types}

Wenn die Zielgruppenvalidierung für Ihre Zielgruppen ausgeführt wird, gibt es zwei verschiedene Arten von Konstrukten, die verletzt werden können: kritische Validierungskonstrukte und Konstrukte zur Leistungsoptimierung.

Wenn ein wichtiges Überprüfungskonstrukt verletzt wird, verhindert das System, dass Sie Ihre Zielgruppe speichern, um die Stabilität Ihrer Sandbox zu schützen. Wenn ein Konstrukt zur Leistungsoptimierung verletzt wird, können Sie Ihre Zielgruppe speichern, es wird jedoch *dringend empfohlen* Sie Ihre Zielgruppendefinition aktualisieren, um Leistungsprobleme zu vermeiden.

## Validierungsprüfungen {#validation-checks}

Derzeit werden die folgenden Validierungen unterstützt:

| Validierung | Typ | Schwellenwert |
| ---------------- | ---- | --------- |
| Logische Komplexität | Kritische Validierung | Die Zielgruppendefinition enthält zu viele Abfragen, was zu unnötiger logischer Komplexität führt. |
| Sequenzielle Ereignisse | Kritische Validierung | Es gibt mehr als 6 sequenzielle Ereignisse innerhalb einer Zielgruppendefinition. |
| Aggregierte Anzahl | Leistungsoptimierung | Es gibt mehr als drei Aggregationsfunktionen innerhalb einer Zielgruppendefinition. |
| Verschachtelte Daten | Leistungsoptimierung | Es gibt mehr als 2 Ebenen verschachtelter Daten (Datentypen „Array“ oder „Zuordnung„) in einer Zielgruppendefinition. |
| Zielgruppengröße | Leistungsoptimierung | Die Größe der Zielgruppenqualifizierung ist größer als 30 % der Gesamtzahl der Profile in der Sandbox. |

### [!BADGE Kritische Validierung]{type=Negative} Logische Komplexität {#logical-complexity}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_rewritescheck"
>title="Warnhinweis zur Abfrageeffizienz"
>abstract="Ihre Zielgruppe enthält zu viele Abfragen, was zu unnötiger logischer Komplexität führt. Vereinfachen Sie Ihre Zielgruppendefinition, bevor Sie fortfahren."

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_cnfcomplexitycheck"
>title="logische Komplexität"
>abstract="Ihre Zielgruppe enthält zu viele Abfragen, was zu unnötiger logischer Komplexität führt. Vereinfachen Sie Ihre Zielgruppendefinition, bevor Sie fortfahren."

Die Validierung der logischen Komplexität analysiert die Struktur Ihrer logischen Aussagen (AND, OR, NOT) innerhalb Ihrer Zielgruppendefinition. Insbesondere sucht sie nach Zielgruppendefinitionen, die das System zwingen, eine übermäßige Anzahl von Vergleichen pro Profil durchzuführen.

Wenn Ihre Zielgruppendefinition eine übermäßige Anzahl von Vergleichen pro Profil aufweist, führt diese erhöhte Komplexität zu einer langsameren Auswertung auf Profilbasis. Dies erhöht die Gesamtzeit für die Zielgruppenbewertung.

Um zu vermeiden, dass diese Validierung ausgelöst wird, sollten Sie Ihre Zielgruppendefinition einfach halten. Wenn Sie Ihre eigene Zielgruppendefinition nicht verstehen, ist sie zu kompliziert, und die Auswertung der Zielgruppe durch Experience Platform kann länger dauern.

**Beispiel**

Nehmen wir an, Sie möchten Kunden finden, die in bestimmten Bundesstaaten leben. Sie _könnten_ dies ineffizient schreiben, indem Sie überprüfen, ob das Profil den Wert für einen Status hat, der einem der 45 aufgelisteten Werte entspricht, wie folgt:

+++ Ineffiziente Zielgruppendefinition

```
State.equals("AL", "AK", "AZ", "AR", "CA", "CO", "CT", "DE", "FL", "GA","HI", "ID", "IL", "IN", "IA", "KS", "KY", "LA", "ME", "MD", "MA", "MI", "MN", "MS", "MO", "MT", "NE", "NV", "NH", "NJ", "NM", "NY", "NC", "ND", "OH", "OK", "OR", "PA", "RI", "SC", "SD", "TN", "TX", "UT")
```

+++

Mit einer Nicht-Prüfung müssen Sie jedoch nur überprüfen, ob das Profil nicht einen der fünf aufgelisteten Werte hat, was zu einer viel effizienteren Abfrage führt.

+++ Effiziente Zielgruppendefinition

```
not(State.equals("VT", "VA", "WA", "WV", "WI", "WY" ))
```

+++

Angenommen, Sie möchten Kunden finden, die Kanadier sind und einen Testplan haben. Ein weniger effizienter Ansatz wäre, nach Kanadiern in Ihrem Testplan zu suchen, indem Sie jeden anderen Plan manuell ausschließen, einen nach dem anderen, und überprüfen, ob das Profil in keinem von ihnen enthalten ist.

+++ Ineffiziente Zielgruppendefinition

```
NOT(
    plan.equals("basic") OR
    plan.equals("standard") OR
    plan.equals("premium") OR
    plan.equals("enterprise")
) AND NOT (
    region.equals("us-east") OR
    region.equals("us-west") OR
    region.equals("eu-central") OR
    region.equals("apac")
)
```

+++

Stattdessen sollten Sie direkt sein und den spezifischen Plan auswählen, den Sie einbeziehen möchten.

+++ Effiziente Zielgruppendefinition

```
plan.equals("trial") AND region.equals("canada")
```

+++

### [!BADGE Kritische Validierung]{type=Negative} Sequenzielle Ereigniskomplexität {#sequential-event-complexity}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_chaincountcheck"
>title="Ereignissequenzlimit"
>abstract="Ihre Zielgruppe enthält zu viele sequenzielle Ereignisse. Es können nur maximal 6 sequenzielle Ereignisse in Ihrer Zielgruppendefinition vorhanden sein. Bitte einige sequenzielle Ereignisse aus Ihrer Zielgruppendefinition entfernen, bevor Sie fortfahren."

Die Validierung der Komplexität sequenzieller Ereignisse beschränkt die Anzahl sequenzieller Ereignisse in einer Sequenz auf 6 Ereignisse.

Die sequenzielle Segmentierung ist einer der kompliziertesten Rechenvorgänge in Experience Platform, da das System den gesamten Verlauf von Erlebnisereignissen eines Kunden scannen, nach Zeitstempel sortieren und überprüfen muss, ob die angegebene Reihenfolge mit Ihrer Abfrage übereinstimmt. Wenn die Kette wächst, steigt daher die Anzahl der Permutationen, die das System berechnen muss, drastisch an.

Um zu vermeiden, dass diese Validierung ausgelöst wird, konzentrieren Sie sich auf die Grundlagen Ihrer sequenziellen Kette, indem Sie den Anfang, die Mitte und das Ende des Journey definieren. Bei der endgültigen Konversion sind oft sofortige Schritte erforderlich.

**Beispiel**

Angenommen, Sie möchten Benutzende ansprechen, die ein Produkt angesehen, zum Warenkorb hinzugefügt und gekauft haben. Ein weniger effizienter Ansatz würde jeden einzelnen Status des Benutzerpfads überprüfen. Die folgende Abfrage durchläuft beispielsweise diese Ereignissequenz: Anmelden bei der Website -> Suche nach Produkt -> Anzeigen einer Produktseite -> Hinzufügen zum Warenkorb -> Navigiert zur Kasse -> Kaufereignis

+++ Ineffiziente Zielgruppendefinition

```
chain(xEvent, timestamp, [ A: WHAT(eventType = "login"), B: WHAT(eventType = "search"), C: WHAT(eventType = "productView"), D: WHAT(eventType = "addToCart"), E: WHAT(eventType = "checkout"), F: WHAT(eventType = "purchase") ])
```

+++

Indem Sie die Sequenz jedoch auf ihren Anfang, ihre Mitte und ihr Ende reduzieren, benötigen Sie nur eine Ereignissequenz, die drei Ereignisse lang ist, was zu einer effizienteren Abfrage führt. Die folgende Abfrage durchläuft beispielsweise diese Ereignissequenz: Anzeigen einer Produktseite -> Zum Warenkorb hinzufügen -> Kaufereignis

+++ Effiziente Zielgruppendefinition

```
chain(xEvent, timestamp, [ A: WHAT(eventType = "productView"), B: WHAT(eventType = "addToCart"), C: WHAT(eventType = "purchase") ])
```

+++

### [!BADGE Leistungsoptimierung]{type=Caution} Aggregierte Anzahl {#aggregated-count}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_countaggregationcheck"
>title="Warnung zum Zählungsfilter"
>abstract="Ihre Zielgruppe enthält zu viele Aggregationsereignisse. Sie sollten maximal drei Aggregationsereignisse in Ihrer Zielgruppe verwenden. Um Leistungsprobleme zu vermeiden, sollten Sie einige Aggregationsereignisse aus Ihrer Zielgruppendefinition entfernen."

Die Prüfung der aggregierten Anzahl begrenzt die Anzahl der in Ihrer Zielgruppe verwendeten Aggregationsereignisse auf drei Bedingungen.

Ein Standardereignis muss nur ein einziges übereinstimmendes Ereignis finden, um einen Benutzer zu qualifizieren. Ein Aggregationsereignis muss jedoch den **gesamten Ereignisverlauf) eines Benutzers lesen und analysieren** bevor es eine Entscheidung treffen kann, was bei mehr Aggregationsereignissen zu langsameren Verarbeitungszeiten führt.

Um zu vermeiden, dass diese Validierung ausgelöst wird, verwenden Sie nur dann bestimmte Zählungen, wenn dies für die Zielgruppendefinition unbedingt erforderlich ist. Wenn Sie beispielsweise nur wissen müssen, ob ein Benutzer einmal interagiert hat, können Sie die Standardlogik „Vorhanden“ verwenden, anstatt ein Ereignis „Anzahl > 0“ zu verwenden.

### [!BADGE Leistungsoptimierung]{type=Caution} Komplexität verschachtelter Daten {#nested-data-complexity}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_arraydepthcheck"
>title="Warnung zu verschachtelten Daten"
>abstract="Ihre Zielgruppe verfügt über zu viele verschachtelte Datenschichten. Sie sollten maximal zwei Datenschichten in Ihrer Audience verwenden. Um Leistungsprobleme zu vermeiden, sollten Sie Ihre Zielgruppendefinition reduzieren."

Die Validierung der Komplexität verschachtelter Daten beschränkt die Anzahl verschachtelter Daten innerhalb einer Zielgruppendefinition auf 2 Ebenen.

Während Experience Platform die Verwendung von Array- und Zuordnungsobjekten zum Speichern komplexer Datentypen unterstützt, erfordert das Entpacken verschachtelter Strukturen zum Suchen eines Werts eine komplexere Durchlauflogik. Je tiefer die Daten in einem Array verschachtelt sind, desto länger dauert es, bis sie zur Validierung abgerufen werden.

Wenn Sie häufig eine Segmentierung für ein tief verschachteltes Attribut durchführen, müssen Sie sich möglicherweise an Ihr Data-Engineering-Team wenden, um das Attribut in eine höhere Ebene im Profilschema zu kopieren, damit der Zugriff erleichtert wird.

### [!BADGE Leistungsoptimierung]{type=Caution} Zielgruppengröße {#audience-size}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_profilestorecheck"
>title="Warnung zur Zielgruppengröße"
>abstract="Ihre Zielgruppe ist zu breit geschrieben. Sie sollten es vermeiden, eine Zielgruppendefinition zu schreiben, die mehr als 30 % der gesamten Profile in Ihrer Sandbox qualifiziert. Um Leistungsprobleme zu vermeiden, sollten Sie Ihre Zielgruppendefinition enger definieren."

Bei der Validierung der Zielgruppengröße wird geprüft, ob Ihre Zielgruppendefinition so breit ist, dass mehr als 30 % der gesamten Profile in Ihrer Sandbox für die Zielgruppe qualifiziert sind.

Experience Platform kann zwar große Zielgruppen verarbeiten, eine zu vage Zielgruppendefinition (z. B. Alle aktiven Kunden) kann jedoch die Auswertungszeit und die Aktivierungslatenz erhöhen.

Wenn Sie eine Zielgruppe erstellen müssen, die für mehr als 30 % Ihres Profilspeichers qualifiziert ist, stellen Sie sicher, dass die erste Auswertung der Zielgruppe mithilfe einer flexiblen Zielgruppenauswertung erfolgt. Die Auswertung der Zielgruppe mit einer On-Demand-Auswertung kann die Gesamtwirkung einer großen Zielgruppe auf den täglichen Segmentierungsauftrag reduzieren.

## Nächste Schritte

Nach dem Lesen dieses Handbuchs wissen Sie besser, wie Experience Platform automatische Validierungen ausführt, um die Bewertung, Stabilität und Skalierbarkeit zu verbessern. Weitere Informationen zum Erstellen von Zielgruppen mithilfe der Benutzeroberfläche finden Sie in der [Segment Builder-Dokumentation](./ui/segment-builder.md).

## Anhang

Im folgenden Anhang finden Sie häufig gestellte Fragen zur Zielgruppenvalidierung in Experience Platform.

### Häufig gestellte Fragen {#faq}

**Was passiert, wenn ich die Warnungen ignoriere und die Audience speichere?**

+++ Antwort

Bei Warnhinweisen zur Leistungsoptimierung wird die Zielgruppe gespeichert und das System versucht, sie auszuwerten. Es kann jedoch zu deutlich langsameren Verarbeitungszeiten kommen. In Extremsituationen kann es vorkommen, dass der Segmentierungsauftrag fehlschlägt oder eine Zeitüberschreitung eintritt, wenn das Datenvolumen hoch genug ist, sodass Sie Ihre Audience neu entwerfen müssen.

Bei kritischen Validierungsfehlern können Sie die Zielgruppe nicht speichern.

+++

**Kann ich eine Erhöhung des Limits für „sequenzielle Ereignisse“ anfordern?**

+++ Antwort

Nein, das ist nicht möglich. Dies ist eine feste Schutzmaßnahme, die die Stabilität der gesamten Experience Platform-Umgebung schützen soll. Wenn Ihre Sequenz mehr als 6 Schritte erfordert, ist dies ein starker Indikator dafür, dass die Logik entweder vereinfacht oder in zwei verschiedene Zielgruppen unterteilt werden sollte (z. B. eine Zielgruppe „Interaktion“ und eine Zielgruppe „Konversion„).

+++

**Werden diese neuen Validierungen meine bestehenden Zielgruppen beschädigen?**

+++ Antwort

Diese Validierungen werden zum Zeitpunkt der **ausgeführt**. Daher werden Ihre bestehenden Zielgruppen weiterhin so ausgeführt, wie sie sind. Wenn Sie jedoch versuchen, eine bestehende Audience zu bearbeiten, die gegen diese Regeln verstößt, müssen Sie sie optimieren, bevor Sie Ihre Änderungen speichern können.

+++

**Ich habe komplexe Datenanforderungen. Wie kann ich die Warnung „Verschachtelte Daten“ vermeiden?**

+++ Antwort

Das Vermeiden der Warnung „Verschachtelte Daten“ wird am besten auf der Datenmodellierungsebene gelöst. Einige Tipps umfassen die Zusammenarbeit mit Ihrem Data-Engineering-Team, um Ihr XDM-Schema zu reduzieren, und die Aufnahme kritischer Attribute (wie `subscriptionStatus` und `loyaltyTier`) in die oberste Ebene des Profils.

+++

**Werden diese Prüfungen für die Zielgruppen „Entwurf“ und „Veröffentlicht“ gelten?**

+++ Antwort

Ja, diese Prüfungen gelten für *alle* Zielgruppen, die in Experience Platform ausgewertet werden.

+++
