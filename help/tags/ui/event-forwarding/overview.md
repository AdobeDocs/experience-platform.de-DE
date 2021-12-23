---
title: Übersicht über die Ereignisweiterleitung
description: Hier erfahren Sie mehr über Adobe Experience Platform, mit dessen Hilfe Sie über das Platform Edge-Netzwerk Aufgaben ausführen können, ohne dabei Ihre Tag-Implementierung zu ändern.
feature: Event Forwarding
exl-id: 18e76b9c-4fdd-4eff-a515-a681bc78d37b
source-git-commit: 64e76c456ac5f59a2a1996e58eda405f1b27efa8
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 14%

---

# Übersicht über die Ereignisweiterleitung

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Mit der Ereignisweiterleitung in Adobe Experience Platform können Sie erfasste Ereignisdaten zur serverseitigen Verarbeitung an ein Ziel senden. Die Ereignisweiterleitung reduziert das Gewicht von Web-Seiten und Programmen, indem das Adobe Experience Platform Edge-Netzwerk verwendet wird, um Aufgaben auszuführen, die normalerweise auf dem Client erledigt werden. Auf ähnliche Weise wie Tags implementiert, können Ereignisweiterleitungsregeln Daten transformieren und an neue Ziele senden. Anstatt diese Daten jedoch von einer Client-Anwendung wie einem Webbrowser zu senden, werden sie von den Servern der Adobe gesendet.

Dieses Dokument bietet einen allgemeinen Überblick über die Ereignisweiterleitung in Platform.

![Ereignisweiterleitung im Datenerfassungs-Ökosystem](../../../collection/images/home/event-forwarding.png)

>[!NOTE]
>
>Informationen dazu, wie die Ereignisweiterleitung in Platform in das Datenerfassungs-Ökosystem passt, finden Sie in der [Datenerfassung - Übersicht](../../../collection/home.md).

