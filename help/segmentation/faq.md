---
title: Häufig gestellte Fragen zu Zielgruppen
description: Hier finden Sie Antworten auf häufig gestellte Fragen zu Audiences.
source-git-commit: 4dbd20dd3ac596052a3390eb6d3731fac7095c0d
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 0%

---


# Häufig gestellte Fragen

Adobe Experience Platform [!DNL Segmentation Service] bietet eine Benutzeroberfläche und RESTful-API, mit der Sie Zielgruppen über Segmentdefinitionen oder andere Quellen aus Ihrer [!DNL Real-Time Customer Profile] Daten. Diese Zielgruppen werden zentral in Platform konfiguriert und gepflegt und stehen für jede Adobe-Lösung zur Verfügung. Im Folgenden finden Sie eine Liste häufig gestellter Fragen zu Zielgruppen und zur Segmentierung.

## Habe ich Zugriff auf Audience Portal und die Zielgruppenkomposition?

Zielgruppenportal und Zielgruppenkomposition stehen allen Kunden von Real-Time CDP Prime und Ultimate (B2C-, B2B- und B2P-Editionen) sowie Journey Optimizer Select-, Prime-, Ultimate Starter- und Ultimate-Kunden zur Verfügung.

Zu diesem Zeitpunkt werden nur profilbasierte Zielgruppen unterstützt. Unterstützung für kontobasierte Zielgruppen wird in einer späteren Version hinzugefügt.

## Werden extern generierte vordefinierte Zielgruppen von Audience Portal unterstützt?

Ja, extern generierte vordefinierte Zielgruppen werden in Audience Portal unterstützt. Zu diesem Zeitpunkt können Sie eine extern generierte Zielgruppe über eine CSV-Datei importieren. Zukünftig können Sie Zielgruppen über Batch- oder Streaming-basierte Quell-Connectoren hinzufügen.

## Kann ich extern generierte Zielgruppendaten mit einem vorhandenen Profil in Platform abstimmen?

Ja, die extern generierte Zielgruppe wird mit dem vorhandenen Profil in Platform zusammengeführt, wenn die primären Kennungen übereinstimmen. Die Abstimmung dieser Daten kann bis zu 24 Stunden dauern. Wenn noch keine Profildaten vorhanden sind, wird bei der Erfassung der Daten ein neues Profil erstellt.

## Kann ich eine extern generierte Zielgruppe verwenden, um andere Zielgruppen zu erstellen?

Ja, alle extern generierten Zielgruppen werden im Zielgruppeninventar angezeigt und können beim Erstellen von Zielgruppen innerhalb der [Segment Builder](./ui/segment-builder.md).

## Kann ich extern hochgeladene Attribute als Teil der Segmentierung verwenden?

Nein, das kannst du nicht. Profilattribute sind dauerhafte Attribute, während extern erstellte Zielgruppendaten, die hochgeladen werden, nur Kontextdaten enthalten, die mit dieser extern generierten Zielgruppe verknüpft sind.

Die Kontextdaten oder Anreicherungsattribute der extern generierten Zielgruppe sind **not** Dauerhaft, da ihr Lebenszyklus an die hochgeladene Zielgruppe gebunden ist. Diese Anreicherungsattribute sind daher aufgrund ihrer Übergangs-Natur **not** zur Verwendung in der Segmentierung verfügbar.

Wenn Sie Ihre Zielgruppen jedoch Batch- oder dateibasierten Zielen zuordnen, können Sie diese extern generierten Anreicherungsattribute verwenden, um Ihre Zielgruppen und weitere nachgelagerte Aktivierungen zu erweitern.

