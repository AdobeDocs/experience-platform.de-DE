---
title: Häufig gestellte Fragen zu Zielgruppen
description: Hier finden Sie Antworten auf häufig gestellte Fragen zu Zielgruppen.
source-git-commit: 4dbd20dd3ac596052a3390eb6d3731fac7095c0d
workflow-type: ht
source-wordcount: '996'
ht-degree: 100%

---


# Häufig gestellte Fragen

Adobe Experience Platform [!DNL Segmentation Service] bietet eine Benutzeroberfläche und eine RESTful-API, mit der Sie anhand von Segmentdefinitionen oder anderen Quellen aus Ihren [!DNL Real-Time Customer Profile]-Daten Zielgruppen erstellen können. Diese Zielgruppen werden zentral auf Platform konfiguriert und gepflegt und stehen für jede Adobe-Lösung zur Verfügung. Im Folgenden finden Sie eine Liste häufig gestellter Fragen zu Zielgruppen und Segmentierung.

## Habe ich Zugriff auf Audience Portal und die Zielgruppenkomposition?

Audience Portal und die Zielgruppenkomposition stehen allen Kundinnen und Kunden von Real-Time CDP Prime und Ultimate (B2C-, B2B- und B2P-Editionen) sowie Journey Optimizer Select, Prime, Ultimate Starter und Ultimate zur Verfügung.

Zu diesem Zeitpunkt werden nur profilbasierte Zielgruppen unterstützt. Unterstützung für kontobasierte Zielgruppen wird in einer späteren Version hinzugefügt.

## Werden extern generierte, vordefinierte Zielgruppen von Audience Portal unterstützt?

Ja, extern generierte, vordefinierte Zielgruppen werden in Audience Portal unterstützt. Zu diesem Zeitpunkt können Sie eine extern generierte Zielgruppe über eine CSV-Datei importieren. Zukünftig können Sie Zielgruppen über Batch- oder Streaming-basierte Quell-Connectoren hinzufügen.

## Kann ich extern generierte Zielgruppendaten mit einem vorhandenen Profil in Platform abstimmen?

Ja, die extern generierte Zielgruppe wird mit dem in Platform vorhandenen Profil zusammengeführt, wenn die primären Kennungen übereinstimmen. Die Abstimmung dieser Daten kann bis zu 24 Stunden dauern. Wenn noch keine Profildaten vorhanden sind, wird bei der Aufnahme der Daten ein neues Profil erstellt.

## Kann ich eine extern generierte Zielgruppe verwenden, um andere Zielgruppen zu erstellen?

Ja, alle extern generierten Zielgruppen werden im Zielgruppeninventar angezeigt und können verwendet werden, wenn Zielgruppen innerhalb des [Segment Builders](./ui/segment-builder.md) erstellt werden.

## Kann ich extern hochgeladene Attribute als Teil der Segmentierung verwenden?

Nein, das ist nicht möglich. Profilattribute sind als dauerhafte Attribute gedacht, während extern erstellte Zielgruppendaten, die hochgeladen werden, nur Kontextdaten enthalten, die mit dieser extern generierten Zielgruppe verknüpft sind.

Die Kontextdaten oder Anreicherungsattribute der extern generierten Zielgruppe sind **nicht** ausreichend lang beständig, da ihr Lebenszyklus an die hochgeladene Zielgruppe gebunden ist. Da diese Anreicherungsattribute von vorübergehender Dauer sind, stehen sie deswegen **nicht** zur Verfügung, um in der Segmentierung verwendet zu werden.

Wenn Sie Ihre Zielgruppen jedoch Batch- oder dateibasierten Zielen zuordnen, können Sie diese extern generierten Anreicherungsattribute verwenden, um Ihre Zielgruppen und weitere nachgelagerte Aktivierungen zu erweitern.

