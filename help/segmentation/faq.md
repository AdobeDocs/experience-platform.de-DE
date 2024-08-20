---
title: Häufig gestellte Fragen zu Zielgruppen
description: Erfahren Sie mehr über Antworten auf häufig gestellte Fragen zu Zielgruppen und anderen segmentierungsbezogenen Konzepten.
exl-id: 79d54105-a37d-43f7-adcb-97f2b8e4249c
source-git-commit: 29d9445e6e71c60f4b596a5e645a56d2b70e133c
workflow-type: tm+mt
source-wordcount: '4235'
ht-degree: 21%

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

Um extern generierte Zielgruppen hochladen zu können, benötigen Sie die Berechtigungen &quot;Segmente anzeigen&quot;, &quot;Segmente verwalten&quot;und &quot;Zielgruppen importieren&quot;. Zum Hochladen extern generierter Zielgruppen sind keine bestimmten rollenbasierten Steuerelemente erforderlich.

### Was passiert, wenn ich eine extern generierte Zielgruppe hochlade?

Wenn Sie eine extern generierte Zielgruppe hochladen, wird ein Datensatz erstellt und im Datensatzbestand sichtbar. Der Name des Datensatzes entspricht dem **gleichen** Namen der extern generierten Zielgruppe, die Sie hochgeladen haben.

### Woraus besteht eine extern generierte Zielgruppe und was passiert mit diesen Daten, wenn sie in Platform importiert werden?

Während des Workflows &quot;Externe Zielgruppe importieren&quot;müssen Sie angeben, welche Spalte in der CSV-Datei der **Primären Identität** entspricht. Ein Beispiel für eine primäre Identität sind E-Mail-Adresse, ECID oder ein unternehmensspezifischer benutzerdefinierter Identitäts-Namespace.

Die mit dieser primären Identitätsspalte verknüpften Daten sind die **nur** -Daten, die an das Profil angehängt sind. Wenn keine vorhandenen Profile vorhanden sind, die mit den Daten in der primären Identitätsspalte übereinstimmen, wird ein neues Profil erstellt. Dieses Profil ist jedoch im Wesentlichen ein verwaistes Profil, da **no** -Attribute oder Erlebnisereignisse mit diesem Profil verknüpft sind.

Alle anderen Daten innerhalb der extern generierten Zielgruppe werden als **Payload-Attribute** betrachtet. Diese Attribute können **nur** zur Personalisierung und Anreicherung während der Aktivierung verwendet werden und sind **nicht** an ein Profil angehängt. Diese Attribute werden jedoch im Data Lake gespeichert.

Während beim Erstellen von Zielgruppen mit Segment Builder auf die extern generierte Zielgruppe verwiesen werden kann, können einzelne Profilattribute **nicht** verwendet werden.

### Kann ich extern generierte Zielgruppendaten mit einem vorhandenen Profil in Platform abstimmen?

Ja, die extern generierte Zielgruppe wird mit dem in Platform vorhandenen Profil zusammengeführt, wenn die primären Kennungen übereinstimmen. Die Abstimmung dieser Daten kann bis zu 24 Stunden dauern. Wenn noch keine Profildaten vorhanden sind, wird bei der Aufnahme der Daten ein neues Profil erstellt.

### Wie werden die Voreinstellungen für die Kundenzustimmung für extern erstellte Zielgruppen berücksichtigt, die in Audience Portal importiert werden?{#consent}

Da Kundendaten aus mehreren Kanälen erfasst werden, ermöglichen Identitätszusammenfügungs- und Zusammenführungsrichtlinien die Konsolidierung dieser Daten in einem einzigen Echtzeit-Kundenprofil. Informationen zu den Zustimmungsvoreinstellungen der Kunden werden auf Profilebene gespeichert und ausgewertet.

Nachgelagerte Ziele überprüfen jedes Profil vor der Aktivierung auf Zustimmungsinformationen. Die Einwilligungsinformationen jedes Profils werden mit den Einwilligungsanforderungen für ein bestimmtes Ziel verglichen. Wenn das Profil die Anforderungen nicht erfüllt, wird dieses Profil nicht an ein Ziel gesendet.

Wenn eine externe Zielgruppe in Audience Portal aufgenommen wird, werden sie mithilfe einer primären ID wie E-Mail oder ECID mit vorhandenen Profilen verbunden. Daher bleiben die bestehenden Zustimmungsrichtlinien während der gesamten Aktivierung in Kraft.