Weitere Informationen zu dieser Funktion finden Sie im Handbuch unter [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](../destinations/ui/activate-batch-profile-destinations.md#mapping).

## Kann ich extern generierte Zielgruppen für Adobe Journey Optimizer aktivieren?

Zu diesem Zeitpunkt nein. Diese Funktion wird jedoch in naher Zukunft verfügbar sein.

## Kann ich eine extern generierte Zielgruppe löschen?

Zu diesem Zeitpunkt nein. Sie können diese Zielgruppe stattdessen entweder deaktivieren oder archivieren. In diesem Status werden Profile **will** für nachgelagerte Anwendungen weiterhin aktiv bleiben. Die Unterstützung für das Löschen extern generierter Zielgruppen wird in einer nachfolgenden Version hinzugefügt.

## Wie interagieren Audience Portal und die Zielgruppenkomposition mit der Veröffentlichung von Real-Time CDP-Partnerdaten?

Audience Portal und die Zielgruppenkomposition interagieren auf zwei Arten mit Partnerdaten:

1. Wenn Sie mithilfe der Prospect Profile-Klasse und des Workflows eine von einem Partner bereitgestellte Interessensliste erfassen, werden die Interessenten beibehalten **separat** aus der Zusammenführung von Kundenprofilen in Profil Service. Dies bedeutet, dass Interessenten-Listen **not** werden entweder in Audience Portal oder in Audience Komposition zur Verwendung angezeigt.
2. Wenn Sie zur Anreicherung von durch Partner bereitgestellten Attributen nutzen **vorhandene** Erstanbieterprofile, diese mit Partnerdaten angereicherten Zielgruppen **will** werden sowohl in Audience Portal als auch in der Zielgruppenkomposition zur Verwendung angezeigt.

## Kann ich extern generierte Zielgruppen in der Zielgruppenkomposition verwenden?

Zu diesem Zeitpunkt nein. Diese Funktion dürfte jedoch in naher Zukunft verfügbar sein.

## Kann ich Zielgruppen von der Zielgruppenzusammensetzung an alle nachgelagerten Ziele und Kanäle senden?

Zu diesem Zeitpunkt nein. Derzeit können Sie Zielgruppen aus der Zielgruppenkomposition in Adobe Journey Optimizer-Kampagnen und Echtzeit-CDP-Zielen verwenden. Adobe Journey Optimizer-Journey werden in einer zukünftigen Version unterstützt.

## Gibt es Limits in Bezug auf die Anzahl der Kompositionen?

Zu diesem Zeitpunkt können Sie **10** veröffentlichte Kompositionen pro Sandbox. Dieser Schutzmechanismus soll in einer zukünftigen Version erhöht werden.

## Welche Workflow-Limits gibt es für die Zielgruppenkomposition?

Die Platzierung der Kompositionskomponente folgt einer starren Struktur wie folgt:

1. You **always** beginnt mit der [!UICONTROL Zielgruppe] -Block, um Ihre Startaktivität auszuwählen. Sie können maximal **one** [!UICONTROL Zielgruppe] blockieren.
2. Sie können optional eine [!UICONTROL Ausschließen] -Block, der auf [!UICONTROL Zielgruppe] blockieren.
3. Sie können optional eine [!UICONTROL Anreichern] -Block, der auf [!UICONTROL Ausschließen] blockieren.
4. Sie können optional eine [!UICONTROL Rang] oder [!UICONTROL Aufspaltung] blockieren. Sie können **only** einen dieser Blöcke pro Komposition haben.
5. You **always** mit [!UICONTROL Speichern] blockieren, um Ihre Audience zu speichern.

Weitere Informationen zur Verwendung der Zielgruppenkomposition finden Sie im Abschnitt [Handbuch zur Benutzeroberfläche für Zielgruppenkomposition](./ui/audience-composition.md).

## Kann ich eine Zielgruppenkomposition in einer anderen Komposition verwenden?

Nein, Zielgruppen, die mithilfe der Zielgruppenkomposition erstellt wurden **cannot** als Eingabe in einer anderen Zielgruppenzusammensetzung verwendet werden.

## Wie funktioniert die Aufteilung in Zielgruppenkomposition?

Durch die Zielgruppenteilung können Sie Ihre Zielgruppe weiter in kleinere Gruppen unterteilen. Diese Aufteilung zwingt zur gegenseitigen Exklusivität zwischen den Gruppen. Wenn also ein Datensatz die Kriterien für mehrere Aufspaltungspfade erfüllt, wird ihm der **first** Pfad von links und **not** einem der anderen Pfade zugewiesen.

Weiterführende Informationen zum Baustein &quot;Aufspaltung&quot;finden Sie im Abschnitt [Handbuch zur Benutzeroberfläche für Zielgruppenkomposition](./ui/audience-composition.md#split).

## Kann ich alle Segmentierungstypen im Workflow Zielgruppenkomposition verwenden?

Ja, alle Segmentierungstypen ([Batch-Segmentierung, Streaming-Segmentierung und Kantensegmentierung](./home.md#evaluate-segments)) werden im Workflow Zielgruppenkomposition unterstützt. Da Kompositionen jedoch derzeit nur einmal pro Tag ausgeführt werden, basiert das Ergebnis auf der Zielgruppenzugehörigkeit zum Zeitpunkt der Komposition, selbst wenn Streaming- oder Edge-bewertete Zielgruppen enthalten sind.

## Wie kann ich die Mitgliedschaft eines Profils in einer Zielgruppe bestätigen?

Um die Zielgruppenmitgliedschaft eines Profils zu bestätigen, besuchen Sie die Seite mit den Profildetails des Profils, das Sie bestätigen möchten. Auswählen **[!UICONTROL Attribute]**, gefolgt von **[!UICONTROL JSON anzeigen]** und Sie können bestätigen, dass `segmentMembership` -Objekt enthält die Kennung der Audience.
