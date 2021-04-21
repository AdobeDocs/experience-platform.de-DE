---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;enum;primäre Identität;primäre Identität;XDM-individuelles Profil;Experience Ereignis;XDM Experience Ereignis;XDM ExperienceEvent;experienceEvent;ExperienceEvent;XDM ExperienceEvent;Schema-Design;Best Practices
solution: Experience Platform
title: Best Practices für die Datenmodellierung
topic-legacy: overview
description: Dieses Dokument bietet Ihnen eine Einführung in Experience-Datenmodell (XDM)-Schemas und die Bausteine, Grundsätze und Best Practices zum Erstellen von Schemas, die in Adobe Experience Platform verwendet werden sollen.
exl-id: 2455a04e-d589-49b2-a3cb-abb5c0b4e42f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2507'
ht-degree: 2%

---

# Bewährte Verfahren für die Datenmodellierung

[!DNL Experience Data Model] (XDM) ist der Kernrahmen, der Kundenerlebnisdaten standardisiert, indem gemeinsame Strukturen und Definitionen für nachgelagerte Adobe Experience Platform-Dienste bereitgestellt werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Ihnen wertvolle Einblicke in Kundenaktionen ermöglicht, Audiencen durch Kundensegmente definiert und Kundenattribute zu Personalisierungszwecken ausdrückt.

Da XDM sehr vielseitig und von Design aus anpassbar ist, ist es daher wichtig, beim Entwerfen Ihrer Schema die Best Practices für die Datenmodellierung zu befolgen. In diesem Dokument werden die wichtigsten Entscheidungen und Überlegungen behandelt, die Sie bei der Zuordnung Ihrer Kundenerlebnisdaten zu XDM treffen müssen.

## Erste Schritte

Bevor Sie dieses Handbuch lesen, lesen Sie sich bitte die [XDM Systemübersicht](../home.md) durch, um eine Einführung in XDM und dessen Rolle in der Experience Platform zu erhalten.

Darüber hinaus konzentriert sich dieser Leitfaden ausschließlich auf wichtige Aspekte in Zusammenhang mit dem Schema-Design. Es wird daher dringend empfohlen, die [Grundlagen der Schema-Komposition](./composition.md) für detaillierte Erläuterungen der einzelnen Schema-Elemente, die in diesem Handbuch erwähnt werden, heranzuziehen.

## Zusammenfassung der Best Practices

Der empfohlene Ansatz zum Entwerfen Ihres Datenmodells für die Verwendung in der Experience Platform lässt sich wie folgt zusammenfassen:

1. Machen Sie sich mit den geschäftlichen Nutzungsszenarien für Ihre Daten vertraut.
1. Identifizieren Sie die primären Datenquellen, die in [!DNL Platform] eingebracht werden sollten, um diese Anwendungsfälle zu beheben.
1. Finden Sie alle sekundären Datenquellen heraus, die ebenfalls von Interesse sein könnten. Wenn zum Beispiel derzeit nur eine Geschäftseinheit in Ihrem Unternehmen daran interessiert ist, ihre Daten an [!DNL Platform] zu übertragen, könnte eine ähnliche Geschäftseinheit auch daran interessiert sein, ähnliche Daten in Zukunft zu portieren. Die Betrachtung dieser sekundären Quellen hilft, das Datenmodell in Ihrer gesamten Organisation zu standardisieren.
1. Erstellen Sie ein hochrangiges Entitätsbeziehungsdiagramm (ERD) für die identifizierten Datenquellen.
1. Konvertieren Sie die ERD auf hoher Ebene in eine [!DNL Platform]-zentrierte ERD (einschließlich Profilen, Experience Ereignisses und Lookup-Entitäten).

