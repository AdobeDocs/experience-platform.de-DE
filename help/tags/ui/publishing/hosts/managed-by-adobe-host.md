---
title: Übersicht über von Adobe verwaltete Hosts
description: Erfahren Sie mehr über die Standard-Hosting-Option für die Bereitstellung von Tag-Bibliotheks-Builds in Adobe Experience Platform.
exl-id: 9042c313-b0d3-4f6e-963d-0051d760fd16
source-git-commit: 85b428b3997d53cbf48e4f112e5c09c0f40f7ee1
workflow-type: tm+mt
source-wordcount: '1173'
ht-degree: 89%

---

# Übersicht über von Adobe verwaltete Hosts

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

Von Adobe verwaltete Hosts sind die Standard-Host-Einstellung für die Bereitstellung Ihrer Tag-Bibliotheks-Builds in Adobe Experience Platform. Wenn Sie eine neue Eigenschaft über die Datenerfassungs-Benutzeroberfläche erstellen, wird ein von Adobe verwalteter Standard-Host für Sie erstellt.

Bei von Adobe verwalteten Hosts werden Bibliotheks-Builds an ein Content Delivery Network (CDN) eines Drittanbieters bereitgestellt, mit dem Adobe Verträge geschlossen hat. Diese CDNs funktionieren unabhängig von Adobe. Selbst wenn Platform gewartet wird oder anderweitig ausfällt, funktioniert der bereitgestellte Code auf Ihren Websites und Anwendungen weiterhin normal. Der Einbettungs-Code für einen von Adobe gewarteten Host verweist auf die Hauptbibliotheksdatei des CDN, damit ein Client-Gerät die Dateien zur Laufzeit abrufen kann.

Dieses Dokument bietet einen Überblick über die von Adobe verwalteten Hosts in Platform und beschreibt, wie Sie einen neuen von Adobe verwalteten Host in der Benutzeroberfläche erstellen.

## Akamai

