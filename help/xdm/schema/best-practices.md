---
keywords: Experience Platform;Startseite;beliebte Themen;Schemas;Schema;Aufzählung;primäre Identität;primäre Identitäten;XDM-Kontaktprofil;Erlebnisereignis;XDM Experience Event;XDM ExperienceEvent;experienceEvent;Experienceevent;XDM Experienceevent;Schemadesign;Best Practices
solution: Experience Platform
title: Best Practices für die Datenmodellierung
description: Dieses Dokument bietet Ihnen eine Einführung in Experience-Datenmodell (XDM)-Schemata und die Bausteine, Grundsätze und Best Practices zum Erstellen von Schemata, die in Adobe Experience Platform verwendet werden können.
exl-id: 2455a04e-d589-49b2-a3cb-abb5c0b4e42f
source-git-commit: 7521273c0ea4383b7141e9d7a82953257ff18c34
workflow-type: tm+mt
source-wordcount: '3236'
ht-degree: 56%

---

# Best Practices für die Datenmodellierung

[!DNL Experience Data Model] (XDM) ist das zentrale Framework, das Kundenerlebnisdaten standardisiert, indem gemeinsame Strukturen und Definitionen für nachgelagerte Adobe Experience Platform-Services bereitgestellt werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert und verwendet werden, um wertvolle Einblicke aus Kundenaktionen zu gewinnen, Kundenzielgruppen zu definieren und Kundenattribute für Personalisierungszwecke auszudrücken.

Da XDM vom Design her äußerst vielseitig und anpassbar ist, ist es wichtig, beim Entwerfen Ihrer Schemata Best Practices für die Datenmodellierung einzuhalten. In diesem Dokument werden die wichtigsten Entscheidungen und Überlegungen behandelt, die Sie beim Zuordnen Ihrer Kundenerlebnisdaten zu XDM treffen müssen.

## Erste Schritte

Bevor Sie dieses Handbuch lesen, sollten Sie sich mit der [Übersicht zum XDM-System](../home.md) beschäftigen, um eine allgemeine Einführung in XDM und seine Rolle in Experience Platform zu erhalten.

Da sich dieses Handbuch ausschließlich auf wichtige Überlegungen zum Schema-Design konzentriert, wird dringend empfohlen, die [Grundlagen der Schemakomposition](./composition.md) zu lesen, um detaillierte Erläuterungen zu den einzelnen Schemaelementen, die in diesem Handbuch erwähnt werden, zu erhalten.

## Zusammenfassung der Best Practices {#summary}

Der empfohlene Ansatz zum Entwerfen Ihres Datenmodells für die Verwendung in Experience Platform kann wie folgt zusammengefasst werden:

1. Machen Sie sich mit den geschäftlichen Anwendungsfällen für Ihre Daten vertraut.
1. Identifizieren Sie die primären Datenquellen, die für diese Anwendungsfälle in Experience Platform integriert werden sollten.
1. Identifizieren Sie alle sekundären Datenquellen, die ebenfalls von Interesse sein könnten. Wenn beispielsweise derzeit nur eine der Geschäftseinheiten in Ihrem Unternehmen daran interessiert ist, ihre Daten nach Experience Platform zu portieren, könnte eine ähnliche Geschäftseinheit in Zukunft auch daran interessiert sein, ähnliche Daten zu portieren. Die Berücksichtigung dieser sekundären Quellen hilft, das Datenmodell in Ihrem gesamten Unternehmen zu standardisieren.
1. Erstellen Sie ein allgemeines Entitätsbeziehungsdiagramm (Entity Relationship Diagram, ERD) für die identifizierten Datenquellen.
1. Konvertieren Sie das allgemeine ERD in ein Experience Platform-orientiertes ERD (einschließlich Profilen, Erlebnisereignissen und Lookup-Entitäten).