Die Schritte zur Ermittlung der für die Durchführung Ihrer geschäftlichen Nutzungsszenarien erforderlichen Datenquellen sind von Unternehmen und Organisation zu Organisation unterschiedlich. Während sich die restlichen Abschnitte in diesem Dokument auf die letzten Schritte der Organisation und des Aufbaus einer ERD nach der Identifizierung der Datenquellen konzentrieren, können die Erläuterungen der verschiedenen Diagrammkomponenten Ihre Entscheidungen darüber informieren, welche Ihrer Datenquellen nach [!DNL Platform] migriert werden sollen.

## Erstellen eines EFD auf hoher Ebene

Nachdem Sie die Datenquellen ermittelt haben, die Sie in [!DNL Platform] einbinden möchten, erstellen Sie eine ERD auf hoher Ebene, die Ihnen bei der Zuordnung Ihrer Daten zu XDM-Schemas helfen soll.

Das folgende Beispiel stellt eine vereinfachte ERD für eine Firma dar, die Daten in [!DNL Platform] einbringen möchte. Das Diagramm zeigt die wesentlichen Entitäten an, die in XDM-Klassen, darunter Kundenkonten, Hotels, Adressen und mehrere gängige E-Commerce-Ereignis, sortiert werden sollten.

![](../images/best-practices/erd.png)

## Sortieren von Entitäten in Profil-, Lookup- und Ereignis-Kategorien

Nachdem Sie eine ERD erstellt haben, um die wesentlichen Entitäten zu identifizieren, die Sie in [!DNL Platform] einbinden möchten, müssen diese Entitäten in Profil-, Lookup- und Ereignis-Kategorien sortiert werden:

| Kategorie | Beschreibung |
| --- | --- |
| Profil-Entitäten | Profil-Entitäten stellen Attribute dar, die sich auf eine Einzelperson beziehen, in der Regel auf einen Kunden. Entitäten, die unter diese Kategorie fallen, sollten durch Schema dargestellt werden, die auf der **[!DNL XDM Individual Profile]class** basieren. |
| Suchentitäten | Suchentitäten stellen Konzepte dar, die sich auf eine einzelne Person beziehen können, die aber nicht direkt zur Identifizierung der Person verwendet werden können. Entitäten, die unter diese Kategorie fallen, sollten durch Schema dargestellt werden, die auf **benutzerspezifischen Klassen** basieren. |
| Ereignis-Entitäten | Ereignis-Entitäten stellen Konzepte dar, die mit Aktionen zusammenhängen, die ein Kunde ausführen kann, Systemkonzepte oder andere Ereignisse, bei denen Sie Änderungen im Laufe der Zeit nachverfolgen möchten. Entitäten, die unter diese Kategorie fallen, sollten durch Schema dargestellt werden, die auf der **[!DNL XDM ExperienceEvent]class** basieren. |

### Überlegungen zur Entitätssortierung

Die folgenden Abschnitte enthalten weitere Anleitungen, wie Sie Ihre Entitäten in die oben genannten Kategorien sortieren können.

#### Kundenattribute

Wenn eine Entität Attribute enthält, die sich auf einen einzelnen Kunden beziehen, ist dies höchstwahrscheinlich eine Profil-Entität. Beispiele für Kundenattribute:

* Persönliche Angaben wie Name, Geburtsdatum, Geschlecht und Konto-ID(s).
* Standortinformationen wie Adressen und GPS-Informationen.
* Kontaktinformationen wie Telefonnummern und E-Mail-Adressen.

#### Verfolgen von Daten über einen bestimmten Zeitraum

Wenn Sie analysieren möchten, wie sich bestimmte Attribute innerhalb einer Entität im Laufe der Zeit ändern, ist dies höchstwahrscheinlich eine Ereignis-Entität. So können zum Beispiel Produktelemente zu einem Einkaufswagen als Add-to-cart-Ereignis in [!DNL Platform] nachverfolgt werden:

| Kunden-ID | Typ | Produkt-ID | Menge | Zeitstempel |
| --- | --- | --- | --- | --- |
| 1234567 | Addieren | 275098 | 2 | 01.10.32 |
| 1234567 | Entfernen | 275098 | 1 | 01.10.33 |
| 1234567 | Addieren | 486502 | 1 | 01.10.41 |
| 1234567 | Addieren | 910482 | 5 | 03.10.15 |

