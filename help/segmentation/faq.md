---
title: Häufig gestellte Fragen zu Zielgruppen
description: Erfahren Sie mehr über Antworten auf häufig gestellte Fragen zu Zielgruppen und anderen segmentierungsbezogenen Konzepten.
source-git-commit: 9a72d85bfb592012b36826135e24d28983f92e40
workflow-type: tm+mt
source-wordcount: '1935'
ht-degree: 52%

---


# Häufig gestellte Fragen

Adobe Experience Platform [!DNL Segmentation Service] bietet eine Benutzeroberfläche und eine RESTful-API, mit der Sie anhand von Segmentdefinitionen oder anderen Quellen aus Ihren [!DNL Real-Time Customer Profile]-Daten Zielgruppen erstellen können. Diese Zielgruppen werden zentral auf Platform konfiguriert und gepflegt und stehen für jede Adobe-Lösung zur Verfügung. Im Folgenden finden Sie eine Liste häufig gestellter Fragen zu Zielgruppen und Segmentierung.

## Audience Portal

Im folgenden Abschnitt werden Fragen im Zusammenhang mit Audience Portal aufgeführt.

### Habe ich Zugriff auf Audience Portal und die Zielgruppenkomposition?

Audience Portal und die Zielgruppenkomposition stehen allen Kundinnen und Kunden von Real-Time CDP Prime und Ultimate (B2C-, B2B- und B2P-Editionen) sowie Journey Optimizer Select, Prime, Ultimate Starter und Ultimate zur Verfügung.

Zu diesem Zeitpunkt werden nur profilbasierte Zielgruppen unterstützt. Unterstützung für kontobasierte Zielgruppen wird in einer späteren Version hinzugefügt.

### Werden extern generierte, vordefinierte Zielgruppen von Audience Portal unterstützt?

Ja, extern generierte, vordefinierte Zielgruppen werden in Audience Portal unterstützt. Zu diesem Zeitpunkt können Sie eine extern generierte Zielgruppe über eine CSV-Datei importieren. Zukünftig können Sie Zielgruppen über Batch- oder Streaming-basierte Quell-Connectoren hinzufügen.

### Kann ich extern generierte Zielgruppendaten mit einem vorhandenen Profil in Platform abstimmen?

Ja, die extern generierte Zielgruppe wird mit dem in Platform vorhandenen Profil zusammengeführt, wenn die primären Kennungen übereinstimmen. Die Abstimmung dieser Daten kann bis zu 24 Stunden dauern. Wenn noch keine Profildaten vorhanden sind, wird bei der Aufnahme der Daten ein neues Profil erstellt.

## Kann ich eine extern generierte Zielgruppe verwenden, um andere Zielgruppen zu erstellen?

Ja, alle extern generierten Zielgruppen werden im Zielgruppeninventar angezeigt und können verwendet werden, wenn Zielgruppen innerhalb des [Segment Builders](./ui/segment-builder.md) erstellt werden.

### Kann ich extern hochgeladene Attribute als Teil der Segmentierung verwenden?

Nein, das ist nicht möglich. Profilattribute sind als dauerhafte Attribute gedacht, während extern erstellte Zielgruppendaten, die hochgeladen werden, nur Kontextdaten enthalten, die mit dieser extern generierten Zielgruppe verknüpft sind.

Die Kontextdaten oder Anreicherungsattribute der extern generierten Zielgruppe sind **nicht** ausreichend lang beständig, da ihr Lebenszyklus an die hochgeladene Zielgruppe gebunden ist. Da diese Anreicherungsattribute von vorübergehender Dauer sind, stehen sie deswegen **nicht** zur Verfügung, um in der Segmentierung verwendet zu werden.

Wenn Sie Ihre Zielgruppen jedoch Batch- oder dateibasierten Zielen zuordnen, können Sie diese extern generierten Anreicherungsattribute verwenden, um Ihre Zielgruppen und weitere nachgelagerte Aktivierungen zu erweitern.

