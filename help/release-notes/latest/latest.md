---
title: Adobe Experience Platform – Versionshinweise
description: Die neuesten Versionshinweise für Adobe Experience Platform.
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: 2c4b0d6dd0884fe81565356c31b18c0555bf973f
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 26%

---

# Adobe Experience Platform – Versionshinweise

**Releasedatum: 17. November 2021**

## Neue Funktionen

Neue Funktionen in Adobe Experience Platform:

- [Echtzeit-Kundendatenplattform B2B Edition](#B2B)
- [(Beta) Aktivieren von Zielgruppensegmenten für Batch-Ziele über die Ad-hoc-Aktivierungs-API](#ad-hoc-activation)

## Aktualisierungen vorhandener Funktionen

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Attribution AI](#attribution-ai)
- [Customer AI](#customer-ai)

### Echtzeit-Kundendatenplattform B2B Edition {#B2B}

**Releasedatum: 12. November 2021**

Real-time Customer Data Platform B2B Edition basiert auf Real-time Customer Data Platform (Real-time CDP) und wurde speziell für Marketing-Experten entwickelt, die in einem Business-to-Business-Service-Modell arbeiten. Es führt Daten aus verschiedenen Quellen zusammen und kombiniert sie zu einer einzigen Ansicht von Personen und Account-Profilen. Diese vereinheitlichten Daten ermöglichen es Marketing-Experten, bestimmte Zielgruppen präzise anzusprechen und über alle verfügbaren Kanäle anzusprechen.

Es gibt Verbesserungen bei einer Reihe von Funktionen von Adobe Experience Platform, die Real-time Customer Data Platform B2B Edition von ihrem B2C-Pendant unterscheiden. Dazu gehören Verbesserungen am Experience-Datenmodell (XDM) für B2B-Anwendungsfälle, Upgrades zur Identitätsauflösung und Profilsegmentierung sowie ein benutzerdefinierter Connector und ein benutzerdefiniertes Ziel für Marketo Engage. Der Marketo-Connector ermöglicht es B2B-Marken, ihre branchenführenden B2B-Interaktionsdaten mit Verhaltensinformationen zu verbinden, um Leads zu fördern und kontobasierte Marketingoperationen zu verbessern.

-[Neue B2B- und B2P-Editionen](#editions)
-[Neue Marketo-Datenquelle- und Ziel-Connectoren](#marketo)
-[Standard B2B XDM](#XDM)

### Neue B2B- und B2P-Editionen {#editions}

Es stehen neue B2B- und B2P-Editionen zur Verfügung, die B2B-Daten und -Funktionen sowohl in der Echtzeit-Kundendatenplattform als auch in Platform Activation-Produkten enthalten.

Weitere Informationen zur Echtzeit-Kundendatenplattform B2B Edition finden Sie unter [Übersicht](../../rtcdp/overview.md).

### Neue Marketo-Datenquelle- und Ziel-Connectoren {#marketo}

Neue Marketo-Datenquellen- und Ziel-Connectoren streamen Marketo-Daten an Platform- und Platform-Zielgruppen zurück nach Marketo. Verfügbar für alle Platform-Benutzer.

| Funktion | Beschreibung |
|----------|-------------|
| Marketo Engage-Quell-Connector | Die [Marketo Engage-Quell-Connector](../../sources/connectors/adobe-applications/marketo/marketo.md) ermöglicht es Marketing-Experten, Daten aus einer oder mehreren Marketo-Instanzen nahtlos in ihre Adobe Experience Platform-Instanz aufzunehmen, und bietet eine Komplettlösung für Lead-Management- und B2B-Marketer. |
| Marketo Engage-Ziel | Die [Marketo-Ziel](../../destinations/catalog/adobe/marketo-engage.md) ermöglicht es Marketingexperten, in Adobe Experience Platform erstellte Segmente per Push an Marketo zu übertragen, wo sie als statische Listen angezeigt werden. |

### Standard B2B XDM {#XDM}

Standardmäßige B2B-XDM-Klassen, Feldergruppen und Datentypen sind für alle Platform-Benutzer verfügbar.

| Funktion | Beschreibung |
|-----------|--------------|
| Standard-B2B-XDM-Klassen | Real-time Customer Data Platform B2B Edition bietet verschiedene Standard-XDM, die Details zu wesentlichen B2B-Datenentitäten wie Konten, Chancen, Kampagnen und mehr erfassen. |

Siehe [Schemata in Real-time Customer Data Platform B2B Edition](../../rtcdp/schemas/b2b.md) Dokumentation , um mehr über die Erfassung von B2B-Datenentitäten zu erfahren.

### (Beta) Aktivieren von Zielgruppensegmenten für Batch-Ziele über die Ad-hoc-Aktivierungs-API {#ad-hoc-activation}

Mit der Ad-hoc-Aktivierungs-API können Marketing-Experten Zielgruppensegmente schnell und effizient für Situationen aktivieren, in denen eine sofortige Aktivierung erforderlich ist. Die Ad-hoc-Zielgruppenaktivierung wird nur von [Batch-dateibasierte Ziele](../../destinations/destination-types.md#file-based) und befindet sich derzeit in der Beta-Phase. Weitere Informationen finden Sie unter [Dokumentation zur Ad-hoc-Aktivierungs-API](../../destinations/api/ad-hoc-activation-api.md).

### Attribution AI {#attribution-ai}

Attribution AI wird verwendet, um Touchpoints Ereignissen zuzuordnen, die zu Konversionen führen. Dies kann von Marketing-Experten genutzt werden, um die Auswirkungen jedes einzelnen Marketing-Touchpoints auf einer Customer Journey zu quantifizieren.

| Funktion | Beschreibung |
|-----------|---------------|
| Unterstützung für mehrere Datensätze | Attribution AI kann jetzt problemlos mehrere Datensätze direkt in der Benutzeroberfläche erfassen, ohne dass jeder Datensatz zugeordnet und zugeordnet werden muss. Diese neue zeitsparende Funktion bietet leistungsfähigere und genauere Ergebnisse mit umfangreicheren Daten aus mehreren Datensätzen. |
| Medienkanal- und Kampagnenfeldzuordnung | Attribution AI unterstützt jetzt die Zuordnung von Medien- und Kampagnenfeldern. Die Zuordnung von Medienkanälen zwischen Datensätzen verbessert die aus Attribution AI gewonnenen Erkenntnisse und liefert klarere Ergebnisse, die einfach zu interpretieren sind. |

Weitere Informationen zu Attribution AIS finden Sie im [Dokumentation zu Attribution AIS](../../intelligent-services/attribution-ai/overview.md).

### Customer AI {#customer-ai}

In Real-time Customer Data Platform verfügbare Customer AI wird verwendet, um benutzerdefinierte Tendenzwerte wie Abwanderung und Konversion für einzelne Profile in großem Maßstab zu generieren. Dies wird erreicht, ohne dass die Geschäftsanforderungen in ein Problem des maschinellen Lernens umgewandelt werden müssen bzw. ein Algorithmus ausgewählt, trainiert oder bereitgestellt werden muss.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
|-----------|-------------|
| Unterstützung für mehrere Datensätze | Customer AI kann jetzt mühelos mehrere Datensätze direkt in der Benutzeroberfläche erfassen, ohne dass jeder Datensatz zugeordnet und zugeordnet werden muss. Diese neue zeitsparende Funktion bietet leistungsfähigere und genauere Ergebnisse mit umfangreicheren Daten aus mehreren Datensätzen. |
| Benutzerdefinierte Profilattribute | Customer AI unterstützt jetzt die Definition benutzerdefinierter Profildatensatzfelder (mit Zeitstempeln) in Ihren Daten zusätzlich zu standardmäßigen Ereignisfeldern. Mit dieser Option können Sie zusätzliche Profilattribute hinzufügen, die Sie als einflussreich erachten, was die Qualität Ihres Modells verbessern und genauere Ergebnisse liefern kann. |

Weitere Informationen zu Customer AI finden Sie im [Dokumentation zu Customer AI](../../intelligent-services/customer-ai/overview.md).

