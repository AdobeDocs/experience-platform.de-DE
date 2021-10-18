---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;Enum;primäre Identität;primäre Identität;XDM-individuelles Profil;Erlebnisereignis;XDM Experience Event;XDM ExperienceEvent;experienceEvent;ExperienceEvent;XDM ExperienceEvent;Schemadesign;Best Practices
solution: Experience Platform
title: Best Practices für die Datenmodellierung
topic-legacy: overview
description: Dieses Dokument bietet Ihnen eine Einführung in Experience-Datenmodell (XDM)-Schemas und die Bausteine, Grundsätze und Best Practices zum Erstellen von Schemas, die in Adobe Experience Platform verwendet werden sollen.
exl-id: 2455a04e-d589-49b2-a3cb-abb5c0b4e42f
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '2524'
ht-degree: 3%

---

# Best Practices für die Datenmodellierung

[!DNL Experience Data Model] (XDM) ist das zentrale Framework, das Kundenerlebnisdaten standardisiert, indem gemeinsame Strukturen und Definitionen für nachgelagerte Adobe Experience Platform-Dienste bereitgestellt werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, mit der Sie wertvolle Einblicke aus Kundenaktionen gewinnen, Kundenzielgruppen über Segmente definieren und Kundenattribute für Personalisierungszwecke ausdrücken können.

Da XDM äußerst vielseitig und designanpassbar ist, ist es daher wichtig, bei der Erstellung Ihrer Schemas Best Practices für die Datenmodellierung einzuhalten. In diesem Dokument werden die wichtigsten Entscheidungen und Überlegungen behandelt, die Sie beim Zuordnen Ihrer Kundenerlebnisdaten zu XDM treffen müssen.

## Erste Schritte

Bevor Sie dieses Handbuch lesen, lesen Sie bitte die [XDM-Systemübersicht](../home.md) , um eine allgemeine Einführung in XDM und dessen Rolle in Experience Platform zu erhalten.

Darüber hinaus konzentriert sich dieses Handbuch ausschließlich auf wichtige Aspekte bei der Schemagestaltung. Es wird daher dringend empfohlen, die [Grundlagen der Schemakomposition](./composition.md) zu nutzen, um detaillierte Erläuterungen der einzelnen Schemaelemente zu erhalten, die in diesem Handbuch erwähnt werden.

## Zusammenfassung der Best Practices

Der empfohlene Ansatz zum Entwerfen Ihres Datenmodells für die Verwendung in Experience Platform kann wie folgt zusammengefasst werden:

1. Machen Sie sich mit den geschäftlichen Nutzungsszenarios für Ihre Daten vertraut.
1. Identifizieren Sie die primären Datenquellen, die in [!DNL Platform] eingebracht werden sollen, um diese Anwendungsfälle zu beheben.
1. Identifizieren Sie alle sekundären Datenquellen, die ebenfalls von Interesse sein könnten. Wenn beispielsweise derzeit nur eine Geschäftseinheit in Ihrem Unternehmen daran interessiert ist, ihre Daten nach [!DNL Platform] zu portieren, könnte auch eine ähnliche Geschäftseinheit daran interessiert sein, ähnliche Daten in Zukunft zu importieren. Die Betrachtung dieser sekundären Quellen hilft, das Datenmodell in Ihrer gesamten Organisation zu standardisieren.
1. Erstellen Sie ein allgemeines Entitätsbeziehungsdiagramm (ERD) für die identifizierten Datenquellen.
1. Konvertieren Sie die allgemeine ERD in eine [!DNL Platform]-zentrierte ERD (einschließlich Profilen, Erlebnisereignissen und Lookup-Entitäten).

Die Schritte zur Identifizierung der für Ihre geschäftlichen Anwendungsfälle erforderlichen Datenquellen variieren von Organisation zu Organisation. Während sich die restlichen Abschnitte in diesem Dokument auf die letzteren Schritte der Organisation und Erstellung einer ERD nach der Identifizierung der Datenquellen konzentrieren, können die Erläuterungen der verschiedenen Komponenten des Diagramms Ihre Entscheidungen darüber informieren, welche Ihrer Datenquellen auf [!DNL Platform] migriert werden sollen.

