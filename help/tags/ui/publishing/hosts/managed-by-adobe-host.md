---
title: Übersicht über von Adobe verwaltete Hosts
description: Erfahren Sie mehr über die standardmäßige Hosting-Option für die Bereitstellung von Tag-Bibliothek-Builds in Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '1173'
ht-degree: 66%

---

# Übersicht über von Adobe verwaltete Hosts

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

Hosts, die von der Adobe verwaltet werden, sind die Standardeinstellung für die Bereitstellung Ihrer Tag-Bibliothek-Builds in Adobe Experience Platform. Wenn Sie über die Datenerfassungs-Benutzeroberfläche eine neue Eigenschaft erstellen, wird ein von der Adobe verwalteter Standardhost für Sie erstellt.

Bei von Adobe verwalteten Hosts werden Bibliotheks-Builds an ein Content Delivery Network (CDN) eines Drittanbieters bereitgestellt, mit dem Adobe Verträge geschlossen hat. Diese CDNs funktionieren unabhängig von Adobe. Selbst wenn Platform gewartet wird oder anderweitig ausfällt, funktioniert der bereitgestellte Code auf Ihren Websites und Anwendungen weiterhin normal. Der Einbettungs-Code für einen von Adobe gewarteten Host verweist auf die Hauptbibliotheksdatei des CDN, damit ein Client-Gerät die Dateien zur Laufzeit abrufen kann.

Dieses Dokument bietet einen Überblick über von Adobe verwaltete Hosts in Platform und beschreibt, wie ein neuer, von Adoben verwalteter Host in der Benutzeroberfläche erstellt werden kann.

## Akamai

