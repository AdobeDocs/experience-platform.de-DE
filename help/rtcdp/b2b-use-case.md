---
keywords: RTCDP; CDP; Real-time Customer Data Platform; Echtzeit-Kundendatenplattform; Echtzeit-CDP; cdp; rtcdp
title: Anwendungsbeispiel für Real-time Customer Data Platform B2B Edition
description: Dieses Beispielszenario bietet ein Beispiel für die Konfiguration Ihrer Implementierung von Real-time Customer Data Platform B2B Edition.
exl-id: 15505980-ac33-44b2-8989-c08cbabd212b
source-git-commit: 4ebc3ef813c3c44aa2b8a7aab5ccabbcc3c332b2
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 1%

---

# Anwendungsbeispiel für Real-time Customer Data Platform B2B Edition

>[!IMPORTANT]
>
>Die Echtzeit-CDP Business to Business Edition befindet sich derzeit in der Betaphase. Die Dokumentation und Funktionalität können sich ändern.

Real-time Customer Data Platform B2B Edition erweitert die bestehenden Angebote der Echtzeit-Kundendatenplattform und Adobe Experience Platform, um B2B-Daten und -Workflows zu unterstützen. In diesem Dokument wird ein Anwendungsbeispiel vorgestellt, in dem die zusätzlichen Vorteile der B2B Edition veranschaulicht werden. Dazu gehören:

- Kombinieren Sie Personen- und Kontodaten aus verschiedenen silodierten Datenquellen, um eine umfassende Ansicht zu erhalten, die ein besseres Verständnis der Kunden und eine präzisere Segmentierung ermöglicht. Weitere Informationen finden Sie in der Dokumentation zu [Erstellen von XDM-Schemabeziehungen](./schemas/b2b.md) zur Verwendung mit unterschiedlichen B2B-Quellen .
- Segmentieren einer Zielgruppe basierend auf Attributen verwandter Entitäten. Dazu gehören Konten, Chancen, Kampagnen und Marketinglisten. Segmente sind nicht mehr nur auf Personen- und Erlebnisereignisse beschränkt. Weitere Beispiele zum Erstellen von B2B-spezifischen Zielgruppen finden Sie in der [Dokumentation zur B2B-Segmentierung](./segmentation/b2b.md) .
- Nativ unterstützen den Anwendungsfall einer Person, die mit mehreren Konten in Verbindung steht.

## Anwendungsfall

Bodea, ein Technologieunternehmen, verfügt über ein neues Produkt und möchte gleichzeitig Kunden mit einer E-Mail- und einer LinkedIn-Werbekampagne ansprechen. Um die Effizienz ihrer Marketingkampagne zu maximieren, möchte Bodea auch die Personen ansprechen, die mit diesem bestehenden Konto verbunden sind, die zuvor über eine Million Dollar für seine Produkte ausgegeben haben UND die die neue Produktseite im letzten Monat besucht haben.

Bodea hat jedoch zwei unterschiedliche Geschäftsfelder. Bodeas erster Geschäftszweig &quot;Line 1&quot; schafft Software für die Automobilindustrie. Der zweite Geschäftsbereich &quot;Line 2&quot;verkauft 3D-Drucker, die Automobilteile herstellen. Aufgrund der beiden Geschäftsbereiche von Bodea werden die Umsatzdaten, die aus den Kundenkonten von Bodea generiert werden, nicht in einer einzigen Ansicht vereinheitlicht.

Jeder Geschäftsbereich verfügt über ein eigenes Vertriebssystem: &quot;CRM 1&quot; und &quot;CRM 2&quot;. Beide CRM-Vertriebssysteme sind mit ihrer eigenen Marketing-Automatisierungsplattform &quot;Marketo 1&quot; und &quot;Marketo 2&quot; verbunden. Daten aus CRM 1 werden nur in Marketo 1 synchronisiert und Daten aus CRM2 werden nur in Marketo 2 synchronisiert. Letztlich werden ihre Daten in verschiedenen Informationsilos des Unternehmens verwaltet.

<!-- ![lines of business diagram](./assets/lines-of-business.png) -->

## Aktuelle Datenlage

Da beide Geschäftsbereiche von Bodea an das Unternehmen Townsend verkaufen, werden die Geschäftsdaten von Townsend in jedem Verkaufssystem als zwei getrennte Konten erfasst.

In Marketo 1 wird Townsend als Konto 1 aufgezeichnet. Es hat zwei verwandte Personen (p1@townsend.com und p2@townsend.com) und eine geschlossene Chance von 200.000 $ (&quot;Chancen 1&quot;) in CRM 1. Diese Daten werden aus CRM 1 in Marketo 1 synchronisiert.

In Marketo 2 wird Townsend als Konto 2 aufgezeichnet. Konto 2 hat auch zwei verwandte Personen (p2@townsend.com und p3@townsend.com) und eine geschlossene Chance von 900.000 $ (&quot;Chancen 2&quot;) in CRM 2. Diese Daten werden aus CRM 2 mit Marketo 2 synchronisiert.

Für Integrationszwecke und zusätzliche Zwecke der Unternehmenssteuerung verfügt Bodea auch über ein Übergeordnetes Daten-Management-System (MDM), in dem es einen Datensatz unterhält, der angibt, dass es sich bei Konto 1 in Marketo 1 (und CRM 1) und Konto 2 in Marketo 2 (und CRM 2) um dasselbe Unternehmen handelt.

Im letzten Monat hat `p2@townsend.com` die neue Produktseite besucht und der Webbesuch wurde von Marketo 1 aufgezeichnet.

![Konto-Info-Diagramm](./assets/account-info.png)