## Erstellen einer allgemeinen ERD

Nachdem Sie die Datenquellen ermittelt haben, die Sie in [!DNL Platform] integrieren möchten, erstellen Sie eine allgemeine ERD, die Sie bei der Zuordnung Ihrer Daten zu XDM-Schemas unterstützen soll.

Das folgende Beispiel stellt eine vereinfachte ERD für ein Unternehmen dar, das Daten in [!DNL Platform] einbringen möchte. Das Diagramm zeigt die wesentlichen Entitäten, die in XDM-Klassen unterteilt werden sollten, einschließlich Kundenkonten, Hotels, Adressen und mehreren häufigen E-Commerce-Ereignissen.

![](../images/best-practices/erd.png)

## Sortieren von Entitäten in Profil-, Nachschlageungs- und Ereigniskategorien

Nachdem Sie eine ERD erstellt haben, um die wesentlichen Entitäten zu identifizieren, die Sie in [!DNL Platform] integrieren möchten, müssen diese Entitäten nach Profil-, Lookup- und Ereigniskategorien sortiert werden:

| Kategorie | Beschreibung |
| --- | --- |
| Profilentitäten | Profilentitäten stellen Attribute dar, die sich auf eine einzelne Person beziehen, normalerweise einen Kunden. Entitäten, die unter diese Kategorie fallen, sollten durch Schemas dargestellt werden, die auf der **[!DNL XDM Individual Profile]-Klasse** basieren. |
| Suchentitäten | Lookup-Entitäten stellen Konzepte dar, die sich auf eine einzelne Person beziehen, aber nicht direkt zur Identifizierung der Person verwendet werden können. Entitäten, die unter diese Kategorie fallen, sollten durch Schemas dargestellt werden, die auf **benutzerdefinierten Klassen** basieren. |
| Ereignisentitäten | Ereignisentitäten stellen Konzepte dar, die sich auf Aktionen beziehen, die ein Kunde ausführen kann, Systemereignisse oder andere Konzepte, bei denen Sie Änderungen im Laufe der Zeit verfolgen möchten. Entitäten, die unter diese Kategorie fallen, sollten durch Schemas dargestellt werden, die auf der **[!DNL XDM ExperienceEvent]-Klasse** basieren. |

{style=&quot;table-layout:auto&quot;}

### Überlegungen zur Sortierung von Entitäten

Die folgenden Abschnitte enthalten weitere Anleitungen zum Sortieren Ihrer Entitäten in die oben genannten Kategorien.

#### Kundenattribute

Wenn eine Entität Attribute enthält, die sich auf einen einzelnen Kunden beziehen, ist sie höchstwahrscheinlich eine Profilentität. Beispiele für Kundenattribute sind:

* Persönliche Daten wie Name, Geburtsdatum, Geschlecht und Konto-ID(s).
* Standortinformationen wie Adressen und GPS-Informationen.
* Kontaktinformationen wie Telefonnummern und E-Mail-Adressen.

#### Zeitverlauf-Tracking von Daten

Wenn Sie analysieren möchten, wie sich bestimmte Attribute innerhalb einer Entität im Laufe der Zeit ändern, handelt es sich höchstwahrscheinlich um eine Ereignisentität. Beispielsweise kann das Hinzufügen von Produktelementen zum Warenkorb als Add-to-Warenkorb-Ereignisse in [!DNL Platform] nachverfolgt werden:

| Kunden-ID | Typ | Produkt-ID | Menge | Zeitstempel |
| --- | --- | --- | --- | --- |
| 1234567 | Addieren | 275098 | 2 | 1. Oktober 10:32 Uhr |
| 1234567 | Entfernen | 275098 | 1 | 1. Oktober 10:33 Uhr |
| 1234567 | Addieren | 486502 | 1 | 1. Oktober 10:41 Uhr |
| 1234567 | Addieren | 910482 | 5 | 3. Oktober, 14:15 |