Beachten Sie bitte, dass Sie **nicht** Einwilligungsinformationen mit einer extern generierten Zielgruppe einbeziehen sollten, da die Payload-Variablen **nicht** im Profilspeicher, sondern im Daten-Pool gespeichert sind. Stattdessen müssen Sie **** einen Adobe Experience Platform-Erfassungskanal verwenden, in den Profildaten importiert werden.

### Kann ich eine extern generierte Zielgruppe verwenden, um andere Zielgruppen zu erstellen?

Ja, alle extern generierten Zielgruppen werden im Zielgruppeninventar angezeigt und können verwendet werden, wenn Zielgruppen innerhalb des [Segment Builders](./ui/segment-builder.md) erstellt werden.

### Wie oft werden extern generierte Zielgruppen ausgewertet?

Extern generierte Zielgruppen werden während des Imports nur **1} ausgewertet.** Da die diesen Importzielgruppen zugeordneten Attribute nicht dauerhaft sind und **nicht** Teil des Profilspeichers sind, wird eine extern generierte Zielgruppe nur aktualisiert, wenn die vorhandene Zielgruppe manuell aktualisiert wird.

### Kann ich extern hochgeladene Attribute als Teil der Segmentierung verwenden?

Nein, das ist nicht möglich. Profilattribute sind als dauerhafte Attribute gedacht, während extern erstellte Zielgruppendaten, die hochgeladen werden, nur Kontextdaten enthalten, die mit dieser extern generierten Zielgruppe verknüpft sind.

Die Kontextdaten oder Anreicherungsattribute der extern generierten Zielgruppe sind **nicht** ausreichend lang beständig, da ihr Lebenszyklus an die hochgeladene Zielgruppe gebunden ist. Da diese Anreicherungsattribute von vorübergehender Dauer sind, stehen sie deswegen **nicht** zur Verfügung, um in der Segmentierung verwendet zu werden.

Wenn Sie Ihre Zielgruppen jedoch Batch- oder dateibasierten Zielen zuordnen, können Sie diese extern generierten Anreicherungsattribute verwenden, um Ihre Zielgruppen und weitere nachgelagerte Aktivierungen zu erweitern.

