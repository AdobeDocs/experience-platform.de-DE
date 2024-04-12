---
keywords: RTCDP;CDP;B2B Edition;Real-time Customer Data Platform;Echtzeit-Kundendatenplattform;Real-Time CDP;b2b;cdp;Kunden-KI
title: Übersicht über Real-Time CDP B2B Edition
description: Übersicht über das Konto in der B2B-Edition von Real-time Customer Data Platform
feature: Get Started, B2B
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 9b45bba4-fc46-4d69-b36a-5cb91f316612
source-git-commit: 2704184446f7945c744e7e2d2a8c3cda3fc12527
workflow-type: tm+mt
source-wordcount: '1050'
ht-degree: 98%

---

# Übersicht über Real-time Customer Data Platform B2B Edition

Real-Time CDP B2B Edition basiert auf Adobe Real-time Customer Data Platform (Real-Time CDP) und wurde speziell für Marketing-Experten und -Expertinnen mit einem Business-to-Business-Service-Modell entwickelt. Es führt Daten aus verschiedenen Quellen zusammen und kombiniert sie zu einer einzigen Ansicht von Personen und Account-Profilen. Diese vereinheitlichten Daten ermöglichen es Marketing-Experten, bestimmte Zielgruppen präzise anzusprechen und über alle verfügbaren Kanäle anzusprechen.

Es gibt Verbesserungen bei einer Reihe von Funktionen von Adobe Experience Platform, die Real-Time CDP B2B Edition vom B2C-Pendant unterscheiden. Dazu gehören Verbesserungen am Experience-Datenmodell (XDM) für B2B-Anwendungsfälle, Upgrades für die Identitätsauflösung und Profilsegmentierung sowie ein maßgeschneiderter Connector und ein Ziel für [!DNL Marketo Engage]. Mit dem [!DNL Marketo]-Connector können B2B-Marken ihre branchenführenden B2B-Interaktionsdaten mit Verhaltensinformationen verknüpfen, um Leads zu pflegen und Maßnahmen für Account-basiertes Marketing zu verbessern.

Mit Real-Time CDP B2B Edition können Sie:

* Daten aus verschiedenen Quellen in einer zentralen Ansicht kombinieren, um ganzheitliche Personen- und Account-Profile zu erstellen.
* All Ihre quellenübergreifenden Daten anreichern, segmentieren und aus einem zentralen Speicher von einheitlichen Account-Profilen exportieren.
* Ihre Daten mithilfe von Data-Governance-Tools verwalten, die bei jedem Schritt des Zentralisierungsprozesses zur Verfügung stehen, um sicherzustellen, dass Ihre Daten den gesetzlichen Vorschriften und Unternehmensrichtlinien entsprechen.

Ausführlichere Details zu den Verbesserungen in Real-Time CDP B2B Edition sind in die folgenden Abschnitte unterteilt.

## XDM

Real-Time CDP B2B Edition bietet mehrere neue XDM-Schemaklassen, Feldgruppen und Beziehungstypen zur Erfassung und Strukturierung Ihrer Daten, speziell für B2B-Zwecke. In der Übersicht über [XDM in Real-Time CDP B2B Edition](./schemas/b2b.md) finden Sie eine Aufschlüsselung der einzelnen Verbesserungen.

Durch die Verwendung vorkonfigurierter B2B-Schemata können Sie Daten in einer standardisierten, umsetzbaren Struktur einbringen. Viele der neuen Schemaklassen entsprechen fast direkt denen, die in gängigen CRM-Systemen wie [!DNL Salesforce], [!DNL Microsoft Dynamics], [!DNL Marketo] und anderen B2B-Datenquellen zu finden sind. Mit Real-Time CDP B2B Edition können Sie Daten aus B2B-Quellen auf unkomplizierte Weise und mit leicht zu überprüfenden Ergebnissen in Platform einbringen.

Diese XDM-Erweiterungen ermöglichen eine bessere Aufnahme und Aktivierung von Daten über B2B-zentrierte Quellen und Ziele und verbessern die Datenvereinheitlichung und -präsentation für vielfältigere und flexiblere Anwendungsfälle.

## Identitätsauflösung

Nach der Definition von Schemata und der Aufnahme von Daten, die diesen Schemata entsprechen, identifiziert Real-Time CDP B2B Edition mithilfe eines leistungsstarken Echtzeit-Identitätsauflösungssystems Quelldatensätze, die reale Personen und Unternehmen repräsentieren.

Das Identitätsauflösungssystem bietet die folgenden Funktionen:

* Kombinierte B2B- und B2C-Personendatensätze
* Eine mehrstufige Account-Hierarchie
* Viele-zu-Viele-, Personen-zu-Account-Verbindungen
* Personen- und Account-Identitäten werden in Echtzeit aufgelöst

Das System zur Identitätsauflösung wurde erweitert, um eine vielseitigere Classification von Personen zu ermöglichen. Das System ermöglicht es, Personen sowohl als Geschäfts-Opportunities als auch als Kunden zu identifizieren.