{style=&quot;table-layout:auto&quot;}

#### Anwendungsfälle für die Segmentierung

Bei der Kategorisierung Ihrer Entitäten ist es wichtig, über die Zielgruppensegmente nachzudenken, die Sie erstellen möchten, um Ihre speziellen geschäftlichen Anwendungsfälle zu beheben.

Ein Unternehmen möchte beispielsweise alle &quot;Gold&quot;- oder &quot;Platin&quot;-Mitglieder seines Treueprogramms kennen, die im letzten Jahr mehr als fünf Käufe getätigt haben. Basierend auf dieser Segmentlogik können die folgenden Schlussfolgerungen zur Darstellung relevanter Entitäten gezogen werden:

* &quot;Gold&quot;und &quot;Platin&quot;stellen den Treuestatus dar, der für einen einzelnen Kunden gilt. Da sich die Segmentlogik nur auf den aktuellen Treuestatus von Kunden bezieht, können diese Daten als Teil eines Profilschemas modelliert werden. Wenn Sie Änderungen des Treuestatus im Zeitverlauf verfolgen möchten, können Sie auch ein zusätzliches Ereignisschema für Änderungen des Treuestatus erstellen.
* Käufe sind Ereignisse, die zu einem bestimmten Zeitpunkt auftreten. Die Segmentlogik bezieht sich auf Kaufereignisse innerhalb eines bestimmten Zeitfensters. Diese Daten sollten daher als Ereignisschema modelliert werden.

#### Anwendungsfälle für Activation

Zusätzlich zu Überlegungen zu Segmentierungsanwendungsfällen sollten Sie auch die Aktivierungsanwendungsfälle für diese Segmente überprüfen, um zusätzliche relevante Attribute zu identifizieren.

Beispielsweise hat ein Unternehmen ein Zielgruppensegment basierend auf der Regel `country = US` erstellt. Wenn Sie dieses Segment dann für bestimmte nachgelagerte Ziele aktivieren, möchte das Unternehmen alle exportierten Profile nach dem Herkunftsstatus filtern. Daher sollte auch ein `state` -Attribut in der entsprechenden Profilentität erfasst werden.

#### Aggregierte Werte

Basierend auf dem Anwendungsfall und der Granularität Ihrer Daten sollten Sie entscheiden, ob bestimmte Werte voraggregiert werden müssen, bevor sie in eine Profil- oder Ereignisentität aufgenommen werden.

Beispiel: Ein Unternehmen möchte ein Segment basierend auf der Anzahl der Warenkorbkäufe erstellen. Sie können festlegen, dass diese Daten mit der niedrigsten Granularität integriert werden, indem Sie jedes Kaufereignis mit Zeitstempel als eigene Entität hinzufügen. Dies kann jedoch manchmal die Anzahl der aufgezeichneten Ereignisse exponentiell erhöhen. Um die Anzahl der aufgenommenen Ereignisse zu reduzieren, können Sie einen aggregierten Wert `numberOfPurchases` über einen Wochen- oder Monatszeitraum erstellen. Andere Aggregatfunktionen wie MIN und MAX können auch auf diese Situationen angewendet werden.

>[!CAUTION]
>
>Experience Platform führt derzeit keine automatische Wertaggregation durch, obwohl dies für zukünftige Versionen geplant ist. Wenn Sie aggregierte Werte verwenden möchten, müssen Sie die Berechnungen extern durchführen, bevor Sie die Daten an [!DNL Platform] senden.

#### Kardinalität

Die in Ihrer ERD festgelegten Kardinalitäten können auch einige Hinweise zur Kategorisierung Ihrer Entitäten liefern. Wenn eine Eins-zu-viele-Beziehung zwischen zwei Entitäten besteht, ist die Entität, die die &quot;viele&quot;darstellt, wahrscheinlich eine Ereignisentität. Es gibt jedoch auch Fälle, in denen &quot;viele&quot;eine Gruppe von Lookup-Entitäten sind, die als Array innerhalb einer Profilentität bereitgestellt werden.

