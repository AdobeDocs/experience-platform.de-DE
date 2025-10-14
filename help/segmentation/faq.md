---
title: Häufig gestellte Fragen zu Zielgruppen
description: Erfahren Sie Antworten auf häufig gestellte Fragen zu Zielgruppen und andere segmentierungsbezogene Konzepte.
exl-id: 79d54105-a37d-43f7-adcb-97f2b8e4249c
source-git-commit: 56bf7ae20c33b013a1710fba8c04d9edc23baf89
workflow-type: tm+mt
source-wordcount: '4849'
ht-degree: 27%

---

# Häufig gestellte Fragen

Adobe Experience Platform [!DNL Segmentation Service] bietet eine Benutzeroberfläche und eine RESTful-API, mit der Sie anhand von Segmentdefinitionen oder anderen Quellen aus Ihren [!DNL Real-Time Customer Profile]-Daten Zielgruppen erstellen können. Diese Zielgruppen werden zentral in Experience Platform konfiguriert und gepflegt und stehen jeder Adobe-Lösung zur Verfügung. Im Folgenden finden Sie eine Liste häufig gestellter Fragen zu Zielgruppen und Segmentierung.

## Zielgruppenportal

Im folgenden Abschnitt finden Sie Fragen zu Audience Portal.

### Habe ich Zugriff auf Audience Portal und die Zielgruppenkomposition?

Audience Portal und die Zielgruppenkomposition stehen allen Kundinnen und Kunden von Real-Time CDP Prime und Ultimate (B2C-, B2B- und B2P-Editionen) sowie Journey Optimizer Select, Prime, Ultimate Starter und Ultimate zur Verfügung.

Zu diesem Zeitpunkt werden nur profilbasierte Zielgruppen unterstützt. Unterstützung für kontobasierte Zielgruppen wird in einer späteren Version hinzugefügt.

### Werden extern generierte, vordefinierte Zielgruppen von Audience Portal unterstützt?

Ja, extern generierte, vordefinierte Zielgruppen werden in Audience Portal unterstützt. Zu diesem Zeitpunkt können Sie eine extern generierte Zielgruppe über eine CSV-Datei importieren. Zukünftig können Sie Zielgruppen über Batch- oder Streaming-basierte Quell-Connectoren hinzufügen.

### Welche Berechtigungen benötige ich, um extern generierte Zielgruppen hochzuladen?

Um extern generierte Zielgruppen hochzuladen, benötigen Sie die Berechtigungen „Segmente anzeigen“, „Segmente verwalten“ und „Zielgruppen importieren“. Es sind keine spezifischen rollenbasierten Steuerelemente zum Hochladen extern generierter Zielgruppen erforderlich.

### Was passiert, wenn ich eine extern generierte Zielgruppe hochlade?

Wenn Sie eine extern generierte Zielgruppe hochladen, wird ein Datensatz erstellt und im Datensatzinventar sichtbar. Der Name des Datensatzes entspricht **Namen** extern generierten Zielgruppe, die Sie hochgeladen haben.

### Woraus besteht eine extern generierte Zielgruppe, und was passiert mit diesen Daten, wenn sie in Experience Platform importiert werden?

Während des Workflows Externe Zielgruppe importieren müssen Sie angeben, welche Spalte in der CSV-Datei der **Primären Identität entspricht**. Ein Beispiel für eine primäre Identität ist eine E-Mail-Adresse, eine ECID oder ein organisationsspezifischer benutzerdefinierter Identity-Namespace.

Die mit dieser primären Identitätsspalte verknüpften Daten sind die **Daten** die an das Profil angehängt sind. Wenn keine Profile vorhanden sind, die den Daten in der primären Identitätsspalte entsprechen, wird ein neues Profil erstellt. Dieses Profil ist jedoch im Wesentlichen ein verwaistes Profil, da **keine** Attribute oder Erlebnisereignisse mit diesem Profil verknüpft sind.

Alle anderen Daten innerhalb der extern generierten Zielgruppe werden als **Payload-Attribute“**. Diese Attribute können **nur** während der Aktivierung für Personalisierung und Anreicherung verwendet werden und **nicht** an ein Profil angehängt. Diese Attribute werden jedoch im Data Lake gespeichert.

Während die extern generierte Zielgruppe beim Erstellen von Zielgruppen mit Segment Builder referenziert werden kann, **einzelne Profilattribute**.

### Kann ich extern generierte Zielgruppendaten mit einem in Experience Platform vorhandenen Profil abstimmen?

Ja, die extern generierte Zielgruppe wird mit dem in Experience Platform vorhandenen Profil zusammengeführt, wenn die primären Kennungen übereinstimmen. Die Abstimmung dieser Daten kann bis zu 24 Stunden dauern. Wenn noch keine Profildaten vorhanden sind, wird bei der Aufnahme der Daten ein neues Profil erstellt.

### Wie werden Voreinstellungen für das Kundeneinverständnis für extern generierte Zielgruppen berücksichtigt, die in das Zielgruppenportal importiert werden?{#consent}

Wenn Kundendaten aus mehreren Kanälen erfasst werden, ermöglichen Identitätszuordnungen und Zusammenführungsrichtlinien die Konsolidierung dieser Daten in einem einzigen Echtzeit-Kundenprofil. Informationen zu den Voreinstellungen für das Einverständnis der Kundinnen und Kunden werden auf Profilebene gespeichert und ausgewertet.

Nachgelagerte Ziele überprüfen jedes Profil vor der Aktivierung auf Einverständnisinformationen. Die Einverständnisinformationen jedes Profils werden mit den Einverständnisanforderungen für ein bestimmtes Ziel verglichen. Wenn das Profil die Anforderungen nicht erfüllt, wird dieses Profil nicht an ein Ziel gesendet.