Die Schritte zur Identifizierung der für Ihre geschäftlichen Anwendungsfälle erforderlichen Datenquellen variieren von Organisation zu Organisation. Während sich die restlichen Abschnitte in diesem Dokument auf die letzteren Schritte der Organisation und Erstellung eines ERD nach der Identifizierung der Datenquellen konzentrieren, können die Erläuterungen der verschiedenen Diagrammkomponenten für Ihre Entscheidungen Informationen darüber liefern, welche Datenquellen nach Experience Platform migriert werden sollen.

## Erstellen eines allgemeinen ERD {#create-an-erd}

Nachdem Sie die Datenquellen ermittelt haben, die Sie in Experience Platform integrieren möchten, erstellen Sie ein allgemeines ERD, das Ihnen dabei hilft, Ihre Daten XDM-Schemata zuzuordnen.

Das folgende Beispiel stellt ein vereinfachtes ERD für ein Unternehmen dar, das Daten in Experience Platform importieren möchte. Das Diagramm zeigt die wesentlichen Entitäten, die in XDM-Klassen unterteilt werden sollten, einschließlich Kundenkonten, Hotels und mehreren gängigen E-Commerce-Ereignissen.

![Ein relationales Entitätsdiagramm, das die wesentlichen Entitäten hervorhebt, die bei der Datenaufnahme in XDM-Klassen sortiert werden sollten.](../images/best-practices/erd.png)

## Sortieren von Entitäten in Profil-, Lookup- und Ereigniskategorien {#sort-entities}

Nachdem Sie ein ERD erstellt haben, um die wesentlichen Entitäten zu identifizieren, die Sie in Experience Platform integrieren möchten, müssen diese Entitäten nach Profil-, Lookup- und Ereigniskategorien sortiert werden:

| Kategorie | Beschreibung |
| --- | --- |
| Profilentitäten | Profilentitäten stellen Attribute dar, die sich auf eine einzelne Person beziehen, normalerweise eine Kundin oder einen Kunden. Entitäten, die unter diese Kategorie fallen, sollten durch Schemata auf Basis der **[!DNL XDM Individual Profile]-Klasse** dargestellt werden. |
| Lookup-Entitäten | Lookup-Entitäten stellen Konzepte dar, die sich auf eine einzelne Person beziehen, aber nicht direkt zur Identifizierung der Person verwendet werden können. Entitäten, die unter diese Kategorie fallen, sollten durch Schemata dargestellt werden, die auf **benutzerdefinierten Klassen** basieren, und sind durch [Schemabeziehungen](../tutorials/relationship-ui.md) mit Profilen und Ereignissen verknüpft. |
| Ereignisentitäten | Ereignisentitäten stellen Konzepte dar, die sich auf Aktionen beziehen, die eine Kundin oder ein Kunde ausführen kann, Systemereignisse oder andere Konzepte, bei denen Sie Änderungen im Laufe der Zeit verfolgen möchten. Entitäten, die unter diese Kategorie fallen, sollten durch Schemata auf Basis der **[!DNL XDM ExperienceEvent]-Klasse** dargestellt werden. |

{style="table-layout:auto"}

### Überlegungen zum Sortieren von Entitäten {#considerations}

Die folgenden Abschnitte enthalten weitere Anleitungen zum Sortieren Ihrer Entitäten in die oben genannten Kategorien.

#### Veränderliche und unveränderliche Daten {#mutable-and-immutable-data}

Eine grundlegende Möglichkeit zur Sortierung zwischen Entitätskategorien besteht darin, ob die erfassten Daten veränderlich sind oder nicht.

Attribute, die zu Profilen oder Lookup-Entitäten gehören, sind normalerweise veränderlich. Beispielsweise können sich die Präferenzen einer Kundin oder eines Kunden im Laufe der Zeit ändern, und die Parameter eines Abonnementplans können je nach Markttrends aktualisiert werden.

