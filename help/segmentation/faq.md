---
title: Häufig gestellte Fragen zu Zielgruppen
description: Erfahren Sie mehr über Antworten auf häufig gestellte Fragen zu Zielgruppen und anderen segmentierungsbezogenen Konzepten.
exl-id: 79d54105-a37d-43f7-adcb-97f2b8e4249c
source-git-commit: 27571f3ed57399eb588865e1a52e7569957ffbff
workflow-type: tm+mt
source-wordcount: '3976'
ht-degree: 23%

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

### Welche Berechtigungen benötige ich, um extern generierte Zielgruppen hochzuladen?

Um extern generierte Zielgruppen hochzuladen, benötigen Sie die Berechtigungen &quot;Zielgruppen/Segmente anzeigen&quot;, &quot;Zielgruppen/Segmente verwalten&quot;, &quot;Datensätze anzeigen&quot;, &quot;Datensätze verwalten&quot;, &quot;Quellen anzeigen&quot;und &quot;Quellen verwalten&quot;. Zum Hochladen extern generierter Zielgruppen sind keine bestimmten rollenbasierten Steuerelemente erforderlich.

### Was passiert, wenn ich eine extern generierte Zielgruppe hochlade?

Wenn Sie eine extern generierte Zielgruppe hochladen, werden die folgenden Elemente erstellt:

- Datensatz
   - Der Datensatz wird im Datensatzinventar angezeigt, und der Name des Datensatzes ist der **same** als Name der extern generierten Zielgruppe, die Sie hochgeladen haben.
- Batch-Auftrag
   - Ein Batch-Auftrag wird **automatisch** ausgeführt werden, wenn Sie eine extern generierte Zielgruppe hochladen. Das bedeutet, dass Sie **not** muss warten, bis der tägliche Segmentierungsauftrag ausgeführt wird, um die extern generierte Zielgruppe zu aktivieren.
- Ad-hoc-Schema
   - A **new** Das XDM-Schema wird für die Verwendung mit der extern generierten Zielgruppe erstellt. Die Felder in diesem XDM-Schema sind Namespaces zur Verwendung mit dem ebenfalls erstellten Datensatz.

### Woraus besteht eine extern generierte Zielgruppe und was passiert mit diesen Daten, wenn sie in Platform importiert werden?

Während des Workflows &quot;Externe Audience importieren&quot;müssen Sie angeben, welche Spalte in der CSV-Datei der **Primäre Identität**. Ein Beispiel für eine primäre Identität sind E-Mail-Adresse, ECID oder ein unternehmensspezifischer benutzerdefinierter Identitäts-Namespace.

Die mit dieser primären Identitätsspalte verknüpften Daten umfassen die **only** Daten, die an das Profil angehängt sind. Wenn keine vorhandenen Profile vorhanden sind, die mit den Daten in der primären Identitätsspalte übereinstimmen, wird ein neues Profil erstellt. Dieses Profil ist jedoch im Wesentlichen ein verwaistes Profil, da **no** -Attribute oder Erlebnisereignisse mit diesem Profil verknüpft sind.

Alle anderen Daten innerhalb der extern generierten Zielgruppe werden berücksichtigt **Payload-Attribute**. Diese Attribute können **only** zur Personalisierung und Anreicherung während der Aktivierung verwendet werden und **not** an ein Profil angehängt. Diese Attribute werden jedoch im Data Lake gespeichert.

Während beim Erstellen von Zielgruppen mit dem Segment Builder auf die extern generierte Zielgruppe verwiesen werden kann, können einzelne Profilattribute **cannot** verwendet werden.

### Kann ich extern generierte Zielgruppendaten mit einem vorhandenen Profil in Platform abstimmen?

Ja, die extern generierte Zielgruppe wird mit dem in Platform vorhandenen Profil zusammengeführt, wenn die primären Kennungen übereinstimmen. Die Abstimmung dieser Daten kann bis zu 24 Stunden dauern. Wenn noch keine Profildaten vorhanden sind, wird bei der Aufnahme der Daten ein neues Profil erstellt.

