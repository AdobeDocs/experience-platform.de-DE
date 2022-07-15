---
keywords: RTCDP;CDP;Real-time Customer Data Platform;Real time Customer Data Platform;Echtzeit-Kundendatenplattform;Real-time CDP;cdp;rtcdp
title: Beispiel für einen Anwendungsfall von Real-time Customer Data Platform B2B Edition
description: Dieses Beispielszenario bietet ein Beispiel für die Konfiguration Ihrer Implementierung von Real-time Customer Data Platform B2B Edition.
exl-id: 15505980-ac33-44b2-8989-c08cbabd212b
source-git-commit: e6f71954d52e0a998955c3420307417cc011c24d
workflow-type: tm+mt
source-wordcount: '1134'
ht-degree: 100%

---

# Beispiel für einen Anwendungsfall von Real-time Customer Data Platform B2B Edition

Real-time Customer Data Platform B2B Edition fügt zum schon bestehenden Angebot von Real-time CDP und Adobe Experience Platform die Unterstützung von B2B-Daten und -Workflows hinzu. Dieses Dokument enthält ein Beispiel für einen Anwendungsfall, der die zusätzlichen Vorteile von B2B Edition verdeutlicht. Dazu gehören:

- Kombinieren Sie Personen- und Account-Daten aus verschiedenen isolierten Datenquellen, um eine umfassende Übersicht zu erhalten, die ein besseres Verständnis der Kunden und eine genauere Segmentierung ermöglicht. Weitere Informationen finden Sie in der Dokumentation zur [Erstellung von XDM-Schema-Beziehungen](./schemas/b2b.md) zur Verwendung mit verschiedenen B2B-Quellen.
- Segmentieren Sie eine Zielgruppe anhand von Attributen verwandter Entitäten. Dazu gehören Accounts, Opportunities, Kampagnen und Marketing-Listen. Segmente sind nicht mehr nur auf Personenattribute und Erlebnisereignisse beschränkt. In der [Dokumentation zur B2B-Segmentierung](./segmentation/b2b.md) finden Sie weitere Beispiele für die Erstellung von B2B-spezifischen Zielgruppen.
- Native Unterstützung für den Anwendungsfall, dass eine Person mit mehreren Accounts verbunden ist.

## Anwendungsfall

Bodea, ein Technologieunternehmen, hat ein neues Produkt und möchte gleichzeitig mit einer E-Mail- und einer LinkedIn-Werbekampagne Kunden ansprechen. Um die Effizienz der Marketing-Kampagne zu maximieren, möchte Bodea auch die Personen ansprechen, die mit diesem bestehenden Account verbunden sind, die zuvor mehr als eine Million Dollar für seine Produkte ausgegeben haben UND die neue Produktseite im letzten Monat besucht haben.

Bodea hat jedoch zwei verschiedene Geschäftssparten. Bodeas erste Geschäftssparte, „Sparte 1“, entwickelt Software für die Automobilbranche. Die zweite Geschäftssparte, „Sparte 2“, verkauft 3D-Drucker für die Herstellung von Autoteilen. Aufgrund der beiden Geschäftssparten von Bodea werden die von den Accounts von Bodea generierten Umsatzdaten nicht in einer zentralen Ansicht zusammengeführt.

Jede Sparte hat ihr eigenes Vertriebssystem: „CRM 1“ und „CRM 2“. Beide CRM-Vertriebssysteme sind mit ihrer eigenen Marketing-Automatisierungsplattform, „Marketo 1“ und „Marketo 2“, verbunden. Daten aus CRM 1 werden nur mit Marketo 1 synchronisiert und Daten aus CRM 2 werden nur mit Marketo 2 synchronisiert. Letztlich werden die Daten in verschiedenen Informationssilos des Unternehmens verwaltet.

## Aktuelle Datenlage

Da beide Geschäftssparten von Bodea an die Firma Townsend verkaufen, werden die Geschäftsdaten von Townsend in jedem Verkaufssystem als zwei getrennte Accounts erfasst.

In Marketo 1 wird Townsend als „Account 1“ erfasst. Es gibt hier zwei verbundene Personen (p1@townsend.com und p2@townsend.com) und eine abgeschlossene Opportunity von 200.000 $ („Opportunity 1“) in CRM 1. Diese Daten werden von CRM 1 mit Marketo 1 synchronisiert.

In Marketo 2 wird Townsend als „Account 2“ erfasst. Account 2 hat auch zwei verbundene Personen (p2@townsend.com und p3@townsend.com) und eine abgeschlossene Opportunity von 900.000 $ („Opportunity 2“) in CRM 2. Diese Daten werden von CRM 2 mit Marketo 2 synchronisiert.

Zur Integration und für zusätzliche Kontrollzwecke verfügt Bodea auch über ein Master-Data-Management-System (MDM), in dem ein Datensatz geführt wird, der angibt, dass Account 1 in Marketo 1 (und CRM 1) und Account 2 in Marketo 2 (und CRM 2) dasselbe Unternehmen sind.

Im letzten Monat hat `p2@townsend.com` die neue Produktseite besucht und dieser Web-Besuch wurde von Marketo 1 aufgezeichnet.

![Account-Informationsdiagramm](./assets/account-info.png)

## Das Problem

Sparte 1 hat gerade ein neues Software-Produkt auf den Markt gebracht und möchte es dem bestehenden Kundenstamm von Bodea als Upsell anbieten. Bodea startet eine Marketing-Kampagne, die genau auf diese Zielgruppe ausgerichtet ist.