Wenn eine externe Zielgruppe in Audience Portal aufgenommen wird, wird sie mit vorhandenen Profilen mithilfe einer primären ID wie E-Mail oder ECID verbunden. Daher bleiben die vorhandenen Einverständnisrichtlinien während der gesamten Aktivierung in Kraft.

Bitte beachten Sie **dass Sie** Einverständnisinformationen mit einer extern generierten Zielgruppe einschließen sollten, da die Payload-Variablen **nicht** im Profilspeicher, sondern im Data Lake gespeichert werden. Stattdessen **müssen** einen Adobe Experience Platform-Aufnahmekanal verwenden, in den Profildaten importiert werden.

### Kann ich eine extern generierte Zielgruppe verwenden, um andere Zielgruppen zu erstellen?

Ja, alle extern generierten Zielgruppen werden im Zielgruppeninventar angezeigt und können verwendet werden, wenn Zielgruppen innerhalb des [Segment Builders](./ui/segment-builder.md) erstellt werden.

### Wie oft werden extern generierte Zielgruppen ausgewertet?

Extern generierte Zielgruppen werden **nur** während des Imports ausgewertet. Da die mit diesen Import-Audiences verknüpften Attribute nicht dauerhaft sind und **nicht** Teil des Profilspeichers sind, wird eine extern generierte Audience nur aktualisiert, wenn die vorhandene Audience manuell aktualisiert wird.

### Kann ich extern hochgeladene Attribute als Teil der Segmentierung verwenden?

Nein, das ist nicht möglich. Profilattribute sind als dauerhafte Attribute gedacht, während extern erstellte Zielgruppendaten, die hochgeladen werden, nur Kontextdaten enthalten, die mit dieser extern generierten Zielgruppe verknüpft sind.

Die Kontextdaten oder Anreicherungsattribute der extern generierten Zielgruppe sind **nicht** ausreichend lang beständig, da ihr Lebenszyklus an die hochgeladene Zielgruppe gebunden ist. Da diese Anreicherungsattribute von vorübergehender Dauer sind, stehen sie deswegen **nicht** zur Verfügung, um in der Segmentierung verwendet zu werden.

Wenn Sie Ihre Zielgruppen jedoch Batch- oder dateibasierten Zielen zuordnen, können Sie diese extern generierten Anreicherungsattribute verwenden, um Ihre Zielgruppen und weitere nachgelagerte Aktivierungen zu erweitern.