Derzeit ist der primäre CDN-Anbieter für Adobe [Akamai](https://www.akamai.com/de). Das robuste CDN von Akamai ist so konzipiert, dass es einem hohen Aufkommen globaler Web-Besucher Inhalte bereitstellen kann. Das CDN betreibt redundante Netzwerke mit lastausgewogenen, geooptimierten Knoten, um Inhalte Besuchern auf der ganzen Welt möglichst schnell bereitstellen zu können.

Akamai verfügt über 137.000 Server in 87 Ländern in mehr als 1.150 Netzwerken. Hinsichtlich der Redundanz routet das CDN nicht nur von einem Server zum anderen, sondern kann bei Bedarf auch von einem Server-Knoten zu einem anderen Server-Knoten weiterleiten. Mit anderen Worten, besteht jeder Knoten aus mehreren Servern. Ein Server-Ausfall wird dadurch nie zu einem Problem, da die anderen Server auf demselben Knoten die jeweiligen Aufgaben übernehmen können.

Wenn ein ganzer Knoten ausfällt, wird Akamai vom nächstgelegenen Knoten mit demselben zwischengespeicherten Inhalt bereitgestellt. Knoten werden basierend auf dem Standort der Besucher, der Traffic-Last und anderen Faktoren dynamisch ausgewählt, sodass Inhalt stets vom jeweils besten lokalen Knoten für jeden Besucher bereitgestellt wird.

Die auf Akamai gehosteten Dateien haben die Domain `assets.adobedtm.com`. Diese kann sicher oder nicht sicher (`http://` oder `https://`) referenziert werden, je nachdem, wie der Aufruf in Ihrem eingebetteten `<script>`-Code erfolgt.

>[!WARNING]
>
>Wenn Ihre Bibliothek nicht über das Akamai-Netzwerk verfügbar ist, kann Platform keine Fehler verhindern, die dadurch entstehen können.

## Zwischenspeicherung von Bibliotheks-Builds

Bei der Verwendung von Hosts, die von Adobe verwaltet werden, werden Ihre Bibliotheks-Builds an zwei Orten zwischengespeichert:

* [Edge-Zwischenspeicherung](#edge)
* [Browser-Cache](#browser)

### Edge-Zwischenspeicherung {#edge}

Der Hauptzweck eines CDN besteht darin, Inhalte intelligent an Server zu verteilen, die geografisch näher an Endbenutzern liegen, damit der Inhalt von Clientgeräten schneller abgerufen werden kann. CDNs erreichen dies, indem sie Kopien des Inhalts auf geografisch verteilten Servern auf der ganzen Welt verfügbar machen („Edge-Knoten“).

Sobald Ihr Build auf dem von Adobe verwalteten Host bereitgestellt wurde, verteilt das CDN den Build auf mehrere zentralisierte Server („Quellen“), die dann Kopien des Builds an viele verschiedene Edge-Knoten auf der ganzen Welt zum Zwischenspeichern senden. Die auf diesen Edge-Knoten zwischengespeicherten Versionen des Builds werden dann letztendlich den Client-Geräten bereitgestellt.

![](../images/cdn-diagram.png)

>[!NOTE]
>
>Bei von Adobe verwalteten Hosts kann es bis zu fünf Minuten dauern, bis die allererste in einer neuen Umgebung veröffentlichte Bibliothek an das globale CDN übertragen wird.

Wenn ein Edge-Knoten eine Anforderung für eine bestimmte Datei erhält (z. B. Ihren Bibliotheks-Build), prüft der Knoten zunächst den TTL-Wert (Time-to-Live) in der Datei. Wenn die TTL noch nicht abgelaufen ist, wird die zwischengespeicherte Version von den Edge-Knoten bereitgestellt. Ist die TTL jedoch abgelaufen, fordert der Edge-Knoten eine neue Kopie von der nächsten Quelle an, stellt die aktualisierte Kopie bereit und cacht die aktualisierte Kopie mit einer neuen TTL.

>[!NOTE]
>
>Neben der Zwischenspeicherung von Edge-Knoten gibt es auch Zwischenspeicherungsnetzwerke (wie Unternehmens- oder Mobilnetzwerke), die ihre eigene Zwischenspeicherung durchführen. Wenn Ihre Builds nicht wie erwartet zwischengespeichert werden, können diese Netzwerke die zugrunde liegende Ursache sein.

#### Edge-Cache-Invalidierung {#invalidation}

Wenn Sie einen neuen Bibliotheks-Build hochladen, werden die Caches auf allen entsprechenden Edge-Knoten invalidiert. Das bedeutet, dass jeder Knoten seine zwischengespeicherte Version als ungültig betrachtet, unabhängig davon, wie kürzlich eine neue Kopie abgerufen wurde. Wenn ein Edge-Knoten das nächste Mal eine Anfrage für diese Datei erhält, ruft der Knoten eine neue Kopie aus der Quelle ab.

Da Akamai über mehrere Ausgangsserver verfügt, die Dateien replizieren, und es nicht möglich ist zu wissen, welcher Ursprung Ihre Datei zuerst erhalten hat, können diese Knotenanforderungen einen Ursprung erreichen, der nicht über die neueste Version verfügt. Anschließend würde die ältere Version erneut zwischengespeichert. Um dies zu verhindern, werden für jeden neuen Build in den folgenden Intervallen mehrere Cache-Invalidierungen durchgeführt:

* Sofort nach dem Hochladen
* 5 Minuten nach dem Hochladen
* 60 Minuten nach dem Hochladen

Diese gestaffelten Cache-Invalidierungen geben den Quell-Server-Gruppen Zeit, die neueste Dateiversion untereinander zu replizieren, sodass sie alle die neueste Version haben, wenn die Datei abgerufen wird.

### Browser-Cache {#browser}

Bibliotheks-Builds werden auch über die `cache-control` HTTP-Kopfzeile im Browser zwischengespeichert. Bei der Verwendung von Hosts, die von Adobe verwaltet werden, haben Sie keine Kontrolle über die Kopfzeilen, die in API-Antworten zurückgegeben werden. Daher wird die Adobe-Standardeinstellung für die Zwischenspeicherung verwendet. Mit anderen Worten können Sie keine benutzerdefinierten Kopfzeilen für von Adobe verwaltete Hosts verwenden. Wenn Sie eine benutzerdefinierte `cache-control`-Kopfzeile benötigen, sollten Sie das Hosting stattdessen [selbst übernehmen](self-hosting-libraries.md).

Die &quot;Time-to-Live&quot;(TTL) für Ihren im Browser zwischengespeicherten Bibliotheks-Build (der durch die `cache-control` -Kopfzeile bestimmt wird) hängt von der verwendeten Tag-Umgebung ab:

| Umgebung | Wert `cache-control` |
| --- | --- |
| Entwicklung | `max-age=0, no-cache, no-store` |
| Staging | `max-age=0, no-cache, no-store` |
| Produktion | `max-age=3600` |

Wie aus der obigen Tabelle hervorgeht, wird die Browser-Zwischenspeicherung in der Entwicklungs- und Staging-Umgebung nicht unterstützt. Daher sollten Sie keine Entwicklungs- oder Staging-Einbettungs-Codes in Kontexten mit hohem Traffic oder Produktionsumgebungen verwenden.

Cache-Control-Header werden nur auf den Hauptbibliotheks-Build angewendet. Alle Unterressourcen unterhalb der Hauptbibliothek werden immer als neu erachtet und müssen daher nicht im Browser zwischengespeichert werden.

## Verwenden von Adobe-verwaltetem Hosting in der Datenerfassungs-Benutzeroberfläche

Wenn Sie zum ersten Mal eine Eigenschaft in der [Datenerfassungs-Benutzeroberfläche](http://launch.adobe.com/de) erstellen, wird automatisch ein von der Adobe verwalteter Host erstellt. Alle verfügbaren Umgebungen mit sofort verwendbaren Eigenschaften werden standardmäßig auch dem von Adobe verwalteten Host zugewiesen.

>[!NOTE]
>
>Wenn die Zuweisung des von Adobe verwalteten Standard-Hosts zu allen Umgebung aufgehoben wird, kann der Host gelöscht werden. Wenn Sie nach diesem Vorgang zu einem von Adobe verwalteten Host zurückkehren möchten, können Sie einen neuen Host wie folgt erstellen:
>
>1. Wählen Sie die Registerkarte **[!UICONTROL Hosts]** in Ihrer Eigenschaft aus und wählen Sie dann **[!UICONTROL Host hinzufügen]** aus.
>1. Geben Sie einen Namen für den Host ein, wählen Sie als Host-Typ **[!UICONTROL Verwaltet von Adobe]** aus und wählen Sie dann **[!UICONTROL Speichern]**.

>
>
Anschließend können Sie Ihre Umgebung nach Bedarf dem von Adobe verwalteten Host erneut zuweisen.

## Nächste Schritte

Dieses Dokument bietet einen Überblick über das von Adobe verwaltete Hosting für Tag-Bibliotheken in Adobe Experience Platform. Informationen zu anderen Hosting-Optionen finden Sie in der folgenden Dokumentation:

* [SFTP-Hosting](./sftp-host.md)
* [Self-Hosting von Bibliotheken](./self-hosting-libraries.md)

Weitere Informationen zum Verwalten von Hosts für Ihre Umgebung finden Sie im Handbuch [Umgebungen](../environments.md).