## Das Problem

Line 1 hat soeben ein neues Softwareprodukt veröffentlicht und möchte es an Bodeas bestehenden erstklassigen Kundenstamm weiterverkaufen. Bodea startet eine Marketing-Kampagne mit dieser bestimmten Zielgruppe.

Da die relevanten Informationen zu Townsend als Konto 1 in Marketo 1 und Konto 2 in Marketo 2 aufgezeichnet werden, kann das Marketing-Team von Bodea die silodierten Informationen nicht effizient nutzen.

Dadurch wird es dem Marketing-Team von Bodea untersagt, mit dieser neuen Möglichkeit auf effiziente Weise spezifische Geschäftskontakte bei diesen Unternehmen auszurichten.

Bis heute hat Townsend über eine Million Dollar kumulativ für Bodea-Produkte auf allen Konten ausgegeben. Ein Segment, das mit seinem alten System erstellt wurde, würde jedoch niemanden aus Townsend einschließen, es sei denn, die in einem einzigen Verkaufssystem insgesamt aufgewendeten Mittel beliefen sich auf mehr als 1 Million Dollar. Dies liegt daran, dass die Umsatzdaten in Konten unter verschiedenen Verkaufssystemen siloliert werden.

Da die Ausgaben von Townsend auf verschiedene Vertriebssysteme aufgeteilt sind und nicht mehr als eine Million pro Person ausmachen, würde das Segment niemanden finden, der sich für Marketo 1 oder Marketo 2 qualifiziert hat.

### Wie die Echtzeit-CDP B2B Edition das Problem löst

Mit der Echtzeit-Kundendatenplattform B2B Edition kann das Marketing-Team von Bodea:

- Kombinieren Sie die Daten aus allen unterschiedlichen Quellen (mehrere Marketo- und CRM-Instanzen und das Übergeordnete Data Management) in der Echtzeit-Kundendatenplattform B2B Edition.

Mit RT-CDP B2B Edition kann Bodea den Marketo Engage Source Connector verwenden, um B2B-Daten aus Marketo 1 und Marketo 2 in Experience Platform zu bringen und diese Daten mithilfe Platform-verbundener Anwendungen auf dem neuesten Stand zu halten. Weitere Informationen finden Sie in der Dokumentation zum Marketo-Quell-Connector](../sources/connectors/adobe-applications/marketo/marketo.md) .[

B2B-Daten (Personen, Konten, Chancen und Aktivitäten ) aus CRM1 werden in Marketo 1 synchronisiert. Ebenso werden alle B2B-Daten aus CRM 2 in Marketo 2 synchronisiert. Sie werden über den Marketo-Quell-Connector mit Adobe Experience Platform synchronisiert. Wenn Bodea jedoch zusätzliche Daten aus einem CRM in die Experience Platform einbringen möchte, kann es vorhandene CRM-Connectoren verwenden.

Aus Gründen der Einfachheit und des Zwecks dieses Beispiels werden Personen anhand ihrer E-Mails identifiziert. Die kombinierten Kontodaten für dieses Beispiel sehen wie folgt aus:

| People |
|---|
| p1@townsend.com |
| p2@townsend.com (wer die neue Produktseite im letzten Monat besucht hat) |
| p3@townsend.com |

| Chancen (geschlossen-gewonnen) |
|---|
| Chancen 1, 200.000 $ |
| Chancen 2, 900.000 $ |

- Erstellen Sie eindeutige Segmente mit diesen aggregierten Daten für verschiedene Marketinginitiativen. In diesem Beispiel findet das Segment alle Personen, die:

   - Verknüpfte Möglichkeiten (für alle Konten) über einen Wert von 1 Million Dollar verfügen
   - UND
   - Sie haben die Produktseite im letzten Monat besucht

- Erstellen Sie eine Zielgruppe, die die effizientesten Empfänger der neuen Marketing-Kampagne von Bodea sind. In diesem Beispiel hilft RT-CDP, B2B Edition dem Marketingspezialisten, `p2@townsend.com` als das richtige Ziel für diese Marketing-Kampagne zu identifizieren.

Durch die Verwendung der Marketo Engage- und LinkedIn-Ziele verfügt Bodea über eine End-to-End-Lösung für das Customer Experience Management (CXM) für sein Marketing-Team. Die in Experience Platform erstellte Zielgruppe wird an das Marketo-Ziel gesendet, wo sie als statische Liste angezeigt wird. Diese Audience wird dann automatisch zu einer Marketo-Marketing-Kampagne hinzugefügt. Gleichzeitig kann die Audience auch von der RT-CDP B2B Edition an eine LinkedIn-Marketing-Kampagne gesendet werden.

## Nächste Schritte

Durch die Lektüre dieses Dokuments haben Sie sich nun mit den Zieltypen und Problemen vertraut gemacht, die mit der Echtzeit-CDP B2B Edition gelöst werden können.

Die folgende Dokumentation wird empfohlen, um Ihr Verständnis der B2B-spezifischen Funktionen zu verbessern:

<!-- PLACEHOLDER Link to B2B tutorial required  -->
- [Quellen in Real-time Customer Data Platform B2B Edition](./sources/b2b.md)
- [Schemata in Real-time Customer Data Platform B2B Edition](./schemas/b2b.md)
- [Beispiele für B2B-Segmentierung](./segmentation/b2b.md)
- [Übersicht über Kontoprofile](./accounts/account-profile-overview.md)
- [Ziele in Real-time Customer Data Platform B2B Edition](./destinations/b2b.md)
- [LinkedIn Matched Audiences-Ziel konfigurieren](../destinations/catalog/social/linkedin.md)