Account-Datensätze, die vom Quell-CRM synchronisiert und über mehrere Pfade innerhalb des Systems verbunden sind, werden von Platform zusammengeführt. Das System fasst die Personen, die mit Opportunities in Verbindung stehen, und die als Kunden erfassten Personen zusammen, ist aber auch in der Lage, die Unterscheidung zwischen ihnen als Attribut zu erhalten, wenn sie identifizierbar sind.

Es werden übereinstimmende Identifikatoren verwendet, um Account-Datensätze aus verschiedenen Systemen miteinander zu verknüpfen und zusammenzuführen. Account-Hierarchien bleiben bei diesem Vorgang erhalten. Mithilfe von Unterscheidungsmerkmalen wird geprüft, ob eine Person mit einem Account verbunden ist oder nicht, und es besteht die Möglichkeit, sie bei Bedarf vom Account zu trennen.

## Profile und Segmentierung

Sobald Real-Time CDP B2B Edition Daten aufgenommen und Identitäten in Bezug auf Personen, Unternehmen, Attribute und Verhaltensweisen aufgelöst hat, werden diese Daten zur Erstellung von Profilen verwendet. Diese Profile können dann in durchsuchbare Zielgruppen segmentiert werden, die dann für verschiedene Ziele aktiviert werden können.

Bei korrekter Implementierung verfolgt das System Personen anhand eindeutiger primärer Identifikatoren und nicht anhand von Attributen, die sich ändern können, wie z. B. E-Mail-Adressen. Das heißt, wenn jemand die Stelle wechselt, folgt ihm das System weiterhin. Die Person ist immer noch dieselbe Entität, sie wird aber mit einem neuen Account verbunden. Diese systemeigene Funktionalität bietet einen großartigen Vektor für die Ausweitung auf neue Accounts, da das System diese Personen als Individuen mit all ihren Eigenschaften und Verhaltensweisen verfolgt.

## B2B-Quellen

Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Mit der [!DNL Marketo]-Quelle können Sie B2B-Daten in Platform streamen und diese Daten mit Platform-verbundenen Programmen auf dem neuesten Stand halten. Dabei wird eine beliebige Anzahl von [!DNL Marketo]-Instanzen unterstützt (was für große Unternehmen mit mehreren Instanzen von Vorteil ist) und in eine einzige Organisation eingebracht, wo die Daten zusammengeführt werden.

>[!NOTE]
>
>Die [!DNL Marketo]-Quelle ist **nicht** erforderlich, um Real-Time CDP B2B Edition zu verwenden.

Weitere Informationen zu Marketo und der Einbindung von B2B-Daten in Platform finden Sie in der Dokumentation zu den [Quellen in Real-Time CDP B2B Edition](./sources/b2b.md).

## B2B-Ziele

Experience Platform-Ziele wie Google Customer Match, Facebook, LinkedIn, Marketo Engage, Amazon S3, Google Display &amp; Video 360, Google Ads und Google Ad Manager sind verfügbar und werden von Real-Time CDP B2B Edition vollständig unterstützt. Das Marketo Engage-Ziel streamt auch Segmentzugehörigkeitsdaten aus Platform und macht diese als Listen in Marketo verfügbar.

Weitere informationen finden Sie in der Übersicht zum [Marketo Engage-Ziel](../destinations/catalog/adobe/marketo-engage.md).

Für Unternehmen mit mehr als einem CRM bietet Real-Time CDP B2B Edition die Möglichkeit, Ziel-Connectoren zu separaten Instanzen von Marketo oder CRM zu konfigurieren. Bei Bedarf können Sie Ziel-Connectoren für jede Instanz konfigurieren und Zielgruppen unabhängig voneinander an jede der CRM-Instanzen senden.

## Nächste Schritte

Da Sie nun die Vorteile von Real-Time CDP B2B Edition für Marketing-Experten bzw. -Expertinnen und die Unterschiede zu Real-Time CDP besser verstehen, können Sie mehr darüber erfahren, wie Sie diese Funktionen in Ihrer eigenen Organisation anwenden können.

Um zu verstehen, wie Ihr Business-to-Business-Service-Modell von Real-Time CDP B2B Edition profitieren kann, lesen Sie die folgende Dokumentation, die Ihnen bei den ersten Schritten hilft:

* [Ein Anwendungsbeispiel für Real-Time CDP B2B Edition](./b2b-use-case.md)
* [Ein Tutorial mit der Beschreibung aller Schritte für Real-time Customer Data Platform B2B Edition](./b2b-tutorial.md)
* [So erfassen Sie Daten](./sources/b2b.md)
* [So rufen Sie Profile auf](./profile/profile-overview.md)
* [Schemata in Real-time Customer Data Platform B2B Edition](./schemas/b2b.md)
* [Erstellen von Zielgruppen](./segmentation/b2b.md)
* [So aktivieren Sie Zielgruppen für Ziele](./destinations/b2b.md)
* [So definieren und setzen Sie Data Governance-Richtlinien um](./privacy/data-governance-overview.md)
