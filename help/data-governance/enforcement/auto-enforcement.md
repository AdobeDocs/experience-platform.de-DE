---
keywords: Experience Platform;Home;beliebte Themen;Richtliniendurchsetzung;Automatische Durchsetzung;API-basierte Durchsetzung;Datenverwaltung
solution: Experience Platform
title: Automatische Richtliniendurchsetzung
topic-legacy: guide
description: In diesem Dokument wird erläutert, wie Datenverwendungsrichtlinien automatisch erzwungen werden, wenn in der Experience Platform Segmente zu Zielen aktiviert werden.
exl-id: c6695285-77df-48c3-9b4c-ccd226bc3f16
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1128'
ht-degree: 19%

---

# Automatische Durchsetzung von Richtlinien

Nachdem Sie Daten gekennzeichnet und Nutzungsrichtlinien definiert haben, können Sie die Einhaltung von Datennutzungsrichtlinien erzwingen. Beim Aktivieren von Segmenten der Audience in Ziele erzwingt Adobe Experience Platform automatisch Nutzungsrichtlinien, falls Verstöße auftreten sollten.

## Voraussetzungen

Dieser Leitfaden erfordert ein funktionierendes Verständnis der Plattformdienste, die bei der automatischen Durchsetzung von Vorschriften beteiligt sind. Lesen Sie die folgende Dokumentation, um mehr zu erfahren, bevor Sie mit diesem Handbuch fortfahren:

* [Adobe Experience Platform-Datenverwaltung](../home.md): Das Framework, mit dem die Plattform die Einhaltung der Datenverwendungskonformität durch die Verwendung von Beschriftungen und Richtlinien erzwingt.
* [Echtzeit-Kundenprofil](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [Adobe Experience Platform-Segmentierungsdienst](../../segmentation/home.md): Die Segmentierungsmaschine, die  [!DNL Platform] verwendet wird, um Audiencen-Segmente aus Ihren Profilen basierend auf Kundenverhalten und -attributen zu erstellen.
* [Ziele](../../destinations/home.md): Ziele sind vorgefertigte Integrationen mit häufig verwendeten Anwendungen, die die nahtlose Aktivierung von Daten von Platform für Cross-Kanal-Marketing-Kampagnen, E-Mail-Kampagnen, gezielte Werbung und mehrY ermöglichen.

## Durchsetzungsfluss {#flow}

Das folgende Diagramm zeigt, wie die Richtliniendurchsetzung in den Datenfluss der Segmentaktivierung integriert wird:

![](../images/enforcement/enforcement-flow.png)

Wenn ein Segment zum ersten Mal aktiviert wird, überprüft [!DNL Policy Service] anhand der folgenden Faktoren, ob Richtlinienverletzungen vorliegen:

* Die Datennutzungsbezeichnungen, die auf Felder und Datensätze innerhalb des zu aktivierenden Segments angewendet werden.
* Marketing-Zweck des Ziels.

>[!NOTE]
>
>Wenn es Datenverwendungsbeschriftungen gibt, die nur auf bestimmte Felder innerhalb eines Datensatzes angewendet wurden (und nicht auf den gesamten Datensatz), erfolgt die Durchsetzung dieser Beschriftungen auf Feldebene bei der Aktivierung nur unter folgenden Bedingungen:
>
>* Die Felder werden in der Segmentdefinition verwendet.
>* Die Felder sind als projizierte Attribute für das Ziel der Zielgruppe konfiguriert.


## Datenzeile {#lineage}

Die Datenleitung spielt eine Schlüsselrolle bei der Durchsetzung von Richtlinien in der Plattform. Generell bezieht sich die Datenlineage auf die Herkunft eines Datensatzes und was mit der Zeit geschieht (oder wo sie sich bewegt).

Im Kontext von [!DNL Data Governance] ermöglicht die Lineage die Übertragung von Datenverwendungsetiketten von Datasets auf nachgelagerte Dienste, die ihre Daten verbrauchen, wie z. B. Echtzeit-Kundendaten und -Profile. Dies ermöglicht die Bewertung und Durchsetzung von Richtlinien an verschiedenen wichtigen Punkten der Journey-through-Plattform der Daten und bietet den Datenverbrauchern einen Kontext darüber, warum eine Richtlinienverletzung aufgetreten ist.

Bei der Experience Platform geht es bei der Durchsetzung der Politik um folgende Abfolge:

1. Daten werden in Plattform erfasst und in **Datasets** gespeichert.
1. Kunden-Profil werden anhand dieser Datensätze identifiziert und erstellt, indem Datenfragmente gemäß der **Mergerichtlinie** zusammengeführt werden.
1. Gruppen von Profilen werden basierend auf allgemeinen Attributen in **** unterteilt.
1. Segmente werden nach unten **Ziele** aktiviert.

Jede Phase in der oben genannten Zeitschiene stellt eine Entität dar, die, wie in der folgenden Tabelle dargestellt, zu einer verletzten Richtlinie beitragen kann:

| Datenleitungsphase | Rolle bei der Durchsetzung der Vorschriften |
| --- | --- |
| Datensatz | Datensätze enthalten Datenverwendungsbeschriftungen (auf Datensatzebene oder Feldebene angewendet), mit denen festgelegt wird, für welche Anwendungsfälle der gesamte Datensatz oder bestimmte Felder verwendet werden können. Richtlinienverletzungen treten auf, wenn ein Datensatz oder ein Feld mit bestimmten Beschriftungen für einen Zweck verwendet wird, den eine Richtlinie einschränkt. |
| Richtlinie zusammenführen | Richtlinien zum Zusammenführen sind die Regeln, die Plattform verwendet, um festzulegen, wie Daten beim Zusammenführen von Fragmenten aus mehreren Datensätzen priorisiert werden. Richtlinienverletzungen treten auf, wenn Ihre Zusammenführungsrichtlinien so konfiguriert sind, dass Datensätze mit eingeschränkten Beschriftungen für ein Ziel aktiviert werden. Weitere Informationen finden Sie im Handbuch [Mergepolicies](../../profile/ui/merge-policies.md). |
| Segment | Segmentregeln definieren, welche Attribute aus den Profilen der Kunden einbezogen werden sollen. Je nachdem, welche Felder eine Segmentdefinition enthält, übernimmt das Segment alle angewendeten Nutzungsbezeichnungen für diese Felder. Richtlinienverletzungen treten auf, wenn Sie ein Segment aktivieren, dessen geerbte Beschriftungen aufgrund der jeweiligen Richtlinien des Zielorts der Zielgruppe je nach Anwendungsfall für das Marketing eingeschränkt sind. |
| Ziel | Beim Einrichten eines Ziels kann eine Marketingaktion (manchmal auch als Marketing-Anwendungsfall bezeichnet) definiert werden. Dieser Verwendungsfall korreliert mit einer Marketingaktion, wie in einer Datenverwendungsrichtlinie definiert. Mit anderen Worten, der Marketing-Verwendungsfall, den Sie für ein Ziel definieren, bestimmt, welche Datenverwendungsrichtlinien für dieses Ziel gelten. Richtlinienverletzungen treten auf, wenn Sie ein Segment aktivieren, dessen Nutzungsbeschriftungen durch die geltenden Richtlinien des Zielgruppen-Ziels eingeschränkt sind. |

Wenn Richtlinienverletzungen auftreten, bieten die in der Benutzeroberfläche angezeigten Meldungen nützliche Werkzeuge, um die beitragende Datenlinie der Verletzung zu untersuchen und so zur Lösung des Problems beizutragen. Weitere Informationen finden Sie im nächsten Abschnitt.

## Meldungen zu Richtlinienverstößen  {#enforcement}

Wenn ein Richtlinienverstoß beim Versuch auftritt, ein Segment zu aktivieren (oder [ein bereits aktiviertes Segment zu bearbeiten](#policy-enforcement-for-activated-segments)), wird die Aktion verhindert und in einem Popup angezeigt, dass gegen eine oder mehrere Richtlinien verstoßen wurden. Nachdem eine Verletzung ausgelöst wurde, ist die Schaltfläche **[!UICONTROL Speichern]** für die Entität, die Sie ändern, deaktiviert, bis die entsprechenden Komponenten aktualisiert wurden, um den Datenverwendungsrichtlinien zu entsprechen.

Wählen Sie einen Richtlinienverstoß in der linken Spalte des Popups aus, um Details zu diesem Verstoß anzuzeigen.

![](../images/enforcement/violation-policy-select.png)

Die Meldung &quot;Verletzung&quot;enthält eine Zusammenfassung der verletzten Richtlinie, einschließlich der Bedingungen, nach denen die Richtlinie überprüft werden soll, der spezifischen Aktion, die die Verletzung ausgelöst hat, und eine Liste möglicher Lösungen für das Problem.

![](../images/enforcement/violation-summary.png)

Unter der Übersicht über die Verletzung wird ein Datenlinien-Diagramm angezeigt, das Ihnen veranschaulicht, welche Datensätze, Zusammenführungsrichtlinien, Segmente und Ziele an der Richtlinienverletzung beteiligt waren. Die Entität, die Sie derzeit ändern, wird im Diagramm hervorgehoben, was angibt, welcher Punkt im Fluss die Verletzung verursacht. Sie können einen Entitätsnamen im Diagramm auswählen, um die Detailseite für die betreffende Entität zu öffnen.

![](../images/enforcement/data-lineage.png)

Sie können auch das Symbol **[!UICONTROL Filter]** (![](../images/enforcement/filter.png)) verwenden, um die angezeigten Entitäten nach Kategorie zu filtern. Damit Daten angezeigt werden, müssen mindestens zwei Kategorien ausgewählt werden.

![](../images/enforcement/lineage-filter.png)

Wählen Sie **[!UICONTROL Liste Ansicht]** aus, um die Datenzeile als Liste anzuzeigen. Um zum visuellen Diagramm zurückzukehren, wählen Sie **[!UICONTROL Path Ansicht]**.

![](../images/enforcement/list-view.png)

## Richtliniendurchsetzung für aktivierte Segmente   {#policy-enforcement-for-activated-segments}

Die Richtliniendurchsetzung gilt auch für Segmente, nachdem sie aktiviert wurden. Dadurch werden Änderungen an einem Segment oder seinem Ziel eingeschränkt, die zu einem Richtlinienverstoß führen würden. Aufgrund der Funktionsweise von [Datenlineage](#lineage) bei der Durchsetzung von Richtlinien können die folgenden Aktionen möglicherweise eine Verletzung des Triggers verursachen:

* Aktualisieren von Datennutzungsbezeichnungen
* Ändern von Datensätzen für ein Segment
* Ändern von Segmenteigenschaften
* Ändern von Zielkonfigurationen

Wenn eine der oben genannten Aktionen einen Verstoß auslöst, wird verhindert, dass diese Aktion gespeichert wird, und eine Richtlinienverstoßmeldung wird angezeigt. Dadurch wird sichergestellt, dass Ihre aktivierten Segmente nach dem Ändern weiterhin den Datennutzungsrichtlinien entsprechen.

## Nächste Schritte

In diesem Dokument wurde erläutert, wie die automatische Durchsetzung der Vorschriften in der Experience Platform funktioniert. Anweisungen zur programmgesteuerten Integration der Richtliniendurchsetzung in Ihre Anwendungen mithilfe von API-Aufrufen finden Sie im Handbuch [API-basierte Durchsetzung](./api-enforcement.md).