Weitere Informationen zu dieser Funktion finden Sie im Handbuch zum [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](../destinations/ui/activate-batch-profile-destinations.md#mapping).

### Kann ich extern generierte Zielgruppen für Adobe Journey Optimizer aktivieren?

Zu diesem Zeitpunkt nicht. Diese Funktion wird jedoch demnächst verfügbar sein.

### Kann ich eine extern generierte Zielgruppe löschen?

Zu diesem Zeitpunkt nicht. Sie können diese Zielgruppe stattdessen entweder deaktivieren oder archivieren. In diesem Zustand werden Profile für nachgelagerte Anwendungen **weiterhin aktiv** bleiben. Die Unterstützung für das Löschen extern generierter Zielgruppen wird in einer nachfolgenden Version hinzugefügt.

### Was stellen die verschiedenen Lebenszyklusstatus dar?

In der folgenden Tabelle werden die verschiedenen Lebenszyklusstatus, ihre Darstellung, wo Zielgruppen mit diesem Status verwendet werden können, sowie die Auswirkungen auf die Limits bei der Segmentierung erläutert.

| Land | Definition | In Audience Portal sichtbar? | In Zielen sichtbar? | Betrifft Segmentierungsbeschränkungen? | Auswirkungen auf dateibasierte Zielgruppen | Auswirkungen auf die Zielgruppenbewertung | In anderen Zielgruppen verwenden? |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Entwurf | Eine Zielgruppe im **Entwurf** state ist eine Zielgruppe, die sich noch in der Entwicklung befindet und noch nicht für andere Dienste verwendet werden kann. | Ja, aber kann ausgeblendet werden. | Nein | Ja | Kann während des Verfeinerungsprozesses importiert oder aktualisiert werden. | Kann ausgewertet werden, um genaue Veröffentlichungszahlen zu erhalten. | Ja, jedoch nicht empfohlen, verwendet zu werden. |
| Veröffentlicht | Eine Zielgruppe im **Veröffentlicht** state ist eine Zielgruppe, die für alle nachgelagerten Dienste verwendet werden kann. | Ja | Ja | Ja | Kann importiert oder aktualisiert werden. | Wird mit Batch-, Streaming- oder Edge-Segmentierung ausgewertet. | Ja |
| Inaktiv | Eine Zielgruppe im **Inaaktiv** state ist eine Zielgruppe, die derzeit nicht verwendet wird. Sie existiert weiterhin in Platform, wird aber **not** verwendet werden, bis es als Entwurf oder veröffentlicht markiert ist. | Nein, aber kann angezeigt werden. | Nein | Nein | Nein länger aktualisiert. | Wird von Platform nicht mehr bewertet oder aktualisiert. | Ja |
| Gelöscht | Eine Zielgruppe im **Gelöscht** state ist eine Zielgruppe, die gelöscht wurde. Das tatsächliche Löschen der Daten kann bis zu einigen Minuten dauern. | Nein | Nein | Nein | Zugrunde liegende Daten werden gelöscht. | Nach Abschluss des Löschvorgangs erfolgt keine Datenauswertung oder -ausführung. | Nein |

### Wie interagieren Audience Portal und die Zielgruppenkomposition mit der Veröffentlichung von Real-Time CDP-Partnerdaten?

Audience Portal und die Zielgruppenkomposition interagieren auf zwei Arten mit Partnerdaten:

1. Wenn Sie mithilfe der Prospect Profile-Klasse und des -Workflows eine von einem Partner bereitgestellte Interessensliste aufnehmen, werden die Interessierten **getrennt** von der Zusammenführung von Kundenprofilen im Profildienst gehalten. Dies bedeutet, dass Interessentenlisten **nicht** in Audience Portal und der Zielgruppenkomposition zur Verwendung angezeigt werden.
2. Wenn Sie zur Anreicherung von durch Partner bereitgestellten Attributen **vorhandene** Erstanbieterprofile nutzen, **werden** diese mit Partnerdaten angereicherten Zielgruppen sowohl in Audience Portal als auch in der Zielgruppenkomposition zur Verwendung angezeigt.

### Wie kann ich zusätzliche Attribute für meine Zielgruppen verwenden?

Mit Zielgruppen gibt es **two** verschiedene Arten zusätzlicher Attribute, die Sie hinzufügen können - Payload-Attribute (kontextbezogen) und Anreicherungsattribute.

Payload-Attribute sind Attribute, die als Teil des CSV-Uploads einer extern generierten Zielgruppe erfasst werden. Diese Attribute sind **not** in das Echtzeit-Kundenprofil aufgenommen, kann jedoch als Teil eines nachgelagerten Ziels verwendet werden.

Anreicherungsattribute sind Attribute, die aus einem Datensatz stammen und in der Zielgruppenkomposition mit einer Zielgruppe verbunden werden. Diese Attribute können derzeit nur in Adobe Journey Optimizer-Kampagnen verwendet werden. Die Unterstützung für Adobe Journey Optimizer-Journey wird in Kürze bereitgestellt, und die Unterstützung für nachgelagerte Ziele steht noch aus.

| Aktivierungskanal | Zielgruppen aus benutzerdefiniertem CSV-Upload | Zielgruppen aus Zielgruppenkomposition |
| --- | --- | --- |
| Real-Time CDP-Ziele | Sowohl die Payload-Attribute als auch die Zielgruppen können aktiviert werden. | Nur die Audience kann aktiviert werden. Anreicherungsattribute **cannot** aktiviert werden. |
| Adobe Journey Optimizer-Kampagnen | Weder die Audience noch die Payload-Attribute können aktiviert werden. | Sowohl die Zielgruppe als auch die Anreicherungsattribute können aktiviert werden. |

## Zielgruppeninventar

In den folgenden Abschnitten werden Fragen im Zusammenhang mit dem Zielgruppeninventar im Audience Portal aufgeführt.

### Benötige ich zusätzliche Berechtigungen, um die Funktionen des Zielgruppeninventars zu verwenden?

Nein, nicht. Solange Sie über Bearbeitungsberechtigungen für Zielgruppen verfügen, können Sie Ihre Ordner und Tags in Audience Portal erstellen, aktualisieren und verwalten. Weitere Informationen zum Verwalten von Berechtigungen finden Sie im Abschnitt [Berechtigungshandbuch verwalten](../access-control/ui/permissions.md).

### Gibt es eine Begrenzung für die Anzahl der Ordner, die ich erstellen kann?

Nein, die Anzahl der Ordner, die Sie erstellen können, ist nicht beschränkt. Weitere Informationen zu Ordnern finden Sie im Abschnitt [Zielgruppeninventarbereich](./ui/overview.md#folders) der Segmentation Service-Benutzeroberfläche - Übersicht.

### Gibt es eine Begrenzung für die Anzahl der Tags, die einer Zielgruppe hinzugefügt werden können?

Nein, die Anzahl der Tags, die einer Audience hinzugefügt werden können, ist unbegrenzt. Weitere Informationen zu Tags finden Sie im Abschnitt [Zielgruppeninventarbereich](./ui/overview.md#tags) der Segmentation Service-Benutzeroberfläche - Übersicht.

### Gibt es eine Begrenzung für die Anzahl der Tags, die ich erstellen kann?

Nein, die Anzahl der Tags, die Sie erstellen können, ist unbegrenzt. Sie können jedoch maximal **100** Kategorien, die für die Tags gelten sollen. Weitere Informationen zum Tag-Management finden Sie unter [Verwalten von Tags-Handbuch](../administrative-tags/ui/managing-tags.md).

### Kann ich beim Suchen nach einer Zielgruppe nach Name oder Tag in einem übergeordneten Ordner auch die zugehörigen untergeordneten Ordner durchsuchen?

Nein, dieses Verhalten wird nicht unterstützt. Sie können die Ansicht des Zielgruppeninventars jedoch ändern, um sie anzuzeigen **Alle Zielgruppen** und durchsuchen dann alle Ordner. Weitere Informationen zur Verwendung der Suche im Zielgruppen-Inventar finden Sie in der [Suchabschnitt](./ui/overview.md#search) der Segmentation Service-Benutzeroberfläche - Übersicht.

### Kann ich zum Zeitpunkt der Erstellung automatisch eine Zielgruppe einem Ordner zuweisen?

Zu diesem Zeitpunkt nicht. Diese Funktion kann jedoch in Zukunft verfügbar sein.

### Kann ich mehrere Zielgruppen gleichzeitig in einen Ordner verschieben?

Zu diesem Zeitpunkt nicht. Diese Funktion kann jedoch in Zukunft verfügbar sein.

## Zielgruppenkomposition

Im folgenden Abschnitt werden Fragen im Zusammenhang mit der Zielgruppenkomposition aufgeführt.

### Wann sollte ich die Zielgruppenkomposition anstelle von Segment Builder verwenden?

Sowohl die Zielgruppenkomposition als auch der Segment Builder haben beim Erstellen von Zielgruppen in Platform wichtige Rollen.

Der Segment Builder eignet sich besser für die Zielgruppe **Erstellung** (um eine Zielgruppe von Grund auf neu zu erstellen), während die Zielgruppenkomposition besser für die Zielgruppe geeignet ist **Kuratierung** (zur Erstellung neuer Zielgruppen auf der Basis einer existierenden Zielgruppe).

Die folgende Tabelle zeigt den Unterschied zwischen den beiden Diensten:

| Segment Builder | Zielgruppenkomposition |
| --------------- | -------------------- |
| <ul><li>Einzelstufige Zielgruppenerstellung</li><li>Erstellt die grundlegenden Bausteine von Zielgruppen aus Profil-, Zeitreihen- und Daten aus mehreren Entitäten</li><li>Wird zur Erstellung verwendet **one** audience</li></ul> | <ul><li>Mehrstufige Zielgruppenerstellung mit set-basierten Vorgängen</li><li>Verwendet die vom Segment Builder erstellten Zielgruppen und wendet Datenanreicherungsoptionen wie Profilattribute an</li><li>Wird zur Erstellung verwendet **multiple** Zielgruppen auf einmal</li></ul> |

Weitere Informationen zum Segment Builder finden Sie in der [Segment Builder-Handbuch](./ui/segment-builder.md). Weitere Informationen zur Zielgruppenkomposition finden Sie im Abschnitt [Handbuch zur Zielgruppenkomposition](./ui/audience-composition.md).

### Kann ich extern generierte Zielgruppen in der Zielgruppenkomposition verwenden?

Zu diesem Zeitpunkt nicht. Diese Funktion sollte jedoch demnächst verfügbar sein.

### Kann ich Zielgruppen von der Zielgruppenzusammensetzung an alle nachgelagerten Ziele und Kanäle senden?

Zu diesem Zeitpunkt nicht. Derzeit können Sie Zielgruppen aus der Zielgruppenkomposition in Adobe Journey Optimizer-Kampagnen und Real-Time CDP-Zielen verwenden. Adobe Journey Optimizer-Journeys werden in einer zukünftigen Version unterstützt.

### Gibt es Leitlinien in Bezug auf die Anzahl der Kompositionen?

Zu diesem Zeitpunkt können Sie nur **10** veröffentlichte Kompositionen pro Sandbox haben. Diese Grenze soll in einer zukünftigen Version erhöht werden.

### Welche Workflow-Limits gibt es für die Zielgruppenkomposition?

Die Platzierung der Kompositionskomponente folgt einer starren Struktur wie folgt:

1. Begonnen wird **immer** mit dem Block [!UICONTROL Zielgruppe], um die Startaktivität auszuwählen. Es kann maximal **ein** Block [!UICONTROL Zielgruppe] ausgewählt werden.
2. Es kann optional ein Block [!UICONTROL Ausschließen], der auf den Block [!UICONTROL Zielgruppe] folgt, hinzugefügt werden.
3. Es kann optional ein Block [!UICONTROL Anreichern] hinzugefügt werden, der auf den Block [!UICONTROL Ausschließen] folgt.
4. Es kann optional ein Block für den [!UICONTROL Rang] oder die [!UICONTROL Aufspaltung] hinzugefügt werden. Es kann **nur** einer dieser Blöcke pro Komposition ausgewählt werden.
5. Es sollte **immer** mit einem Block zum [!UICONTROL Speichern] abgeschlossen werden, um die Zielgruppe zu speichern.

Weitere Informationen zur Verwendung der Zielgruppenkomposition finden Sie im [Handbuch zur Benutzeroberfläche der Zielgruppenkomposition](./ui/audience-composition.md).

### Kann ich eine Zielgruppen-Komposition in einer anderen Komposition verwenden?

Nein, Zielgruppen, die mithilfe der Zielgruppen-Komposition erstellt wurden, können **nicht** als Eingabe in einer anderen Zielgruppen-Komposition verwendet werden.

### Wie funktioniert die Aufteilung in Zielgruppen-Kompositionen?

Durch die Aufteilung von Zielgruppen können Zielgruppen in weitere kleinere Gruppen unterteilt werden. Diese Aufteilung erzwingt, dass sich die Gruppen gegenseitig ausschließen. Wenn also ein Eintrag die Kriterien für mehrere Aufspaltungspfade erfüllt, wird ihm der **erste** Pfad von links und **keiner** der anderen Pfade zugewiesen.

Weiterführende Informationen zum Block „Aufspaltung“ finden Sie im [Handbuch zur Benutzeroberfläche der Zielgruppenkomposition](./ui/audience-composition.md#split).

### Kann ich alle Segmentierungstypen im Workflow „Zielgruppenkomposition“ verwenden?

Ja, alle Segmenttypen ([Batch-Segmentierung, Streaming-Segmentierung und Edge-Segmentierung](./home.md#evaluate-segments)) werden im Workflow „Zielgruppenkomposition“ unterstützt. Da Kompositionen jedoch derzeit nur einmal pro Tag ausgeführt werden, basiert das Ergebnis auf der Zielgruppenzugehörigkeit zum Zeitpunkt der Komposition, selbst wenn Streaming- oder Edge-bewertete Zielgruppen enthalten sind.

## Wie kann ich die Mitgliedschaft eines Profils in einer Zielgruppe bestätigen?

Um die Zielgruppenmitgliedschaft eines Profils zu bestätigen, besuchen Sie die Seite mit den Profildetails des Profils, das Sie bestätigen möchten. Wählen Sie **[!UICONTROL Attribute]** gefolgt von **[!UICONTROL JSON anzeigen]** aus, und Sie können bestätigen, dass das `segmentMembership`-Objekt die ID der Zielgruppe enthält.
