---
keywords: RTCDP;CDP;B2B Edition;Real-time Customer Data Platform;Echtzeit-Kundendatenplattform;Real-time CDP;b2b;cdp;Kunden-KI
title: Real-time CDP B2B Edition– Überblick
seo-title: Real-time Customer Data Platform B2B Edition overview
description: Überblick über das Konto von Real-time Customer Data Platform B2B Edition
seo-description: Overview of Real-time Customer Data Platform B2B Edition Account
exl-id: 9b45bba4-fc46-4d69-b36a-5cb91f316612
source-git-commit: 6b582683483046efaf880e46e33d7f30a44a61bf
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 89%

---

# Überblick über Real-time Customer Data Platform B2B Edition

>[!IMPORTANT]
>
>Real-time Customer Data Platform B2B Edition befindet sich derzeit im Beta-Stadium. Die Dokumentation und Funktionalität können sich ändern.

Real-time Customer Data Platform B2B Edition basiert auf Real-time Customer Data Platform (Real-time CDP) und wurde speziell für Marketing-Experten entwickelt, die in einem Business-to-Business-Service-Modell arbeiten. Es führt Daten aus verschiedenen Quellen zusammen und kombiniert sie zu einer einzigen Ansicht von Personen und Account-Profilen. Diese vereinheitlichten Daten ermöglichen es Marketing-Experten, bestimmte Zielgruppen präzise anzusprechen und über alle verfügbaren Kanäle anzusprechen.

Es gibt Verbesserungen bei einer Reihe von Funktionen von Adobe Experience Platform, die Real-time Customer Data Platform B2B Edition von ihrem B2C-Pendant unterscheiden. Dazu gehören Verbesserungen am Experience-Datenmodell (XDM) für B2B-Anwendungsfälle, Upgrades für die Identitätsauflösung und Profilsegmentierung sowie ein maßgeschneiderter Connector und ein Ziel für [!DNL Marketo Engage]. Mit dem [!DNL Marketo]-Connector können B2B-Marken ihre branchenführenden B2B-Interaktionsdaten mit Verhaltensinformationen verknüpfen, um Leads zu pflegen und Maßnahmen für Account-basiertes Marketing zu verbessern.

Mit Real-time CDP B2B Edition können Sie:

* Daten aus verschiedenen Quellen in einer zentralen Ansicht kombinieren, um ganzheitliche Personen- und Account-Profile zu erstellen.
* All Ihre quellenübergreifenden Daten anreichern, segmentieren und aus einem zentralen Speicher von einheitlichen Account-Profilen exportieren.
* Ihre Daten mithilfe von Data-Governance-Tools verwalten, die bei jedem Schritt des Zentralisierungsprozesses zur Verfügung stehen, um sicherzustellen, dass Ihre Daten den gesetzlichen Vorschriften und Unternehmensrichtlinien entsprechen.

Ausführlichere Details zu den Verbesserungen in Real-time CDP B2B Edition sind in die folgenden Abschnitte unterteilt.

## XDM

Real-time Customer Data Platform B2B Edition bietet mehrere neue XDM-Schemaklassen, Feldgruppen und Beziehungstypen zur Erfassung und Strukturierung Ihrer Daten speziell für B2B-Zwecke. In der Übersicht über [XDM in Real-time CDP B2B Edition](./schemas/b2b.md) finden Sie eine Aufschlüsselung der einzelnen Verbesserungen.

Durch die Verwendung vorkonfigurierter B2B-Schemas können Sie Daten in einer standardisierten, umsetzbaren Struktur einbringen. Viele der neuen Schemaklassen entsprechen fast direkt denen, die in gängigen CRM-Systemen wie [!DNL Salesforce], [!DNL Microsoft Dynamics], [!DNL Marketo] und anderen B2B-Datenquellen zu finden sind. Mit Real-time Customer Data Platform B2B Edition können Sie Daten aus B2B-Quellen auf unkomplizierte Weise und mit leicht zu überprüfenden Ergebnissen in Platform einbringen.

Diese XDM-Erweiterungen ermöglichen eine bessere Aufnahme und Aktivierung von Daten über B2B-zentrierte Quellen und Ziele und verbessern die Datenvereinheitlichung und -präsentation für vielfältigere und flexiblere Anwendungsfälle.

## Identitätsauflösung

Nach der Definition von Schemas und der Aufnahme von Daten, die diesen Schemas entsprechen, identifizier Real-time Customer Data Platform B2B Edition Quelldatensätze, die reale Personen und Unternehmen repräsentieren, mithilfe eines leistungsstarken Echtzeit-Identitätsauflösungssystems.

Das Identitätsauflösungssystem bietet die folgenden Funktionen:

* Kombinierte B2B- und B2C-Personendatensätze
* Eine mehrstufige Account-Hierarchie
* Viele-zu-Viele-, Personen-zu-Account-Verbindungen
* Personen- und Account-Identitäten werden in Echtzeit aufgelöst

