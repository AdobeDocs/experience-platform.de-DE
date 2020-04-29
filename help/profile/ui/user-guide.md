---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Handbuch zum Echtzeit-Profil
topic: guide
translation-type: tm+mt
source-git-commit: ab289f07475abcbe966c723423825fd392eb3615

---


# Handbuch zum Echtzeit-Profil

Das Echtzeit-Kundenprofil erstellt eine ganzheitliche Sicht Ihrer einzelnen Kunden und fasst Daten aus mehreren Kanälen (einschließlich Online-, Offline-, CRM- und Drittanbieter-Daten) zusammen.

Dieses Dokument dient als Leitfaden für die Interaktion mit Echtzeit-Kundendaten in der Benutzeroberfläche der Adobe Experience Platform.

## Erste Schritte

Dieses Benutzerhandbuch erfordert ein Verständnis der verschiedenen Experience Platform-Dienste, die mit der Verwaltung von Echtzeit-Kundendaten verbunden sind. Bevor Sie dieses Benutzerhandbuch lesen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

* [Echtzeit-Profil](../home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [Identitätsdienst](../../identity-service/home.md): Ermöglicht Kunden-Profil in Echtzeit durch Überbrückung von Identitäten aus unterschiedlichen Datenquellen, die in Plattform integriert werden.
* [Erlebnisdatenmodell (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Plattform Kundenerlebnisdaten organisiert.

## Profil – Übersicht

Klicken Sie in der Benutzeroberfläche [der](http://platform.adobe.com)Experience Platform im linken Navigationsbereich auf **Profile** , um die Registerkarte _Übersicht_ im Arbeitsbereich _Profile_ zu öffnen. Auf dieser Registerkarte werden verschiedene Widgets angezeigt, die allgemeine Informationen zum Profil-Store enthalten, darunter die gesamte adressierbare Audience, die Anzahl der in der letzten Woche erfassten Profil-Datensätze sowie Statistiken zu erfolgreichen und fehlgeschlagenen Datensätzen für den gleichen Zeitraum.

![](../images/user-guide/profile-overview.png)

## Beispiele für Ansicht Profil

Klicken Sie auf **Durchsuchen** , um eine Liste der verfügbaren Profil Ansicht. Dieses Beispiel umfasst bis zu 50 Profil Ihrer gesamten [Profil-Anzahl](#profile-count). Die Beispiele werden durch einen automatischen Auftrag aktualisiert, der neue Profil-Daten während der Erfassung abruft. Jedes aufgelistete Profil zeigt seine ID, seinen Vornamen, seinen Nachnamen und seine persönliche E-Mail-Adresse an. Wenn Sie auf die ID eines aufgelisteten Profils klicken, werden dessen Details im [Profil-Viewer](#profile-viewer)angezeigt.

![](../images/user-guide/profile-samples.png)

Sie können die in der Liste angezeigten Attribute anpassen, indem Sie auf das Symbol für die Spaltenauswahl klicken. Dadurch wird eine Dropdown-Liste mit allgemeinen Profil-Attributen angezeigt, die Sie hinzufügen oder entfernen können.

![](../images/user-guide/column-selector.png)

### Anzahl der Profil {#profile-count}

Die Anzahl der Profil zeigt die Gesamtzahl der Profil an, die Ihr Unternehmen in Experience Platform hat, nachdem die standardmäßige Zusammenführungsrichtlinie Ihres Unternehmens Profil-Fragmente zusammengeführt hat, um für jeden einzelnen Kunden ein Profil zu bilden. Mit anderen Worten, Ihr Unternehmen verfügt möglicherweise über mehrere Produktfragmente, die sich auf einen einzelnen Profil beziehen, der mit Ihrer Marke über verschiedene Kanal hinweg interagiert. Diese Fragmente werden jedoch zusammengeführt (gemäß der standardmäßigen Fusionsrichtlinie) und geben ein &quot;1&quot;-Profil zurück, da sie alle mit derselben Person zusammenhängen.

Die Profil-Anzahl umfasst auch Profil mit Attributen (Datensatzdaten) sowie Profil (wie Adobe Analytics-Profil), die nur Zeitreihendaten (Ereignis) enthalten. Die Anzahl wird regelmäßig aktualisiert, um eine aktuelle Gesamtanzahl von Profilen innerhalb der Plattform bereitzustellen. Wenn eine Erfassung von Profilen die Anzahl um mehr als 5 % erhöht oder verringert, wird automatisch ein Auftrag ausgelöst, um die Anzahl zu aktualisieren. Wenn Ihr Unternehmen Streaming-Erfassung verwendet, sind die Aufträge für die Erfassung neu erfasster Daten für jede Stunde geplant.

![](../images/user-guide/profile-count.png)

### Profil-Suche

Wenn Sie eine verknüpfte Identität für ein bestimmtes Profil kennen (z. B. seine E-Mail-Adresse), können Sie dieses Profil nachschlagen, indem Sie auf &quot; **Profil** suchen&quot;klicken. Dies ist die zuverlässigste Möglichkeit, auf ein bestimmtes Profil zuzugreifen, unabhängig davon, ob es in der Liste von Beispielen angezeigt wird.

![](../images/user-guide/find-a-profile.png)

Wählen Sie im angezeigten Dialogfeld einen entsprechenden ID-Namensraum aus der Dropdown-Liste (&quot;E-Mail&quot; in diesem Beispiel) und geben Sie den ID-Wert unten ein, bevor Sie auf **OK** klicken. Wenn Sie die Informationen zum Targeting-Profil gefunden haben, werden diese wie im nächsten Abschnitt beschrieben im Profil-Viewer angezeigt.

![](../images/user-guide/find-a-profile-details.png)

### Profilansicht {#profile-viewer}

Wenn Sie ein bestimmtes Profil auswählen oder suchen, wird der Bildschirm &quot; _Details_ &quot;des Profil-Viewers geöffnet. Auf dieser Seite finden Sie Informationen zum ausgewählten Profil, wie z. B. die Grundattribute des Profils, verknüpfte Identitäten und verfügbare Kanal. Die angezeigten Profil-Informationen wurden aus mehreren Profil-Fragmenten zusammengeführt, um eine Ansicht des jeweiligen Kunden zu bilden.

![](../images/user-guide/profile-viewer-detail.png)

Der Profil-Viewer bietet außerdem Registerkarten, mit denen Sie mit diesem Profil verbundene Ereignis und Segmentmitgliedschaften, sofern vorhanden, Ansichten durchführen können.

![](../images/user-guide/profile-viewer-events-seg.png)

## Zusammenführungsrichtlinien

Klicken Sie auf Richtlinien **zusammenführen** , um eine Liste der zu Ihrem Unternehmen gehörenden Zusammenführungsrichtlinien Ansicht. Jede aufgelistete Richtlinie zeigt ihren Namen an, unabhängig davon, ob es sich um die standardmäßige Zusammenführungsrichtlinie handelt oder nicht, und das Schema, für das sie gilt.

![](../images/user-guide/profile-merge-policies.png)

Weitere Informationen zum Arbeiten mit Zusammenführungsrichtlinien in der Benutzeroberfläche finden Sie im Benutzerhandbuch [](merge-policies.md)&quot;Richtlinien zusammenführen&quot;.

## Vereinigung Schema

Klicken Sie auf **Vereinigung Schema** , um die Schema der Vereinigung für Ihren Profil-Datenspeicher Ansicht. Ein Vereinigung-Schema ist eine Zusammenführung aller Erlebnis-Datenmodellfelder (XDM) derselben Klasse, deren Schema für die Verwendung im Echtzeit-Customer-Profil aktiviert wurden. Klicken Sie auf eine Klasse in der linken Liste, um die Struktur des Schemas &quot;Vereinigung&quot;auf der Arbeitsfläche Ansicht.

![](../images/user-guide/profile-union-schema.png)

Weitere Informationen zu Schemas der Vereinigung und ihrer Rolle im Echtzeit-Profil finden Sie im Abschnitt zu Schemas zur Vereinigung im [Schema-Kompositionshandbuch](../../xdm/schema/composition.md) .

## Nächste Schritte

Durch Lesen dieses Handbuchs wissen Sie jetzt, wie Sie Ihre Profil-Daten mithilfe der Experience Platform-Benutzeroberfläche Ansicht und verwalten. Informationen zur Nutzung von Echtzeit-Kundendaten zur Erstellung von Audiencen-Profilen finden Sie in der [Segmentierungsdokumentation](../../segmentation/home.md).