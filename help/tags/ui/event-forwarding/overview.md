---
title: Übersicht über die Ereignisweiterleitung
description: Erfahren Sie mehr über die Ereignisweiterleitung in Adobe Experience Platform, mit der Sie mit dem Platform Edge Network Aufgaben ausführen können, ohne die Tag-Implementierung zu ändern.
source-git-commit: 7a6bec77895458cf1735bc7a00d16b78df9776a5
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 42%

---

# Übersicht über die Ereignisweiterleitung

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Die Ereignisweiterleitung in Adobe Experience Platform verringert die Web- und App-Gewichtung, indem Adobe Experience Platform Edge Network verwendet wird, um Aufgaben auszuführen, die normalerweise auf dem Client ausgeführt werden. Mit Regeln für die Ereignisweiterleitung können Daten umgewandelt und an neue Ziele gesendet werden, ohne die clientseitigen Implementierungen zu ändern.

Die Ereignisweiterleitung in Kombination mit den Adobe Experience Platform Web- und Mobile-SDKs ermöglicht Folgendes:

* Führen Sie einen einzelnen Aufruf von der Seite aus, die eine Payload von Daten enthält. Die Daten werden dann Server-seitig verbunden, um den clientseitigen Netzwerk-Traffic zu reduzieren und Kunden ein schnelleres Erlebnis zu bieten.
* Verringern Sie die Ladezeit von Webseiten, sodass Ihre Site den Best Practices der Branche bezüglich der Leistung entspricht.
* Erhöhen Sie die Transparenz und Kontrolle darüber, welche Datentypen wohin über alle Tag-Eigenschaften gesendet werden.
* Erstellen Sie eine Ereignisweiterleitungsregel, um zuvor verfolgte Daten an ein neues Ziel zu senden.

## Verbesserte Leistung

In einer zunehmend wettbewerbsorientierten Umgebung müssen Unternehmen der Leistung Vorrang einräumen, um ihren Marktanteil zu halten und zu vergrößern. Die Ereignisweiterleitung verbessert die Leistung von Websites und Apps auf mobilen, IoT- und OTT-Geräten. Konversionsraten von Websites können aufgrund der schnelleren Ladezeit steigen, mobile Anwendungen entleeren den Akku nicht so schnell, und OTT-Anwendungen fühlen sich genauso reaktionsschnell an wie die gleichen Anwendungen, die auf mobilen Geräten laufen. Mit steigender Leistung steigt häufig auch die Konversionsrate.

## Bessere Data Governance

In dem Maße, wie sich die Technologie entwickelt und Daten an immer mehr Ziele gesendet werden, wird es immer schwieriger, zu kontrollieren, welche Daten wohin gesendet werden. Die Normalisierung von Vorschriften wie DSGVO und CCPA zwingt Unternehmen, mehr Kontrolle über ein Datenproblem auszuüben, das immer schwieriger wird.

Die Ereignisweiterleitung hilft Marketingteams, ihr Geschäft auszubauen und gleichzeitig Daten zu kontrollieren. Dadurch wird die Menge der Client-seitigen Technologien verringert, die Marketing-Experten zum Erreichen ihres Zielmarkts und zum Senden von Daten an andere Zielorte als Adobe benötigen. Dies erleichtert Implementierungs-Teams die Verwaltung der Daten, die vom Client an verschiedene Ziele gesendet werden.

## Unterschiede zwischen Ereignisweiterleitung und Tags

Beachten Sie die folgenden Unterschiede zwischen der Ereignisweiterleitung und den Tags:

* Tokenisierung von Datenelementen

   * Tags: In einer Regel werden Datenelemente mit einem `%` -Token am Anfang und am Ende des Datenelementnamens versehen. Beispiel: `%viewportHeight%`.

   * Ereignisweiterleitung: In einer Regel werden Datenelemente mit `{{` am Anfang und `}}` am Ende des Datenelementnamens markiert. Beispiel: `{{viewportHeight}}`.

* Wie Daten referenziert werden

   Um Daten aus dem Edge-Netzwerk zu referenzieren, muss der Datenelementpfad `arc.event._<element>_` sein.

   `arc` steht für Adobe Response Context.

   Beispiel: `arc.event.xdm.web.webPageDetails.URL`

   >[!IMPORTANT]
   >
   >Wenn dieser Pfad falsch angegeben wird, werden keine Daten erfasst.


* Sequenz von Regelaktionen

   Im Aktionsabschnitt einer Regel werden Ereignisweiterleitungsregeln immer nacheinander ausgeführt. Stellen Sie beim Speichern einer Regel sicher, dass die Reihenfolge der Aktionen korrekt ist. Diese Ausführungssequenz kann nicht so gewählt werden wie mit Tags.

* JavaScript-Versionen mit benutzerdefiniertem Code

   Tags verwenden JavaScript-Version es5. Die Ereignisweiterleitung verwendet Version es6.

<!--doc Adobe Cloud Connector extension, get from Jon-->