Da die relevanten Townsend-Informationen in Marketo 1 als Account 1 und in Marketo 2 als Account 2 gespeichert sind, kann das Marketing-Team von Bodea die Informationen in den beiden Silos nicht effizient nutzen.

Dies hindert das Marketing-Team von Bodea daran, bestimmte Geschäftskontakte in diesen Unternehmen mit dieser neuen Möglichkeit effizient anzusprechen.

Bis heute hat Townsend über sämtliche Accounts insgesamt mehr als eine Million Dollar für Bodea-Produkte ausgegeben. Ein mit dem alten System erstelltes Segment würde jedoch niemanden von Townsend einschließen, es sei denn, die Gesamtausgaben innerhalb eines einzigen Vertriebssystems beliefen sich auf mehr als 1 Million Dollar. Der Grund dafür ist, dass die Umsatzdaten in den Accounts der verschiedenen Vertriebssysteme getrennt sind.

Da die Ausgaben von Townsend auf verschiedene Vertriebssysteme aufgeteilt sind und einzeln nicht mehr als eine Million betragen, würde das Segment weder in Marketo 1 noch in Marketo 2 jemanden finden, der qualifiziert ist.

### Wie Real-time CDP B2B Edition das Problem löst

Mit Real-time CDP B2B Edition kann das Marketing-Team von Bodea:

- Die Daten aus allen getrennten Quellen (mehrere Marketo- und CRM-Instanzen und Master Data Management) in Real-time Customer Data Platform B2B Edition kombinieren.

Mit Real-time Customer Data Platform B2B Edition kann Bodea den Marketo Engage-Quell-Connector nutzen, um B2B-Daten aus Marketo 1 und Marketo 2 in Experience Platform zu bringen und diese Daten mithilfe von an Platform angeschlossenen Programmen aktuell zu halten. Weitere Informationen finden Sie in der Dokumentation zum [Marketo-Quell-Connector](../sources/connectors/adobe-applications/marketo/marketo.md).

B2B-Daten (Personen, Accounts, Opportunities und Aktivitäten) aus CRM 1 werden mit Marketo 1 synchronisiert. In ähnlicher Weise werden alle B2B-Daten aus CRM 2 mit Marketo 2 synchronisiert. Sie werden über den Marketo-Quell-Connector mit Adobe Experience Platform synchronisiert. Wenn Bodea jedoch zusätzliche Daten aus einem CRM in Experience Platform einbringen möchte, können bestehende CRM-Connectoren verwendet werden.

Der Einfachheit halber und für den Zweck dieses Beispiels werden die Personen anhand ihrer E-Mails identifiziert. Die kombinierten Kontodaten für dieses Beispiel sehen wie folgt aus:

| People |
|---|
| p1@townsend.com |
| p2@townsend.com (der im letzten Monat die neue Produktseite besucht hat) |
| p3@townsend.com |

| Opportunities (geschlossen-gewonnen) |
|---|
| Opportunity 1, 200.000 Dollar |
| Opportunity 2, 900.000 Dollar |

- Erstellen Sie anhand dieser aggregierten Daten einzigartige Segmente für verschiedene Marketing-Initiativen. In diesem Beispiel findet das Segment alle Personen, die:

   - Verbundene Opportunities (für ALLE Accounts) mit einem Wert von über 1 Million Dollar haben
   - UND
   - Die Produktseite im letzten Monat besucht haben

- Schaffen Sie eine Zielgruppe, die die neue Marketing-Kampagne von Bodea am effizientesten aufnimmt. In diesem Beispiel hilft Real-time Customer Data Platform B2B Edition dem Marketing-Experten, `p2@townsend.com` als das richtige Ziel für diese Marketing-Kampagne zu identifizieren.

Durch den Einsatz von Marketo Engage und LinkedIn verfügt Bodea über eine End-to-End-Lösung für das Customer Experience Management (CXM) für sein Marketing-Team. Die in Experience Platform erstellte Zielgruppe wird an das Marketo-Ziel übertragen, wo sie als statische Liste erscheint. Diese Zielgruppe wird dann automatisch zu einer Marketo-Marketing-Kampagne hinzugefügt. Gleichzeitig kann die Zielgruppe auch über Real-time Customer Data Platform B2B Edition an eine Marketing-Kampagne auf LinkedIn weitergeleitet werden.

## Nächste Schritte

Durch die Lektüre dieses Dokuments haben Sie nun eine Einführung in die Arten von Zielen und Problemen erhalten, die mit Real-time Customer Data Platform B2B Edition gelöst werden können.

Zum besseren Verständnis der B2B-spezifischen Funktionen wird die folgende Dokumentation empfohlen:

- [Vollständiges Tutorial zu Real-time Customer Data Platform B2B Edition](./b2b-tutorial.md)
- [Quellen in Real-time Customer Data Platform B2B Edition](./sources/b2b.md)
- [Schemas in Real-time Customer Data Platform B2B Edition](./schemas/b2b.md)
- [Beispiele für B2B-Segmentierung](./segmentation/b2b.md)
- [Übersicht über Account-Profile](./accounts/account-profile-overview.md)
- [Ziele in Real-time Customer Data Platform B2B Edition](./destinations/b2b.md)
- [Konfigurieren eines Ziels für abgeglichene LinkedIn-Zielgruppen](../destinations/catalog/social/linkedin.md)