Weitere Informationen zu dieser Funktion finden Sie im Handbuch zum [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](../destinations/ui/activate-batch-profile-destinations.md#mapping).

### Gibt es eine spezifische Zusammenführungsrichtlinie für extern generierte Zielgruppen?

Die unternehmensspezifische standardmäßige Zusammenführungsrichtlinie wird beim Hochladen von extern generierten Zielgruppen automatisch angewendet. Sie können jedoch die Zusammenführungsrichtlinie ändern, die während des Import-Audience-Workflows auf die extern generierte Audience angewendet wird.

### Wo kann ich extern generierte Zielgruppen aktivieren?

Eine extern generierte Zielgruppe kann jedem Ziel zugeordnet und in Adobe Journey Optimizer-Kampagnen verwendet werden.

### Kann ich eine extern generierte Zielgruppe löschen?

Ja! Extern generierte Zielgruppen können in Audience Portal gelöscht werden.

### Was sollte ich tun, wenn ich versehentlich eine extern generierte Zielgruppe hochgeladen habe?

Wenn Sie versehentlich eine extern generierte Audience hochgeladen haben und die Daten entfernen möchten, können Sie die mit der Audience verknüpften Profile löschen, indem Sie eine CSV-Datei mit einer Zeile und ohne Daten hochladen.

### Wie lange halten extern generierte Zielgruppen an?

Die aktuelle Datengültigkeit für extern generierte Zielgruppen beträgt **30 Tage**. Diese Datengültigkeit wurde ausgewählt, um die Menge an überschüssigen Daten zu reduzieren, die in Ihrem Unternehmen gespeichert werden.

Nach Ablauf des Datenablaufzeitraums ist der verknüpfte Datensatz weiterhin im Datensatzbestand sichtbar, Sie können jedoch **nicht** die Zielgruppe aktivieren, und die Profilanzahl wird als null angezeigt.

### Gibt es eine maximale Anzahl von extern generierten Zielgruppen, die ich importieren kann?

Die Anzahl der extern generierten Zielgruppen, die Sie importieren können, ist unbegrenzt. Beachten Sie jedoch, dass die importierten Zielgruppen **do** mit dem Gesamtzielgruppenlimit angerechnet werden.

### Wie interagieren Audience Portal und die Zielgruppenkomposition mit der Veröffentlichung von Real-Time CDP-Partnerdaten?

Audience Portal und die Zielgruppenkomposition interagieren auf zwei Arten mit Partnerdaten:

1. Wenn Sie mithilfe der Prospect Profile-Klasse und des -Workflows eine von einem Partner bereitgestellte Interessensliste aufnehmen, werden die Interessierten **getrennt** von der Zusammenführung von Kundenprofilen im Profildienst gehalten. Dies bedeutet, dass Interessentenlisten **nicht** in Audience Portal und der Zielgruppenkomposition zur Verwendung angezeigt werden.
2. Wenn Sie zur Anreicherung von durch Partner bereitgestellten Attributen **vorhandene** Erstanbieterprofile nutzen, **werden** diese mit Partnerdaten angereicherten Zielgruppen sowohl in Audience Portal als auch in der Zielgruppenkomposition zur Verwendung angezeigt.

### Wie kann ich zusätzliche Attribute für meine Zielgruppen verwenden?

Bei Zielgruppen gibt es **zwei** verschiedene Typen von zusätzlichen Attributen, die Sie hinzufügen können - Payload-Attribute (kontextbezogene Attribute) und Anreicherungsattribute.

Payload-Attribute sind Attribute, die als Teil des CSV-Uploads einer extern generierten Zielgruppe erfasst werden. Diese Attribute sind **nicht**, die im Echtzeit-Kundenprofil erfasst werden, können jedoch als Teil eines nachgelagerten Ziels verwendet werden.

Anreicherungsattribute sind Attribute, die aus einem Datensatz stammen und in der Zielgruppenkomposition mit einer Zielgruppe verbunden werden. Diese Attribute können derzeit nur in Adobe Journey Optimizer-Kampagnen verwendet werden. Die Unterstützung für Adobe Journey Optimizer-Journey wird in Kürze bereitgestellt, und die Unterstützung für nachgelagerte Ziele steht noch aus.

| Aktivierungskanal | Zielgruppen aus benutzerdefiniertem CSV-Upload | Zielgruppen aus Zielgruppenkomposition |
| --- | --- | --- |
| Real-Time CDP-Ziele | Sowohl die Payload-Attribute als auch die Zielgruppen können aktiviert werden. | Nur die Audience kann aktiviert werden. Anreicherungsattribute **können nicht** aktiviert werden. |
| Adobe Journey Optimizer-Kampagnen | Weder die Audience noch die Payload-Attribute können aktiviert werden. | Sowohl die Zielgruppe als auch die Anreicherungsattribute können aktiviert werden. |

## Lebenszyklusstatus {#lifecycle-states}

Im folgenden Abschnitt finden Sie Fragen zu Lebenszyklusstatus und Lebenszyklusstatusverwaltung in Audience Portal.

### Was stellen die verschiedenen Lebenszyklusstatus dar?

In der folgenden Tabelle werden die verschiedenen Lebenszyklusstatus, ihre Darstellung, wo Zielgruppen mit diesem Status verwendet werden können, sowie die Auswirkungen auf die Limits bei der Segmentierung erläutert.

| Land | Definition | In Audience Portal sichtbar? | In Zielen sichtbar? | Betrifft Segmentierungsbeschränkungen? | Auswirkungen auf dateibasierte Zielgruppen | Auswirkungen auf die Zielgruppenbewertung | In anderen Zielgruppen verwenden? | Bearbeitbar |
| --- | --- | --- | --- | --- | --- | --- | --- | -- |
| Entwurf | Eine Zielgruppe im Status **Entwurf** ist eine Zielgruppe, die sich noch in der Entwicklung befindet und noch nicht für andere Dienste verwendet werden kann. | Ja, aber kann ausgeblendet werden. | Nein | Ja | Kann während des Verfeinerungsprozesses importiert oder aktualisiert werden. | Wird ausgewertet, um präzise Veröffentlichungszahlen zu erhalten. | Ja, jedoch nicht empfohlen, verwendet zu werden. | Ja |
| Veröffentlicht | Eine Zielgruppe im Status **Veröffentlicht** ist eine Zielgruppe, die für alle nachgelagerten Dienste verwendet werden kann. | Ja | Ja | Ja | Kann importiert oder aktualisiert werden. | Wird mit Batch-, Streaming- oder Edge-Segmentierung ausgewertet. | Ja | Ja |
| Inaktiv | Eine Zielgruppe im Status **Inaktiv** ist eine Zielgruppe, die derzeit nicht verwendet wird. Sie existiert weiterhin in Platform, kann jedoch **nicht** verwendet werden, bis sie als Entwurf oder veröffentlicht markiert ist. | Nein, aber kann angezeigt werden. | Nein | Nein | Wird nicht mehr aktualisiert. | Wird von Platform nicht mehr bewertet oder aktualisiert. | Nein | Ja |
| Gelöscht | Eine Zielgruppe im Status **Gelöscht** ist eine Zielgruppe, die gelöscht wurde. Das tatsächliche Löschen der Daten kann bis zu einigen Minuten dauern. | Nein | Nein | Nein | Zugrunde liegende Daten werden gelöscht. | Nach Abschluss des Löschvorgangs erfolgt keine Datenauswertung oder -ausführung. | Nein | Nein |

### In welchen Status kann ich meine Zielgruppen bearbeiten?

Zielgruppen können in den folgenden Lebenszyklusstatus bearbeitet werden:

- **Entwurf**: Wenn eine Zielgruppe im Entwurfsstatus bearbeitet wird, bleibt sie im Entwurfsstatus, es sei denn, sie wird explizit veröffentlicht.
- **Veröffentlicht**: Wenn eine Zielgruppe im Veröffentlichungsstatus bearbeitet wird, bleibt sie veröffentlicht und die Zielgruppe wird automatisch aktualisiert.
- **Inaktiv**: Wenn eine Zielgruppe im inaktiven Status bearbeitet wird, bleibt sie inaktiv. Dies bedeutet, dass sie weder bewertet noch aktualisiert wird. Wenn Sie die Audience aktualisieren müssen, müssen Sie die Audience veröffentlichen.

Nachdem eine Zielgruppe gelöscht wurde, kann sie **nicht mehr** bearbeitet werden.

### In welchen Lebenszyklusstatus kann ich eine Zielgruppe verschieben?

Der mögliche Lebenszyklus gibt an, dass eine Zielgruppe je nach dem aktuellen Status der Zielgruppe verschoben werden kann.

![Ein Diagramm, das die möglichen Übergänge des Lebenszyklusstatus darstellt, die für Zielgruppen verfügbar sind.](./images/faq/lifecycle-state-transition.png)

Wenn Ihre Zielgruppe im Entwurfsstatus ist, können Sie sie entweder veröffentlichen oder löschen, wenn die Zielgruppe keine abhängigen Elemente aufweist.

Wenn sich Ihre Zielgruppe im Veröffentlichungsstatus befindet, können Sie sie deaktivieren oder löschen, wenn die Zielgruppe keine abhängigen Elemente aufweist.

Wenn Ihre Zielgruppe im inaktiven Status ist, können Sie sie entweder erneut veröffentlichen oder löschen, wenn die Zielgruppe keine abhängigen Elemente aufweist.

### Gibt es Einschränkungen für Zielgruppen in bestimmten Lebenszyklusstatus?

Zielgruppen im Veröffentlichungsstatus können nur dann in einen anderen Status verschoben werden, wenn die Zielgruppe **nicht** über abhängige Elemente verfügt. Wenn Ihre Zielgruppe also in einem nachgelagerten Dienst verwendet wird, kann sie nicht deaktiviert oder gelöscht werden.

Wenn eine Zielgruppe, die mithilfe der Batch-Segmentierung ausgewertet wird, erneut veröffentlicht wird, d. h. wenn eine Zielgruppe von inaktiv zu publiziert wechselt, aktualisiert die Zielgruppe **nach** den täglichen Batch-Auftrag. Wenn sie zum ersten Mal erneut veröffentlicht wird, entsprechen die Profile und Daten **demselben Wert** wie bei der Inaktivität der Zielgruppe.

### Wie setze ich eine Zielgruppe in den Entwurfsstatus?

Die Methode zum Einfügen einer Zielgruppe in den Entwurfsstatus hängt von der Herkunft der Zielgruppe ab.

Für Zielgruppen, die mit Segment Builder erstellt wurden, können Sie die Zielgruppe auf den Entwurfsstatus setzen, indem Sie &quot;[!UICONTROL Als Entwurf speichern]&quot;im Segmentaufbau auswählen.

Für in Zielgruppenkomposition erstellte Zielgruppen werden Zielgruppen bis zur Veröffentlichung automatisch als Entwurf gespeichert.

Zielgruppen, die extern erstellt werden, werden automatisch veröffentlicht.

Sobald sich eine Zielgruppe im Veröffentlichungsstatus befindet, können Sie die ursprüngliche Zielgruppe **nicht mehr in den Entwurfsstatus ändern.** Wenn Sie die Zielgruppe jedoch kopieren, befindet sich die neu kopierte Zielgruppe im Entwurfsstatus.

### Wie platziere ich eine Zielgruppe in den Veröffentlichungsstatus?

Für Zielgruppen, die mit Segment Builder oder Audience Komposition erstellt wurden, können Sie die Zielgruppe auf den Veröffentlichungsstatus setzen, indem Sie &quot;[!UICONTROL Publish]&quot;in den entsprechenden Benutzeroberflächen auswählen.

Von außen erstellte Zielgruppen werden automatisch auf &quot;Publizieren&quot;gesetzt.

### Wie stelle ich eine Zielgruppe in den inaktiven Status?

Sie können eine veröffentlichte Zielgruppe in den inaktiven Status versetzen, indem Sie das Schnellaktionsmenü in Audience Portal öffnen und &quot;[!UICONTROL Deaktivieren]&quot; auswählen.

### Wie kann ich eine Zielgruppe erneut veröffentlichen?

>[!NOTE]
>
>Der Status &quot;Neu veröffentlicht&quot;entspricht dem Veröffentlichungsstatus für das Zielgruppenverhalten.

Sie können eine Zielgruppe erneut veröffentlichen, indem Sie eine Zielgruppe mit inaktivem Status auswählen, das Schnellaktionsmenü in Audience Portal öffnen und [!UICONTROL Publish] auswählen.

### Wie setze ich eine Zielgruppe in den gelöschten Status?

>[!IMPORTANT]
>
>Sie können nur Zielgruppen löschen, die in nachfolgenden Aktivierungen verwendet werden, nämlich **nicht**. Darüber hinaus können Sie keine Zielgruppe löschen, auf die in einer anderen Zielgruppe verwiesen wird. Wenn Sie Ihre Audience nicht löschen können, stellen Sie sicher, dass Sie sie **nicht** in nachfolgenden Diensten oder als Baustein einer anderen Audience verwenden.

Sie können eine Zielgruppe in den Löschstatus versetzen, indem Sie das Schnellaktionsmenü in Audience Portal öffnen und [!UICONTROL Löschen] auswählen.

### Gibt es Einschränkungen bei Übergängen vom Lebenszyklusstatus?

Ja, es gibt Einschränkungen, die Sie beachten müssen, wenn Sie Zielgruppen in nachgelagerten Diensten wie Adobe Journey Optimizer oder nicht kundenbasierten Zielgruppen wie kontobasierten Zielgruppen verwenden.

Zu diesem Zeitpunkt müssen Sie **** manuell überprüfen, ob die Zielgruppe in Adobe Journey Optimizer nachgelagert verwendet wird, da dieser Status derzeit nicht automatisch überprüft wird.

Darüber hinaus müssen Sie **** manuell überprüfen, ob die Zielgruppe als Komponente einer kontobasierten Zielgruppe verwendet wird, da dieser Status derzeit ebenfalls nicht automatisch überprüft wird.

### Was passiert, wenn ich eine Zielgruppe kopiere? {#copy}

Beim Kopieren einer Zielgruppe befindet sich die neue Zielgruppe im Entwurfsstatus und behält die Ordner, Tags und Beschriftungen bei, die auf die ursprüngliche Zielgruppe angewendet wurden.

### Beeinflusst die Verwendung einer Zielgruppe als untergeordnete Zielgruppe die Transitionen des Lebenszyklusstatus?

>[!NOTE]
>
>Eine übergeordnete Zielgruppe ist eine Zielgruppe, die **** als Abhängigkeit für die Zielgruppe eine andere Zielgruppe verwendet.
>
>Eine untergeordnete Zielgruppe ist eine Zielgruppe, die **als** als Abhängigkeit für die Zielgruppe verwendet wird.

Ja, die Verwendung einer Zielgruppe als untergeordnete Zielgruppe wirkt sich darauf aus, welche Lebenszyklusstatus von der untergeordneten und übergeordneten Zielgruppe übernommen werden können.

Damit eine untergeordnete Zielgruppe in den Veröffentlichungsstatus verschoben werden kann, muss sich die gesamte übergeordnete Zielgruppe **1} im Veröffentlichungsstatus befinden.** Übergeordnete Zielgruppen können entweder veröffentlicht werden, bevor die untergeordnete Zielgruppe veröffentlicht wird, oder, falls der Benutzer dies bestätigt, automatisch veröffentlicht werden, wenn die untergeordnete Zielgruppe veröffentlicht wird.