Weitere Informationen zu dieser Funktion finden Sie im Handbuch zum [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](../destinations/ui/activate-batch-profile-destinations.md#mapping).

### Gibt es eine bestimmte Zusammenführungsrichtlinie für extern generierte Zielgruppen?

Die organisationsspezifische standardmäßige Zusammenführungsrichtlinie wird beim Hochladen extern generierter Zielgruppen automatisch angewendet. Sie können jedoch die Zusammenführungsrichtlinie ändern, die während des Workflows „Zielgruppe importieren“ auf die extern generierte Zielgruppe angewendet wird.

### Wo kann ich extern generierte Zielgruppen für aktivieren?

Eine extern generierte Zielgruppe kann jedem Ziel zugeordnet und in Adobe Journey Optimizer-Kampagnen und Journey-Kampagnen verwendet werden.

### Kann ich eine extern generierte Zielgruppe löschen?

Ja! Extern generierte Zielgruppen können in Audience Portal gelöscht werden.

### Was sollte ich tun, wenn ich versehentlich eine extern generierte Zielgruppe hochgeladen habe?

Wenn Sie versehentlich eine extern generierte Zielgruppe hochgeladen haben und die Daten entfernen möchten, können Sie die mit der Zielgruppe verknüpften Profile löschen, indem Sie eine CSV-Datei mit einer Zeile und ohne Daten hochladen.

### Wie lange halten extern generierte Zielgruppen?

Die aktuelle Datengültigkeit für extern generierte Zielgruppen beträgt **30 Tage**. Dieser Ablauf der Daten wurde gewählt, um die Menge der überschüssigen Daten zu reduzieren, die in Ihrer Organisation gespeichert sind.

Nach Ablauf des Datenablaufzeitraums ist der verknüpfte Datensatz weiterhin im Datensatzinventar sichtbar, aber Sie können **Zielgruppe** aktivieren und die Profilanzahl wird als null angezeigt.

### Gibt es eine maximale Anzahl extern generierter Zielgruppen, die ich importieren kann?

Die Anzahl der extern generierten Zielgruppen, die importiert werden können, ist unbegrenzt. Beachten Sie jedoch, dass die importierten Zielgruppen **nicht** gegen das Gesamtlimit für Zielgruppen zählen.

### Wie interagieren Audience Portal und die Zielgruppenkomposition mit der Veröffentlichung von Real-Time CDP-Partnerdaten?

Audience Portal und die Zielgruppenkomposition interagieren auf zwei Arten mit Partnerdaten:

1. Wenn Sie mithilfe der Prospect Profile-Klasse und des -Workflows eine von einem Partner bereitgestellte Interessensliste aufnehmen, werden die Interessierten **getrennt** von der Zusammenführung von Kundenprofilen im Profildienst gehalten. Dies bedeutet, dass Interessentenlisten **nicht** in Audience Portal und der Zielgruppenkomposition zur Verwendung angezeigt werden.
2. Wenn Sie zur Anreicherung von durch Partner bereitgestellten Attributen **vorhandene** Erstanbieterprofile nutzen, **werden** diese mit Partnerdaten angereicherten Zielgruppen sowohl in Audience Portal als auch in der Zielgruppenkomposition zur Verwendung angezeigt.

### Wie kann ich zusätzliche Attribute mit meinen Zielgruppen verwenden?

Bei Audiences gibt es **zwei** verschiedene Arten von zusätzlichen Attributen, die Sie hinzufügen können - Payload-(kontextuelle) Attribute und Anreicherungsattribute.

Payload-Attribute sind Attribute, die im Rahmen des CSV-Uploads einer extern generierten Zielgruppe aufgenommen werden. Diese Attribute werden **nicht** in das Echtzeit-Kundenprofil aufgenommen, können jedoch als Teil eines nachgelagerten Ziels verwendet werden.

Anreicherungsattribute sind Attribute, die aus einem Datensatz stammen und in der Zielgruppenkomposition mit einer Zielgruppe verbunden sind. Diese Attribute können derzeit nur in Adobe Journey Optimizer-Kampagnen verwendet werden. Die Unterstützung für Adobe Journey Optimizer Journey wird bald verfügbar sein, und für nachgelagerte Ziele steht die Unterstützung durch die Veröffentlichung in der Zukunft an.

| Aktivierungskanal | Zielgruppen aus benutzerdefiniertem CSV-Upload | Audiences aus Audience-Komposition |
| --- | --- | --- |
| Real-Time CDP-Ziele | Sowohl die Payload-Attribute als auch die Zielgruppen können aktiviert werden. | Es kann nur die Zielgruppe aktiviert werden. Anreicherungsattribute **können nicht** aktiviert werden. |
| Adobe Journey Optimizer-Kampagnen | Weder die Zielgruppe noch die Payload-Attribute können aktiviert werden. | Sowohl die Zielgruppe als auch die Anreicherungsattribute können aktiviert werden. |

## Lebenszyklusstatus {#lifecycle-states}

Im folgenden Abschnitt finden Sie Fragen zu Lebenszyklusstatus und Verwaltung des Lebenszyklusstatus im Zielgruppenportal.

### Was bedeuten die verschiedenen Lebenszyklusstatus?

Im folgenden Diagramm werden die verschiedenen Lebenszyklusstatus, was sie darstellen, wo Zielgruppen mit diesem Status verwendet werden können und welche Auswirkungen dies auf die Segmentierungsleitplanken hat.

| Land | Definition | Im Zielgruppenportal sichtbar? | In Zielen sichtbar? | Wirkt sich auf Segmentierungsbeschränkungen aus? | Auswirkungen auf dateibasierte Zielgruppen | Auswirkungen auf die Zielgruppenauswertung | Sind sie auch für andere Zielgruppen geeignet? | Bearbeitbar |
| --- | --- | --- | --- | --- | --- | --- | --- | -- |
| Entwurf | Eine Zielgruppe im Status **Entwurf** ist eine Zielgruppe, die sich noch in der Entwicklung befindet und noch nicht für die Verwendung in anderen Services bereit ist. | Ja, aber kann ausgeblendet werden. | Nein | Ja | Kann während des Verfeinerungsprozesses importiert oder aktualisiert werden. | Ausgewertet, um genaue Veröffentlichungszahlen zu erhalten. | Ja, aber nicht empfohlen. | Ja |
| Veröffentlicht | Eine Zielgruppe im Status **Veröffentlicht** ist eine Zielgruppe, die für alle nachgelagerten Services verwendet werden kann. | Ja | Ja | Ja | Kann importiert oder aktualisiert werden. | Wird mithilfe von Batch-, Streaming- oder Edge-Segmentierung bewertet. | Ja | Ja |
| Inaktiv | Eine Zielgruppe im Status **Inaktiv** ist eine Zielgruppe, die derzeit nicht verwendet wird. Sie ist zwar noch in Experience Platform vorhanden, **jedoch** verwendet werden können, bis sie als Entwurf oder veröffentlicht gekennzeichnet ist. | Nein, kann aber angezeigt werden. | Nein | Nein | Nicht mehr aktualisiert. | Von Experience Platform nicht mehr ausgewertet oder aktualisiert. | Nein | Ja |
| Gelöscht | Eine Zielgruppe im Status **Gelöscht** ist eine Zielgruppe, die gelöscht wurde. Die tatsächliche Löschung der Daten kann bis zu einigen Minuten dauern. | Nein | Nein | Nein | Zugrunde liegende Daten werden gelöscht. | Nach Abschluss des Löschvorgangs erfolgt keine Datenauswertung oder -ausführung. | Nein | Nein |

### In welchen Status kann ich meine Zielgruppen bearbeiten?

Zielgruppen können in den folgenden Lebenszyklusstatus bearbeitet werden:

- **Entwurf**: Wenn eine Zielgruppe im Entwurfsstatus bearbeitet wird, bleibt sie im Entwurfsstatus, es sei denn, sie wird explizit veröffentlicht.
- **Veröffentlicht**: Wenn eine Zielgruppe im Veröffentlichungsstatus bearbeitet wird, bleibt sie veröffentlicht und die Zielgruppe wird automatisch aktualisiert.
- **Inaktiv**: Wenn eine Zielgruppe im inaktiven Status bearbeitet wird, bleibt sie inaktiv. Dies bedeutet, dass es nicht ausgewertet oder aktualisiert wird. Wenn Sie die Zielgruppe aktualisieren müssen, müssen Sie die Zielgruppe veröffentlichen.

Nachdem eine Zielgruppe gelöscht wurde, **sie** bearbeitet werden.

### In welche Lebenszyklusstatus kann ich eine Zielgruppe verschieben?

Der mögliche Lebenszyklus gibt an, dass eine Zielgruppe in verschoben werden kann, hängt vom aktuellen Status der Zielgruppe ab.

![Ein Diagramm mit den möglichen Lebenszyklusstatus-Übergängen, die für Zielgruppen verfügbar sind.](./images/faq/lifecycle-state-transition.png)

Wenn sich Ihre Zielgruppe im Entwurfsstatus befindet, können Sie sie entweder veröffentlichen oder löschen, wenn die Zielgruppe keine abhängigen Elemente hat.

Wenn sich Ihre Zielgruppe im Veröffentlichungsstatus befindet, können Sie sie entweder deaktivieren oder löschen, wenn die Zielgruppe keine abhängigen Elemente hat.

Wenn sich Ihre Zielgruppe im inaktiven Status befindet, können Sie sie entweder erneut veröffentlichen oder löschen, wenn die Zielgruppe keine abhängigen Elemente hat.

### Gibt es Einschränkungen für Zielgruppen in bestimmten Lebenszyklusstatus?

Zielgruppen im Status Veröffentlicht können nur in einen anderen Status verschoben werden, wenn die Zielgruppe **keine** abhängigen Elemente hat. Das bedeutet, dass Ihre Zielgruppe, wenn sie in einem nachgelagerten Service verwendet wird, nicht deaktiviert oder gelöscht werden kann.

Wenn eine Zielgruppe, die mithilfe der Batch-Segmentierung ausgewertet wird, erneut veröffentlicht wird, d. h. wenn eine Zielgruppe von inaktiv in veröffentlicht wechselt, wird **Zielgruppe** täglichen Batch-Vorgang aktualisiert. Bei der ersten erneuten Veröffentlichung entsprechen die Profile und Daten **dem Zeitpunkt** zu dem die Zielgruppe inaktiv war.

### Wie bringe ich eine Zielgruppe in den Entwurfsstatus?

Die Methode, um eine Zielgruppe in den Entwurfsstatus zu versetzen, hängt von der Herkunft der Zielgruppe ab.

Bei Zielgruppen, die mit Segment Builder erstellt wurden, können Sie die Zielgruppe in den Entwurfsstatus versetzen, indem Sie in Segment Builder [!UICONTROL Als Entwurf speichern] auswählen.

Für Zielgruppen, die in der Zielgruppenkomposition erstellt wurden, werden Zielgruppen bis zur Veröffentlichung automatisch als Entwurf gespeichert.

Bei Zielgruppen, die extern erstellt werden, werden Zielgruppen automatisch veröffentlicht.

Sobald sich eine Zielgruppe im Status „Veröffentlicht“ befindet **können Sie** ursprüngliche Zielgruppe wieder in den Status „Entwurf“ ändern. Wenn Sie die Zielgruppe jedoch kopieren, befindet sich die neu kopierte Zielgruppe im Status Entwurf .

### Wie setze ich eine Zielgruppe in den Status „Veröffentlicht“?

Bei Zielgruppen, die mit Segment Builder oder Zielgruppenkomposition erstellt wurden, können Sie die Zielgruppe in den Status „Veröffentlicht“ versetzen, indem Sie [!UICONTROL Veröffentlichen] in den entsprechenden Benutzeroberflächen auswählen.

Audiences, die extern erstellt werden, werden automatisch auf „Veröffentlicht“ gesetzt.

### Wie versetze ich eine Zielgruppe in den inaktiven Status?

Sie können eine veröffentlichte Zielgruppe in den inaktiven Status versetzen, indem Sie das Schnellaktionsmenü in Audience Portal öffnen und auf &quot;[!UICONTROL &quot; &#x200B;].

### Wie veröffentliche ich eine Zielgruppe erneut?

>[!NOTE]
>
>Der Status „erneut veröffentlicht“ entspricht dem Veröffentlichungsstatus für das Zielgruppenverhalten.

Sie können eine Zielgruppe erneut veröffentlichen, indem Sie eine Zielgruppe im inaktiven Status auswählen, das Schnellaktionsmenü im Zielgruppen-Portal öffnen und [!UICONTROL Veröffentlichen] auswählen.

### Wie versetze ich eine Zielgruppe in den Status „Gelöscht“?

>[!IMPORTANT]
>
>Sie können nur Zielgruppen löschen, **in nachgelagerten Aktivierungen** verwendet werden. Darüber hinaus können Sie keine Zielgruppe löschen, auf die in einer anderen Zielgruppe verwiesen wird. Wenn Sie Ihre Zielgruppe nicht löschen können, stellen Sie sicher **dass Sie sie** in nachgelagerten Services oder als Baustein einer anderen Zielgruppe verwenden.

Sie können eine Zielgruppe in den Löschstatus versetzen, indem Sie das Schnellaktionsmenü in Audience Portal öffnen und [!UICONTROL Löschen] auswählen.

### Gibt es Einschränkungen für Lebenszyklusstatusübergänge?

Ja, es gibt einige Einschränkungen, die zu beachten sind, wenn Sie Zielgruppen in nachgelagerten Services wie Adobe Journey Optimizer oder nicht kundenbasierten Zielgruppen wie kontobasierten Zielgruppen verwenden.

Zu diesem Zeitpunkt **Sie** manuell überprüfen, ob die Zielgruppe nachgelagert in Adobe Journey Optimizer verwendet wird, da dieser Status derzeit nicht automatisch überprüft wird.

Darüber hinaus **Sie** manuell überprüfen, ob die Zielgruppe als Komponente einer kontobasierten Zielgruppe verwendet wird, da dieser Status derzeit ebenfalls nicht automatisch überprüft wird.

### Was passiert, wenn ich eine Zielgruppe kopiere? {#copy}

Wenn Sie eine Zielgruppe kopieren, befindet sich die neue Zielgruppe im Entwurfsstatus und behält dieselben Ordner, Tags und Beschriftungen bei, die auf die ursprüngliche Zielgruppe angewendet wurden.

### Wirkt sich die Verwendung einer Zielgruppe als untergeordnete Zielgruppe auf Lebenszyklusstatus-Transitionen aus?

>[!NOTE]
>
>Eine übergeordnete Zielgruppe ist eine Zielgruppe **die** andere Zielgruppe als Abhängigkeit für die Zielgruppe verwendet.
>
>Eine untergeordnete Zielgruppe ist eine Zielgruppe, **als** für die Zielgruppe verwendet wird.

Ja, die Verwendung einer Zielgruppe als untergeordnete Zielgruppe hat Auswirkungen darauf, welche Lebenszykluszustandsübergänge die untergeordnete und die übergeordnete Zielgruppe durchführen kann.

Damit eine untergeordnete Zielgruppe in den Veröffentlichungsstatus verschoben werden kann, muss sich ihre gesamte übergeordnete Zielgruppe **&#x200B;**) im Veröffentlichungsstatus befinden. Die übergeordneten Zielgruppen können entweder vor der Veröffentlichung der untergeordneten Zielgruppe veröffentlicht werden oder, falls der Benutzer dies bestätigt, bei der Veröffentlichung der untergeordneten Zielgruppe automatisch veröffentlicht werden.

Damit die übergeordnete Zielgruppe in den inaktiven oder gelöschten Status verschoben werden kann, müssen alle ihre untergeordneten Zielgruppen **&#x200B;**&#x200B;deaktiviert oder gelöscht werden.

### Kann ich auf eine Zielgruppe verweisen, die sich in einem anderen Lebenszyklusstatus befindet?

Ja! Wenn sich Ihre Zielgruppe derzeit im Entwurfsstatus befindet, können Sie entweder im Entwurfsstatus oder im Veröffentlichungsstatus auf Zielgruppen verweisen. Um diese Zielgruppe zu veröffentlichen, müssen **jedoch** anderen übergeordneten Zielgruppen veröffentlichen.

## Zielgruppen-Inventar

Im folgenden Abschnitt finden Sie Fragen zum Zielgruppen-Inventar im Zielgruppen-Portal.

### Benötige ich zusätzliche Berechtigungen zur Verwendung von Zielgruppeninventar-Funktionen?

Nein, das tun Sie nicht. Sofern Sie Bearbeitungsberechtigungen für Zielgruppen haben, können Sie Ihre Ordner und Tags im Zielgruppenportal erstellen, aktualisieren und verwalten. Weitere Informationen zum Verwalten von Berechtigungen finden Sie im [Handbuch zum Verwalten von Berechtigungen](../access-control/ui/permissions.md).

### Gibt es eine Begrenzung für die Anzahl der Ordner, die ich erstellen kann?

Nein, es gibt keine Begrenzung für die Anzahl der Ordner, die Sie erstellen können. Weitere Informationen zu Ordnern finden Sie im Abschnitt [Zielgruppeninventar“ &#x200B;](./ui/audience-portal.md#folders) Übersicht über die Segmentierungs-Service-Benutzeroberfläche.

### Gibt es eine Begrenzung für die Anzahl der Tags, die einer Zielgruppe hinzugefügt werden können?

Nein, es gibt keine Begrenzung für die Anzahl der Tags, die einer Zielgruppe hinzugefügt werden können. Weitere Informationen zu Tags finden Sie im Abschnitt [Zielgruppen-Inventar](./ui/audience-portal.md#tags) der Übersicht über die Segmentierungs-Service-Benutzeroberfläche.

### Gibt es eine Begrenzung für die Anzahl der Tags, die ich erstellen kann?

Nein, es gibt keine Begrenzung für die Anzahl der Tags, die Sie erstellen können. Sie können jedoch maximal 100 **Kategorien erstellen** um sie auf Tags anzuwenden. Weitere Informationen zum Tag-Management finden Sie im [Handbuch zum Verwalten von Tags](../administrative-tags/ui/managing-tags.md).

### Kann ich, wenn ich in einem übergeordneten Ordner nach einer Zielgruppe anhand ihres Namens oder Tags suche, auch die zugehörigen untergeordneten Ordner durchsuchen?

Nein, dieses Verhalten wird nicht unterstützt. Sie können jedoch die Ansicht „Zielgruppen-Inventar“ ändern, sodass **Alle Zielgruppen** angezeigt wird und dann alle Ordner durchsucht werden. Weitere Informationen zur Verwendung der Suche im Zielgruppeninventar finden Sie im [Suchabschnitt](./ui/audience-portal.md#search) der Übersicht über die Segmentierungs-Service-Benutzeroberfläche.

### Kann ich eine Zielgruppe zum Zeitpunkt der Erstellung automatisch einem Ordner zuweisen?

Zu diesem Zeitpunkt nicht. Diese Funktion könnte jedoch in Zukunft verfügbar sein.

### Kann ich mehrere Zielgruppen gleichzeitig in einen Ordner verschieben?

Zu diesem Zeitpunkt nicht. Diese Funktion könnte jedoch in Zukunft verfügbar sein.

## Zielgruppenkomposition

Im folgenden Abschnitt finden Sie Fragen zur Audience-Komposition.

### Wann sollte ich die Zielgruppenkomposition anstelle von Segment Builder verwenden?

Sowohl Zielgruppenkomposition als auch Segment Builder spielen beim Erstellen von Zielgruppen in Experience Platform eine wichtige Rolle.

Segment Builder eignet sich besser für die Erstellung **Zielgruppe (** Erstellen einer Zielgruppe von Grund auf), während die Komposition von Zielgruppen besser für die **(Kuratierung und Personalisierung** (Erstellung neuer Zielgruppen basierend auf einer bestehenden Zielgruppe) geeignet ist.

Die folgende Tabelle veranschaulicht den Unterschied zwischen den beiden Services:

| Segment Builder | Zielgruppenkomposition |
| --------------- | -------------------- |
| <ul><li>Einstufige Zielgruppenerstellung</li><li>Erstellt die grundlegenden Blöcke von Audiences aus Profil-, Zeitreihen- und Daten mit mehreren Entitäten</li><li>Dient zum Erstellen **einer** Zielgruppe</li></ul> | <ul><li>Mehrstufige Zielgruppenerstellung mithilfe von set-basierten Vorgängen</li><li>Verwendet die von Segment Builder erstellten Zielgruppen und wendet Optionen zur Datenanreicherung wie die Rangfolge von Profilattributen und die Aufteilung in Unterzielgruppen an</li><li>Wird verwendet, um **mehrere** Zielgruppen gleichzeitig zu erstellen</li></ul> |

Weitere Informationen zum Segment Builder finden Sie im [Segment Builder-Handbuch](./ui/segment-builder.md). Weitere Informationen zur Audience-Komposition finden Sie im [Handbuch zur Audience-Komposition](./ui/audience-composition.md).

### Kann ich extern generierte Zielgruppen in der Zielgruppenkomposition verwenden?

Zu diesem Zeitpunkt nicht. Diese Funktion sollte jedoch demnächst verfügbar sein.

### Kann ich Zielgruppen von der Zielgruppenkomposition an alle nachgelagerten Ziele und Kanäle senden?

Ja! Sie können Zielgruppen aus der Zielgruppenkomposition in Adobe Journey Optimizer-Kampagnen, Real-Time CDP-Zielen und Adobe Journey Optimizer-Journey verwenden.

### Gibt es Leitlinien in Bezug auf die Anzahl der Kompositionen?

>[!IMPORTANT]
>
>Diese Leitplanke gilt nur für Kompositionen, die mit Zielgruppenkomposition erstellt wurden, und gilt **nicht** für Kompositionen, die mit Federated Zielgruppenkomposition erstellt wurden.

Zu diesem Zeitpunkt können Sie nur **10** veröffentlichte Kompositionen pro Sandbox haben. Diese Grenze soll in einer zukünftigen Version erhöht werden.

### Welche Workflow-Limits gibt es für die Zielgruppenkomposition?

Die Platzierung der Kompositionskomponente folgt einer starren Struktur wie folgt:

1. Begonnen wird **immer** mit dem Block [!UICONTROL Zielgruppe], um die Startaktivität auszuwählen. Es kann maximal **ein** Block [!UICONTROL Zielgruppe] ausgewählt werden.
2. Es kann optional ein Block [!UICONTROL Ausschließen], der auf den Block [!UICONTROL Zielgruppe] folgt, hinzugefügt werden.
3. Sie können optional einen Block [!UICONTROL Anreichern] hinzufügen, der auf den Block [!UICONTROL Ausschließen] folgt. Pro Komposition kann nur **Block**&#x200B;[!UICONTROL Anreichern] verwendet werden.
4. Es kann optional ein Block für den [!UICONTROL Rang] oder die [!UICONTROL Aufspaltung] hinzugefügt werden. Es kann **nur** einer dieser Blöcke pro Komposition ausgewählt werden.
5. Es sollte **immer** mit einem Block zum [!UICONTROL Speichern] abgeschlossen werden, um die Zielgruppe zu speichern.

Darüber hinaus gelten die folgenden Einschränkungen bei der Verwendung dieser Blöcke:

- Block „Aufspaltung“
   - Dieser Block unterstützt nur **String**-Datentypen. Der Block Aufspaltung unterstützt **nicht** das Datum oder den booleschen Datentyp.
   - Darüber hinaus unterstützt dieser Block **nicht** Anreicherungsattribute.
- Block „Ausschließen“
   - Dieser Block unterstützt **nicht** das Datum oder den booleschen Datentyp.
- Block „Rang“
   - Dieser Block unterstützt **Anreicherungsattribute**.

Weitere Informationen zur Verwendung der Zielgruppenkomposition finden Sie im [Handbuch zur Benutzeroberfläche der Zielgruppenkomposition](./ui/audience-composition.md).

### Wann werden Zielgruppen, die mithilfe der Zielgruppenkomposition erstellt wurden, gespeichert und ausgewertet?

Audiences werden beim Erstellen in der Audience-Komposition automatisch gespeichert. Bei der Erstellungszeit der Zielgruppe wird diese automatische Speicherung zum ersten Mal durchgeführt.

Nachdem die Zielgruppenkomposition erstellt wurde, kann es bis zu 48 Stunden dauern, bis sie ausgewertet und für die Verwendung in nachgelagerten Services wie einem Real-Time CDP-Ziel oder Adobe Journey Optimizer-Kanal aktiviert wird.

### Wann kann ich die von mir erstellte Zielgruppe verwenden?

Die in Zielgruppenkomposition erstellte Zielgruppe wird **sofort** im Zielgruppenportal angezeigt. Um sie jedoch in nachgelagerten Services wie Adobe Journey Optimizer verwenden zu können, müssen Sie nach der Auswertung mindestens 24 Stunden warten.

### Sind Auswertungsaufträge im Monitoring-Abschnitt sichtbar?

Derzeit werden Auswertungsaufträge in der Monitoring **Benutzeroberfläche** angezeigt.

### Kann ich eine Zielgruppenkomposition in einer anderen Komposition verwenden?

Nein, Zielgruppen, die mithilfe der Zielgruppenkomposition erstellt wurden, können **nicht** als Eingabe in einer anderen Zielgruppenkomposition verwendet werden.

### Wie funktioniert die Aufteilung in Zielgruppenkompositionen?

Durch die Zielgruppenteilung können Sie Ihre Zielgruppe in kleinere Gruppen unterteilen.

Bei der Aufteilung nach Attribut besteht eine gegenseitige Exklusivität zwischen den Gruppen. Wenn also ein Eintrag die Kriterien für mehrere Aufspaltungspfade erfüllt, wird ihm der **erste** Pfad von links und **keiner** der anderen Pfade zugewiesen.

Bei der Aufteilung nach Prozentsatz werden Aufspaltungen **zufällig** durchgeführt. Das bedeutet, dass die Profile jedem Pfad nach dem Zufallsprinzip zugewiesen werden.

Weiterführende Informationen zum Block „Aufspaltung“ finden Sie im [Handbuch zur Benutzeroberfläche der Zielgruppenkomposition](./ui/audience-composition.md#split).

### Kann ich alle Segmentierungstypen im Workflow „Zielgruppenkomposition“ verwenden?

Ja, alle Segmenttypen ([Batch-Segmentierung, Streaming-Segmentierung und Edge-Segmentierung](./home.md#evaluate-segments)) werden im Workflow „Zielgruppenkomposition“ unterstützt. Da Kompositionen jedoch derzeit nur einmal pro Tag ausgeführt werden, basiert das Ergebnis auf der Zielgruppenzugehörigkeit zum Zeitpunkt der Komposition, selbst wenn Streaming- oder Edge-bewertete Zielgruppen enthalten sind.

## Zielgruppenmitgliedschaft

Im folgenden Abschnitt finden Sie Fragen zur Zielgruppenzugehörigkeit.

### Wie kann ich die Mitgliedschaft eines Profils in einer Zielgruppe bestätigen?

Um die Zielgruppenmitgliedschaft eines Profils zu bestätigen, besuchen Sie die Seite mit den Profildetails des Profils, das Sie bestätigen möchten. Wählen Sie **[!UICONTROL Attribute]** gefolgt von **[!UICONTROL JSON anzeigen]** aus, und Sie können bestätigen, dass das `segmentMembership`-Objekt die ID der Zielgruppe enthält.

### Kann die Zielgruppenzugehörigkeit zwischen idealer und tatsächlicher Zugehörigkeit variieren?

Ja, die Zielgruppenzugehörigkeit kann zwischen idealer und tatsächlicher Zugehörigkeit wechseln, wenn eine Zielgruppe mithilfe der Streaming-Segmentierung **und** diese Zielgruppe auf einer Zielgruppe basiert, die mithilfe der Batch-Segmentierung bewertet wurde.

Wenn beispielsweise Zielgruppe A auf Zielgruppe B basiert und Zielgruppe B mithilfe der Batch-Segmentierung ausgewertet wird, entfernt sich Zielgruppe A weiter von den tatsächlichen Daten, bis sie mit den Aktualisierungen von Zielgruppe B erneut synchronisiert wird, da Zielgruppe B nur alle 24 Stunden aktualisiert wird.

## Batch-Segmentierung {#batch-segmentation}

Im folgenden Abschnitt finden Sie Fragen zur Batch-Segmentierung.

### Wie löst die Batch-Segmentierung die Profilzugehörigkeit auf?

Zielgruppen, die mithilfe der Batch-Segmentierung ausgewertet werden, werden täglich aufgelöst, wobei die Ergebnisse der Zielgruppenzugehörigkeit im `segmentMembership` des Profils aufgezeichnet werden. Die Profilsuche generiert zum Zeitpunkt der Suche eine neue Version des Profils, aktualisiert jedoch **nicht** die Ergebnisse der Batch-Segmentierung.

Wenn also Änderungen am Profil vorgenommen werden, z. B. das Zusammenführen zweier Profile, **werden** beim Nachschlagen im Profil angezeigt, aber **nicht** im `segmentMembership`, bis der Segmentauswertungsauftrag erneut ausgeführt wurde.

Nehmen wir beispielsweise an, Sie haben zwei sich gegenseitig ausschließende Zielgruppen erstellt: Zielgruppe A ist für Menschen, die in Washington leben, und Zielgruppe B ist für Menschen, die **nicht** in Washington leben. Es gibt zwei Profile - Profil 1 für eine Person, die in Washington lebt, und Profil 2 für eine Person, die in Oregon lebt.

Wenn der Batch-Segmentierungs-Auswertungsauftrag ausgeführt wird, wird Profil 1 an Zielgruppe A und Profil 2 an Zielgruppe B gesendet. Später, aber vor der Ausführung des Batch-Segmentierungs-Auswertungsauftrags am nächsten Tag, tritt ein Ereignis, das die beiden Profile miteinander in Einklang bringt, in Experience Platform ein. Daher wird ein einzelnes zusammengeführtes Profil erstellt, das die Profile 1 und 2 enthält.

Bis zum Ausführen des nächsten Batch-Segmentauswertungsauftrags weist das neue zusammengeführte Profil eine Zielgruppenzugehörigkeit in (**)** Profil 1 und Profil 2 auf. Als Ergebnis bedeutet dies, dass es Mitglied von **beiden)** Audience A und Audience B ist, trotz der Tatsache, dass diese Audiences widersprüchliche Definitionen aufweisen. Für den Endbenutzer ist dies die **exakt gleiche Situation** wie vor der Verbindung der Profile, da immer nur eine Person beteiligt war und Experience Platform einfach **nicht** genügend Informationen hatte, um die beiden Profile miteinander zu verbinden.

Wenn Sie die Profilsuche verwenden, um das neu erstellte Profil abzurufen, und sich die Zielgruppenzugehörigkeit ansehen, wird angezeigt, dass es Mitglied von **beiden** Zielgruppe A und Zielgruppe B ist, obwohl diese beiden Zielgruppen widersprüchliche Definitionen aufweisen. Sobald der tägliche Batch-Segmentierungs-Auswertungsauftrag ausgeführt wird, wird die Zielgruppenzugehörigkeit aktualisiert, um diesen aktualisierten Status der Profildaten widerzuspiegeln.

Wenn Sie eine höhere Zielgruppenauflösung in Echtzeit benötigen, verwenden Sie Streaming oder Edge-Segmentierung.

### Wie lange dauert es, bis Streaming-Daten in Batch-Segmentierungs-Workflows verfügbar sind?

Es kann bis zu drei Stunden dauern, bis Streaming-Daten in Batch-Segmentierungs-Workflows verfügbar sind.

Wenn beispielsweise ein Batch-Segmentierungsauftrag um 21 Uhr ausgeführt wird, enthält er garantiert Streaming-aufgenommene Daten **bis 18**. Das Streaming aufgenommener Daten, die nach 18 Uhr, aber vor 21 Uhr aufgenommen wurden **kann** werden.

## Edge-Segmentierung {#edge-segmentation}

Im folgenden Abschnitt finden Sie Fragen zur Edge-Segmentierung.

### Wie lange dauert es, bis eine Segmentdefinition im Edge Network verfügbar ist?

Es dauert bis zu einer Stunde, bis eine Segmentdefinition im Edge Network verfügbar ist.

## Streaming-Segmentierung  {#streaming-segmentation}

Im folgenden Abschnitt finden Sie Fragen zur Streaming-Segmentierung.

### Tritt die „Nicht-Qualifizierung“ der Streaming-Segmentierung auch in Echtzeit auf?

In den meisten Fällen geschieht die Aufhebung der Qualifizierung von Streaming-Segmentierungen in Echtzeit. Für Streaming-Segmente, die Segmente von Segmenten verwenden, wird die Qualifizierung jedoch **nicht** in Echtzeit aufgehoben, sondern erst nach 24 Stunden.

### Mit welchen Daten arbeitet die Streaming-Segmentierung?

Die Streaming-Segmentierung funktioniert bei allen Daten, die über eine Streaming-Quelle aufgenommen wurden. Daten, die über eine Batch-basierte Quelle aufgenommen werden, werden jede Nacht ausgewertet, selbst wenn sie für die Streaming-Segmentierung geeignet sind. In das System gestreamte Ereignisse mit einem Zeitstempel, der älter als 24 Stunden ist, werden im nachfolgenden Batch-Vorgang verarbeitet.

### Wie werden Segmente als Batch- oder Streaming-Segmentierung definiert?

Eine Segmentdefinition wird – basierend auf einer Kombination aus Abfragetyp und Ereignisverlaufsdauer – als Batch-, Streaming- oder Edge-Segmentierung definiert. Eine Liste der Segmente, die als Streaming-Segmentdefinitionen ausgewertet werden, finden Sie im [Abschnitt zu Abfragetypen von Streaming-Segmentierungen](#query-types).

Bitte beachten Sie, dass eine Segmentdefinition, die **sowohl** einen `inSegment`-Ausdruck als auch eine direkte Einzelereigniskette enthält, nicht für die Streaming-Segmentierung infrage kommt. Wenn Sie möchten, dass diese Segmentdefinition für die Streaming-Segmentierung qualifiziert wird, sollten Sie die direkte Einzelereigniskette zu einem eigenen Segment machen.

### Warum steigt die Anzahl der „insgesamt qualifizierten“ Segmente weiter an, während die Anzahl unter „Letzte X Tage“ im Abschnitt Segmentdefinitionsdetails bei null bleibt?

Die Anzahl der insgesamt qualifizierten Segmente wird aus dem täglichen Segmentierungsauftrag abgerufen, der Zielgruppen enthält, die sich sowohl für Batch- als auch für Streaming-Segmente qualifizieren. Dieser Wert wird sowohl für Batch- als auch für Streaming-Segmente angezeigt.

Die Zahl unter „Letzte X Tage“ umfasst **nur** Zielgruppen, die für Streaming-Segmentierung qualifiziert sind. Sie erhöht sich **nur** dann, wenn Sie Daten in das System gestreamt haben, und zählt dann für diese Streaming-Definition. Dieser Wert wird **nur** für Streaming-Segmente angezeigt. Daher **kann** dieser Wert für Batch-Segmente als 0 angezeigt werden.

Wenn Sie also feststellen, dass die Zahl unter „Letzte X Tage“ null ist und das Liniendiagramm ebenfalls null zeigt, haben Sie **nicht** alle Profile in das System gestreamt, die für dieses Segment qualifiziert wären.

### Wie lange dauert es, bis eine Segmentdefinition verfügbar ist?

Es dauert bis zu einer Stunde, bis eine Segmentdefinition verfügbar ist.

### Gibt es Einschränkungen bei den Daten, die in gestreamt werden?

Stellen Sie bei Verwendung der Edge- oder Streaming-Segmentierung sicher, dass die Ereignisse für jedes Profil einen Abstand aufweisen. Wenn innerhalb derselben Sekunde zu viele Ereignisse gestreamt werden, behandelt Experience Platform diese Ereignisse als von Bots generierte Daten und verwirft sie. Als Best Practice sollten Sie **mindestens** fünf Sekunden zwischen den Ereignisdaten haben, um sicherzustellen, dass die Daten ordnungsgemäß verwendet werden.