#### Anwendungsfälle für die Segmentierung

Bei der Kategorisierung Ihrer Entitäten ist es wichtig, über die Audiencen nachzudenken, die Sie erstellen möchten, um Ihre speziellen Geschäftszwecke zu bearbeiten.

Eine Firma möchte beispielsweise alle &quot;Gold&quot;- oder &quot;Platin&quot;-Mitglieder ihres Loyalitätsjahrs kennen, die im letzten Programm mehr als fünf Einkäufe getätigt haben. Auf der Grundlage dieser Segmentlogik können folgende Schlussfolgerungen zur Vertretung relevanter Stellen gezogen werden:

* &quot;Gold&quot;und &quot;Platinum&quot;stellen den Treuestatus eines einzelnen Kunden dar. Da die Segmentlogik nur den aktuellen Kundenloyalitätsstatus betrifft, können diese Daten als Teil eines Profil-Schemas modelliert werden. Wenn Sie Änderungen des Treuestatus im Laufe der Zeit verfolgen möchten, können Sie auch ein zusätzliches Ereignis-Schema für Änderungen des Treuestatus erstellen.
* Einkäufe sind Ereignis, die zu einem bestimmten Zeitpunkt auftreten, und die Segmentlogik bezieht sich auf Ereignis innerhalb eines bestimmten Zeitraums. Diese Daten sollten daher als Ereignis-Schema modelliert werden.

#### Anwendungsfälle der Aktivierung

Zusätzlich zu Überlegungen zu den Anwendungsfällen für die Segmentierung sollten Sie auch die Anwendungsfälle für die Aktivierung dieser Segmente überprüfen, um weitere relevante Attribute zu identifizieren.

Eine Firma hat beispielsweise ein Audiencen-Segment basierend auf der Regel `country = US` erstellt. Beim Aktivieren dieses Segments in bestimmten nachgelagerten Zielgruppen möchte die Firma dann alle exportierten Profil auf Grundlage des Heimatstatus filtern. Daher sollte ein `state`-Attribut auch in der entsprechenden Profil-Entität erfasst werden.

#### Aggregierte Werte

Je nach Anwendungsfall und Granularität Ihrer Daten sollten Sie entscheiden, ob bestimmte Werte voraggregiert werden müssen, bevor sie in eine Profil- oder Ereignis-Entität aufgenommen werden.

Eine Firma möchte beispielsweise ein Segment basierend auf der Anzahl der Einkaufswagen erstellen. Sie können diese Daten mit der niedrigsten Granularität einbeziehen, indem Sie jedes Ereignis mit Zeitstempel als eigene Entität einbeziehen. Dies kann jedoch manchmal die Anzahl der aufgezeichneten Ereignis exponentiell erhöhen. Um die Anzahl der erfassten Ereignis zu reduzieren, können Sie einen Aggregat-Wert `numberOfPurchases` über einen Wochen- oder Monatszeitraum erstellen. Andere Aggregat-Funktionen wie MIN und MAX können auch auf diese Situationen angewendet werden.

>[!CAUTION]
>
>Experience Platform führt derzeit keine automatische Wertaggregation durch, obwohl dies für zukünftige Versionen geplant ist. Wenn Sie aggregierte Werte verwenden möchten, müssen Sie die Berechnungen extern durchführen, bevor Sie die Daten an [!DNL Platform] senden.

#### Kardinalität

Die in Ihrer ERD festgelegten Kardinalitäten können auch Hinweise zur Kategorisierung Ihrer Entitäten liefern. Wenn es eine Eins-zu-viele-Beziehung zwischen zwei Entitäten gibt, wird die Entität, die das &quot;viele&quot;darstellt, wahrscheinlich eine Entität des Ereignisses sein. Es gibt jedoch auch Fälle, in denen &quot;viele&quot;eine Reihe von Nachschlageentitäten sind, die als Array innerhalb einer Profil-Entität bereitgestellt werden.