Im Gegensatz dazu sind Ereignisdaten normalerweise unveränderlich. Da Ereignisse mit einem bestimmten Zeitstempel verbunden sind, ändert sich der von einem Ereignis bereitgestellte „System-Schnappschuss“ nicht. Beispielsweise kann ein Ereignis die Kundenpräferenzen beim Kassengang erfassen. Dies ändert sich auch dann nicht, wenn sich die Kundenpräferenzen später ändern. Ereignisdaten können nach ihrer Aufzeichnung nicht mehr geändert werden.

Zusammenfassend lässt sich sagen, dass Profile und Lookup-Entitäten veränderliche Attribute enthalten und aktuelle Informationen über die von ihnen erfassten Themen darstellen, während es sich bei Ereignissen um unveränderliche Aufzeichnungen des Systems zu einem bestimmten Zeitpunkt handelt.

#### Kundenattribute {#customer-attributes}

Wenn eine Entität Attribute enthält, die sich auf eine einzelne Kundin oder einen einzelnen Kunden beziehen, ist sie höchstwahrscheinlich eine Profilentität. Beispiele für Kundenattribute sind:

* Persönliche Daten wie Name, Geburtsdatum, Geschlecht und Konto-ID(s).
* Standortinformationen wie Adressen und GPS-Informationen.
* Kontaktinformationen wie Telefonnummern und E-Mail-Adressen.

#### Tracking von Daten im Laufe der Zeit {#track-data}

Wenn Sie analysieren möchten, wie sich bestimmte Attribute innerhalb einer Entität im Laufe der Zeit ändern, handelt es sich höchstwahrscheinlich um eine Ereignisentität. Das Hinzufügen von Produktelementen zum Warenkorb kann beispielsweise in Experience Platform als Ereignis vom Typ „In den Warenkorb legen“ verfolgt werden:

| Kunden-ID | Typ | Produkt-ID | Menge | Zeitstempel |
| --- | --- | --- | --- | --- |
| 1234567 | Hinzufügen | 275098 | 2 | 1. Oktober, 10:32 Uhr |
| 1234567 | Entfernen | 275098 | 1 | 1. Oktober, 10:33 Uhr |
| 1234567 | Hinzufügen | 486502 | 1 | 1. Oktober, 10:41 Uhr |
| 1234567 | Hinzufügen | 910482 | 5 | 3. Oktober, 14:15 Uhr |

{style="table-layout:auto"}

#### Anwendungsfälle für die Segmentierung {#segmentation-use-cases}

Bei der Kategorisierung Ihrer Entitäten ist es wichtig, über die Zielgruppen nachzudenken, die Sie für Ihre speziellen geschäftlichen Anwendungsfälle erstellen möchten.

Ein Unternehmen möchte beispielsweise alle „Gold“- oder „Platin“-Mitglieder seines Treueprogramms kennen, die im letzten Jahr mehr als fünf Käufe getätigt haben. Basierend auf dieser Segmentierungslogik können die folgenden Schlussfolgerungen zur Darstellung relevanter Entitäten gezogen werden:

* „Gold“ und „Platin“ stellen den Treuestatus einer Kundin oder eines Kunden dar. Da sich die Segmentierungslogik nur auf den aktuellen Treuestatus von Kundinnen und Kunden bezieht, können diese Daten als Teil eines Profilschemas modelliert werden. Wenn Sie jedoch Änderungen des Treuestatus im Laufe der Zeit verfolgen möchten, können Sie auch ein zusätzliches Ereignisschema für Änderungen des Treuestatus erstellen.
* Käufe sind Ereignisse, die zu einem bestimmten Zeitpunkt auftreten. Die Segmentierungslogik bezieht sich auf Kaufereignisse innerhalb eines bestimmten Zeitfensters. Diese Daten sollten daher als Ereignisschema modelliert werden.

#### Anwendungsfälle für die Aktivierung {#activation-use-cases}

Zusätzlich zu Überlegungen zu Anwendungsfällen für die Segmentierung sollten Sie auch die Anwendungsfälle für die Aktivierung für diese Zielgruppen überprüfen, um zusätzliche relevante Attribute zu identifizieren.