### Kann ich eine extern generierte Zielgruppe verwenden, um andere Zielgruppen zu erstellen?

Ja, alle extern generierten Zielgruppen werden im Zielgruppeninventar angezeigt und können verwendet werden, wenn Zielgruppen innerhalb des [Segment Builders](./ui/segment-builder.md) erstellt werden.

### Kann ich extern hochgeladene Attribute als Teil der Segmentierung verwenden?

Nein, das ist nicht möglich. Profilattribute sind als dauerhafte Attribute gedacht, während extern erstellte Zielgruppendaten, die hochgeladen werden, nur Kontextdaten enthalten, die mit dieser extern generierten Zielgruppe verknüpft sind.

Die Kontextdaten oder Anreicherungsattribute der extern generierten Zielgruppe sind **nicht** ausreichend lang beständig, da ihr Lebenszyklus an die hochgeladene Zielgruppe gebunden ist. Da diese Anreicherungsattribute von vorübergehender Dauer sind, stehen sie deswegen **nicht** zur Verfügung, um in der Segmentierung verwendet zu werden.

Wenn Sie Ihre Zielgruppen jedoch Batch- oder dateibasierten Zielen zuordnen, können Sie diese extern generierten Anreicherungsattribute verwenden, um Ihre Zielgruppen und weitere nachgelagerte Aktivierungen zu erweitern.

