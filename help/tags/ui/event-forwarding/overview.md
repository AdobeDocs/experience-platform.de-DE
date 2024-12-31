---
title: Übersicht über die Ereignisweiterleitung
description: Hier erfahren Sie mehr über Adobe Experience Platform, mit dessen Hilfe Sie über das Platform Edge-Netzwerk Aufgaben ausführen können, ohne dabei Ihre Tag-Implementierung zu ändern.
feature: Event Forwarding
exl-id: 18e76b9c-4fdd-4eff-a515-a681bc78d37b
source-git-commit: 16f9ee9d14326f857b444c2361b894aca06b04d6
workflow-type: tm+mt
source-wordcount: '1178'
ht-degree: 75%

---

# Übersicht über die Ereignisweiterleitung

>[!NOTE]
>
>Die Ereignisweiterleitung ist eine gebührenpflichtige Funktion, die im Rahmen von Adobe Real-time Customer Data Platform Connections, Prime und Ultimate angeboten wird.

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Mit der Ereignisweiterleitung in Adobe Experience Platform können Sie erfasste Ereignisdaten zur Server-seitigen Verarbeitung an ein Ziel senden. Die Ereignisweiterleitung reduziert den Umfang von Web-Seiten und Mobile Apps. Dabei wird das Adobe Experience Platform Edge-Netzwerk verwendet, um Aufgaben auszuführen, die normalerweise auf dem Client laufen. Ereignisweiterleitungsregeln werden auf ähnliche Weise wie Tags implementiert und können Daten transformieren und an neue Ziele senden. Anstatt diese Daten jedoch von einer Client-Anwendung wie einem Webbrowser zu senden, werden sie von den Servern von Adobe gesendet.

Dieses Dokument bietet einen Überblick über die Ereignisweiterleitung in Platform.

![Ereignisweiterleitung im Datenerfassungs-Ökosystem.](../../../collection/images/home/event-forwarding.png)

>[!NOTE]
>
>Informationen dazu, wie die Ereignisweiterleitung in Platform in das Datenerfassungs-Ökosystem passt, finden Sie in der [Übersicht zur Datenerfassung](../../../collection/home.md).

