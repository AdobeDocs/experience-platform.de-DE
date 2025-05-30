---
title: Adobe Experience Platform – Versionshinweise November 2021
description: Versionshinweise von November 2021 für Adobe Experience Platform.
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 81%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 17. November 2021**

## Neue Funktionen

Neue Funktionen in Adobe Experience Platform:

- [Real-Time Customer Data Platform B2B Edition](#B2B)
- [(Beta) Aktivieren von Zielgruppensegmenten für Batch-Ziele über die Ad-hoc-Aktivierungs-API](#ad-hoc-activation)

## Aktualisierungen vorhandener Funktionen

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Attributions-KI](#attribution-ai)
- [Kunden-KI](#customer-ai)

### Real-Time Customer Data Platform B2B Edition {#B2B}

**Veröffentlichungsdatum: 12. November 2021**

Real-Time CDP B2B Edition basiert auf Real-time Customer Data Platform (Real-Time CDP) und wurde speziell für Marketingexpertinnen und -experten mit einem Business-to-Business-Service-Modell entwickelt. Es führt Daten aus verschiedenen Quellen zusammen und kombiniert sie zu einer einzigen Ansicht von Personen und Account-Profilen. Diese vereinheitlichten Daten ermöglichen es Marketing-Experten, bestimmte Zielgruppen präzise anzusprechen und über alle verfügbaren Kanäle anzusprechen.

Es gibt Verbesserungen bei einer Reihe von Funktionen von Adobe Experience Platform, die Real-Time CDP B2B Edition vom B2C-Pendant unterscheiden. Dazu gehören Verbesserungen am Experience-Datenmodell (XDM) für B2B-Anwendungsfälle, Upgrades für die Identitätsauflösung und die Profilsegmentierung sowie ein maßgeschneiderter Connector und ein Ziel für Marketo Engage. Mit dem Marketo-Connector können B2B-Marken ihre branchenführenden B2B-Interaktionsdaten mit Verhaltensinformationen verknüpfen, um Leads zu pflegen und Maßnahmen für Account-basiertes Marketing zu verbessern.

-[Neue B2B- und B2P-Editionen](#editions)
-[Neue Marketo-Connectoren für Datenquelle und Ziel](#marketo)
-[Standard-B2B-XDM](#XDM)

### Neue B2B- und B2P-Editionen {#editions}

Neue B2B- und B2P-Editionen, die B2B-Daten und -Funktionen sowohl in Real-Time CDP als auch in Experience Platform Activation-Produkten ermöglichen, sind zum Kauf verfügbar.

Weitere Informationen zu Real-Time CDP B2B edition finden Sie in der [Übersicht](../../rtcdp/overview.md).

### Neue Marketo-Connectoren für Datenquelle und Ziel {#marketo}

Neue Marketo-Connectoren für Datenquelle und Ziel ermöglichen das Streamen von Marketo-Daten in Experience Platform und von Experience Platform-Zielgruppen zurück an Marketo. Verfügbar für alle Experience Platform-Benutzer.

| Funktion | Beschreibung |
|----------|-------------|
| Marketo Engage-Quell-Connector | Der [Marketo Engage-Quell-Connector](../../sources/connectors/adobe-applications/marketo/marketo.md) ermöglicht es Marketing-Experten, Daten aus einer oder mehreren Marketo-Instanzen nahtlos in ihre Adobe Experience Platform-Instanz aufzunehmen, und bietet eine Komplettlösung für Lead-Management und B2B-Marketing. |
| Marketo Engage-Ziel | Das [Marketo-Ziel](../../destinations/catalog/adobe/marketo-engage.md) ermöglicht es Marketing-Experten, in Adobe Experience Platform erstellte Segmente per Push an Marketo zu übertragen, wo sie als statische Listen angezeigt werden. |

### Standard-B2B-XDM {#XDM}

Standardmäßige B2B-XDM-Klassen, -Feldergruppen und -Datentypen sind für alle Experience Platform-Benutzer verfügbar.

| Funktion | Beschreibung |
|-----------|--------------|
| Standard-B2B-XDM-Klassen | Real-Time Customer Data Platform B2B edition bietet mehrere standardmäßige XDM-Dateien, die Details zu wesentlichen B2B-Datenentitäten wie Konten, Chancen und Kampagnen erfassen. |

Weitere Informationen zur [ von B2B-Datenentitäten finden Sie ](../../rtcdp/schemas/b2b.md) der Dokumentation zu Schemas in Real-Time Customer Data Platform B2B edition .

### (Beta) Aktivieren von Zielgruppensegmenten für Batch-Ziele über die Ad-hoc-Aktivierungs-API {#ad-hoc-activation}

Mit der Ad-hoc-Aktivierungs-API können Marketing-Experten Zielgruppensegmente schnell und effizient für Situationen aktivieren, in denen eine sofortige Aktivierung erforderlich ist. Die Ad-hoc-Zielgruppenaktivierung wird nur von [Batch-dateibasierten Zielen](../../destinations/destination-types.md#file-based) unterstützt und befindet sich derzeit in der Beta-Phase. Weitere Informationen finden Sie in der [Dokumentation zur Ad-hoc-Aktivierungs-API](../../destinations/api/ad-hoc-activation-api.md).

### Attributions-KI {#attribution-ai}

Attributions-KI wird verwendet, um Touchpoints Ereignissen zuzuordnen, die zu Konversionen führen. Dies kann von Marketing-Fachleuten genutzt werden, um auf diversen Customer Journeys die Auswirkungen jedes einzelnen Marketing-Touchpoints zu quantifizieren.

| Funktion | Beschreibung |
|-----------|---------------|
| Unterstützung für mehrere Datensätze | Attributions-KI kann jetzt problemlos mehrere Datensätze direkt in der Benutzeroberfläche aufnehmen, ohne dass jeder Datensatz zugeordnet und zusammengefügt werden muss. Diese neue zeitsparende Funktion bietet leistungsfähigere und genauere Scores mit umfangreicheren Daten aus mehreren Datensätzen. |
| Medienkanal- und Kampagnenfeldzuordnung | Attributions-KI unterstützt jetzt die Zuordnung von Medienkanal- und Kampagnenfeldern. Die Zuordnung von Medienkanälen zwischen Datensätzen verbessert die aus Attributions-KI gewonnenen Insights und liefert klarere Ergebnisse, die einfach zu interpretieren sind. |

Weitere Informationen zu Attributions-KI finden Sie in der [Dokumentation zu Attributions-KI](../../intelligent-services/attribution-ai/overview.md).

### Kunden-KI {#customer-ai}

Die in Real-time Customer Data Platform verfügbare Kunden-KI dient dazu, in großem Umfang benutzerdefinierte Tendenzwerte wie Abwanderung und Konversion für einzelne Profile zu generieren. Dies wird erreicht, ohne dass die Geschäftsanforderungen in ein Problem des maschinellen Lernens umgewandelt werden müssen bzw. ein Algorithmus ausgewählt, trainiert oder bereitgestellt werden muss.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
|-----------|-------------|
| Unterstützung für mehrere Datensätze | Kunden-KI kann jetzt mühelos mehrere Datensätze direkt in der Benutzeroberfläche erfassen, ohne dass jeder Datensatz zugeordnet und zusammengeführt werden muss. Diese neue zeitsparende Funktion bietet leistungsfähigere und genauere Scores mit umfangreicheren Daten aus mehreren Datensätzen. |
| Benutzerdefinierte Profilattribute | Kunden-KI unterstützt jetzt die Definition benutzerdefinierter Profildatensatzfelder (mit Zeitstempeln) in Ihren Daten zusätzlich zu standardmäßigen Ereignisfeldern. Mit dieser Option können Sie zusätzliche, von Ihnen als einflussreich erachtete Profilattribute hinzufügen, was die Qualität Ihres Modells verbessern und genauere Ergebnisse liefern kann. |

Weitere Informationen zu Kunden-KI finden Sie in der [Dokumentation zu Kunden-KI](../../intelligent-services/customer-ai/overview.md).