Das System zur Identitätsauflösung wurde erweitert, um eine vielseitigere Klassifizierung von Personen zu ermöglichen. Das System ermöglicht es, Personen sowohl als Geschäfts-Opportunities als auch als Kunden zu identifizieren.

Account-Datensätze, die vom Quell-CRM synchronisiert und über mehrere Pfade innerhalb des Systems verbunden sind, werden von Platform zusammengeführt. Das System fasst die Personen, die mit Opportunities in Verbindung stehen, und die als Kunden erfassten Personen zusammen, ist aber auch in der Lage, die Unterscheidung zwischen ihnen als Attribut zu erhalten, wenn sie identifizierbar sind.

Es werden übereinstimmende Identifikatoren verwendet, um Account-Datensätze aus verschiedenen Systemen miteinander zu verknüpfen und zusammenzuführen. Account-Hierarchien bleiben bei diesem Vorgang erhalten. Mithilfe von Unterscheidungsmerkmalen wird geprüft, ob eine Person mit einem Account verbunden ist oder nicht, und es besteht die Möglichkeit, sie bei Bedarf vom Account zu trennen.

## Profile und Segmentierung

Sobald Real-time CDP B2B Edition Daten aufgenommen und Identitäten in Bezug auf Personen, Unternehmen, Attribute und Verhaltensweisen aufgelöst hat, werden diese Daten zur Erstellung von Profilen verwendet. Diese Profile können dann in durchsuchbare Zielgruppen segmentiert werden, die dann für verschiedene Ziele aktiviert werden können.

Bei korrekter Implementierung verfolgt das System Personen anhand eindeutiger primärer Identifikatoren und nicht anhand von Attributen, die sich ändern können, wie z. B. E-Mail-Adressen. Das heißt, wenn jemand die Stelle wechselt, folgt ihm das System weiterhin. Die Person ist immer noch dieselbe Entität, sie wird aber mit einem neuen Account verbunden. Diese systemeigene Funktionalität bietet einen großartigen Vektor für die Ausweitung auf neue Accounts, da das System diese Personen als Individuen mit all ihren Eigenschaften und Verhaltensweisen verfolgt.

## B2B-Quellen

Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Mit der [!DNL Marketo]-Quelle können Sie B2B-Daten in Platform streamen und diese Daten mit Platform-verbundenen Programmen auf dem neuesten Stand halten. Dabei wird eine beliebige Anzahl von [!DNL Marketo]-Instanzen unterstützt (was für große Unternehmen mit mehreren Instanzen von Vorteil ist) und bringt sie in eine einzige IMS-Organisation ein, wo die Daten zusammengeführt werden.

>[!NOTE]
>
>Die [!DNL Marketo]-Quelle ist **nicht** erforderlich, um Real-time CDP B2B Edition zu verwenden.

Weitere Informationen zu Marketo und zur Einbindung von B2B-Daten in Platform finden Sie in der Dokumentation [Quellen in der Echtzeit-Kundendatenplattform B2B Edition](./sources/b2b.md) .

## B2B-Ziele

Experience Platform-Ziele wie Google, LinkedIn und Facebook sind verfügbar und werden von der Echtzeit-Kundendatenplattform B2B Edition vollständig unterstützt. Es gibt auch ein Marketo Engage-Ziel, das Segmentmitgliedsdaten aus Platform streamt und als Listen in Marketo verfügbar macht.

Für Unternehmen mit mehr als einem CRM-System bietet die Echtzeit-Kundendatenplattform B2B Edition die Möglichkeit, Ziel-Connectoren für separate Instanzen von Marketo oder CRM zu konfigurieren. Bei Bedarf können Sie Ziel-Connectoren für jede Instanz konfigurieren und Zielgruppen unabhängig voneinander an jede der CRM-Instanzen senden.

## Nächste Schritte

Jetzt, da Sie die Vorteile von Real-time CDP B2B Edition für Marketing-Experten und die Unterschiede zu Real-time CDP besser verstehen, können Sie mehr darüber erfahren, wie Sie diese Funktionen in Ihrer eigenen IMS-Organisation anwenden können.

Um zu verstehen, wie die B2B Edition der Echtzeit-Kundendatenplattform Ihr Business-to-Business-Service-Modell nutzen kann, lesen Sie den [Beispielanwendungsfall für die Echtzeit-Kundendatenplattform B2B Edition](./b2b-use-case.md). Alternativ können Sie auch die Dokumentation [Schemas in Real-time Customer Data Platform B2B Edition](./schemas/b2b.md) zu Rate ziehen, um eine genauere Anleitung zur Erstellung von Schemas und zur Definition von Beziehungen für wichtige B2B-Datenentitäten zu erhalten.