Weitere Informationen zu dieser Funktion finden Sie im Handbuch zum [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](../destinations/ui/activate-batch-profile-destinations.md#mapping).

### Gibt es eine spezifische Zusammenführungsrichtlinie für extern generierte Zielgruppen?

Die unternehmensspezifische standardmäßige Zusammenführungsrichtlinie wird beim Hochladen von extern generierten Zielgruppen automatisch angewendet. Sie können jedoch die Zusammenführungsrichtlinie ändern, die während des Import-Audience-Workflows auf die extern generierte Audience angewendet wird.

### Wo kann ich extern generierte Zielgruppen aktivieren?

Eine extern generierte Zielgruppe kann jedem RTCDP-Ziel zugeordnet und in Adobe Journey Optimizer-Kampagnen verwendet werden.

### Wie bald sind extern generierte Zielgruppen zur Aktivierung bereit?

Bei Aktivierung für ein Streaming-Ziel stehen die Daten aus der extern generierten Zielgruppe innerhalb von zwei Stunden zur Verfügung.

Wenn sie für ein Batch-Ziel aktiviert wird, werden die Daten aus der extern generierten Zielgruppe mit dem nächsten 24-Stunden-Segmentierungsauftrag synchronisiert.

### Kann ich eine extern generierte Zielgruppe löschen?

Ja! Extern generierte Zielgruppen können in Audience Portal gelöscht werden.

### Was sollte ich tun, wenn ich versehentlich eine extern generierte Zielgruppe hochgeladen habe?

Wenn Sie versehentlich eine extern generierte Audience hochgeladen haben und die Daten entfernen möchten, können Sie die mit der Audience verknüpften Profile löschen, indem Sie eine CSV-Datei mit einer Zeile und ohne Daten hochladen.

### Wie lange halten extern generierte Zielgruppen an?

Der aktuelle Datenablauf für extern generierte Zielgruppen lautet **30 Tage**. Diese Datengültigkeit wurde ausgewählt, um die Menge an überschüssigen Daten zu reduzieren, die in Ihrem Unternehmen gespeichert werden.

Nach Ablauf des Datenablaufzeitraums ist der zugehörige Datensatz weiterhin im Datensatzbestand sichtbar, Sie werden dies jedoch tun. **not** die Audience aktivieren können und die Profilanzahl als Null angezeigt wird.

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

## Lebenszyklusstatus {#lifecycle-states}

Im folgenden Abschnitt finden Sie Fragen zu Lebenszyklusstatus und Lebenszyklusstatusverwaltung in Audience Portal.

### Was stellen die verschiedenen Lebenszyklusstatus dar?

In der folgenden Tabelle werden die verschiedenen Lebenszyklusstatus, ihre Darstellung, wo Zielgruppen mit diesem Status verwendet werden können, sowie die Auswirkungen auf die Limits bei der Segmentierung erläutert.

| Land | Definition | In Audience Portal sichtbar? | In Zielen sichtbar? | Betrifft Segmentierungsbeschränkungen? | Auswirkungen auf dateibasierte Zielgruppen | Auswirkungen auf die Zielgruppenbewertung | In anderen Zielgruppen verwenden? | Bearbeitbar |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Entwurf | Eine Zielgruppe im **Entwurf** state ist eine Zielgruppe, die sich noch in der Entwicklung befindet und noch nicht für andere Dienste verwendet werden kann. | Ja, aber kann ausgeblendet werden. | Nein | Ja | Kann während des Verfeinerungsprozesses importiert oder aktualisiert werden. | Kann ausgewertet werden, um genaue Veröffentlichungszahlen zu erhalten. | Ja, jedoch nicht empfohlen, verwendet zu werden. | Ja |
| Veröffentlicht | Eine Zielgruppe im **Veröffentlicht** state ist eine Zielgruppe, die für alle nachgelagerten Dienste verwendet werden kann. | Ja | Ja | Ja | Kann importiert oder aktualisiert werden. | Wird mit Batch-, Streaming- oder Edge-Segmentierung ausgewertet. | Ja | Ja |
| Inaktiv | Eine Zielgruppe im **Inaaktiv** state ist eine Zielgruppe, die derzeit nicht verwendet wird. Sie existiert weiterhin in Platform, wird aber **not** verwendet werden, bis es als Entwurf oder veröffentlicht markiert ist. | Nein, aber kann angezeigt werden. | Nein | Nein | Wird nicht mehr aktualisiert. | Wird von Platform nicht mehr bewertet oder aktualisiert. | Ja | Ja |
| Gelöscht | Eine Zielgruppe im **Gelöscht** state ist eine Zielgruppe, die gelöscht wurde. Das tatsächliche Löschen der Daten kann bis zu einigen Minuten dauern. | Nein | Nein | Nein | Zugrunde liegende Daten werden gelöscht. | Nach Abschluss des Löschvorgangs erfolgt keine Datenauswertung oder -ausführung. | Nein | Nein |

### In welchen Status kann ich meine Zielgruppen bearbeiten?

Zielgruppen können in den folgenden Lebenszyklusstatus bearbeitet werden:

- **Entwurf**: Wenn eine Zielgruppe im Entwurfsstatus bearbeitet wird, bleibt sie im Entwurfsstatus, es sei denn, sie wird explizit veröffentlicht.
- **Veröffentlicht**: Wenn eine Zielgruppe im Veröffentlichungsstatus bearbeitet wird, bleibt sie veröffentlicht und die Zielgruppe wird automatisch aktualisiert.
- **Inaaktiv**: Wenn eine Zielgruppe im inaktiven Status bearbeitet wird, bleibt sie inaktiv. Dies bedeutet, dass sie weder bewertet noch aktualisiert wird. Wenn Sie die Audience aktualisieren müssen, müssen Sie die Audience veröffentlichen.

Nachdem eine Zielgruppe gelöscht wurde, **cannot** bearbeitet werden.

### In welchen Lebenszyklusstatus kann ich eine Zielgruppe verschieben?

Der mögliche Lebenszyklus gibt an, dass eine Zielgruppe je nach dem aktuellen Status der Zielgruppe verschoben werden kann.

![Ein Diagramm mit den möglichen Übergängen des Lebenszyklusstatus, die für Zielgruppen verfügbar sind.](./images/faq/lifecycle-state-transition.png)

Wenn Ihre Zielgruppe im Entwurfsstatus ist, können Sie sie entweder veröffentlichen oder löschen, wenn die Zielgruppe keine abhängigen Elemente aufweist.

Wenn sich Ihre Zielgruppe im Veröffentlichungsstatus befindet, können Sie sie deaktivieren oder löschen, wenn die Zielgruppe keine abhängigen Elemente aufweist.

Wenn Ihre Zielgruppe im inaktiven Status ist, können Sie sie entweder erneut veröffentlichen oder löschen, wenn die Zielgruppe keine abhängigen Elemente aufweist.

### Gibt es Einschränkungen für Zielgruppen in bestimmten Lebenszyklusstatus?

Zielgruppen im Veröffentlichungsstatus können nur dann in einen anderen Status verschoben werden, wenn die Zielgruppe **not** haben Abhängigkeiten. Wenn Ihre Zielgruppe also in einem nachgelagerten Dienst verwendet wird, kann sie nicht deaktiviert oder gelöscht werden.

Wenn eine Zielgruppe, die mithilfe der Batch-Segmentierung ausgewertet wird, erneut veröffentlicht wird, d. h. wenn eine Zielgruppe von inaktiv zu publiziert wechselt, wird die Zielgruppe aktualisiert **after** den täglichen Batch-Auftrag. Bei der ersten erneuten Veröffentlichung werden die Profile und Daten als **same** als die Zielgruppe inaktiv gemacht wurde.

### Wie setze ich eine Zielgruppe in den Entwurfsstatus?

Die Methode zum Einfügen einer Zielgruppe in den Entwurfsstatus hängt von der Herkunft der Zielgruppe ab.

Für Zielgruppen, die mit Segment Builder erstellt wurden, können Sie die Zielgruppe auf den Entwurfsstatus setzen, indem Sie &quot;[!UICONTROL Als Entwurf speichern]&quot;in Segment Builder.

Für in Zielgruppenkomposition erstellte Zielgruppen werden Zielgruppen bis zur Veröffentlichung automatisch als Entwurf gespeichert.

Zielgruppen, die extern erstellt werden, werden automatisch veröffentlicht.

Sobald sich eine Zielgruppe im Veröffentlichungsstatus befindet, **cannot** ändern Sie die ursprüngliche Zielgruppe wieder in den Entwurfsstatus. Wenn Sie die Zielgruppe jedoch kopieren, befindet sich die neu kopierte Zielgruppe im Entwurfsstatus.

### Wie platziere ich eine Zielgruppe in den Veröffentlichungsstatus?

Für Zielgruppen, die mit Segment Builder oder Zielgruppenkomposition erstellt wurden, können Sie die Zielgruppe auf den Veröffentlichungsstatus setzen, indem Sie &quot;[!UICONTROL Veröffentlichen]&quot; in den jeweiligen Benutzeroberflächen angezeigt.

Von außen erstellte Zielgruppen werden automatisch auf &quot;Publizieren&quot;gesetzt.

### Wie stelle ich eine Zielgruppe in den inaktiven Status?

Sie können eine veröffentlichte Zielgruppe in den inaktiven Status versetzen, indem Sie das Schnellaktionsmenü in Audience Portal öffnen und auf &quot;[!UICONTROL Deaktivieren]&quot;.

### Wie kann ich eine Zielgruppe erneut veröffentlichen?

>[!NOTE]
>
>Der Status &quot;Neu veröffentlicht&quot;entspricht dem Veröffentlichungsstatus für das Zielgruppenverhalten.

Sie können eine Zielgruppe erneut veröffentlichen, indem Sie eine Zielgruppe mit inaktivem Status auswählen, das Schnellaktionsmenü in Audience Portal öffnen und auswählen [!UICONTROL Veröffentlichen].

### Wie setze ich eine Zielgruppe in den gelöschten Status?

>[!IMPORTANT]
>
>Sie können nur Zielgruppen löschen, die **not** bei jeder nachgelagerten Aktivierung verwendet werden. Darüber hinaus können Sie keine Zielgruppe löschen, auf die in einer anderen Zielgruppe verwiesen wird. Wenn Sie Ihre Audience nicht löschen können, stellen Sie bitte sicher, dass Sie **not** Verwendung in nachfolgenden Diensten oder als Baustein einer anderen Zielgruppe.

Sie können eine Zielgruppe in den Löschstatus versetzen, indem Sie das Schnellaktionsmenü in Audience Portal öffnen und [!UICONTROL Löschen].

### Beeinflusst die Verwendung einer Zielgruppe als untergeordnete Zielgruppe die Transitionen des Lebenszyklusstatus?

>[!NOTE]
>
>Eine übergeordnete Zielgruppe ist eine Zielgruppe, die **uses** eine andere Zielgruppe als Abhängigkeit für die Zielgruppe.
>
>Eine untergeordnete Zielgruppe ist eine Zielgruppe, die **verwendet als** eine Abhängigkeit für die Zielgruppe.

Ja, die Verwendung einer Zielgruppe als untergeordnete Zielgruppe wirkt sich darauf aus, welche Lebenszyklusstatus von der untergeordneten und übergeordneten Zielgruppe übernommen werden können.

Damit eine untergeordnete Zielgruppe in den Veröffentlichungsstatus verschoben werden kann, muss die gesamte übergeordnete Zielgruppe **must** sich im Veröffentlichungsstatus befinden. Übergeordnete Zielgruppen können entweder veröffentlicht werden, bevor die untergeordnete Zielgruppe veröffentlicht wird, oder, falls der Benutzer dies bestätigt, automatisch veröffentlicht werden, wenn die untergeordnete Zielgruppe veröffentlicht wird.

Damit die übergeordnete Zielgruppe in den Status &quot;Inaktiv&quot;oder &quot;Gelöscht&quot;versetzt wird, müssen alle untergeordneten Zielgruppen **must** deaktiviert oder gelöscht werden.

### Kann ich auf eine Zielgruppe verweisen, die sich in einem anderen Lebenszyklusstatus befindet?

Ja! Wenn Ihre Zielgruppe sich derzeit im Entwurfsstatus befindet, können Sie auf Zielgruppen im Veröffentlichungsstatus oder im inaktiven Status verweisen. Um diese Audience jedoch zu veröffentlichen, müssen Sie **must** die anderen übergeordneten Zielgruppen veröffentlichen.

## Zielgruppeninventar

Im folgenden Abschnitt werden Fragen im Zusammenhang mit dem Zielgruppeninventar im Audience Portal aufgeführt.

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

Der Segment Builder eignet sich besser für die Zielgruppe **Erstellung** (um eine Zielgruppe von Grund auf neu zu erstellen), während die Zielgruppenkomposition besser für die Zielgruppe geeignet ist **Kuratierung und Personalisierung** (zur Erstellung neuer Zielgruppen auf der Basis einer existierenden Zielgruppe).

Die folgende Tabelle zeigt den Unterschied zwischen den beiden Diensten:

| Segment Builder | Zielgruppenkomposition |
| --------------- | -------------------- |
| <ul><li>Einzelstufige Zielgruppenerstellung</li><li>Erstellt die grundlegenden Bausteine von Zielgruppen aus Profil-, Zeitreihen- und Daten aus mehreren Entitäten</li><li>Wird zur Erstellung verwendet **one** audience</li></ul> | <ul><li>Mehrstufige Zielgruppenerstellung mit set-basierten Vorgängen</li><li>Verwendet die vom Segment Builder erstellten Zielgruppen und wendet Anreicherungsoptionen für Daten an, z. B. Profilattribute einordnen und in Unterzielgruppen unterteilen</li><li>Wird zur Erstellung verwendet **multiple** Zielgruppen auf einmal</li></ul> |

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
3. Sie können optional eine [!UICONTROL Anreichern] -Block, der auf [!UICONTROL Ausschließen] blockieren. Sie können **one** [!UICONTROL Anreichern] Block pro Komposition.
4. Es kann optional ein Block für den [!UICONTROL Rang] oder die [!UICONTROL Aufspaltung] hinzugefügt werden. Es kann **nur** einer dieser Blöcke pro Komposition ausgewählt werden.
5. Es sollte **immer** mit einem Block zum [!UICONTROL Speichern] abgeschlossen werden, um die Zielgruppe zu speichern.

Zusätzlich werden die folgenden Einschränkungen(?) bei Verwendung dieser Blöcke anwenden:

- Geteilter Block
   - Dieser Block unterstützt nur **Zeichenfolge** Datentypen. Der Aufspaltungsbaustein **not** unterstützt das Datum oder den booleschen Datentyp.
   - Außerdem bewirkt dieser Block **not** unterstützt Anreicherungsattribute.
- Block ausschließen
   - Dieser Block **not** unterstützt das Datum oder den booleschen Datentyp.
- Rang-Block
   - Dieser Block **not** unterstützt Anreicherungsattribute.

Weitere Informationen zur Verwendung der Zielgruppenkomposition finden Sie im [Handbuch zur Benutzeroberfläche der Zielgruppenkomposition](./ui/audience-composition.md).

### Wann werden Zielgruppen, die mit der Zielgruppenkomposition erstellt wurden, gespeichert und ausgewertet?

Zielgruppen werden automatisch gespeichert, während sie in der Zielgruppenkomposition erstellt werden. Die Erstellungszeit der Zielgruppe ist das erste Mal, dass diese automatische Speicherung erfolgt.

Nach der Erstellung der Audience kann die Auswertung bis zu 24 Stunden dauern.

### Wann kann ich die erstellte Zielgruppe verwenden?

Die in der Zielgruppenkomposition erstellte Zielgruppe wird **sofort** in Audience Portal angezeigt. Um es jedoch in Adobe Journey Optimizer verwenden zu können, müssen Sie mindestens 24 Stunden nach der Auswertung warten.

### Sind Auswertungsaufträge im Monitoring-Abschnitt sichtbar?

Derzeit sind Auswertungsaufträge **not** in der Monitoring-Benutzeroberfläche angezeigt.

### Kann ich eine Zielgruppen-Komposition in einer anderen Komposition verwenden?

Nein, Zielgruppen, die mithilfe der Zielgruppen-Komposition erstellt wurden, können **nicht** als Eingabe in einer anderen Zielgruppen-Komposition verwendet werden.

### Wie funktioniert die Aufteilung in Zielgruppen-Kompositionen?

Durch die Zielgruppenteilung können Sie Ihre Zielgruppe weiter in kleinere Gruppen unterteilen.

Bei der Aufteilung nach Attribut besteht eine gegenseitige Exklusivität zwischen den Gruppen. Wenn also ein Eintrag die Kriterien für mehrere Aufspaltungspfade erfüllt, wird ihm der **erste** Pfad von links und **keiner** der anderen Pfade zugewiesen.

Beim Aufteilen nach Prozentsatz werden Aufspaltungen **zufällig** getan. Dies bedeutet, dass die Profile zufällig jedem Pfad zugewiesen werden. Die Aufteilung ist **not** persistent sein, sodass sich das Profil bei jeder Auswertung in einer anderen Unterzielgruppe befinden könnte.

Weiterführende Informationen zum Block „Aufspaltung“ finden Sie im [Handbuch zur Benutzeroberfläche der Zielgruppenkomposition](./ui/audience-composition.md#split).

### Kann ich alle Segmentierungstypen im Workflow „Zielgruppenkomposition“ verwenden?

Ja, alle Segmenttypen ([Batch-Segmentierung, Streaming-Segmentierung und Edge-Segmentierung](./home.md#evaluate-segments)) werden im Workflow „Zielgruppenkomposition“ unterstützt. Da Kompositionen jedoch derzeit nur einmal pro Tag ausgeführt werden, basiert das Ergebnis auf der Zielgruppenzugehörigkeit zum Zeitpunkt der Komposition, selbst wenn Streaming- oder Edge-bewertete Zielgruppen enthalten sind.

## Zielgruppenmitgliedschaft

Im folgenden Abschnitt finden Sie Fragen zur Zielgruppenzugehörigkeit.

### Wie kann ich die Mitgliedschaft eines Profils in einer Zielgruppe bestätigen?

Um die Zielgruppenmitgliedschaft eines Profils zu bestätigen, besuchen Sie die Seite mit den Profildetails des Profils, das Sie bestätigen möchten. Wählen Sie **[!UICONTROL Attribute]** gefolgt von **[!UICONTROL JSON anzeigen]** aus, und Sie können bestätigen, dass das `segmentMembership`-Objekt die ID der Zielgruppe enthält.

### Wie löst die Batch-Segmentierung die Profilmitgliedschaft auf?

Zielgruppen, die mithilfe der Batch-Segmentierung bewertet werden, werden täglich aufgelöst, wobei die Ergebnisse der Zielgruppenmitgliedschaft in der Profilgruppe aufgezeichnet werden. `segmentMembership` -Attribut. Die Profilsuche generieren eine neue Version des Profils zum Zeitpunkt der Suche, aber sie tut es. **not** die Ergebnisse der Batch-Segmentierung aktualisieren.

Wenn also Änderungen am Profil vorgenommen werden, z. B. das Zusammenführen von zwei Profilen, ändern sich diese **will** erscheinen im Profil, wenn sie nachgeschlagen werden, aber **not** im `segmentMembership` -Attribut fest, bis der Segmentbewertungsauftrag erneut ausgeführt wurde.

Angenommen, Sie haben zwei sich gegenseitig ausschließende Zielgruppen erstellt: Zielgruppe A ist für Personen bestimmt, die in Washington leben, und Zielgruppe B für Personen, die dies tun **not** leben in Washington. Es gibt zwei Profile - Profil 1 für eine Person, die in Washington lebt, und Profil 2 für eine Person, die in Oregon lebt.

Wenn der Batch-Segmentierungsauswertungsauftrag ausgeführt wird, geht Profil 1 an Zielgruppe A, während Profil 2 an Zielgruppe B geht. Später, aber bevor der Batch-Segmentierungsauswertungsauftrag des nächsten Tages ausgeführt wird, wird ein Ereignis, das die beiden Profile abgleicht, in Platform eintreten. Daher wird ein einzelnes zusammengeführtes Profil erstellt, das die Profile 1 und 2 enthält.

Bis der nächste Batch-Segmentbewertungsauftrag ausgeführt wird, hat das neue zusammengeführte Profil die Zielgruppenzugehörigkeit in **both** Profil 1 und Profil 2. Das bedeutet, dass es Mitglied von **both** Zielgruppe A und Zielgruppe B, obwohl diese Zielgruppen widersprüchliche Definitionen aufweisen. Für den Endbenutzer ist dies die **exakt dieselbe Situation** wie vor der Verbindung der Profile, da immer nur eine Person beteiligt war und Platform dies gerade tat **not** über genügend Informationen verfügen, um die beiden Profile miteinander zu verbinden.

Wenn Sie die Profilsuche verwenden, um das neu erstellte Profil abzurufen und sich die Zielgruppenmitgliedschaft anzusehen, wird angezeigt, dass es Mitglied von **both** Zielgruppe A und Zielgruppe B, obwohl beide Zielgruppen widersprüchliche Definitionen aufweisen. Sobald der tägliche Batch-Segmentierungsbewertungsauftrag ausgeführt wird, wird die Zielgruppenzugehörigkeit aktualisiert, um diesen aktualisierten Status der Profildaten widerzuspiegeln.

Wenn Sie eine höhere Auflösung der Zielgruppe in Echtzeit benötigen, verwenden Sie Streaming oder Kantensegmentierung.

### Wie lange dauert es, bis Streaming-Daten in Batch-Segmentierungs-Workflows verfügbar sind?

Es kann bis zu drei Stunden dauern, bis Streaming-Daten in Batch-Segmentierungs-Workflows verfügbar sind.

Wenn beispielsweise ein Batch-Segmentierungsauftrag um 21 Uhr ausgeführt wird, ist es garantiert, aufgenommene Streaming-Daten zu enthalten. **bis** 18 Uhr. Streaming erfasster Daten, die nach 18 Uhr, aber vor 21 Uhr erfasst wurden **kann** enthalten sein.

