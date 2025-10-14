---
title: Architekturaktualisierungen auf Real-Time CDP B2B edition
description: Lesen Sie dieses Dokument, um mehr über die umfassenden Architekturupgrades auf Real-Time CDP B2B edition zu erfahren.
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: d958a947-e195-4dd4-a04c-63ad82829728
source-git-commit: 1a3be99ca3c270dda6e8dc559359cbe21bb8f4fb
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 0%

---

# Architekturupgrades auf Real-Time CDP B2B edition

>[!IMPORTANT]
>
>In diesem Dokument werden architektonische Upgrades für die Real-Time CDP B2B- und B2P-Editionen beschrieben. Die Upgrades erfordern von den meisten Kunden keine Aktionen. Es gibt jedoch Zielgruppen, die nicht automatisch aktualisiert werden können. Adobe arbeitet bei der Lösung dieser Probleme direkt mit Ihnen zusammen. In diesem Dokument finden Sie Informationen darüber, wie sich die Upgrades auf bestehende Funktionen von Adobe Experience Platform auswirken. Wenden Sie sich bei Fragen an Ihr Adobe Account Team.

Adobe hat die Real-Time CDP B2B- und B2P-Editionen neu gestaltet, um Skalierbarkeit, Leistung und Zuverlässigkeit zu verbessern und gleichzeitig erweiterte B2B-Anwendungsfälle zu unterstützen. Um sicherzustellen, dass alle Kunden von diesen Verbesserungen profitieren, aktualisiert Adobe alle bestehenden B2B- und B2P-Kunden auf die neue Architektur.

Nutzen Sie die erweiterte Architektur für die folgenden Vorteile:

* **Skalierbarkeit der Datenaufnahme**: Verbesserte Unterstützung für B2B-Beziehungen mit hoher Kardinalität, z. B. Konten, die mit Tausenden von Personen verbunden sind.
* **Leistungsfähige und zuverlässige Zielgruppenauswertung**: Schnellere und robustere Segmentierung für komplexe B2B-Zielgruppen.
* **Entitätsauflösung**: Verbesserte Identitätsauflösung für B2B-Entitäten, verbesserte Datenqualität und reduzierte Duplizierung, um eine genauere Segmentierung und Aggregation zu ermöglichen.

## Neue Funktionen

Im Folgenden finden Sie wichtige Verbesserungen, die beim Architekturupgrade enthalten sind.

### Konto-Momentaufnahmen für die Zielgruppenzugehörigkeit

Mit der neuen B2B-Architektur sind jetzt Details zur Zielgruppenzugehörigkeit für Kontoentitäten in Schnappschuss-Exporten enthalten. Mit dieser Funktion können Sie auf den Zielgruppenstatus auf Kontoebene, Zeitstempel und Mitgliedschaftsindikatoren zugreifen.

Mit diesem Upgrade haben Sie jetzt folgende Möglichkeiten:

* Marketing- und Operations-Teams die direkte Validierung der Mitgliedschaft in der Konto-Zielgruppe ermöglichen.
* Funktionsgleichheit zwischen Ihren Profil- (Personen-) und Account-Segmentierungsmodellen erzielen und so ein konsistentes Erlebnis über Entitäten hinweg sicherstellen

Weitere Informationen finden Sie in der Dokumentation [Konto](../segmentation/types/account-audiences.md)Zielgruppen“.

### Anzahl der Zielgruppen für Zielgruppen, die B2B-Entitäten enthalten

Schätzungen der Zielgruppengröße für Zielgruppen mit B2B-Entitäten werden jetzt mit exakter Genauigkeit berechnet. Diese Schätzungen stehen während der Vorschau zur Verfügung und bieten genauere und zuverlässigere Einblicke für Zielgruppen, bei denen komplexe B2B-Beziehungen eine Rolle spielen.

Mit diesem Upgrade haben Sie jetzt folgende Möglichkeiten:

* Verwenden Sie Einblicke aus präzisen Schätzungen der Zielgruppengröße, um die Planung und Entscheidungsfindung während des Erstellungsprozesses der Zielgruppe zu verbessern.
* Entwerfen Sie vertrauensvoll komplexe B2B-Zielgruppen mit Kenntnissen in Bezug auf eine genauere Zielgruppenschätzung.
* Ermöglichen Sie eine intelligentere Kampagnenplanung, eine präzisere Zielgruppenbestimmung und eine bessere Ressourcenzuweisung.

Weitere Informationen finden Sie in der Dokumentation [Konto](../segmentation/types/account-audiences.md)Zielgruppen“.

## Aktualisierungen vorhandener Funktionen

Die folgenden Funktionen wurden im Rahmen der B2B-Architekturupgrades aktualisiert.

### Aktualisierungen für Zielgruppen mit mehreren Entitäten mit B2B-Attributen und Erlebnisereignissen

Im Rahmen des neuen Architekturupgrades können Erlebnisereignisfilter nicht mehr in einer einzelnen Zielgruppe mit mehreren Entitäten verwendet werden, die B2B-Attribute enthält.

Um dieselbe Zielgruppenlogik zu erreichen, können Sie Segment Builder verwenden, um Zielgruppen [&#x200B; und zu referenzieren](../segmentation/ui/segment-builder.md#adding-audiences)

Beispiel:

* Erstellen einer Zielgruppe für Erlebnisereignisse
   * Definieren Sie die Verhaltensbedingung separat. Beispiel: „Personen, die die Seite „Preise“ in den letzten drei Tagen besucht haben.“
* Erstellen Sie eine Zielgruppe mit mehreren Entitäten mit B2B-Attributen.
   * Von hier aus können Sie die Zielgruppe des Erlebnisereignisses als Teil der Kriterien dieser Zielgruppe referenzieren. Beispiel: „Personen, die **Entscheidungsträger sind** erhalten jede Möglichkeit, bei der das Konto in der Finanzbranche der **&#x200B;**&#x200B;ist, und Mitglieder der Zielgruppe, die die Preisseite in den letzten drei Tagen besucht hat.

Nach Abschluss des Upgrades müssen alle neuen Zielgruppen mit mehreren Entitäten mit B2B-Attributen und Erlebnisereignissen mithilfe des [Segment-of-Segment](../segmentation/methods/edge-segmentation.md#edge-segmentation-query-types)-Ansatzes erstellt werden.

>[!TIP]
>
>Ein **Segment von Segmenten** ist eine Segmentdefinition, die ein oder mehrere Batch- oder Edge-Segmente enthält. **Hinweis**: Wenn Sie ein Segment von Segmenten verwenden, erfolgt **alle 24 Stunden** eine Profildisqualifizierung.

### Entitätsauflösung und Zeitpriorität für die Zusammenführung in B2B-Zielgruppen

Im Rahmen des Architekturupgrades führt Adobe die Entitätsauflösung für Accounts und Opportunities ein. Die Entitätsauflösung basiert auf einem deterministischen ID-Abgleich und auf den neuesten Daten. Der Vorgang zur Entitätsauflösung wird täglich während der Batch-Segmentierung ausgeführt, bevor Zielgruppen mit mehreren Entitäten mit B2B-Attributen bewertet werden.

>[!BEGINSHADEBOX]

#### Wie funktioniert die Entitätsauflösung?

* **Vor**: Wenn eine DUNS-Nummer (Data Universal Numbering System) als zusätzliche Identität verwendet wurde und die DUNS-Nummer des Kontos in einem Quellsystem wie CRM aktualisiert wurde, ist die Konto-ID mit alten und neuen DUNS-Nummern verknüpft.
* **Nachher**: Wenn die DUNS-Nummer als zusätzliche Identität verwendet wurde und die DUNS-Nummer des Kontos in einem Quellsystem wie einem CRM aktualisiert wurde, ist die Konto-ID nur mit der neuen DUNS-Nummer verknüpft und spiegelt somit den aktuellen Kontostand genauer wider.

>[!ENDSHADEBOX]

Mit diesem Upgrade haben Sie jetzt folgende Möglichkeiten:

* Verwenden Sie die [!DNL Profile Access]-APIs, um die neuesten Zusammenführungsprofile anzuzeigen, sobald die täglichen Entitätsauflösungsaufträge abgeschlossen sind.
* Nutzen Sie die verbesserte Genauigkeit und Konsistenz Ihrer Konto- und Opportunity-Daten für die Segmentierung, Aktivierung und Analyse.

Weitere Informationen finden [[!DNL Profile Access]  in &#x200B;](../profile/api/entities.md)API“.

### Unterstützung von Zusammenführungsrichtlinien in B2B-Zielgruppen mit mehreren Entitäten

Zielgruppen mit mehreren Entitäten mit B2B-Attributen unterstützen jetzt eine einzige Zusammenführungsrichtlinie - die standardmäßige Zusammenführungsrichtlinie, die Sie konfigurieren - anstelle mehrerer Zusammenführungsrichtlinien.

Weitere Informationen finden [&#x200B; im Benutzerhandbuch für Segmentierungsanwendungsfälle &#x200B;](./segmentation/b2b.md) Real-Time CDP B2B edition.

### Einstellung der B2B-Entitätssuche und -löschung in der [!DNL Profile Access]-API

Die folgenden Suchfunktionen für B2B-Entitäten, die die [!DNL Profile Access]-API verwenden, werden nicht mehr unterstützt:

* Konto-Personen-Beziehung
* Opportunity-Person-Beziehung
* Campaign
* Kampagnenmitglied
* Marketing-Liste
* Mitglieder der Marketing-Liste

Löschanfragen für die folgenden B2B-Entitäten, die die [!DNL Profile Access]-API verwenden, werden nicht mehr unterstützt:

* Konto
* Konto-Personen-Beziehung
* Opportunity
* Opportunity-Person-Beziehung
* Campaign
* Kampagnenmitglied
* Marketing-Liste
* Mitglieder der Marketing-Liste

Weitere Informationen finden [[!DNL Profile Access]  in &#x200B;](../profile/api/entities.md)API“.

### Konto- und Opportunity-Profilsuche

Sie können jetzt Konto- und Opportunity-Schemata erst abrufen, nachdem sie den täglichen Entitätsauflösungsprozess abgeschlossen haben. Neu aufgenommene Datensätze stehen erst dann für die Profilanreicherung oder Segmentdefinitionen zur Verfügung, wenn der nächste Entitätsauflösungszyklus abgeschlossen ist (normalerweise alle 24 Stunden).

<!-- ### Deprecation of audience creation via API for B2B entities

Creation of audiences using B2B entities via API is being deprecated. The list of affected B2B entities include:

* Account
* Opportunity
* Account-Person Relation
* Opportunity-Person Relation
* Campaign
* Campaign Member
* Marketing List
* Marketing List Member

Read the [segment definitions endpoint API guide](../segmentation/api/segment-definitions.md) for more information. -->

### Änderungen an Audience-Importen mit mehreren Entitäten in Sandbox-Tools

Mit den Architekturupgrades können Sie keine Zielgruppen mit mehreren Entitäten mit B2B-Attributen und Erlebnisereignissen mehr importieren, wenn ein Paket, das diese Zielgruppen enthält, vor dem Upgrade veröffentlicht wurde. Diese Zielgruppen können nicht importiert werden und können nicht automatisch in die neue Architektur konvertiert werden. Um diese Einschränkung zu umgehen, müssen Sie ein neues Paket mit den aktualisierten Zielgruppen erstellen und sie dann mithilfe von Sandbox-Tools in ihre jeweiligen Ziel-Sandboxes importieren.

Entwicklungs-Sandboxes werden auf die neue Architektur aktualisiert. Zielgruppen, die automatisch aktualisiert werden können, werden aktualisiert. Zielgruppen, die nicht automatisch aktualisiert werden können, werden deaktiviert. Deaktivierte Zielgruppen müssen nach dem Upgrade neu erstellt werden.

Weitere Informationen finden [&#x200B; im Sandbox](../sandboxes/ui/sandbox-tooling.md)Toolinghandbuch .