Damit die übergeordnete Zielgruppe in den Status &quot;Inaktiv&quot;oder &quot;Gelöscht&quot;versetzt wird, müssen alle untergeordneten Zielgruppen **1} deaktiviert oder gelöscht werden.**

### Kann ich auf eine Zielgruppe verweisen, die sich in einem anderen Lebenszyklusstatus befindet?

Ja! Wenn Ihre Zielgruppe sich derzeit im Entwurfsstatus befindet, können Sie auf Zielgruppen im Entwurfsstatus oder im Veröffentlichungsstatus verweisen. Um diese Zielgruppe zu veröffentlichen, müssen Sie jedoch **1} die anderen übergeordneten Zielgruppen veröffentlichen.**

## Zielgruppeninventar

Im folgenden Abschnitt werden Fragen im Zusammenhang mit dem Zielgruppeninventar im Audience Portal aufgeführt.

### Benötige ich zusätzliche Berechtigungen, um die Funktionen des Zielgruppeninventars zu verwenden?

Nein, nicht. Solange Sie über Bearbeitungsberechtigungen für Zielgruppen verfügen, können Sie Ihre Ordner und Tags in Audience Portal erstellen, aktualisieren und verwalten. Weitere Informationen zum Verwalten von Berechtigungen finden Sie im [Berechtigungshandbuch verwalten](../access-control/ui/permissions.md).