Derzeit ist der primäre CDN-Anbieter für Adobe [Akamai](https://www.akamai.com/de). Das robuste CDN von Akamai ist so konzipiert, dass es einem hohen Aufkommen globaler Web-Besucher Inhalte bereitstellen kann. Das CDN betreibt redundante Netzwerke mit lastausgewogenen, geooptimierten Knoten, um Inhalte Besuchern auf der ganzen Welt möglichst schnell bereitstellen zu können.

Akamai verfügt über 137.000 Server in 87 Ländern in mehr als 1.150 Netzwerken. Hinsichtlich der Redundanz routet das CDN nicht nur von einem Server zum anderen, sondern kann bei Bedarf auch Daten von einem Server-Knoten zu einem anderen Server-Knoten weiterleiten. Mit anderen Worten, besteht jeder Knoten aus mehreren Servern. Ein Server-Ausfall wird dadurch nie zu einem Problem, da die anderen Server auf demselben Knoten die jeweiligen Aufgaben übernehmen können.

Wenn ein ganzer Knoten ausfällt, bedient Akamai vom nächstgelegenen Knoten mit demselben zwischengespeicherten Inhalt. Knoten werden basierend auf dem Standort der Besucher, der Traffic-Last und anderen Faktoren dynamisch ausgewählt, sodass Inhalt stets vom jeweils besten lokalen Knoten für jeden Besucher bereitgestellt wird.

Die auf Akamai gehosteten Dateien haben die Domain `assets.adobedtm.com`. Diese kann sicher oder nicht sicher (`http://` oder `https://`) referenziert werden, je nachdem, wie der Aufruf in Ihrem eingebetteten `<script>`-Code erfolgt.

>[!WARNING]
>
>Wenn Ihre Bibliothek nicht über das Akamai-Netzwerk verfügbar ist, kann Platform keine Fehler verhindern, die dadurch entstehen können.

## Zwischenspeicherung von Bibliotheks-Builds

Bei der Verwendung von Hosts, die von Adobe verwaltet werden, werden Ihre Bibliotheks-Builds an zwei Orten zwischengespeichert:

* [Edge-Zwischenspeicherung](#edge)
* [Browser-Cache](#browser)

### Edge-Zwischenspeicherung {#edge}

Der primäre Zweck eines CDN besteht darin, Inhalte intelligent an Server zu verteilen, die geografisch näher an Endbenutzern liegen, damit die Inhalte schneller von Client-Geräten abgerufen werden können. CDNs erreichen dies, indem sie Kopien des Inhalts auf geografisch verteilten Servern auf der ganzen Welt verfügbar machen („Edge-Knoten“).

Sobald Ihr Build auf dem von Adobe verwalteten Host bereitgestellt wurde, verteilt das CDN den Build auf mehrere zentralisierte Server („Quellen“), die dann Kopien des Builds an viele verschiedene Edge-Knoten auf der ganzen Welt zum Zwischenspeichern senden. Die auf diesen Edge-Knoten zwischengespeicherten Versionen des Builds werden dann letztendlich den Client-Geräten bereitgestellt.

![](../images/cdn-diagram.png)

>[!NOTE]
>
>Bei von Adobe verwalteten Hosts kann es bis zu fünf Minuten dauern, bis die allererste in einer neuen Umgebung veröffentlichte Bibliothek an das globale CDN übertragen wird.

Wenn ein Edge-Knoten eine Anforderung für eine bestimmte Datei erhält (z. B. Ihren Bibliotheks-Build), prüft der Knoten zunächst die Ablaufzeit für die Datei. Wenn die Zeit nicht abgelaufen ist, stellt der Edge-Knoten die zwischengespeicherte Version bereit. Wenn die Zeit abgelaufen ist, fordert der Edge-Knoten eine neue Kopie von der nächsten Quelle an, stellt diese aktualisierte Kopie bereit und speichert dann die aktualisierte Kopie mit einer neuen Ablaufzeit zwischen.

>[!NOTE]
>
>Neben der Zwischenspeicherung von Edge-Knoten gibt es auch Zwischenspeicherungsnetzwerke (wie Unternehmens- oder Mobilnetzwerke), die ihre eigene Zwischenspeicherung durchführen. Wenn Ihre Builds nicht wie erwartet zwischengespeichert werden, können diese Netzwerke die zugrunde liegende Ursache sein.

#### Edge-Cache-Invalidierung {#invalidation}

Wenn Sie einen neuen Bibliotheks-Build hochladen, werden die Caches auf allen entsprechenden Edge-Knoten invalidiert. Das bedeutet, dass jeder Knoten seine zwischengespeicherte Version als ungültig betrachtet, unabhängig davon, vor welcher Zeit er eine frische Kopie abgerufen hat. Wenn ein Edge-Knoten das nächste Mal eine Anfrage für diese Datei erhält, ruft der Knoten eine neue Kopie aus der Quelle ab.

Da Akamai über mehrere Ursprungs-Server verfügt, die Dateien untereinander replizieren, und da es keine Möglichkeit gibt, herauszufinden, welcher Ursprung Ihre Datei zuerst erhalten hat, können diese Knotenanfragen auf einen Ursprung treffen, der nicht die neueste Version verwendet. Dann würde wieder die ältere Version zwischengespeichert. Um dies zu verhindern, werden bei jedem neuen Build in den folgenden Intervallen mehrere Cache-Invalidierungen durchgeführt:

* Sofort nach dem Hochladen
* 5 Minuten nach dem Hochladen
* 60 Minuten nach dem Hochladen

Diese gestaffelten Cache-Invalidierungen geben den Quell-Server-Gruppen Zeit, die neueste Dateiversion untereinander zu replizieren, sodass sie alle die neueste Version haben, wenn die Datei abgerufen wird.

### Browser-Cache {#browser}

Bibliotheks-Builds werden auch über den `cache-control`-HTTP-Header im Browser zwischengespeichert. Bei der Verwendung von Hosts, die von Adobe verwaltet werden, haben Sie keine Kontrolle über die Header, die in API-Antworten zurückgegeben werden. Daher wird die Adobe-Standardeinstellung für die Zwischenspeicherung verwendet. Mit anderen Worten können Sie keine benutzerdefinierten Header für von Adobe verwaltete Hosts verwenden. Wenn Sie einen benutzerdefinierten `cache-control`-Header benötigen, sollten Sie das Hosting stattdessen [selbst übernehmen](self-hosting-libraries.md).

Die Ablaufzeit für Ihren im Browser zwischengespeicherten Bibliotheks-Build (bestimmt durch die Variable `cache-control` -Kopfzeile) hängt von der verwendeten Tag-Umgebung ab:

| Umgebung | Wert `cache-control` |
| --- | --- |
| Entwicklung | `max-age=0, no-cache, no-store` |
| Staging | `max-age=0, no-cache, no-store` |
| Produktion | `max-age=3600` |

Wie aus der obigen Tabelle hervorgeht, wird die Browser-Zwischenspeicherung in der Entwicklungs- und Staging-Umgebung nicht unterstützt. Daher sollten Sie keine Entwicklungs- oder Staging-Einbettungs-Codes in Kontexten mit hohem Traffic oder Produktionsumgebungen verwenden.

Cache-Steuerungs-Header werden nur für den Hauptbibliotheks-Build angewendet. Alle Unterressourcen unterhalb der Hauptbibliothek werden immer als neu erachtet und müssen daher nicht im Browser zwischengespeichert werden.

## Verwenden von Adobe-verwaltetem Hosting in der Benutzeroberfläche

Wenn Sie zum ersten Mal eine Eigenschaft in der Platform-Benutzeroberfläche oder der Datenerfassungs-Benutzeroberfläche erstellen, wird automatisch ein von der Adobe verwalteter Host erstellt. Alle verfügbaren Umgebungen, die sofort nutzbare Eigenschaften haben, werden standardmäßig auch dem von Adobe verwalteten Host zugewiesen.

>[!NOTE]
>
>Wenn die Zuweisung des von Adobe verwalteten Standard-Hosts zu allen Umgebung aufgehoben wird, kann der Host gelöscht werden. Wenn Sie nach diesem Vorgang zu einem von Adobe verwalteten Host zurückkehren möchten, können Sie einen neuen Host wie folgt erstellen:
>
>1. Wählen Sie die Registerkarte **[!UICONTROL Hosts]** in Ihrer Eigenschaft aus und wählen Sie dann **[!UICONTROL Host hinzufügen]** aus.
>1. Geben Sie einen Namen für den Host ein, wählen Sie als Host-Typ **[!UICONTROL Verwaltet von Adobe]** aus und wählen Sie dann **[!UICONTROL Speichern]**.

>
>Anschließend können Sie Ihre Umgebung nach Bedarf dem von Adobe verwalteten Host erneut zuweisen.

## Nächste Schritte

Dieses Dokument bietet einen Überblick über das von Adobe verwaltete Hosting für Tag-Bibliotheken in Adobe Experience Platform. Informationen zu anderen Hosting-Optionen finden Sie in der folgenden Dokumentation:

* [SFTP-Hosting](./sftp-host.md)
* [Self-Hosting von Bibliotheken](./self-hosting-libraries.md)

Weitere Informationen zum Verwalten von Hosts für Ihre Umgebung finden Sie im Handbuch [Umgebungen](../environments.md).