Die Ereignisweiterleitung in Kombination mit dem [Web SDK](/help/web-sdk/home.md) und dem [Mobile SDK](https://experienceleague.adobe.com/docs/platform-learn/data-collection/mobile-sdk/overview.html?lang=de) von Adobe Experience Platform bietet die folgenden Vorteile:

**Performance**:

* Führen Sie einen einzelnen Aufruf von einer Seite aus, die eine Payload von Daten enthält, die dann Server-seitig zusammengeführt werden, um den Client-seitigen Netzwerkverkehr zu reduzieren und so Kunden ein schnelleres Erlebnis zu bieten.
* Verringern Sie die Ladezeit von Web-Seiten, um die Site-Performance zu verbessern.
* Verringern Sie die Anzahl der erforderlichen Client-seitigen Technologien, um Ihr Erlebnis bereitzustellen und Daten an viele Ziele zu senden.

**Data Governance**:

* Erhöhen Sie über alle Properties hinweg die Transparenz und Kontrolle darüber, welche Daten wohin gesendet werden.

## Unterschiede zwischen Ereignisweiterleitung und Tags {#differences-from-tags}

In Bezug auf die Konfiguration verwendet die Ereignisweiterleitung viele Konzepte von Tags, z. B. [Regeln](../managing-resources/rules.md), [Datenelemente](../managing-resources/data-elements.md) und [Erweiterungen](../managing-resources/extensions/overview.md). Der Hauptunterschied zwischen den beiden kann wie folgt zusammengefasst werden:

* Tags **sammeln** Ereignisdaten von einer Website oder nativen Mobile App und sendet sie an das Platform Edge Network.
* Die Ereignisweiterleitung **sendet** eingehende Ereignisdaten vom Platform Edge Network an einen Endpunkt, der ein endgültiges Ziel darstellt, oder an einen Endpunkt, der Daten bereitstellt, mit denen Sie die ursprüngliche Payload anreichern können.

Während Tags Ereignisdaten mithilfe der Platform Web- und Mobile-SDKs direkt auf Ihrer Site oder in Ihrer nativen Mobile App erfassen, müssen bei der Ereignisweiterleitung Ereignisdaten über das Platform Edge Network gesendet werden, um an Ziele weitergeleitet zu werden. Mit anderen Worten: Sie müssen das Platform Web- oder Mobile-SDK in Ihre digitale Property implementieren (entweder über Tags oder mithilfe von Roh-Code), um die Ereignisweiterleitung verwenden zu können.

### Properties {#properties}

Die Ereignisweiterleitung verwaltet einen eigenen Speicher mit Properties, die von Tags getrennt sind. Diese können Sie in der Experience Platform-Benutzeroberfläche oder der Datenerfassungs-Benutzeroberfläche durch Auswahl von **[!UICONTROL Ereignisweiterleitung]** im linken Navigationsbereich anzeigen.

>[!TIP]
>
>Verwenden Sie die produktinterne Hilfe im rechten Bereich, um mehr über die Ereignisweiterleitung zu erfahren und zusätzliche verfügbare Ressourcen anzuzeigen.

![Properties der Ereignisweiterleitung in der Datenerfassungs-Benutzeroberfläche.](../../images/ui/event-forwarding/overview/properties.png)

Alle Properties der Ereignisweiterleitung führen **[!UICONTROL Edge]** als ihre Plattform auf. Sie unterscheiden nicht zwischen Web oder Mobile, da sie nur Daten verarbeiten, die vom Platform Edge Network empfangen werden, das selbst Ereignisdaten sowohl von Web- als auch von mobilen Plattformen empfangen kann.

### Erweiterungen {#extensions}

Die Ereignisweiterleitung verfügt über einen eigenen Katalog kompatibler Erweiterungen, z. B. die [Core](../../extensions/server/core/overview.md)-Erweiterung und die [Adobe Cloud Connector](../../extensions/server/cloud-connector/overview.md)-Erweiterung. Sie können die verfügbaren Erweiterungen für Properties der Ereignisweiterleitung in der Benutzeroberfläche anzeigen, indem Sie im linken Navigationsbereich auf **[!UICONTROL Erweiterungen]** und dann auf **[!UICONTROL Katalog]** klicken.

Sie können zusätzliche verfügbare Ressourcen anzeigen, um mehr über diese Funktion zu erfahren, indem Sie ![about](../../images/ui/event-forwarding/overview/about.png) im rechten Bedienfeld auswählen.

![Erweiterungen für die Ereignisweiterleitung in der Datenerfassungs-Benutzeroberfläche.](../../images/ui/event-forwarding/overview/extensions.png)

### Datenelemente {#data-elements}

Die Typen der in der Ereignisweiterleitung verfügbaren Datenelemente sind auf den Katalog der kompatiblen [Erweiterungen](#extensions) beschränkt, die sie bereitstellen.

Während die Datenelemente selbst in der Ereignisweiterleitung auf die gleiche Weise erstellt und konfiguriert werden wie Tags, gibt es einige wichtige Syntaxunterschiede bei der Referenzierung von Daten im Platform Edge Network.

#### Referenzieren von Daten im Platform Edge Network {#data-element-path}

Um Daten im Platform Edge Network zu referenzieren, müssen Sie ein Datenelement erstellen, das einen gültigen Pfad zu diesen Daten bereitstellt. Wählen Sie beim Erstellen des Datenelements in der Benutzeroberfläche die Option **[!UICONTROL Core]** für die Erweiterung und **[!UICONTROL Pfad]** für den Typ.

Der Wert **[!UICONTROL Pfad]** für das Datenelement muss dem Muster `arc.event.{ELEMENT}` entsprechen (z. B.: `arc.event.xdm.web.webPageDetails.URL`). Dieser Pfad muss korrekt angegeben werden, damit Daten gesendet werden können.

Sie können zusätzliche verfügbare Ressourcen anzeigen, um mehr über diese Funktion zu erfahren, indem Sie ![about](../../images/ui/event-forwarding/overview/about.png) im rechten Bedienfeld auswählen.

![Beispiel eines Datenelements vom Typ Pfad für die Ereignisweiterleitung.](../../images/ui/event-forwarding/overview/data-reference.png)

### Regeln {#rules}

Das Erstellen von Regeln in den Properties der Ereignisweiterleitung funktioniert ähnlich wie Tags, wobei der wesentliche Unterschied darin besteht, dass Sie Ereignisse nicht als Regelkomponenten auswählen können. Stattdessen verarbeitet eine Ereignisweiterleitungsregel alle Ereignisse, die sie vom [Datenstrom](../../../datastreams/overview.md) erhält, und leitet diese Ereignisse an Ziele weiter, wenn bestimmte Bedingungen erfüllt sind.

Darüber hinaus gibt es eine maximale Wartezeit von 30 Sekunden, die für ein einzelnes Ereignis gilt, da es über alle Regeln (und somit alle Aktionen) hinweg in einer Ereignisweiterleitungs-Eigenschaft verarbeitet wird. Das bedeutet, dass alle Regeln und Aktionen für ein einzelnes Ereignis innerhalb dieses Zeitraums abgeschlossen sein müssen.

Sie können zusätzliche verfügbare Ressourcen anzeigen, um mehr über diese Funktion zu erfahren, indem Sie ![about](../../images/ui/event-forwarding/overview/about.png) im rechten Bedienfeld auswählen.

![Regeln für die Ereignisweiterleitung in der Datenerfassungs-Benutzeroberfläche.](../../images/ui/event-forwarding/overview/rules.png)

#### Tokenisierung von Datenelementen {#tokenization}

In Tag-Regeln werden Datenelemente am Anfang und am Ende des Datenelementnamens mit einem `%`-Token versehen (zum Beispiel: `%viewportHeight%`). In Ereignisweiterleitungsregeln dagegen werden Datenelemente mit einem `{{`-Token am Anfang und einem `}}`-Token am Ende des Datenelementnamens versehen (zum Beispiel: `{{viewportHeight}}`).

Sie können zusätzliche verfügbare Ressourcen anzeigen, um mehr über diese Funktion zu erfahren, indem Sie ![about](../../images/ui/event-forwarding/overview/about.png) im rechten Bedienfeld auswählen.

![Beispiel eines Datenelements vom Typ Pfad für die Ereignisweiterleitung.](../../images/ui/event-forwarding/overview/tokenization.png)

#### Sequenz von Regelaktionen {#action-sequencing}

Der Abschnitt [!UICONTROL Aktionen] einer Ereignisweiterleitungsregel wird immer sequentiell ausgeführt. Wenn eine Regel beispielsweise zwei Aktionen hat, beginnt die zweite Aktion erst dann mit der Ausführung, wenn die vorherige Aktion abgeschlossen ist (und in Fällen, in denen eine Antwort von einem Endpunkt erwartet wird, hat dieser Endpunkt geantwortet). Stellen Sie also beim Speichern einer Regel sicher, dass die Reihenfolge der Aktionen korrekt ist. Diese Ausführungssequenz kann im Gegensatz zu Tag-Regeln nicht asynchron ausgeführt werden.

## Geheimnisse {#secrets}

Bei der Ereignisweiterleitung können Sie Geheimnisse erstellen, verwalten und speichern, die für die Authentifizierung bei den Servern verwendet werden können, an die Sie Daten senden. Siehe das Handbuch zu [Geheimnissen](./secrets.md), um zu erfahren, welche Geheimnistypen es gibt und wie sie in der Benutzeroberfläche implementiert sind.

## Videoüberblick {#video}

Das folgende Video soll Ihnen dabei helfen, die Ereignisweiterleitung und Real-Time CDP-Verbindungen besser zu verstehen.

>[!VIDEO](https://video.tv.adobe.com/v/3429308)

## Nächste Schritte

In diesem Abschnitt haben Sie einen Überblick über die Ereignisweiterleitung erhalten. Weitere Informationen zum Einrichten dieser Funktion für Ihr Unternehmen finden Sie im Abschnitt [Erste Schritte](./getting-started.md).
