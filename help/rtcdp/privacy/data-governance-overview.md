---
title: Data Governance – Übersicht
seo-title: Data Governance in der Echtzeit-Kundendatenplattform
description: 'Mit Data Governance können Sie Kundendaten verwalten und bei der Verwendung von Daten die Einhaltung von Vorschriften, Einschränkungen und Richtlinien sicherstellen. '
seo-description: 'Mit Data Governance können Sie Kundendaten verwalten und bei der Verwendung von Daten die Einhaltung von Vorschriften, Einschränkungen und Richtlinien sicherstellen. '
translation-type: tm+mt
source-git-commit: e21cf6794e6c9ee522482cd9ccb95d66b06d330a

---


# Data Governance in der Echtzeit-Kundendatenplattform

Die Echtzeit-Kundendatenplattform führt Daten aus verschiedenen Unternehmenssystemen zusammen, damit Marketer ihre Kunden besser ermitteln, verstehen und ansprechen können. Diese Daten können Nutzungsbeschränkungen unterliegen, die von Ihrem Unternehmen oder durch gesetzliche Bestimmungen festgelegt werden. Daher muss sichergestellt sein, dass die Echtzeit-Kundendatenplattform bei der Verarbeitung Ihrer Daten mit den Nutzungsrichtlinien konform ist.

Mit Data Governance in Adobe Experience Platform können Sie Kundendaten verwalten und bei der Verwendung von Daten die Einhaltung von Vorschriften, Einschränkungen und Richtlinien sicherstellen. Data Governance spielt in der Echtzeit-Kundendatenplattform eine zentrale Rolle und erlaubt es Ihnen, Nutzungsrichtlinien zu definieren, Daten anhand dieser Richtlinien zu kategorisieren und bei Ausführung bestimmter Marketing-Aktionen auf Richtlinienverletzungen zu prüfen.

Die Echtzeit-Kundendatenplattform basiert auf Adobe Experience Platform. Daher werden die meisten Data Governance-Funktionen in der Experience Platform-Dokumentation behandelt. Dieses Dokument dient als Ergänzung zu [Data Governance – Übersicht](../../data-governance/home.md) für Experience Platform und bietet Informationen zu den Governance-Funktionen, die in der Echtzeit-Kundendatenplattform verfügbar sind. Folgende Themen werden behandelt:

* [Nutzungsbezeichnungen auf Daten anwenden](#labels)
* [Richtlinien zur Datennutzung verwalten](#policies)
* [Einhaltung von Datennutzungsrichtlinien durchsetzen](#enforcement)

## Nutzungsbezeichnungen auf Daten anwenden {#labels}

Mit Data Governance können Sie Nutzungsbezeichnungen auf Ihre Daten anwenden, entweder auf der Datensatz- oder der Datensatzfeldebene. Mit Datennutzungsbezeichnungen können Sie Daten anhand der für diese Daten geltenden Nutzungsrichtlinien kategorisieren.

Genauere Informationen zum Arbeiten mit Datennutzungsbezeichnungen finden Sie im [Benutzerhandbuch für Datennutzungsbezeichnungen](../../data-governance/labels/overview.md) für Adobe Experience Platform.

## Beschränkungen für Ziele festlegen

Sie können Datenverwendungsbeschränkungen für ein Ziel festlegen, indem Sie Anwendungsfälle für das Marketing für dieses Ziel definieren. Wenn Sie Anwendungsfälle für Ziele definieren, können Sie prüfen, ob Verstöße gegen die Nutzungsrichtlinien vorliegen, und sicherstellen, dass alle an dieses Ziel gesendeten Profil oder Segmente mit den Datenverwaltungsregeln kompatibel sind.

Anwendungsfälle für Marketing können während der _Setup_ -Phase des Arbeitsablaufs &quot;Ziel _bearbeiten_ &quot;definiert werden. Weitere Informationen finden Sie in der Zieldokumentation.


## Richtlinien zur Datennutzung verwalten {#policies}

Damit Datennutzungsbezeichnungen die Datenkonformität effektiv unterstützen können, müssen Sie Datennutzungsrichtlinien definieren und aktivieren. Datennutzungsrichtlinien sind Regeln, die die Arten von Marketing-Aktionen beschreiben, die Sie für Daten in der Echtzeit-Kundendatenplattform ausführen bzw. nicht ausführen dürfen. Weiterführende Informationen dazu finden Sie im Abschnitt „Datennutzungsrichtlinien“ unter [Data Governance – Übersicht](../../data-governance/home.md) für Experience Platform.

Adobe Experience Platform bietet verschiedene **zentrale Richtlinien** für gängige Anwendungsfälle bei Kundenerlebnissen. Diese Richtlinien können angezeigt werden, indem Sie eine Anfrage an die [DULE Policy Service-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) richten, wie im Abschnitt „Alle Richtlinien auflisten“ des [Policy Service-Entwicklerhandbuchs](../../data-governance/policies/overview.md) dargestellt. Alternativ können Sie eigene **benutzerdefinierte Richtlinien** erstellen, um benutzerdefinierte Nutzungsbeschränkungen zu modellieren (wie im Abschnitt „Richtlinie erstellen“ des Entwicklerhandbuchs beschrieben).

## (Beta) Enforce data usage compliance {#enforce-data-usage-compliance}

>[!IMPORTANT]
>Diese Funktion befindet sich derzeit in der Betaphase und steht nicht allen Benutzern zur Verfügung. Sie kann auf Anfrage aktiviert werden. Dokumentation und Funktionalität können sich ändern.

Nachdem Sie Daten gekennzeichnet und Nutzungsrichtlinien definiert haben, können Sie die Einhaltung von Datennutzungsrichtlinien erzwingen. Beim Aktivieren von Segmenten der Audience in CDP in Echtzeit erzwingt die Datenverwaltung automatisch Nutzungsrichtlinien, falls Verstöße auftreten sollten.

Das folgende Diagramm zeigt, wie die Richtliniendurchsetzung in den Datenfluss der SegmentAktivierung integriert wird:

![](assets/enforcement-flow.png)

Wenn ein Segment zum ersten Mal aktiviert wird, prüft der DULE-Policy-Dienst anhand der folgenden Faktoren, ob Richtlinienverletzungen vorliegen:

* Die Datenverwendungsbeschriftungen, die auf Felder und Datensätze innerhalb des zu aktivierenden Segments angewendet werden.
* Der Vermarktungszweck der Bestimmung.

### Richtlinienverletzungsmeldungen {#enforcement}

Wenn eine Richtlinienverletzung beim Versuch auftritt, ein Segment zu aktivieren (oder ein bereits aktiviertes Segment [zu](#policy-enforcement-for-activated-segments)bearbeiten), wird die Aktion verhindert und ein Popup angezeigt, das anzeigt, dass eine oder mehrere Richtlinien verletzt wurden. Wählen Sie eine Richtlinienverletzung in der linken Spalte des Popup aus, um Details zu dieser Verletzung anzuzeigen.

![](assets/violation-popover.png)

Die Registerkarte &quot; *Details* &quot;des Popup-Fensters zeigt die Aktion an, die die Verletzung ausgelöst hat, den Grund für die Verletzung und enthält Vorschläge, wie das Problem möglicherweise gelöst werden kann.

Klicken Sie auf **Datenlineare** , um die Ziele, Segmente, Zusammenführungsrichtlinien oder Datensätze zu verfolgen, deren Datenbeschriftungen die Verletzung ausgelöst haben.

![](assets/data-lineage.png)

Nachdem eine Verletzung ausgelöst wurde, wird die Schaltfläche **Speichern** für die Aktivierung deaktiviert, bis die entsprechenden Komponenten aktualisiert wurden, um den Datenverwendungsrichtlinien zu entsprechen.

### Richtliniendurchsetzung für aktivierte Segmente {#policy-enforcement-for-activated-segments}

Die Richtliniendurchsetzung gilt auch für Segmente, nachdem sie aktiviert wurden. Dadurch werden Änderungen an einem Segment oder seinem Ziel eingeschränkt, die zu einer Richtlinienverletzung führen würden. Aufgrund der zahlreichen Komponenten, die beim Aktivieren von Segmenten zu Zielen beteiligt sind, kann eine der folgenden Aktionen möglicherweise eine Verletzung auslösen:

* Aktualisieren von Beschriftungen für die Datenverwendung
* Ändern von Datensätzen für ein Segment
* Segmentvorhersagen ändern
* Ändern der Zielkonfigurationen

Wenn eine der oben genannten Aktionen eine Verletzung auslöst, wird verhindert, dass diese Aktion gespeichert wird und eine Richtlinienverletzungsmeldung angezeigt wird. Dadurch wird sichergestellt, dass Ihre aktivierten Segmente beim Ändern der Datenverwendungsrichtlinien weiterhin eingehalten werden.

## Nächste Schritte

Nach der Vorstellung der wichtigsten Data Governance-Funktionen in der Echtzeit-Kundendatenplattform und deren Aktivierung durch Experience Platform lesen Sie nun die [Data Governance-Dokumentation für Adobe Experience Platform](../../data-governance/home.md). Die Dokumentation bietet einen Überblick über wesentliche Data Governance-Konzepte sowie schrittweise Workflows zum Verwalten von Datennutzungsbezeichnungen und -richtlinien.