>[!NOTE]
>
>Da es keinen universellen Ansatz gibt, um alle Anwendungsfälle anzupassen, ist es wichtig, die Vor- und Nachteile jeder Situation bei der Kategorisierung von Entitäten auf der Grundlage der Kardinalität zu berücksichtigen. Weitere Informationen finden Sie im [nächsten Abschnitt](#pros-and-cons) .

In der folgenden Tabelle sind einige allgemeine Entitätsbeziehungen und die daraus abgeleiteten Kategorien aufgeführt:

| Beziehung | Kardinalität | Entitätskategorien |
| --- | --- | --- |
| Kunden und Warenkorb-Checkouts | Eins bis viele | Ein einzelner Kunde kann über viele Warenkorbvorgänge verfügen, bei denen es sich um Ereignisse handelt, die über einen bestimmten Zeitraum verfolgt werden können. Kunden wären daher eine Profilentität, während Warenkorb-Checkouts eine Ereignisentität wäre. |
| Kunden und Treuekonten | Eins bis eins | Ein einzelner Kunde kann nur über ein Treuekonto verfügen und umgekehrt. Da es sich um eine Eins-zu-Eins-Beziehung handelt, stellen sowohl Kunden als auch Treuekonten Profilentitäten dar. |
| Kunden und Abonnements | Eins bis viele | Ein einzelner Kunde kann über viele Abonnements verfügen. Da es sich bei dem Unternehmen nur um die aktuellen Abonnements eines Kunden handelt, handelt es sich bei Kunden um eine Profilentität, während Abonnements eine Lookup-Entität ist. |

{style=&quot;table-layout:auto&quot;}

### Vor- und Nachteile verschiedener Entitätsklassen {#pros-and-cons}

Im vorherigen Abschnitt wurden zwar einige allgemeine Richtlinien für die Entscheidung, wie Sie Ihre Entitäten kategorisieren, festgelegt, es ist jedoch wichtig zu verstehen, dass es häufig Vor- und Nachteile bei der Auswahl einer Entitätskategorie gegenüber einer anderen geben kann. Die folgende Fallstudie soll veranschaulichen, wie Sie in diesen Situationen Ihre Optionen in Betracht ziehen können.

Ein Unternehmen verfolgt aktive Abonnements für seine Kunden, bei denen ein Kunde über viele Abonnements verfügen kann. Das Unternehmen möchte auch Abonnements für Anwendungsfälle der Segmentierung einbeziehen, z. B. das Auffinden aller Benutzer mit aktiven Abonnements.

In diesem Szenario hat das Unternehmen zwei Möglichkeiten, die Abonnements eines Kunden in seinem Datenmodell zu repräsentieren:

1. [Profilattribute verwenden](#profile-approach)
1. [Ereignisentitäten verwenden](#event-approach)

#### Ansatz 1: Profilattribute verwenden {#profile-approach}

Der erste Ansatz besteht darin, ein Array von Abonnements als Attribute in die Profilentität für Kunden aufzunehmen. Objekte in diesem Array enthalten Felder für `category`, `status`, `planName`, `startDate` und `endDate`.

<img src="../images/best-practices/profile-schema.png" width="800"><br>

**Vorteile**

* Die Segmentierung ist für den vorgesehenen Anwendungsfall möglich.
* Das Schema behält nur die neuesten Abonnementdatensätze für einen Kunden bei.

**Nachteile**

* Das gesamte Array muss jedes Mal neu gekennzeichnet werden, wenn Änderungen an einem Feld im Array auftreten.
* Wenn verschiedene Datenquellen oder Geschäftseinheiten Daten in das Array einspeisen, wird es schwierig, das neueste aktualisierte Array über alle Kanäle hinweg zu synchronisieren.

#### Ansatz 2: Ereignisentitäten verwenden {#event-approach}

Der zweite Ansatz besteht darin, Ereignisschemata zur Darstellung von Abonnements zu verwenden. Dazu müssen dieselben Abonnementfelder wie beim ersten Ansatz erfasst werden, wobei eine Anmelde-ID, eine Kunden-ID und ein Zeitstempel hinzugefügt werden, aus denen hervorgeht, wann das Abonnementereignis eingetreten ist.

<img src="../images/best-practices/event-schema.png" width="800"><br>

**Vorteile**

* Segmentierungsregeln können flexibler sein (z. B. die Suche nach allen Kunden, die ihre Abonnements in den letzten 30 Tagen geändert haben).
* Wenn sich der Abonnementstatus eines Kunden ändert, müssen Sie kein langes, potenziell komplexes Array mehr innerhalb der Profilattribute des Kunden aktualisieren. Dies ist besonders nützlich, wenn gleichzeitige Änderungen an der Abonnementliste des Kunden aus mehreren Quellen auftreten.

**Nachteile**

* Die Segmentierung wird für den ursprünglich geplanten Anwendungsfall komplexer (d. h. die Identifizierung des Status der neuesten Abonnements von Kunden). Das Segment benötigt jetzt zusätzliche Logik, um das letzte Abonnementereignis für einen Kunden zu kennzeichnen, um seinen Status zu überprüfen.

## Erstellen Sie Schemata basierend auf Ihren kategorisierten Entitäten.

Nachdem Sie Ihre Entitäten in Profil-, Such- und Ereigniskategorien unterteilt haben, können Sie mit der Konvertierung Ihres Datenmodells in XDM-Schemas beginnen. Zu Demonstrationszwecken wurde das zuvor dargestellte Datenmodell im folgenden Diagramm in geeignete Kategorien unterteilt:

<img src="../images/best-practices/erd-sorted.png" width="800"><br>

Die Kategorie, unter der eine Entität sortiert wurde, sollte die XDM-Klasse bestimmen, auf der Sie ihr Schema basieren. Ich wiederhole:

* Profilentitäten sollten die Klasse [!DNL XDM Individual Profile] verwenden.
* Ereignisentitäten sollten die Klasse [!DNL XDM ExperienceEvent] verwenden.
* Lookup-Entitäten sollten benutzerdefinierte XDM-Klassen verwenden, die von Ihrem Unternehmen definiert wurden.

>[!NOTE]
>
>Während Ereignisentitäten fast immer durch separate Schemas dargestellt werden, können Entitäten in Profil- oder Lookup-Kategorien je nach Kardinalität in einem einzelnen XDM-Schema kombiniert werden.
>
>Da beispielsweise die Entität Kunden eine Eins-zu-Eins-Beziehung zur Entität LoyaltyAccounts hat, könnte das Schema für die Entität Customers auch ein `LoyaltyAccount` -Objekt enthalten, das die entsprechenden Treuefelder für jeden Kunden enthält. Wenn die Beziehung jedoch eine zu vielen ist, kann die Entität, die die &quot;viele&quot;darstellt, je nach ihrer Komplexität durch ein separates Schema oder ein Array von Profilattributen dargestellt werden.

Die folgenden Abschnitte enthalten allgemeine Anleitungen zum Erstellen von Schemas basierend auf Ihrer ERD.

### Anwendung eines iterativen Modellierungsansatzes

Die [Regeln der Schemaentwicklung](./composition.md#evolution) bestimmen, dass nur zerstörungsfreie Änderungen an Schemas vorgenommen werden können, nachdem sie implementiert wurden. Mit anderen Worten: Wenn Sie einem Schema ein Feld hinzufügen und Daten für dieses Feld erfasst wurden, kann das Feld nicht mehr entfernt werden. Daher ist es wichtig, beim ersten Erstellen Ihrer Schemas einen iterativen Modellierungsansatz zu verwenden, beginnend mit einer vereinfachten Implementierung, die im Laufe der Zeit immer komplexer wird.

Wenn Sie nicht sicher sind, ob ein bestimmtes Feld für die Aufnahme in ein Schema erforderlich ist, empfiehlt es sich, es auszuschließen. Wenn später festgestellt wird, dass das Feld erforderlich ist, kann es immer in der nächsten Iteration des Schemas hinzugefügt werden.

### Identitätsfelder

In Experience Platform werden als Identitäten markierte XDM-Felder verwendet, um Informationen über einzelne Kunden aus mehreren Datenquellen zusammenzufügen. Obwohl ein Schema mehrere Felder enthalten kann, die als Identitäten markiert sind, muss eine einzige primäre Identität definiert werden, damit das Schema zur Verwendung in [!DNL Real-time Customer Profile] aktiviert werden kann. Weitere Informationen zum Anwendungsfall dieser Felder finden Sie im Abschnitt [Identitätsfelder](./composition.md#identity) in den Grundlagen der Schemakomposition .

Beim Entwerfen Ihrer Schemas sind alle Primärschlüssel in Ihren relationalen Datenbanktabellen wahrscheinlich Kandidaten für primäre Identitäten. Weitere Beispiele für anwendbare Identitätsfelder sind E-Mail-Adressen von Kunden, Telefonnummern, Konto-IDs und [ECID](../../identity-service/ecid.md).

### Feldgruppen des Adobe-Anwendungsschemas

Experience Platform bietet mehrere vordefinierte XDM-Schemafeldgruppen zur Erfassung von Daten, die sich auf die folgenden Adobe Apps beziehen:

* Adobe Analytics
* Adobe Audience Manager
* Adobe Campaign
* Adobe Target

Beispielsweise können Sie mit der Feldergruppe [[!UICONTROL Adobe Analytics ExperienceEvent Template]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json) [!DNL Analytics]-spezifische Felder Ihren XDM-Schemas zuordnen. Je nach den Adobe Apps, mit denen Sie arbeiten, sollten Sie diese von der Adobe bereitgestellten Feldgruppen in Ihren Schemas verwenden.

<img src="../images/best-practices/analytics-field-group.png" width="700"><br>

Feldergruppen der Adobe App weisen mithilfe des Felds `identityMap` automatisch eine primäre Standardidentität zu. Hierbei handelt es sich um ein systemgeneriertes, schreibgeschütztes Objekt, das Standardidentitätswerte für einen einzelnen Kunden zuordnet.

Bei Adobe Analytics ist ECID die primäre Standardidentität. Wenn ein ECID-Wert nicht von einem Kunden bereitgestellt wird, lautet die primäre Identität stattdessen &quot;AAID&quot;.

>[!IMPORTANT]
>
>Bei der Verwendung von Feldgruppen für Adobe Apps sollten keine anderen Felder als primäre Identität markiert werden. Wenn es zusätzliche Eigenschaften gibt, die als Identitäten markiert werden müssen, müssen diese Felder stattdessen als sekundäre Identitäten zugewiesen werden.

## Nächste Schritte

In diesem Dokument wurden die allgemeinen Richtlinien und Best Practices zum Entwerfen Ihres Datenmodells für die Experience Platform behandelt. Zusammenfassung:

* Verwenden Sie einen Top-Down-Ansatz, indem Sie Ihre Datentabellen in Profil-, Such- und Ereigniskategorien sortieren, bevor Sie Ihre Schemas erstellen.
* Es gibt oft mehrere Ansätze und Optionen beim Entwerfen von Schemas für unterschiedliche Zwecke.
* Ihr Datenmodell sollte Ihre geschäftlichen Anwendungsfälle wie Segmentierung oder Journey-Analyse unterstützen.
* Machen Sie Ihre Schemata so einfach wie möglich und fügen Sie nur dann neue Felder hinzu, wenn dies unbedingt erforderlich ist.

Sobald Sie fertig sind, finden Sie im Tutorial zum Erstellen eines Schemas in der Benutzeroberfläche](../tutorials/create-schema-ui.md) schrittweise Anweisungen zum Erstellen eines Schemas, zum Zuweisen der entsprechenden Klasse für die Entität und zum Hinzufügen von Feldern zum Zuordnen Ihrer Daten.[
