---
title: Architekturaktualisierungen auf Real-Time CDP B2B edition
description: Lesen Sie dieses Dokument, um mehr über die umfassenden Architekturupgrades auf Real-Time CDP B2B edition zu erfahren.
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
hide: true
hidefromtoc: true
source-git-commit: 78444555178773a8305ba27aaaf7998fe279a71d
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 0%

---

# Architekturupgrades auf Real-Time CDP B2B edition

>[!IMPORTANT]
>
>In diesem Dokument werden architektonische Upgrades für die Real-Time CDP B2B- und B2P-Editionen beschrieben. **Keine Aktion von Ihnen erforderlich** an dieser Stelle. In diesem Dokument finden Sie Informationen darüber, wie sich die Upgrades auf bestehende Funktionen von Adobe Experience Platform auswirken. Wenden Sie sich bei Fragen an Ihr Adobe Account Team.

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

### Vollständiger Lookback für Ereignisse auf Benutzerebene in Konto-Zielgruppen

Account-Zielgruppen können jetzt den vollständigen Verlauf von Ereignissen auf Personenebene nutzen, der über das vorherige 30-tägige Lookback-Fenster hinausgeht.

Mit diesem Upgrade haben Sie jetzt folgende Möglichkeiten:

* Erstellen Sie umfassendere Zielgruppen basierend auf dem vollständigen Verlauf der zugehörigen Ereignisse auf Personenebene.
* Durch die Nutzung langfristiger Verhaltensdaten werden umfassendere und genauere Zielgruppendefinitionen ermöglicht.
* Identifizieren Sie hochwertige Konten basierend auf tieferen Interaktionsmustern im Laufe der Zeit.
* Support-Anwendungsfälle, die Einblicke aus historischen Aktionen erfordern, wie z. B. lange Verkaufszyklen oder verzögerte Kaufsignale.

Weitere Informationen finden Sie in der Dokumentation [Konto](../segmentation/types/account-audiences.md)Zielgruppen“.

## Aktualisierungen vorhandener Funktionen

Die folgenden Funktionen wurden im Rahmen der B2B-Architekturupgrades aktualisiert.

### Aktualisierungen für Zielgruppen mit mehreren Entitäten mit B2B-Attributen und Erlebnisereignissen

Im Rahmen des neuen Architekturupgrades können Erlebnisereignisfilter nicht mehr in einer einzelnen Zielgruppe mit mehreren Entitäten verwendet werden, die B2B-Attribute enthält.

Verwenden Sie zum Erreichen derselben Zielgruppenlogik den Ansatz nach Segmenten:

1. Zielgruppe für Erlebnisereignisse erstellen: Definieren Sie die Verhaltensbedingung separat. Beispiel: „Personen, die die Seite „Preise“ in den letzten drei Tagen besucht haben.“
2. Erstellen einer Zielgruppe mit mehreren Entitäten mit B2B-Attributen: Verweisen Sie auf die Zielgruppe des Erlebnisereignisses als Teil der Kriterien dieser Zielgruppe. Beispiel: „Personen, die **Entscheidungsträger sind** erhalten jede Möglichkeit, bei der das Konto in der Finanzbranche der **** ist, und Mitglieder der Zielgruppe, die die Preisseite in den letzten drei Tagen besucht hat.

Nach Abschluss des Upgrades müssen alle neuen Zielgruppen mit mehreren Entitäten mit B2B-Attributen und Erlebnisereignissen mithilfe des Segmentansatzes erstellt werden. Darüber hinaus müssen Sie die Zielgruppenzugehörigkeit überprüfen, um das erwartete Verhalten sicherzustellen.

### Entitätsauflösung und Zeitpriorität für die Zusammenführung in B2B-Zielgruppen

Im Rahmen des Architekturupgrades hat Adobe die tägliche Entitätsauflösung für Konten und Opportunitys eingeführt. Diese Verbesserung ermöglicht es Experience Platform, mehrere Datensätze zu identifizieren und zu konsolidieren, die dieselbe reale Entität repräsentieren, wodurch die Datenkonsistenz verbessert und eine genauere Zielgruppensegmentierung ermöglicht wird.