Zum Beispiel hat ein Unternehmen eine Zielgruppe basierend auf der Regel `country = US` erstellt. Wenn diese Zielgruppe dann für bestimmte nachgelagerte Ziele aktiviert wird, möchte das Unternehmen alle exportierten Profile nach dem Heimat-Bundesstaat filtern. Daher sollte ein `state`-Attribut auch in der entsprechenden Profilentität erfasst werden.

#### Aggregierte Werte {#aggregated-values}

Basierend auf dem Anwendungsfall und der Granularität Ihrer Daten sollten Sie entscheiden, ob bestimmte Werte vorab aggregiert werden müssen, bevor sie in eine Profil- oder Ereignisentität aufgenommen werden.

Beispielsweise möchte ein Unternehmen eine Zielgruppe basierend auf der Anzahl der Warenkorbkäufe erstellen. Sie können festlegen, dass diese Daten mit der niedrigsten Granularität integriert werden, indem Sie jedes Kaufereignis mit Zeitstempel als eigene Entität hinzufügen. Dadurch kann sich jedoch manchmal die Anzahl der aufgezeichneten Ereignisse exponentiell erhöhen. Um die Anzahl der aufgenommenen Ereignisse zu reduzieren, können Sie einen Aggregatwert `numberOfPurchases` über einen langen Wochen- oder Monatszeitraum erstellen. Andere Aggregatfunktionen wie MIN und MAX können ebenfalls auf diese Situationen angewendet werden.

>[!CAUTION]
>
>Experience Platform führt derzeit keine automatische Wertaggregation durch, obwohl dies für zukünftige Versionen geplant ist. Wenn Sie aggregierte Werte verwenden möchten, müssen Sie die Berechnungen extern durchführen, bevor Sie die Daten an Experience Platform senden.

#### Kardinalität {#cardinality}

Die in Ihrem ERD festgelegten Kardinalitäten können auch einige Hinweise zur Kategorisierung Ihrer Entitäten liefern. Wenn eine Eins-zu-viele-Beziehung zwischen zwei Entitäten besteht, ist die Entität, die für „viele“ steht, wahrscheinlich eine Ereignisentität. Es gibt jedoch auch Fälle, in denen es sich bei „viele“ um eine Gruppe von Lookup-Entitäten handelt, die als Array innerhalb einer Profilentität bereitgestellt werden.

