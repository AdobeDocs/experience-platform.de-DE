---
keywords: RTCDP;CDP;B2B Edition;Real-time Customer Data Platform;Echtzeit-Kundendatenplattform;Echtzeit-Kundendatenplattform;b2b;cdp;Customer AI
title: Übersicht über die Echtzeit-Kundendatenplattform B2B Edition
seo-title: Real-time Customer Data Platform B2B Edition overview
description: Übersicht über das Real-time Customer Data Platform B2B Edition-Konto
seo-description: Overview of Real-time Customer Data Platform B2B Edition Account
exl-id: 9b45bba4-fc46-4d69-b36a-5cb91f316612
source-git-commit: 6b582683483046efaf880e46e33d7f30a44a61bf
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 3%

---

# Übersicht über Real-time Customer Data Platform B2B Edition

>[!IMPORTANT]
>
>Die Echtzeit-CDP B2B Edition befindet sich derzeit in der Betaphase. Die Dokumentation und Funktionalität können sich ändern.

Die auf Real-time Customer Data Platform (Echtzeit-Kundendatenplattform) aufbauende Echtzeit-Kundendatenplattform B2B Edition ist speziell für Marketing-Experten konzipiert, die in einem Business-to-Business-Servicemodell arbeiten. Es führt Daten aus mehreren Quellen zusammen und kombiniert sie in einer einzigen Ansicht von Personen und Kontoprofilen. Diese einheitlichen Daten ermöglichen es Marketingexperten, spezifische Zielgruppen präzise anzusprechen und diese Zielgruppen über alle verfügbaren Kanäle hinweg zu erreichen.

Es gibt Verbesserungen an einer Vielzahl von Adobe Experience Platform-Funktionen, die die Echtzeit-Kundendatenplattform B2B Edition von ihrem B2C-Gegenstück unterscheiden. Dazu gehören Verbesserungen am Experience-Datenmodell (XDM) für B2B-Anwendungsfälle, Upgrades zur Identitätsauflösung und Profilsegmentierung sowie ein benutzerdefinierter Connector und ein Ziel für [!DNL Marketo Engage]. Der Connector [!DNL Marketo] ermöglicht es B2B-Marken, ihre branchenführenden B2B-Interaktionsdaten mit Verhaltensinformationen zu verbinden, um Leads zu fördern und kontobasierte Marketingoperationen zu verbessern.

Mit der Echtzeit-CDP B2B Edition können Sie:

* Kombinieren von Daten, die aus mehreren Quellen gesammelt wurden, in einer Ansicht, um ganzheitliche Personen und Kontoprofile zu erstellen.
* Anreichern, Segmentieren und Exportieren aller Quelldaten aus einem zentralen Speicher mit einheitlichen Kontoprofilen.
* Verwalten Sie Ihre Daten mithilfe von Data Governance-Tools, die in jedem Schritt des Zentralisierungsprozesses verfügbar sind, um sicherzustellen, dass Ihre Daten den gesetzlichen Vorschriften und Geschäftsrichtlinien entsprechen.

Umfassendere Details zu den Verbesserungen für die Echtzeit-CDP B2B Edition sind in die folgenden Abschnitte unterteilt.

## XDM

Die Echtzeit-Kundendatenplattform B2B Edition bietet mehrere neue XDM-Schemaklasse, Feldgruppen und Beziehungstypen, um Ihre Daten speziell für B2B-Zwecke zu erfassen und zu strukturieren. Eine Aufschlüsselung dieser Verbesserungen finden Sie in der Übersicht zu [XDM in der Echtzeit-Kundendatenplattform B2B edition](./schemas/b2b.md) .

Durch die Verwendung vorkonfigurierter B2B-Schemata können Sie Daten in einer standardisierten, umsetzbaren Struktur einbringen. Viele der neuen Schemaklassen werden fast direkt auf die in Standard-CRMs aufgetretenen Schemaklassen zugeordnet, z. B. [!DNL Salesforce], [!DNL Microsoft Dynamics], [!DNL Marketo] und andere B2B-Datenquellen. Mit der Echtzeit-CDP B2B Edition können Sie Daten aus B2B-Quellen unkompliziert und mit leicht zu prüfenden Ergebnissen in Platform einbringen.

Diese XDM-Erweiterungen ermöglichen es Ihnen, Daten besser über B2B-orientierte Quellen und Ziele zu erfassen und zu aktivieren und so die Vereinheitlichung und Präsentation von Daten für verschiedene und flexiblere Anwendungsfälle zu verbessern.

## Identitätsauflösung

Nachdem Schemas definiert und Daten gemäß diesen Schemas erfasst wurden, identifiziert die Echtzeit-Kundendatenplattform B2B Edition Quelldatensätze, die über ein leistungsstarkes Echtzeit-Identitätsauflösungssystem Personen und Unternehmen in der realen Welt repräsentieren.

Das Identitätsauflösungssystem bietet die folgenden Funktionen:

* Datensätze zu kombinierten B2B- und B2C-Personen
* Eine mehrstufige Kontohierarchie
* Viele-zu-viele-Verbindungen von Mensch zu Konto
* Personen und Kontoidentitäten werden in Echtzeit aufgelöst

Das System zur Identitätsauflösung wurde erweitert, um eine facettenreichere Klassifizierung von Personen zu unterstützen. Das System ermöglicht es, Personen als Leads in Geschäftsmöglichkeiten sowie Kunden zu identifizieren.

Vom Quell-CRM synchronisierte und über mehrere Pfade im System verbundene Kontodatensätze werden von Platform zusammengeführt. Das System führt die Personen zusammen, die mit Geschäftschancen verbunden sind und die als Kunden erfasst werden, kann aber auch die Unterscheidung zwischen ihnen als Attribut beibehalten, wenn sie identifizierbar sind.

Übereinstimmende Kennungen werden verwendet, um Kontodatensätze über mehrere Systeme hinweg zu verknüpfen und zusammenzuführen. Kontohierarchien bleiben während dieses Prozesses erhalten. Mithilfe von Differenzatoren wird geprüft, ob eine Person mit einem Konto verknüpft ist oder nicht, und es wird die Möglichkeit geboten, sie bei Bedarf vom Konto zu trennen.

## Profile und Segmentierung

Sobald die Echtzeit-Kundendatenplattform B2B Edition Daten und aufgelöste Identitäten im Zusammenhang mit Personen, Unternehmen, Attributen und Verhaltensweisen erfasst hat, werden diese Daten zur Erstellung von Profilen verwendet. Diese Profile können dann in Browser-fähige Zielgruppen segmentiert werden, die dann für verschiedene Ziele aktiviert werden können.

Bei ordnungsgemäßer Implementierung verfolgt das System Personen anhand eindeutiger primärer Kennungen und nicht anhand von Attributen, die sich ändern können, z. B. E-Mail-Adressen. Das bedeutet, dass das System bei einer Änderung von Aufträgen diese immer noch befolgt. Die Person ist immer noch dieselbe Entität, sondern ist stattdessen mit einem neuen Konto verknüpft. Diese native Funktionalität bietet einen großartigen Vektor für die Erweiterung in neue Konten, da das System diesen Personen als Einzelpersonen folgt, einschließlich all ihrer Attribute und Verhaltensweisen.

## B2B-Quellen

 Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Mit der Quelle [!DNL Marketo] können Sie B2B-Daten in Platform streamen und mithilfe von Anwendungen, die mit Platform verbunden sind, auf dem neuesten Stand halten. Es unterstützt eine beliebige Anzahl von Instanzen von [!DNL Marketo] (was für große Unternehmen mit mehreren Instanzen von Vorteil ist) und ruft eine IMS-Organisation ab, in der die Daten zusammengeführt werden.

>[!NOTE]
>
>Die [!DNL Marketo]-Quelle ist **nicht** erforderlich, um die Echtzeit-CDP B2B Edition zu verwenden.

Weitere Informationen zu Marketo und zur Einbindung von B2B-Daten in Platform finden Sie in der Dokumentation [Quellen in der Echtzeit-Kundendatenplattform B2B Edition](./sources/b2b.md) .

## B2B-Ziele

Experience Platform-Ziele wie Google, LinkedIn und Facebook sind verfügbar und werden von der Echtzeit-Kundendatenplattform B2B Edition vollständig unterstützt. Es gibt auch ein Marketo Engage-Ziel, das Segmentmitgliedsdaten aus Platform streamt und als Listen in Marketo verfügbar macht.

Für Unternehmen mit mehr als einem CRM-System bietet die Echtzeit-Kundendatenplattform B2B Edition die Möglichkeit, Ziel-Connectoren für separate Instanzen von Marketo oder CRM zu konfigurieren. Bei Bedarf können Sie Ziel-Connectoren für jede Instanz konfigurieren und Zielgruppen unabhängig an jede der CRM-Instanzen senden.

## Nächste Schritte

Jetzt, da Sie die Vorteile für Marketing-Experten, die die Echtzeit-Kundendatenplattform B2B Edition bietet, und die Unterschiede zwischen ihr und der Echtzeit-Kundendatenplattform besser verstehen, können Sie mehr darüber erfahren, wie Sie diese Funktionen auf Ihre eigene IMS-Organisation anwenden.

Um zu verstehen, wie die B2B Edition der Echtzeit-Kundendatenplattform Ihr Business-to-Business-Service-Modell nutzen kann, lesen Sie den [Beispielanwendungsfall für die Echtzeit-Kundendatenplattform B2B Edition](./b2b-use-case.md). Alternativ können Sie in der Dokumentation [Schemas in Real-time Customer Data Platform B2B Edition](./schemas/b2b.md) genauere Anleitungen zum Erstellen von Schemas und zum Definieren von Beziehungen für wichtige B2B-Datenentitäten finden.