>[!NOTE]
>
>Da es keinen universellen Ansatz gibt, um alle Anwendungsfälle zu berücksichtigen, ist es wichtig, bei der Kategorisierung von Entitäten auf der Grundlage der Kardinalität die Vor- und Nachteile jeder einzelnen Situation zu berücksichtigen. Weitere Informationen finden Sie unter [nächster Abschnitt](#pros-and-cons).

In der folgenden Tabelle sind einige allgemeine Entitätsbeziehungen und die daraus abgeleiteten Kategorien aufgeführt:

| Beziehung | Kardinalität | Entitäts-Kategorien |
| --- | --- | --- |
| Kunden und Warenkorb-Kassengänge | Eins zu viele | Ein einzelner Kunde hat möglicherweise viele Einkaufswagen-Kassengänge, bei denen es sich um Ereignis handelt, die im Laufe der Zeit verfolgt werden können. Kunden wären daher eine Profil-Entität, während Warenkorb-Kassengänge eine Ereignis-Entität wären. |
| Kunden- und Treuhandkonten | Eins | Ein einzelner Kunde kann nur ein Treuekonto haben und umgekehrt. Da es sich bei der Beziehung um eine Eins-zu-eins-Beziehung handelt, repräsentieren sowohl Kunden- als auch Treuhandkonten Profil-Entitäten. |
| Kunden und Abonnement | Eins zu viele | Ein einzelner Kunde hat möglicherweise viele Abonnements. Da es sich bei der Firma nur um die aktuellen Abonnement eines Kunden handelt, handelt es sich bei Customers um eine Profil-Entität, während Abonnements eine Nachschlagewerk ist. |

### Vor- und Nachteile verschiedener Entitätsklassen {#pros-and-cons}

Während im vorherigen Abschnitt einige allgemeine Richtlinien für die Entscheidung, wie Sie Ihre Entitäten kategorisieren, angegeben wurden, ist es wichtig zu verstehen, dass es oft Vor- und Nachteile für die Auswahl einer Entitäts-Kategorie gegenüber einer anderen geben kann. Die folgende Fallstudie soll zeigen, wie Sie in diesen Situationen Ihre Optionen in Betracht ziehen können.

Eine Firma verfolgt aktive Abonnement für ihre Kunden, bei denen ein Kunde viele Abonnement haben kann. Die Firma möchte auch Abonnement für Anwendungsfälle der Segmentierung einschließen, z. B. alle Benutzer mit aktiven Abonnements suchen.

In diesem Szenario verfügt die Firma über zwei potenzielle Optionen zur Darstellung der Abonnement eines Kunden in ihrem Datenmodell:

1. [Profil-Attribute verwenden](#profile-approach)
1. [Ereignis-Entitäten verwenden](#event-approach)

#### Ansatz 1: Profil-Attribute {#profile-approach} verwenden

Der erste Ansatz besteht darin, ein Array von Abonnements als Attribute in die Kundenentität des Profils einzuschließen. Objekte in diesem Array enthalten Felder für `category`, `status`, `planName`, `startDate` und `endDate`.

<img src="../images/best-practices/profile-schema.png" width="800"><br>

**Vorteile**

* Die Segmentierung ist für den vorgesehenen Verwendungsfall möglich.
* Das Schema bewahrt nur die neuesten Kundendatensätze auf.

**Nachteile**

* Das gesamte Array muss bei jeder Änderung an einem Feld im Array neu angegeben werden.
* Wenn verschiedene Datenquellen oder Geschäftseinheiten Daten in das Array einspeisen, wird es schwierig, das neueste aktualisierte Array über alle Kanal hinweg zu synchronisieren.

#### Ansatz 2: Ereignis-Entitäten {#event-approach} verwenden

Der zweite Ansatz wäre, Ereignis-Schema zur Darstellung von Abonnements zu verwenden. Hierzu müssen dieselben Abonnement-Felder wie beim ersten Ansatz verwendet werden, wobei eine Abonnement-ID, eine Kunden-ID und ein Zeitstempel zum Zeitpunkt des Ereignisses des Abonnements hinzugefügt werden müssen.

<img src="../images/best-practices/event-schema.png" width="800"><br>

**Vorteile**

* Segmentierungsregeln können flexibler sein (z. B. bei der Suche nach allen Kunden, die ihre Abonnement in den letzten 30 Tagen geändert haben).
* Wenn sich der Status des Abonnements eines Kunden ändert, müssen Sie kein langes, potenziell komplexes Array mehr innerhalb der Kundenattribute aktualisieren. Dies ist besonders dann nützlich, wenn die Liste des Abonnements des Kunden aus mehreren Quellen gleichzeitig geändert wird.

**Nachteile**

* Die Segmentierung wird für den ursprünglich vorgesehenen Anwendungsfall komplexer (d. h. die Identifizierung des Status der letzten Abonnement des Kunden). Das Segment benötigt nun zusätzliche Logik, um das Ereignis des letzten Abonnements für einen Kunden zu kennzeichnen, um dessen Status zu überprüfen.

## Erstellen Sie Schema basierend auf Ihren kategorisierten Entitäten

Nachdem Sie Ihre Entitäten in Profil-, Lookup- und Ereignis-Kategorien sortiert haben, können Sie Ihren Beginn zur Konvertierung Ihres Datenmodells in XDM-Schema verwenden. Zu Demonstrationszwecken wurde das zuvor dargestellte Datenmodell im folgenden Diagramm in geeignete Kategorien sortiert:

<img src="../images/best-practices/erd-sorted.png" width="800"><br>

Die Kategorie, unter der eine Entität sortiert wurde, sollte die XDM-Klasse bestimmen, auf der das Schema basiert. Zu wiederholen:

* Profil-Entitäten sollten die [!DNL XDM Individual Profile]-Klasse verwenden.
* Ereignis-Entitäten sollten die [!DNL XDM ExperienceEvent]-Klasse verwenden.
* Suchentitäten sollten benutzerdefinierte XDM-Klassen verwenden, die von Ihrem Unternehmen definiert wurden.

>[!NOTE]
>
>Während Ereignis-Entitäten fast immer durch separate Schema repräsentiert werden, können Entitäten im Profil oder Lookup-Kategorien in einem einzigen XDM-Schema kombiniert werden, je nach Kardinalität.
>
>Da die Kundenentität beispielsweise eine Eins-zu-Eins-Beziehung zur LoyaltyAccounts-Entität unterhält, könnte das Schema für die Kundenentität auch ein `LoyaltyAccount`-Objekt enthalten, das die entsprechenden Treuefelder für jeden Kunden enthält. Wenn die Beziehung jedoch eine zu viele ist, könnte die Entität, die die &quot;viele&quot;darstellt, je nach Komplexität durch ein separates Schema oder ein Array von Profil-Attributen dargestellt werden.

Die folgenden Abschnitte enthalten allgemeine Anleitungen zum Aufbau von Schemas auf Basis Ihrer ERD.

### Anwenden eines iterativen Modellierungsansatzes

Die [Regeln der Schema-Evolution](./composition.md#evolution) schreiben vor, dass nur nicht-destruktive Änderungen an Schemas vorgenommen werden können, sobald sie implementiert wurden. Mit anderen Worten, wenn Sie einem Schema ein Feld hinzufügen und Daten für dieses Feld erfasst wurden, kann das Feld nicht mehr entfernt werden. Daher ist es unerlässlich, beim ersten Erstellen Ihrer Schema einen iterativen Modellierungsansatz zu wählen, beginnend mit einer vereinfachten Implementierung, die im Laufe der Zeit immer komplexer wird.

Wenn Sie sich nicht sicher sind, ob ein bestimmtes Feld in ein Schema einbezogen werden muss, sollten Sie es am besten auslassen. Wenn später festgestellt wird, dass das Feld erforderlich ist, kann es immer in der nächsten Iteration des Schemas hinzugefügt werden.

### Identitätsfelder

In der Experience Platform werden als Identitäten markierte XDM-Felder verwendet, um Informationen über einzelne Kunden aus mehreren Datenquellen zusammenzuführen. Obwohl ein Schema mehrere Felder haben kann, die als Identitäten markiert sind, muss eine einzige primäre Identität definiert werden, damit das Schema für die Verwendung in [!DNL Real-time Customer Profile] aktiviert werden kann. Detailliertere Informationen zum Verwendungsfall dieser Schemas finden Sie im Abschnitt [Identitätsfelder](./composition.md#identity) in den Grundlagen der Feldzusammensetzung.

Beim Entwerfen Ihrer Schema sind alle Primärschlüssel in Ihren relationalen Datenbanktabellen wahrscheinlich Kandidaten für primäre Identitäten. Weitere Beispiele für anwendbare Identitätsfelder sind E-Mail-Adressen von Kunden, Telefonnummern, Konto-IDs und [ECID](../../identity-service/ecid.md).

### Adobe-Applikationsmischungen

Experience Platform bietet mehrere vordefinierte XDM-Mixins zur Erfassung von Daten zu den folgenden Adoben:

* Adobe Analytics
* Adobe Audience Manager
* Adobe Campaign
* Adobe Target

Beispielsweise können Sie mit dem [[!UICONTROL Adobe Analytics ExperienceEvent Template Mixin]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json) [!DNL Analytics]-spezifischen Feldern Ihren XDM-Schemas zuordnen. Abhängig von den Adobe-Anwendungen, mit denen Sie arbeiten, sollten Sie diese mit Adobe bereitgestellten Mixins in Ihren Schemas verwenden.

<img src="../images/best-practices/analytics-mixin.png" width="700"><br>

Bei Anwendungsanwendung-Mixins wird automatisch eine primäre Standardidentität zugewiesen, indem das Feld `identityMap` verwendet wird. Dabei handelt es sich um ein systemgeneriertes schreibgeschütztes Objekt, das Standardidentitätswerte für einen einzelnen Adobe zuordnet.

Bei Adobe Analytics ist die ECID die primäre Standardidentität. Wenn kein ECID-Wert von einem Kunden bereitgestellt wird, lautet die primäre Identität stattdessen standardmäßig AAID.

>[!IMPORTANT]
>
>Bei Verwendung von Adobe-Anwendungs-Mixins sollten keine anderen Felder als primäre Identität gekennzeichnet werden. Wenn es zusätzliche Eigenschaften gibt, die als Identitäten gekennzeichnet werden müssen, müssen diese Felder stattdessen als sekundäre Identitäten zugewiesen werden.

## Nächste Schritte

In diesem Dokument wurden die allgemeinen Richtlinien und Best Practices für das Entwerfen Ihres Datenmodells zur Experience Platform behandelt. Zusammenfassung:

* Verwenden Sie einen Top-Down-Ansatz, indem Sie Ihre Datentabellen in Profil-, Lookup- und Ereignis-Kategorien sortieren, bevor Sie Ihre Schema erstellen.
* Es gibt oft mehrere Ansätze und Optionen, wenn es darum geht, Schema für unterschiedliche Zwecke zu gestalten.
* Ihr Datenmodell sollte Ihre geschäftlichen Anwendungsfälle wie Segmentierung oder Journey-Analyse unterstützen.
* Machen Sie Ihre Schemas so einfach wie möglich und fügen Sie nur dann neue Felder hinzu, wenn dies unbedingt erforderlich ist.

Sobald Sie bereit sind, finden Sie im Lernprogramm unter [Erstellen eines Schemas in der Benutzeroberfläche](../tutorials/create-schema-ui.md) schrittweise Anweisungen zum Erstellen eines Schemas, zum Zuweisen der entsprechenden Klasse für die Entität und zum Hinzufügen von Feldern zur Zuordnung Ihrer Daten.