Weitere Informationen zu dieser Funktion finden Sie im Handbuch zum [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](../destinations/ui/activate-batch-profile-destinations.md#mapping).

## Kann ich extern generierte Zielgruppen für Adobe Journey Optimizer aktivieren?

Zu diesem Zeitpunkt nicht. Diese Funktion wird jedoch demnächst verfügbar sein.

## Kann ich eine extern generierte Zielgruppe löschen?

Zu diesem Zeitpunkt nicht. Sie können diese Zielgruppe stattdessen entweder deaktivieren oder archivieren. In diesem Zustand werden Profile für nachgelagerte Anwendungen **weiterhin aktiv** bleiben. Die Unterstützung für das Löschen extern generierter Zielgruppen wird in einer nachfolgenden Version hinzugefügt.

## Wie interagieren Audience Portal und die Zielgruppenkomposition mit der Veröffentlichung von Real-Time CDP-Partnerdaten?

Audience Portal und die Zielgruppenkomposition interagieren auf zwei Arten mit Partnerdaten:

1. Wenn Sie mithilfe der Prospect Profile-Klasse und des -Workflows eine von einem Partner bereitgestellte Interessensliste aufnehmen, werden die Interessierten **getrennt** von der Zusammenführung von Kundenprofilen im Profildienst gehalten. Dies bedeutet, dass Interessentenlisten **nicht** in Audience Portal und der Zielgruppenkomposition zur Verwendung angezeigt werden.
2. Wenn Sie zur Anreicherung von durch Partner bereitgestellten Attributen **vorhandene** Erstanbieterprofile nutzen, **werden** diese mit Partnerdaten angereicherten Zielgruppen sowohl in Audience Portal als auch in der Zielgruppenkomposition zur Verwendung angezeigt.

## Kann ich extern generierte Zielgruppen in der Zielgruppenkomposition verwenden?

Zu diesem Zeitpunkt nicht. Diese Funktion sollte jedoch demnächst verfügbar sein.

## Kann ich Zielgruppen von der Zielgruppenzusammensetzung an alle nachgelagerten Ziele und Kanäle senden?

Zu diesem Zeitpunkt nicht. Derzeit können Sie Zielgruppen aus der Zielgruppenkomposition in Adobe Journey Optimizer-Kampagnen und Real-Time CDP-Zielen verwenden. Adobe Journey Optimizer-Journeys werden in einer zukünftigen Version unterstützt.

## Gibt es Leitlinien in Bezug auf die Anzahl der Kompositionen?

Zu diesem Zeitpunkt können Sie nur **10** veröffentlichte Kompositionen pro Sandbox haben. Diese Grenze soll in einer zukünftigen Version erhöht werden.

## Welche Workflow-Limits gibt es für die Zielgruppenkomposition?

Die Platzierung der Kompositionskomponente folgt einer starren Struktur wie folgt:

1. Begonnen wird **immer** mit dem Block [!UICONTROL Zielgruppe], um die Startaktivität auszuwählen. Es kann maximal **ein** Block [!UICONTROL Zielgruppe] ausgewählt werden.
2. Es kann optional ein Block [!UICONTROL Ausschließen], der auf den Block [!UICONTROL Zielgruppe] folgt, hinzugefügt werden.
3. Es kann optional ein Block [!UICONTROL Anreichern] hinzugefügt werden, der auf den Block [!UICONTROL Ausschließen] folgt.
4. Es kann optional ein Block für den [!UICONTROL Rang] oder die [!UICONTROL Aufspaltung] hinzugefügt werden. Es kann **nur** einer dieser Blöcke pro Komposition ausgewählt werden.
5. Es sollte **immer** mit einem Block zum [!UICONTROL Speichern] abgeschlossen werden, um die Zielgruppe zu speichern.

Weitere Informationen zur Verwendung der Zielgruppenkomposition finden Sie im [Handbuch zur Benutzeroberfläche der Zielgruppenkomposition](./ui/audience-composition.md).

## Kann ich eine Zielgruppen-Komposition in einer anderen Komposition verwenden?

Nein, Zielgruppen, die mithilfe der Zielgruppen-Komposition erstellt wurden, können **nicht** als Eingabe in einer anderen Zielgruppen-Komposition verwendet werden.

## Wie funktioniert die Aufteilung in Zielgruppen-Kompositionen?

Durch die Aufteilung von Zielgruppen können Zielgruppen in weitere kleinere Gruppen unterteilt werden. Diese Aufteilung erzwingt, dass sich die Gruppen gegenseitig ausschließen. Wenn also ein Eintrag die Kriterien für mehrere Aufspaltungspfade erfüllt, wird ihm der **erste** Pfad von links und **keiner** der anderen Pfade zugewiesen.

Weiterführende Informationen zum Block „Aufspaltung“ finden Sie im [Handbuch zur Benutzeroberfläche der Zielgruppenkomposition](./ui/audience-composition.md#split).

## Kann ich alle Segmentierungstypen im Workflow „Zielgruppenkomposition“ verwenden?

Ja, alle Segmenttypen ([Batch-Segmentierung, Streaming-Segmentierung und Edge-Segmentierung](./home.md#evaluate-segments)) werden im Workflow „Zielgruppenkomposition“ unterstützt. Da Kompositionen jedoch derzeit nur einmal pro Tag ausgeführt werden, basiert das Ergebnis auf der Zielgruppenzugehörigkeit zum Zeitpunkt der Komposition, selbst wenn Streaming- oder Edge-bewertete Zielgruppen enthalten sind.

## Wie kann ich die Mitgliedschaft eines Profils in einer Zielgruppe bestätigen?

Um die Zielgruppenmitgliedschaft eines Profils zu bestätigen, besuchen Sie die Seite mit den Profildetails des Profils, das Sie bestätigen möchten. Wählen Sie **[!UICONTROL Attribute]** gefolgt von **[!UICONTROL JSON anzeigen]** aus, und Sie können bestätigen, dass das `segmentMembership`-Objekt die ID der Zielgruppe enthält.