>[!NOTE]
>
>Da es keinen universellen Ansatz für alle Anwendungsfälle gibt, ist es wichtig, die Vor- und Nachteile jeder Situation bei der Kategorisierung von Entitäten auf Grundlage der Kardinalität zu berücksichtigen. Weitere Informationen finden Sie im [nächsten Abschnitt](#pros-and-cons).

In der folgenden Tabelle sind einige allgemeine Entitätsbeziehungen und die daraus abgeleiteten Kategorien aufgeführt:

| Beziehung | Kardinalität | Entitätskategorien |
| --- | --- | --- |
| Kunden- und Warenkorb-Checkout | Eins zu viele | Eine Kundin oder ein Kunde kann über viele Warenkorb-Kassengänge verfügen, bei denen es sich um Ereignisse handelt, die im Laufe der Zeit verfolgt werden können. Der Kunde wäre daher eine Profilentität, während der Warenkorb-Checkout eine Ereignisentität wäre. |
| Kunden- und Treuekonto | Eins zu eins | Eine Kundin oder ein Kunde kann nur über ein Treuekonto verfügen und ein Treuekonto kann nur zu einer Kundin oder einem Kunden gehören. Da es sich um eine Eins-zu-eins-Beziehung handelt, stellen sowohl Kunden- als auch Treuekontenentitäten Profilentitäten dar. |
| Kunde und Abonnement | Eins zu viele | Eine Kundin oder ein Kunde kann über viele Abonnements verfügen. Da es dem Unternehmen nur um die aktuellen Abonnements einer Kundin oder eines Kunden geht, ist die Kundin oder der Kunde eine Profilentität, während das Abonnement eine Lookup-Entität ist. |

{style="table-layout:auto"}

### Vor- und Nachteile verschiedener Entitätsklassen {#pros-and-cons}

Der vorherige Abschnitt liefert zwar einige allgemeine Richtlinien zur Kategorisierung von Entitäten, es ist jedoch wichtig zu verstehen, dass es häufig Vor- und Nachteile bei der Auswahl einer Entitätskategorie gegenüber einer anderen geben kann. Die folgende Fallstudie soll veranschaulichen, wie Sie in diesen Situationen Ihre Möglichkeiten abwägen können.

Ein Unternehmen verfolgt die aktiven Abonnements seiner Kundschaft nach, bei denen eine Kundin oder ein Kunde über viele Abonnements verfügen kann. Das Unternehmen möchte auch Abonnements für Anwendungsfälle zur Segmentierung einbeziehen, z. B. alle Benutzende mit aktiven Abonnements finden.

In diesem Szenario hat das Unternehmen zwei Möglichkeiten, die Abonnements einer Kundin oder eines Kunden in seinem Datenmodell darzustellen:

1. [Verwenden von Profilattributen](#profile-approach)
1. [Verwenden von Ereignisentitäten](#event-approach)

#### Ansatz 1: Verwenden von Profilattributen {#profile-approach}

Der erste Ansatz besteht darin, ein Array von `subscriptionID` in die Profilentität für den Kunden aufzunehmen.

![Das Kundenschema im Schema-Editor mit hervorgehobener Klasse und Struktur](../images/best-practices/profile-schema.png)

**Vorteile**

* Eine Segmentierung ist für den vorgesehenen Anwendungsfall möglich.
* Das Schema behält nur die neuesten Abonnementdatensätze für eine Kundin oder einen Kunden bei.

**Nachteile**

* Das gesamte Array muss jedes Mal neu aufgenommen werden, wenn Änderungen an einem Feld im Array auftreten.
* Wenn verschiedene Datenquellen oder Geschäftseinheiten Daten in das Array einspeisen, wird es schwierig, das neueste aktualisierte Array über alle Kanäle hinweg zu synchronisieren.

#### Ansatz 2: Verwenden von Ereignisentitäten {#event-approach}

Der zweite Ansatz besteht darin, Ereignisschemata zur Darstellung eines Abonnementereignisses zu verwenden. Dazu gehören die Abonnement-ID zusammen mit einer Kunden-ID und einem Zeitstempel, der angibt, wann das Abonnementereignis aufgetreten ist.

![Ein Diagramm des Abonnementereignisschemas mit hervorgehobener XDM-Erlebnisereignisklasse und hervorgehobener Abonnementstruktur.](../images/best-practices/event-schema.png)

**Vorteile**

* Segmentierungsregeln können flexibler sein (z. B. Suchen nach allen Kundinnen und Kunden, die ihre Abonnements in den letzten 30 Tagen geändert haben).
* Wenn sich der Abonnementstatus einer Kundin oder eines Kunden ändert, müssen Sie kein langes, potenziell komplexes Array mehr innerhalb der Profilattribute der Kundin oder des Kunden aktualisieren. Dies ist besonders nützlich, wenn gleichzeitige Änderungen an der Abonnement-Liste der Kundin oder des Kunden aus mehreren Quellen auftreten.

**Nachteile**

* Die Segmentierung wird für den ursprünglich vorgesehenen Anwendungsfall komplexer (Identifizierung des Status der neuesten Abonnements von Kundinnen und Kunden). Die Zielgruppe benötigt jetzt zusätzliche Logik, um das letzte Abonnementereignis zu kennzeichnen, damit eine Kundin oder ein Kunde seinen Status überprüfen kann.
* Bei Ereignissen besteht ein höheres Risiko, dass sie automatisch ablaufen und aus dem Profilspeicher gelöscht werden. Weitere Informationen finden Sie im Handbuch zum [Ablaufen von Erlebnisereignissen](../../profile/event-expirations.md).

## Erstellen von Schemata basierend auf kategorisierten Entitäten {#schemas-for-categorized-entities}

Nachdem Sie Ihre Entitäten nach Profil-, Lookup- und Ereigniskategorien sortiert haben, können Sie mit der Konvertierung Ihres Datenmodells in XDM-Schemata beginnen. Zu Demonstrationszwecken wurde das zuvor dargestellte Datenmodell im folgenden Diagramm in geeignete Kategorien unterteilt:

![Ein Diagramm der in den Profil-, Lookup- und Ereignisentitäten enthaltenen Schemata](../images/best-practices/erd-sorted.png)

Die Kategorie, in der eine Entität eingeordnet wurde, sollte die XDM-Klasse bestimmen, auf der Sie deren Schema basieren. Zur Wiederholung:

* Profilentitäten sollten die [!DNL XDM Individual Profile]-Klasse verwenden.
* Ereignisentitäten sollten die [!DNL XDM ExperienceEvent]-Klasse verwenden.
* Lookup-Entitäten sollten benutzerdefinierte XDM-Klassen verwenden, die von Ihrem Unternehmen definiert wurden. Profil- und Ereignisentitäten können diese Lookup-Entitäten dann über Schemabeziehungen referenzieren.

>[!NOTE]
>
>Während Ereignisentitäten fast immer durch separate Schemata dargestellt werden, können Entitäten in Profil- oder Lookup-Kategorien je nach Kardinalität in einem einzelnen XDM-Schema kombiniert werden.
>
>Da beispielsweise die Entität „Kunde“ eine Eins-zu-eins-Beziehung zur Entität „Treuekonto“ hat, könnte das Schema für die Entität „Kunde“ auch ein `LoyaltyAccount`-Objekt mit den entsprechenden Treuefeldern für jede Kundin oder jeden Kunden enthalten. Bei einer Eins-zu-viele-Beziehung kann die Entität, die für „viele“ steht, je nach ihrer Komplexität durch ein separates Schema oder ein Array von Profilattributen dargestellt werden.

Die folgenden Abschnitte enthalten allgemeine Anleitungen zum Erstellen von Schemata basierend auf Ihrem ERD.

### Anwendung eines iterativen Modellierungsansatzes {#iterative-modeling}

Die [Regeln zur Schemaentwicklung](./composition.md#evolution) schreiben vor, dass nur zerstörungsfreie Änderungen an Schemata vorgenommen werden können, nachdem sie implementiert wurden. Mit anderen Worten: Wenn Sie einem Schema ein Feld hinzufügen und Daten für dieses Feld aufgenommen wurden, kann das Feld nicht mehr entfernt werden. Daher ist es wichtig, bei der Ersterstellung Ihrer Schemata einen iterativen Modellierungsansatz anzuwenden, beginnend mit einer vereinfachten Implementierung, die im Laufe der Zeit immer komplexer wird.

Wenn Sie nicht sicher sind, ob ein bestimmtes Feld für die Aufnahme in ein Schema erforderlich ist, empfiehlt es sich, es auszuschließen. Wenn später festgestellt wird, dass das Feld erforderlich ist, kann es jederzeit bei der nächsten Iteration des Schemas hinzugefügt werden.

### Identitätsfelder {#identity-fields}

In Experience Platform werden als Identitäten markierte XDM-Felder verwendet, um Informationen über einzelne Kundinnen und Kunden aus mehreren Datenquellen zusammenzufügen. Obwohl ein Schema mehrere als Identitäten markierte Felder enthalten kann, muss eine einzige primäre Identität definiert werden, damit das Schema zur Verwendung in [!DNL Real-Time Customer Profile] aktiviert wird. Ausführlichere Informationen zum Anwendungsfall für diese Felder finden Sie im Abschnitt zu [Identitätsfeldern](./composition.md#identity) in den Grundlagen der Schemakomposition.

Beim Entwerfen Ihrer Schemata sind alle Primärschlüssel in Ihren relationalen Datenbanktabellen mögliche Kandidaten für primäre Identitäten. Weitere Beispiele für anwendbare Identitätsfelder sind E-Mail-Adressen, Telefonnummern, Konto-IDs und [ECID](../../identity-service/features/ecid.md) der Kundschaft.

### Schemafeldgruppen für Adobe-Anwendungen {#adobe-application-schema-field-groups}

Experience Platform bietet mehrere vordefinierte XDM-Schemafeldgruppen zur Erfassung von Daten, die sich auf die folgenden Adobe-Anwendungen beziehen:

* Adobe Analytics
* Adobe Audience Manager
* Adobe Campaign
* Adobe Target

Beispielsweise können Sie die [[!UICONTROL Adobe Analytics ExperienceEvent-Vorlage] Feldergruppe](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json) verwenden, um [!DNL Analytics] Felder Ihren XDM-Schemata zuzuordnen. Je nach den Adobe-Anwendungen, mit denen Sie arbeiten, sollten Sie diese von Adobe bereitgestellten Feldergruppen in Ihren Schemata verwenden.

![Schemadiagramm der [!UICONTROL Adobe Analytics ExperienceEvent-Vorlage].](../images/best-practices/analytics-field-group.png)

Feldergruppen der Adobe-Anwendungen weisen automatisch eine standardmäßige primäre Identität über das Feld `identityMap` zu, ein systemgeneriertes, schreibgeschütztes Objekt, das standardmäßige Identitätswerte für einzelne Kundinnen und Kunden zuordnet.

Bei Adobe Analytics ist ECID die standardmäßige primäre Identität. Wenn ein ECID-Wert nicht von einem Kunden bereitgestellt wird, ist für die primäre Identität stattdessen „AAID“ festgelegt.

>[!IMPORTANT]
>
>Bei Verwendung von Feldergruppen für Adobe-Anwendungen sollten keine anderen Felder als primäre Identität markiert werden. Wenn es zusätzliche Eigenschaften gibt, die als Identitäten markiert werden müssen, müssen diese Felder stattdessen als sekundäre Identitäten zugewiesen werden.

## Datenvalidierungsfelder {#data-validation-fields}

Wenn Sie Daten in den Data Lake aufnehmen, wird die Datenvalidierung nur für eingeschränkte Felder erzwungen. Um ein bestimmtes Feld während einer Batch-Aufnahme zu überprüfen, müssen Sie das Feld im XDM-Schema als eingeschränkt markieren. Um zu verhindern, dass fehlerhafte Daten in Experience Platform aufgenommen werden, wird empfohlen, beim Erstellen der Schemata die Kriterien für die Validierung auf Feldebene zu definieren.

>[!IMPORTANT]
>
>Die Validierung gilt nicht für verschachtelte Spalten. Wenn sich das Feldformat in einer Array-Spalte befindet, werden die Daten nicht validiert.

Um Einschränkungen für ein bestimmtes Feld festzulegen, wählen Sie das Feld aus dem Schema-Editor aus, um die Seitenleiste **[!UICONTROL Feldeigenschaften]** zu öffnen. Genaue Beschreibungen der [&#x200B; Felder finden Sie in der Dokumentation &#x200B;](../ui/fields/overview.md#type-specific-properties)Typspezifische Feldeigenschaften“.

![Der Schema-Editor mit den Einschränkungsfeldern, die in der Seitenleiste [!UICONTROL Feldeigenschaften] hervorgehoben sind.](../images/best-practices/data-validation-fields.png)

### Tipps zur Wahrung der Datenintegrität {#data-integrity-tips}

Im Folgenden finden Sie eine Sammlung von Vorschlägen zur Wahrung der Datenintegrität beim Erstellen eines Schemas.

* **Primäre Identitäten berücksichtigen**: Bei Adobe-Produkten wie Web SDK, Mobile SDK, Adobe Analytics und Adobe Journey Optimizer dient das Feld `identityMap` häufig als primäre Identität. Vermeiden Sie es, zusätzliche Felder als primäre Identitäten für dieses Schema festzulegen.
* **Stellen Sie sicher, dass `_id` nicht als Identität verwendet wird**: Das Feld &quot;`_id`&quot; in Erlebnisereignis-Schemata kann nicht als Identität verwendet werden, da es für die Eindeutigkeit von Datensätzen vorgesehen ist.
* **Längenbeschränkungen festlegen**: Es empfiehlt sich, Mindest- und Höchstlängen für Felder festzulegen, die als Identitäten markiert sind. Eine Warnung Trigger, wenn Sie versuchen, einem Identitätsfeld einen benutzerdefinierten Namespace zuzuweisen, ohne die Begrenzungen der minimalen und maximalen Länge zu erfüllen. Diese Einschränkungen helfen bei der Aufrechterhaltung der Konsistenz und der Datenqualität.
* **Muster auf konsistente Werte anwenden**: Wenn Ihre Identitätswerte einem bestimmten Muster folgen, sollten Sie die Einstellung **[!UICONTROL Muster]** verwenden, um diese Einschränkung zu erzwingen. Diese Einstellung kann Regeln wie nur Ziffern, Groß- oder Kleinbuchstaben oder bestimmte Zeichenkombinationen enthalten. Verwenden Sie reguläre Ausdrücke, um Muster in Ihren Zeichenfolgen abzugleichen.
* **eVars in Analytics-Schemata begrenzen**: Normalerweise sollte ein Analytics-Schema nur über eine eVar verfügen, die als Identität gekennzeichnet ist. Wenn Sie mehr als einen eVar als Identität verwenden möchten, sollten Sie überprüfen, ob die Datenstruktur optimiert werden kann.
* **Eindeutigkeit eines ausgewählten Felds sicherstellen**: Das ausgewählte Feld sollte im Vergleich zur primären Identität im Schema eindeutig sein. Ist dies nicht der Fall, markieren Sie sie nicht als Identität. Wenn beispielsweise mehrere Kunden dieselbe E-Mail-Adresse angeben können, ist dieser Namespace keine geeignete Identität. Dieses Prinzip gilt auch für andere Identity-Namespaces wie Telefonnummern. Das Markieren eines nicht eindeutigen Felds als Identität könnte zu einem unerwünschten Profilausfall führen.
* **Mindestlänge der Zeichenfolge überprüfen**: Alle Zeichenfolgenfelder sollten mindestens ein Zeichen lang sein, da Zeichenfolgenwerte niemals leer sein sollten. Null-Werte für nicht erforderliche Felder sind jedoch zulässig. Neue Zeichenfolgenfelder haben standardmäßig eine Mindestlänge von einem Zeichen.

## Nächste Schritte

In diesem Dokument wurden die allgemeinen Richtlinien und Best Practices zum Entwerfen Ihres Datenmodells für Experience Platform behandelt. Zur Zusammenfassung:

* Verwenden Sie einen Oben-nach-unten-Ansatz, indem Sie Ihre Datentabellen nach Profil-, Lookup- und Ereigniskategorien sortieren, bevor Sie Ihre Schemata erstellen.
* Es gibt oft mehrere Ansätze und Optionen beim Entwerfen von Schemata für unterschiedliche Zwecke.
* Ihr Datenmodell sollte Ihre geschäftlichen Anwendungsfälle wie Segmentierung oder Analyse der Customer Journey unterstützen.
* Machen Sie Ihre Schemata so einfach wie möglich und fügen Sie nur dann neue Felder hinzu, wenn dies unbedingt erforderlich ist.

Wenn Sie fertig sind, finden Sie im Tutorial zum [Erstellen eines Schemas in der Benutzeroberfläche](../tutorials/create-schema-ui.md) schrittweise Anweisungen zum Erstellen eines Schemas, Zuweisen der entsprechenden Klasse für die Entität und Hinzufügen von Feldern, um diesen Daten zuzuordnen.