### Gibt es eine Begrenzung für die Anzahl der Ordner, die ich erstellen kann?

Nein, die Anzahl der Ordner, die Sie erstellen können, ist nicht beschränkt. Weitere Informationen zu Ordnern finden Sie im Abschnitt [Zielgruppeninventar](./ui/audience-portal.md#folders) der Übersicht über die Segmentation Service-Benutzeroberfläche.

### Gibt es eine Begrenzung für die Anzahl der Tags, die einer Zielgruppe hinzugefügt werden können?

Nein, die Anzahl der Tags, die einer Audience hinzugefügt werden können, ist unbegrenzt. Weitere Informationen zu Tags finden Sie im Abschnitt [Zielgruppeninventar](./ui/audience-portal.md#tags) der Übersicht über die Segmentation Service-Benutzeroberfläche.

### Gibt es eine Begrenzung für die Anzahl der Tags, die ich erstellen kann?

Nein, die Anzahl der Tags, die Sie erstellen können, ist unbegrenzt. Sie können jedoch maximal **100** Kategorien erstellen, die auf die Tags angewendet werden sollen. Weitere Informationen zum Tag-Management finden Sie im Leitfaden [Verwalten von Tags](../administrative-tags/ui/managing-tags.md) .

### Kann ich beim Suchen nach einer Zielgruppe nach Name oder Tag in einem übergeordneten Ordner auch die zugehörigen untergeordneten Ordner durchsuchen?

Nein, dieses Verhalten wird nicht unterstützt. Sie können jedoch die Ansicht des Zielgruppeninventars ändern, um **Alle Zielgruppen** anzuzeigen und dann alle Ordner zu durchsuchen. Weitere Informationen zur Verwendung der Suche im Zielgruppen-Inventar finden Sie im Abschnitt [Suchen](./ui/audience-portal.md#search) der Übersicht über die Segmentation Service-Benutzeroberfläche.

### Kann ich zum Zeitpunkt der Erstellung automatisch eine Zielgruppe einem Ordner zuweisen?

Zu diesem Zeitpunkt nicht. Diese Funktion kann jedoch in Zukunft verfügbar sein.

### Kann ich mehrere Zielgruppen gleichzeitig in einen Ordner verschieben?

Zu diesem Zeitpunkt nicht. Diese Funktion kann jedoch in Zukunft verfügbar sein.

## Zielgruppenkomposition

Im folgenden Abschnitt werden Fragen im Zusammenhang mit der Zielgruppenkomposition aufgeführt.

### Wann sollte ich die Zielgruppenkomposition anstelle von Segment Builder verwenden?

Sowohl die Zielgruppenkomposition als auch der Segment Builder haben beim Erstellen von Zielgruppen in Platform wichtige Rollen.

Der Segment Builder eignet sich besser für die Erstellung der Zielgruppe **1} (zum Erstellen einer neuen Zielgruppe), während die Zielgruppenzusammensetzung besser für die Kuratierung und Personalisierung der Zielgruppe** 3} geeignet ist (zum Erstellen neuer Zielgruppen basierend auf einer vorhandenen Zielgruppe).****

Die folgende Tabelle zeigt den Unterschied zwischen den beiden Diensten:

| Segment Builder | Zielgruppenkomposition |
| --------------- | -------------------- |
| <ul><li>Einzelstufige Zielgruppenerstellung</li><li>Erstellt die grundlegenden Bausteine von Zielgruppen aus Profil-, Zeitreihen- und Daten aus mehreren Entitäten</li><li>Dient zum Erstellen einer **one** -Zielgruppe</li></ul> | <ul><li>Mehrstufige Zielgruppenerstellung mit set-basierten Vorgängen</li><li>Verwendet die vom Segment Builder erstellten Zielgruppen und wendet Anreicherungsoptionen für Daten an, z. B. Profilattribute einordnen und in Unterzielgruppen unterteilen</li><li>Wird verwendet, um **mehrere** Zielgruppen gleichzeitig zu erstellen</li></ul> |

Weitere Informationen zum Segment Builder finden Sie im [Segment Builder-Handbuch](./ui/segment-builder.md). Weitere Informationen zur Zielgruppenkomposition finden Sie im Handbuch [Zielgruppenkomposition](./ui/audience-composition.md) .

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
3. Sie können optional einen Baustein vom Typ [!UICONTROL Anreicherung] hinzufügen, der dem Block [!UICONTROL Ausschließen] folgt. Sie können pro Komposition nur den Block **1** [!UICONTROL Anreicherung] verwenden.
4. Es kann optional ein Block für den [!UICONTROL Rang] oder die [!UICONTROL Aufspaltung] hinzugefügt werden. Es kann **nur** einer dieser Blöcke pro Komposition ausgewählt werden.
5. Es sollte **immer** mit einem Block zum [!UICONTROL Speichern] abgeschlossen werden, um die Zielgruppe zu speichern.

Zusätzlich werden die folgenden Einschränkungen(?) bei Verwendung dieser Blöcke anwenden:

- Geteilter Block
   - Dieser Block unterstützt nur Datentypen vom Typ **String** . Der Aufspaltungsblock unterstützt den Datums- oder booleschen Datentyp **nicht**.
   - Darüber hinaus unterstützt dieser Block **nicht** Anreicherungsattribute.
- Block ausschließen
   - Dieser Block unterstützt den Datums- oder booleschen Datentyp **nicht**.
- Rang-Block
   - Dieser Block unterstützt die Anreicherungsattribute **nicht**.

Weitere Informationen zur Verwendung der Zielgruppenkomposition finden Sie im [Handbuch zur Benutzeroberfläche der Zielgruppenkomposition](./ui/audience-composition.md).

### Wann werden Zielgruppen, die mit der Zielgruppenkomposition erstellt wurden, gespeichert und ausgewertet?

Zielgruppen werden automatisch gespeichert, während sie in der Zielgruppenkomposition erstellt werden. Die Erstellungszeit der Zielgruppe ist das erste Mal, dass diese automatische Speicherung erfolgt.

Nachdem die Zielgruppenzusammensetzung erstellt wurde, kann es bis zu 48 Stunden dauern, bis sie ausgewertet und für nachgelagerte Dienste wie ein Real-Time CDP-Ziel oder einen Adobe Journey Optimizer-Kanal aktiviert wird.

### Wann kann ich die erstellte Zielgruppe verwenden?

Die in Zielgruppenkomposition erstellte Zielgruppe wird in Audience Portal **sofort** angezeigt. Um es jedoch in Adobe Journey Optimizer verwenden zu können, müssen Sie mindestens 24 Stunden nach der Auswertung warten.

### Sind Auswertungsaufträge im Monitoring-Abschnitt sichtbar?

Derzeit werden Auswertungsaufträge in der Monitoring-Benutzeroberfläche mit **nicht** angezeigt.

### Kann ich eine Zielgruppen-Komposition in einer anderen Komposition verwenden?

Nein, Zielgruppen, die mithilfe der Zielgruppen-Komposition erstellt wurden, können **nicht** als Eingabe in einer anderen Zielgruppen-Komposition verwendet werden.

### Wie funktioniert die Aufteilung in Zielgruppen-Kompositionen?

Durch die Zielgruppenteilung können Sie Ihre Zielgruppe weiter in kleinere Gruppen unterteilen.

Bei der Aufteilung nach Attribut besteht eine gegenseitige Exklusivität zwischen den Gruppen. Wenn also ein Eintrag die Kriterien für mehrere Aufspaltungspfade erfüllt, wird ihm der **erste** Pfad von links und **keiner** der anderen Pfade zugewiesen.

Beim Aufteilen nach Prozentsatz werden die Aufspaltungen **zufällig** vorgenommen. Dies bedeutet, dass die Profile zufällig jedem Pfad zugewiesen werden.

Weiterführende Informationen zum Block „Aufspaltung“ finden Sie im [Handbuch zur Benutzeroberfläche der Zielgruppenkomposition](./ui/audience-composition.md#split).

### Kann ich alle Segmentierungstypen im Workflow „Zielgruppenkomposition“ verwenden?

Ja, alle Segmenttypen ([Batch-Segmentierung, Streaming-Segmentierung und Edge-Segmentierung](./home.md#evaluate-segments)) werden im Workflow „Zielgruppenkomposition“ unterstützt. Da Kompositionen jedoch derzeit nur einmal pro Tag ausgeführt werden, basiert das Ergebnis auf der Zielgruppenzugehörigkeit zum Zeitpunkt der Komposition, selbst wenn Streaming- oder Edge-bewertete Zielgruppen enthalten sind.

## Zielgruppenmitgliedschaft

Im folgenden Abschnitt finden Sie Fragen zur Zielgruppenzugehörigkeit.

### Wie kann ich die Mitgliedschaft eines Profils in einer Zielgruppe bestätigen?

Um die Zielgruppenmitgliedschaft eines Profils zu bestätigen, besuchen Sie die Seite mit den Profildetails des Profils, das Sie bestätigen möchten. Wählen Sie **[!UICONTROL Attribute]** gefolgt von **[!UICONTROL JSON anzeigen]** aus, und Sie können bestätigen, dass das `segmentMembership`-Objekt die ID der Zielgruppe enthält.

### Wie löst die Batch-Segmentierung die Profilmitgliedschaft auf?

Zielgruppen, die mit der Batch-Segmentierung ausgewertet werden, werden täglich aufgelöst, wobei die Ergebnisse der Zielgruppenmitgliedschaft im Attribut `segmentMembership` des Profils aufgezeichnet werden. Die Profilsuche generieren zum Zeitpunkt der Suche eine neue Version des Profils, aktualisieren jedoch die Batch-Segmentierungsergebnisse **nicht**.

Wenn also Änderungen am Profil vorgenommen werden, z. B. das Zusammenführen von zwei Profilen, erscheinen diese Änderungen **wird** im Profil, wenn sie nachgeschlagen werden, werden jedoch **nicht** im Attribut `segmentMembership` angezeigt, bis der Segmentbewertungsauftrag erneut ausgeführt wird.

Nehmen wir beispielsweise an, Sie haben zwei sich gegenseitig ausschließende Zielgruppen erstellt: Zielgruppe A ist für Personen bestimmt, die in Washington leben, und Zielgruppe B für Personen, die **nicht** in Washington leben. Es gibt zwei Profile - Profil 1 für eine Person, die in Washington lebt, und Profil 2 für eine Person, die in Oregon lebt.

Wenn der Batch-Segmentierungsauswertungsauftrag ausgeführt wird, geht Profil 1 an Zielgruppe A, während Profil 2 an Zielgruppe B geht. Später, aber bevor der Batch-Segmentierungsauswertungsauftrag des nächsten Tages ausgeführt wird, wird ein Ereignis, das die beiden Profile abgleicht, in Platform eintreten. Daher wird ein einzelnes zusammengeführtes Profil erstellt, das die Profile 1 und 2 enthält.

Bis der nächste Batch-Segmentbewertungsauftrag ausgeführt wird, hat das neue zusammengeführte Profil die Zielgruppenzugehörigkeit in **sowohl in** Profil 1 als auch in Profil 2. Daher bedeutet dies, dass es Mitglied von **sowohl** Zielgruppe A als auch von Zielgruppe B sein wird, obwohl diese Zielgruppen widersprüchliche Definitionen aufweisen. Für den Endbenutzer ist dies die **genaue gleiche Situation** wie vor der Verbindung der Profile, da immer nur die eine Person beteiligt war und Platform gerade **nicht** über genügend Informationen verfügte, um die beiden Profile miteinander zu verbinden.

Wenn Sie die Profilsuche verwenden, um das neu erstellte Profil abzurufen und sich die Zielgruppenmitgliedschaft anzusehen, wird angezeigt, dass es Mitglied von **sowohl** Zielgruppe A als auch Zielgruppe B ist, obwohl beide Zielgruppen widersprüchliche Definitionen aufweisen. Sobald der tägliche Batch-Segmentierungsbewertungsauftrag ausgeführt wird, wird die Zielgruppenzugehörigkeit aktualisiert, um diesen aktualisierten Status der Profildaten widerzuspiegeln.

Wenn Sie eine höhere Auflösung der Zielgruppe in Echtzeit benötigen, verwenden Sie Streaming oder Kantensegmentierung.

### Wie lange dauert es, bis Streaming-Daten in Batch-Segmentierungs-Workflows verfügbar sind?

Es kann bis zu drei Stunden dauern, bis Streaming-Daten in Batch-Segmentierungs-Workflows verfügbar sind.

Wenn beispielsweise ein Batch-Segmentierungsauftrag um 21 Uhr ausgeführt wird, ist es garantiert, aufgenommene Streaming-Daten **bis** 18 Uhr zu enthalten. Streaming erfasster Daten, die nach 18.00 Uhr, aber vor 21.00 Uhr erfasst wurden, dürfen **enthalten.**