Ereignisweiterleitung in Kombination mit Adobe Experience Platform [Web SDK](../../../edge/home.md) und [Mobile SDK](https://aep-sdks.gitbook.io/docs/) bietet die folgenden Vorteile:

**Leistung**:

* Führen Sie einen einzelnen Aufruf von einer Seite aus durch, die eine Payload von Daten enthält, die dann serverseitig verbunden werden, um den clientseitigen Netzwerk-Traffic zu reduzieren und Kunden ein schnelleres Erlebnis zu bieten.
* Verringern Sie die Ladezeit von Webseiten, um die Site-Leistung zu verbessern.
* Verringern Sie die Anzahl der erforderlichen clientseitigen Technologien, um Ihr Erlebnis bereitzustellen und Daten an viele Ziele zu senden.

**Data Governance**:

* Erhöhen Sie die Transparenz und Kontrolle darüber, welche Daten wohin über alle Eigenschaften hinweg gesendet werden.

## Unterschiede zwischen Ereignisweiterleitung und Tags {#differences-from-tags}

In Bezug auf die Konfiguration verwendet die Ereignisweiterleitung viele der gleichen Konzepte wie Tags, z. B. [Regeln](../managing-resources/rules.md), [Datenelemente](../managing-resources/data-elements.md)und [Erweiterungen](../managing-resources/extensions/overview.md). Der Hauptunterschied zwischen den beiden kann wie folgt zusammengefasst werden:

* Tags **sammelt** Ereignisdaten von einer Website oder nativen mobilen Anwendung und senden sie an das Platform Edge Network.
* Ereignisweiterleitung **sendet** eingehende Ereignisdaten vom Platform Edge Network an einen Endpunkt weitergeleitet werden, der ein endgültiges Ziel oder einen Endpunkt darstellt, der Daten bereitstellt, mit denen Sie die ursprüngliche Payload anreichern möchten.

Während Tags Ereignisdaten mithilfe der Platform Web- und Mobile-SDKs direkt von Ihrer Site oder nativen mobilen Anwendung erfassen, erfordert die Ereignisweiterleitung, dass Ereignisdaten bereits über das Platform Edge Network gesendet werden, um sie an Ziele weiterzuleiten. Mit anderen Worten: Sie müssen das Platform Web- oder Mobile-SDK in Ihre digitale Eigenschaft implementieren (entweder über Tags oder mithilfe von Rohcode), um die Ereignisweiterleitung verwenden zu können.

### Eigenschaften {#properties}

Die Ereignisweiterleitung verwaltet einen eigenen Speicher mit Eigenschaften, die von Tags getrennt sind. Diese können Sie in der Datenerfassungs-Benutzeroberfläche durch Auswahl von anzeigen **[!UICONTROL Ereignisweiterleitung]** in der linken Navigation.

![Eigenschaften für die Ereignisweiterleitung in der Datenerfassungs-Benutzeroberfläche](../../images/ui/event-forwarding/overview/properties.png)

Liste aller Eigenschaften für die Ereignisweiterleitung **[!UICONTROL Edge]** als Plattform. Sie unterscheiden nicht zwischen Web oder Mobilgerät, da sie nur Daten verarbeiten, die vom Platform Edge Network empfangen werden und die selbst Ereignisdaten von Web- und mobilen Plattformen empfangen können.

### Erweiterungen {#extensions}

Die Ereignisweiterleitung verfügt über einen eigenen Katalog kompatibler Erweiterungen, z. B. die [Core](../../extensions/web/core/event-forwarding.md) Erweiterung und [Adobe Cloud Connector](../../extensions/web/cloud-connector/overview.md) -Erweiterung. Sie können die verfügbaren Erweiterungen für Eigenschaften der Ereignisweiterleitung in der Benutzeroberfläche anzeigen, indem Sie **[!UICONTROL Erweiterungen]** im linken Navigationsbereich, gefolgt von **[!UICONTROL Katalog]**.

![Erweiterungen für die Ereignisweiterleitung in der Datenerfassungs-Benutzeroberfläche](../../images/ui/event-forwarding/overview/extensions.png)

### Datenelemente {#data-elements}

Die in der Ereignisweiterleitung verfügbaren Datenelementtypen sind auf den Katalog kompatibler [Erweiterungen](#extensions) die sie bereitstellen.

Während Datenelemente selbst in der Ereignisweiterleitung auf die gleiche Weise erstellt und konfiguriert werden wie Tags, gibt es einige wichtige Syntaxunterschiede bei der Referenzierung von Daten aus Platform Edge Network.

#### Referenzieren von Daten aus Platform Edge Network {#edge}

Um Daten aus Platform Edge Network zu referenzieren, müssen Sie ein Datenelement erstellen, das einen gültigen Pfad zu diesen Daten bereitstellt. Wählen Sie beim Erstellen des Datenelements in der Benutzeroberfläche die Option **[!UICONTROL Core]** für die Erweiterung und **[!UICONTROL Pfad]** für den Typ.

Die **[!UICONTROL Pfad]** -Wert für das Datenelement muss dem Muster entsprechen `arc.event.{ELEMENT}` (z. B.: `arc.event.xdm.web.webPageDetails.URL`). Dieser Pfad muss korrekt angegeben werden, damit Daten gesendet werden können.

![Beispiel eines Datenelements vom Pfadtyp für die Ereignisweiterleitung](../../images/ui/event-forwarding/overview/data-reference.png)

### Regeln {#rules}

Das Erstellen von Regeln in den Eigenschaften der Ereignisweiterleitung funktioniert ähnlich wie Tags, wobei der wesentliche Unterschied darin besteht, dass Sie Ereignisse nicht als Regelkomponenten auswählen können. Stattdessen verarbeitet eine Ereignisweiterleitungsregel alle Ereignisse, die sie vom [datastream](../../../edge/fundamentals/datastreams.md) und leitet diese Ereignisse an Ziele weiter, wenn bestimmte Bedingungen erfüllt sind.

![Regeln für die Ereignisweiterleitung in der Datenerfassungs-Benutzeroberfläche](../../images/ui/event-forwarding/overview/rules.png)

#### Tokenisierung von Datenelementen {#tokenization}

In Tag-Regeln werden Datenelemente mit einem -Token versehen. `%` am Anfang und am Ende des Datenelementnamens (z. B.: `%viewportHeight%`). In den Ereignisweiterleitungsregeln werden Datenelemente stattdessen mit einem -Token versehen `{{` am Anfang und `}}` am Ende des Datenelementnamens (z. B.: `{{viewportHeight}}`).

![Beispiel eines Datenelements vom Pfadtyp für die Ereignisweiterleitung](../../images/ui/event-forwarding/overview/tokenization.png)

#### Sequenz von Regelaktionen {#action-sequencing}

Die [!UICONTROL Aktionen] -Abschnitt einer Ereignisweiterleitungsregel immer sequenziell ausgeführt wird. Stellen Sie beim Speichern einer Regel sicher, dass die Reihenfolge der Aktionen korrekt ist. Diese Ausführungssequenz kann nicht asynchron mit Tags ausgeführt werden.

## Geheime Daten {#secrets}

Mit der Ereignisweiterleitung können Sie Geheimnisse erstellen, verwalten und speichern, die für die Authentifizierung bei den Servern verwendet werden können, an die Sie Daten senden. Siehe Handbuch unter [Geheimnisse](./secrets.md) zu den verschiedenen Arten verfügbarer geheimer Typen und deren Implementierung in der Benutzeroberfläche.

## Nächste Schritte

Dieses Dokument bietet eine allgemeine Einführung in die Ereignisweiterleitung. Weitere Informationen zum Einrichten dieser Funktion für Ihr Unternehmen finden Sie unter [Erste Schritte](./getting-started.md).
