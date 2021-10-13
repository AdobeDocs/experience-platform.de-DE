---
title: Übersicht über die Ereignisweiterleitung
description: Hier erfahren Sie mehr über Adobe Experience Platform, mit dessen Hilfe Sie über das Platform Edge-Netzwerk Aufgaben ausführen können, ohne dabei Ihre Tag-Implementierung zu ändern.
feature: Event Forwarding
exl-id: 18e76b9c-4fdd-4eff-a515-a681bc78d37b
source-git-commit: 5218e6cf82b74efbbbcf30495395a4fe2ad9fe14
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 100%

---

# Übersicht über die Ereignisweiterleitung

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Die Ereignisweiterleitung in Adobe Experience Platform reduziert das Gewicht von Web-Seiten und Programmen, indem das Adobe Experience Platform Edge-Netzwerk verwendet wird, um Aufgaben auszuführen, die normalerweise auf dem Client erledigt werden. Regeln für die Ereignisweiterleitung können Daten transformieren und an neue Ziele senden, ohne die Client-seitigen Implementierungen zu ändern.

Die Ereignisweiterleitung in Kombination mit den Web- und Mobile-SDKs von Adobe Experience Platform ermöglicht Folgendes:

* Führen Sie einen einzelnen Aufruf von der Seite aus, die eine Payload von Daten enthält. Die Daten werden dann Server-seitig verbunden, um den Client-seitigen Netzwerk-Traffic zu reduzieren und Kunden ein schnelleres Erlebnis zu bieten.
* Verringern Sie die Ladezeit von Webseiten, sodass Ihre Site den Best Practices der Branche bezüglich der Leistung entspricht.
* Erhöhen Sie die Transparenz und Kontrolle darüber, welche Datentypen wohin gesendet werden, über alle Tag-Eigenschaften hinweg.
* Erstellen Sie eine Regel für die Ereignisweiterleitung, um zuvor verfolgte Daten an ein neues Ziel zu senden.

## Verbesserte Leistung

In einer zunehmend wettbewerbsorientierten Umgebung müssen Unternehmen der Leistung Vorrang einräumen, um ihren Marktanteil zu halten und zu vergrößern. Die Ereignisweiterleitung verbessert die Leistung von Websites und Programmen auf Mobil-, IoT- und OTT-Geräten. Konversionsraten von Websites können aufgrund der schnelleren Ladezeit steigen, mobile Anwendungen entleeren den Akku nicht so schnell, und OTT-Anwendungen fühlen sich genauso reaktionsschnell an wie die gleichen Anwendungen, die auf mobilen Geräten laufen. Mit steigender Leistung steigt häufig auch die Konversionsrate.

## Bessere Data Governance

In dem Maße, wie sich die Technologie entwickelt und Daten an immer mehr Ziele gesendet werden, wird es immer schwieriger, zu kontrollieren, welche Daten wohin gesendet werden. Die Normalisierung von Regelungen wie DSGVO und CCPA zwingt Firmen, mehr Kontrolle über eine Herausforderung in Bezug auf Daten auszuüben, die immer schwieriger wird.

Die Ereignisweiterleitung hilft Marketing-Teams, ihr Geschäft auszubauen und gleichzeitig Daten zu kontrollieren. Dadurch wird die Menge der Client-seitigen Technologien verringert, die Marketing-Experten zum Erreichen ihres Zielmarkts und zum Senden von Daten an andere Zielorte als Adobe benötigen. Dies erleichtert Implementierungs-Teams die Verwaltung der Daten, die vom Client an verschiedene Ziele gesendet werden.

## Unterschiede zwischen Ereignisweiterleitung und Tags

Beachten Sie die folgenden Unterschiede zwischen Ereignisweiterleitung und Tags:

* Tokenisierung von Datenelementen

   * Tags: In einer Regel werden Datenelemente am Anfang und am Ende des Datenelementnamens mit einem `%`-Token versehen. Beispiel: `%viewportHeight%`.

   * Ereignisweiterleitung: In einer Regel werden Datenelemente mit einem `{{`-Token am Anfang und einem `}}`-Token am Ende des Datenelementnamens versehen. Beispiel: `{{viewportHeight}}`.

* Wie Daten referenziert werden

   Um Daten aus dem Edge-Netzwerk zu referenzieren, muss der Datenelementpfad `arc.event._<element>_` sein.

   `arc` steht für Adobe Response Context.

   Beispiel: `arc.event.xdm.web.webPageDetails.URL`

   >[!IMPORTANT]
   >
   >Wenn dieser Pfad falsch angegeben ist, werden keine Daten erfasst.


* Sequenz von Regelaktionen

   Im Aktionsabschnitt einer Regel werden Regeln zur Ereignisweiterleitung immer nacheinander ausgeführt. Stellen Sie beim Speichern einer Regel sicher, dass die Reihenfolge der Aktionen korrekt ist. Diese Ausführungssequenz kann nicht so gewählt werden, wie es mit Tags möglich ist.

* JavaScript-Versionen mit benutzerdefiniertem Code

   Tags verwenden die JavaScript-Version es5. Die Ereignisweiterleitung verwendet Version es6.

<!--doc Adobe Cloud Connector extension, get from Jon-->