Mit diesem Upgrade haben Sie jetzt folgende Möglichkeiten:

* Verwenden Sie die [!DNL Profile Access]-APIs, um die neuesten Zusammenführungsprofile anzuzeigen, sobald die täglichen Entitätsauflösungsaufträge abgeschlossen sind.
* Nutzen Sie die verbesserte Genauigkeit und Konsistenz Ihrer Konto- und Opportunity-Daten für die Segmentierung, Aktivierung und Analyse.

Weitere Informationen finden [[!DNL Profile Access]  in ](../profile/api/entities.md)API“.

### Unterstützung von Zusammenführungsrichtlinien in B2B-Zielgruppen mit mehreren Entitäten

Zielgruppen mit mehreren Entitäten mit B2B-Attributen unterstützen jetzt eine einzige Zusammenführungsrichtlinie - die standardmäßige Zusammenführungsrichtlinie, die Sie konfigurieren - anstelle mehrerer Zusammenführungsrichtlinien.

Zielgruppen, die sich zuvor auf eine nicht standardmäßige Zusammenführungsrichtlinie verlassen haben, können andere Ergebnisse erzielen. Um die potenziellen Änderungen bei der Zielgruppenkomposition zu verstehen, überprüfen und testen Sie jede Ihrer Zielgruppen, die auf einer nicht standardmäßigen Zusammenführungsrichtlinie basieren. Überwachen Sie außerdem die Aktivierungsergebnisse, um Verschiebungen in der Zielgruppenkomposition aufgrund der Änderung der Zusammenführungsrichtlinie zu erkennen.

Weitere Informationen finden [ im Benutzerhandbuch für Segmentierungsanwendungsfälle ](./segmentation/b2b.md) Real-Time CDP B2B edition.

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

Weitere Informationen finden [[!DNL Profile Access]  in ](../profile/api/entities.md)API“.

### Konto- und Opportunity-Profilsuche

Sie können jetzt Konto- und Opportunity-Schemata erst abrufen, nachdem sie den täglichen Entitätsauflösungsprozess abgeschlossen haben. Neu aufgenommene Datensätze stehen erst dann für die Profilanreicherung oder Segmentdefinitionen zur Verfügung, wenn der nächste Entitätsauflösungszyklus abgeschlossen ist (normalerweise alle 24 Stunden).

Es wird empfohlen, alle Anwendungsfälle zu überprüfen, die Echtzeitzugriff auf Konto- und Opportunity-Daten erfordern. Darüber hinaus wird empfohlen, beim Entwerfen oder Aktualisieren von Workflows, die auf Lookup-basierter Segmentierung oder Personalisierung mit Konto- und Opportunity-Entitäten basieren, einen Latenzzeitraum von bis zu 24 Stunden einzuplanen.

### Einstellung der Zielgruppenerstellung über API für B2B-Entitäten

Die Erstellung von Zielgruppen mithilfe von B2B-Entitäten über die API wird nicht mehr unterstützt. Die Liste der betroffenen B2B-Entitäten umfasst:

* Konto
* Opportunity
* Konto-Personen-Beziehung
* Opportunity-Person-Beziehung
* Campaign
* Kampagnenmitglied
* Marketing-Liste
* Marketing-Listenabonnent

Weitere Informationen finden [ im Handbuch ](../segmentation/api/segment-definitions.md) Segmentdefinitionen-Endpunkt-API .

### Änderungen an Audience-Importen mit mehreren Entitäten in Sandbox-Tools

Mit den Architekturupgrades können Sie keine Zielgruppen mit mehreren Entitäten mit B2B-Attributen und Erlebnisereignissen mehr importieren, wenn diese vor dem Upgrade exportiert wurden. Diese Zielgruppen können nicht importiert werden und können nicht automatisch in die neue Architektur konvertiert werden. Um diese Einschränkung zu umgehen, müssen Sie diese Zielgruppen erneut exportieren und sie dann mithilfe von Sandbox-Tools in ihre jeweiligen Ziel-Sandboxes importieren.

Weitere Informationen finden [ im Sandbox](../sandboxes/ui/sandbox-tooling.md)Toolinghandbuch .