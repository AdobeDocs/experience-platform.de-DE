---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Grundlagen der Schema-Komposition
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '2761'
ht-degree: 0%

---


# Grundlagen der Schema-Komposition

Dieses Dokument bietet eine Einführung in Experience Data Model-(XDM-)Schema und die Bausteine, Grundsätze und Best Practices zum Erstellen von Schemas, die in der Adobe Experience Platform verwendet werden sollen. Allgemeine Informationen zu XDM und dessen Verwendung in der Platform finden Sie in der [XDM-Systemübersicht](../home.md).

## Schemas verstehen

Ein Schema ist ein Regelsatz, der die Datenstruktur und das Datenformat darstellt und überprüft. Auf hoher Ebene bieten Schema eine abstrakte Definition eines realen Objekts (z. B. einer Person) und legen dar, welche Daten in jeder Instanz dieses Objekts enthalten sein sollen (z. B. Vorname, Nachname, Geburtstag usw.).

Zusätzlich zur Beschreibung der Datenstruktur wenden Schema Einschränkungen und Erwartungen auf Daten an, damit sie bei der Migration zwischen Systemen validiert werden können. Mit diesen Standarddefinitionen können Daten unabhängig von der Herkunft konsistent interpretiert werden. Zudem entfällt die Notwendigkeit für anwendungsübergreifende Übersetzungen.

Experience Platform behält diese semantische Normalisierung durch den Einsatz von Schemas bei. Schema sind die Standardmethode zur Beschreibung von Daten in der Experience Platform, sodass alle Daten, die Schemas entsprechen, innerhalb eines Unternehmens problemlos wiederverwendet werden können und sogar für mehrere Unternehmen freigegeben werden können.

### Relationale Tabellen im Vergleich zu eingebetteten Objekten

Beim Arbeiten mit relationalen Datenbanken umfassen die Best Practices die Normalisierung von Daten oder die Übernahme einer Entität und deren Aufteilung in einzelne Teile, die dann über mehrere Tabellen hinweg angezeigt werden. Um die Daten als Ganzes zu lesen oder die Entität zu aktualisieren, müssen Lese- und Schreibvorgänge über viele einzelne Tabellen mit JOIN durchgeführt werden.

Durch den Einsatz von eingebetteten Objekten können XDM-Schema komplexe Daten direkt darstellen und in eigenständigen Dokumenten mit hierarchischer Struktur speichern. Einer der Hauptvorteile dieser Struktur besteht darin, dass Sie damit die Daten Abfrage haben, ohne die Entität durch teure Verbindungen zu mehreren denormalisierten Tabellen rekonstruieren zu müssen.

### Schemas und Big Data

Moderne digitale Systeme generieren enorme Mengen von Verhaltenssignalen (Transaktionsdaten, Weblogs, Internet von Dingen, Anzeige usw.). Diese Big-Data-Daten bieten außergewöhnliche Möglichkeiten zur Optimierung von Erlebnissen, sind aber aufgrund der Größe und Vielfalt der Daten schwierig zu nutzen. Um aus den Daten Nutzen zu ziehen, müssen Struktur, Format und Definitionen standardisiert werden, damit sie konsistent und effizient verarbeitet werden können.

Schemas lösen dieses Problem, indem sie die Integration von Daten aus mehreren Quellen, die Standardisierung durch gemeinsame Strukturen und Definitionen und die lösungsübergreifende gemeinsame Nutzung ermöglichen. Dadurch können nachfolgende Prozesse und Dienste jede Art von Frage beantworten, die von den Daten gestellt wird, und sich von dem herkömmlichen Ansatz zur Datenmodellierung abwenden, bei dem alle Fragen, die an die Daten gestellt werden, im Voraus bekannt sind und die Daten modelliert werden, um diesen Erwartungen zu entsprechen.

### Schema-basierte Workflows in Experience Platform

Die Normung ist ein Schlüsselbegriff für die Experience Platform. XDM, unterstützt von Adobe, ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Standard-Schema für das Kundenerlebnis-Management zu definieren.

Die als XDM-System bekannte Infrastruktur, auf der die Experience Platform aufgebaut ist, erleichtert Schema-basierte Workflows und umfasst die Schema-Registrierung, den Schema-Editor, Schema-Metadaten und Dienstverbrauchsmuster. See the [XDM System overview](../home.md) for more information.

## Planen Ihres Schemas

Der erste Schritt beim Erstellen eines Schemas besteht darin, das Konzept oder das Objekt der realen Welt zu bestimmen, das Sie im Schema erfassen möchten. Sobald Sie das Konzept, das Sie beschreiben möchten, identifizieren, können Sie mit der Planung Ihres Schemas beginnen, indem Sie über Dinge wie die Art der Daten, potenzielle Identitätsfelder und wie sich das Schema in Zukunft entwickeln könnte.

### Datenverhalten in der Experience Platform

Daten, die zur Verwendung in der Experience Platform vorgesehen sind, werden in zwei Verhaltenstypen unterteilt:

* **Daten** aufzeichnen: Stellt Informationen zu den Attributen eines Betreffs bereit. Ein Thema könnte eine Organisation oder eine Einzelperson sein.
* **Zeitreihendaten**: Stellt eine Momentaufnahme des Systems zum Zeitpunkt dar, zu dem eine Aktion entweder direkt oder indirekt von einem Datensatzsubjekt durchgeführt wurde.

Alle XDM-Schema beschreiben Daten, die als Datensatz- oder Zeitreihen kategorisiert werden können. Das Datenverhalten eines Schemas wird durch die **Klasse** des Schemas definiert, die einem Schema beim ersten Erstellen zugewiesen wird. XDM-Klassen werden weiter unten in diesem Dokument detailliert beschrieben.

Sowohl Schemas der Datensatz- als auch der Zeitreihen enthalten eine Zuordnung der Identitäten (`xdm:identityMap`). Dieses Feld enthält die Identitätsdarstellung eines Betreffs, die aus den als &quot;Identität&quot;markierten Feldern gezogen wird, wie im nächsten Abschnitt beschrieben.

### Identität

Schema werden zur Erfassung von Daten in die Experience Platform verwendet. Diese Daten können über mehrere Dienste hinweg verwendet werden, um eine einzelne, einheitliche Ansicht einer einzelnen Entität zu erstellen. Daher ist es wichtig, wenn man über Schema nachdenkt, über &quot;Identität&quot; nachzudenken und welche Felder zur Identifizierung eines Fächers verwendet werden können, unabhängig davon, woher die Daten kommen.

Um diesen Prozess zu unterstützen, können Schlüsselfelder als &quot;Identität&quot;markiert werden. Bei der Datenerfassung werden die Daten in diesen Feldern in das &quot;Identitätsdiagramm&quot; für die betreffende Person eingefügt. Die Diagrammdaten können dann vom [Echtzeit-Kundenservice](../../profile/home.md) und anderen Experience Platformen aufgerufen werden, um eine zusammengeführte Ansicht der einzelnen Kunden zu bieten.

Zu den Feldern, die häufig als &quot;Identität&quot;gekennzeichnet werden, gehören: E-Mail-Adresse, Telefonnummer, [Experience Cloud-ID (ECID)](https://docs.adobe.com/content/help/de-DE/id-service/using/home.html), CRM-ID oder andere eindeutige ID-Felder. Sie sollten außerdem alle eindeutigen IDs berücksichtigen, die für Ihr Unternehmen spezifisch sind, da es sich hierbei auch um gute &quot;Identität&quot;-Felder handeln kann.

Es ist wichtig, während der Planungsphase des Schemas über Kundenidentitäten nachzudenken, um sicherzustellen, dass Daten zusammengeführt werden, um ein möglichst stabiles Profil zu schaffen. In der Übersicht über den [Identitätsdienst](../../identity-service/home.md) erfahren Sie mehr darüber, wie Identitätsinformationen Ihnen dabei helfen können, Ihren Kunden digitale Erlebnisse bereitzustellen.

### Schema Evolutionsprinzipien {#evolution}

Mit zunehmender Entwicklung der digitalen Erfahrungen müssen auch die Schema, die sie repräsentieren, weiterentwickelt werden. Ein gut konzipiertes Schema ist daher in der Lage, sich je nach Bedarf anzupassen und weiterzuentwickeln, ohne zerstörerische Änderungen an früheren Versionen des Schemas zu verursachen.

Da die Abwärtskompatibilität für die Entwicklung von Schemas entscheidend ist, setzt die Experience Platform ein rein additives Versionsprinzip um, um sicherzustellen, dass Änderungen am Schema nur zu nicht-destruktiven Aktualisierungen und Änderungen führen. Mit anderen Worten, **Umbrüche werden nicht unterstützt.**

| Unterstützte Änderungen | Breaking changes (nicht unterstützt) |
|------------------------------------|---------------------------------|
| <ul><li>Hinzufügen neuer Felder zu einem vorhandenen Schema</li><li>Ein obligatorisches Feld als optional definieren</li></ul> | <ul><li>Entfernen zuvor definierter Felder</li><li>Neue obligatorische Felder</li><li>Umbenennen oder Neudefinieren vorhandener Felder</li><li>Entfernen oder Eingrenzen zuvor unterstützter Feldwerte</li><li>Verschieben von Attributen an eine andere Position in der Struktur</li></ul> |

>[!NOTE]
>
>Wenn ein Schema noch nicht zum Erfassen von Daten in die Experience Platform verwendet wurde, können Sie eine Umbruchänderung an diesem Schema vornehmen. Sobald das Schema jedoch in der Platform verwendet wurde, muss es der Richtlinie für die additive Versionierung entsprechen.

### Schema und Datenerfassung

Damit Daten in die Experience Platform aufgenommen werden können, muss zunächst ein Datensatz erstellt werden. Datasets sind die Bausteine für die Datenumwandlung und -verfolgung für den [Katalogdienst](../../catalog/home.md)und stellen im Allgemeinen Tabellen oder Dateien dar, die erfasste Daten enthalten. Alle Datensätze basieren auf vorhandenen XDM-Schemas, die Einschränkungen dafür enthalten, was die erfassten Daten enthalten und wie sie strukturiert sein sollten. Weitere Informationen finden Sie in der Übersicht zur Dateneinbettung in der [Adobe Experience Platform](../../ingestion/home.md) .

## Bausteine eines Schemas

Experience Platform verwendet einen Kompositionsansatz, bei dem Standardbausteine kombiniert werden, um Schema zu erstellen. Dieser Ansatz fördert die Wiederverwendbarkeit bestehender Komponenten und sorgt für Standardisierung in der gesamten Branche, um Schema und Komponenten in der Platform zu unterstützen.

Schema werden nach folgender Formel zusammengestellt:

**Klasse + Mixin&amp;ast; = XDM-Schema**

&amp;ast;Ein Schema besteht aus einer Klasse und _Null oder mehr_ Mixins. Das bedeutet, dass Sie ein DataSet-Schema ohne Mixins zusammenstellen können.

### Class

Das Erstellen eines Schemas beginnt mit dem Zuweisen einer Klasse. Klassen definieren die Verhaltensaspekte der Daten, die das Schema enthalten soll (Datensatz oder Zeitreihen). Darüber hinaus beschreiben Klassen die kleinste Anzahl gemeinsamer Eigenschaften, die alle Schema, die auf dieser Klasse basieren, einschließen müssen, und bieten eine Möglichkeit zum Zusammenführen mehrerer kompatibler Datensätze.

Eine Klasse bestimmt auch, welche Mixins für die Verwendung im Schema zugelassen werden. Dies wird im folgenden Abschnitt [mixin](#mixin) ausführlicher erläutert.

Es gibt Standardklassen, die bei jeder Integration von Experience Platformen, auch als &quot;Branchenklassen&quot;bezeichnet, bereitgestellt werden. Branchenklassen sind allgemein anerkannte Industriestandards, die für eine breite Palette von Anwendungsfällen gelten. Beispiele für Branchenklassen sind die von Adobe bereitgestellten XDM Individual Profil- und XDM ExperienceEvent-Klassen.

Experience Platform ermöglicht auch &quot;Händlerklassen&quot;, bei denen es sich um von Experience Platformen-Partnern definierte Klassen handelt, die allen Kunden zur Verfügung gestellt werden, die diesen Service oder diese Anwendung innerhalb der Platform verwenden.

Es gibt auch Klassen, die zur Beschreibung speziellerer Anwendungsfälle für einzelne Unternehmen in der Platform, so genannte &quot;Kundenklassen&quot;, verwendet werden. Kundenklassen werden von einer Organisation definiert, wenn keine Branchen- oder Händlerklassen zur Beschreibung eines individuellen Anwendungsfalls verfügbar sind.

Beispielsweise beschreibt ein Schema, das Mitglieder eines Loyalty-Programms darstellt, Datensatzdaten über eine Person und kann daher auf der XDM Individual Profil-Klasse basieren, einer von Adobe definierten Standardbranchenklasse.

### Mixin {#mixin}

Ein Mixin ist eine wiederverwendbare Komponente, die ein oder mehrere Felder definiert, die bestimmte Funktionen wie persönliche Details, Hotelpräferenzen oder Adressen implementieren. Mixins sind als Teil eines Schemas vorgesehen, das eine kompatible Klasse implementiert.

Mixins definieren, mit welcher Klasse(n) sie kompatibel sind, basierend auf dem Verhalten der Daten, die sie darstellen (Datensatz- oder Zeitreihen). Das bedeutet, dass nicht alle Mixins für alle Klassen verfügbar sind.

Mixins haben denselben Umfang und dieselbe Definition wie Klassen: Es gibt Branchenmixins, Vendor-Mixins und Customer-Mixins, die von einzelnen Unternehmen mithilfe von Platform definiert werden. Experience Platform umfasst viele standardmäßige Branchenmixins und erlaubt Anbietern, Mixins für ihre Anwender zu definieren. Individuelle Anwender können Mixins für ihre eigenen spezifischen Konzepte definieren.

Wenn Sie beispielsweise Details wie &quot;Vorname&quot;und &quot;Hausanschrift&quot;für Ihr Schema &quot;Treuemitglieder&quot;erfassen möchten, können Sie Standardmixins verwenden, die diese allgemeinen Begriffe definieren. Konzepte, die für seltener auftretende Anwendungsfälle spezifisch sind (z. B. &quot;Treuhandstufe&quot;), haben jedoch häufig keine voreingestellte Mischung. In diesem Fall müssen Sie Ihr eigenes Mixin definieren, um diese Informationen zu erfassen.

Denken Sie daran, dass Schema aus &quot;Null oder mehr&quot; Mixins bestehen, sodass Sie ein gültiges Schema ohne jegliche Mixins zusammenstellen können.

### Data type {#data-type}

Datentypen werden als Referenzfeldtypen in Klassen oder Schemas auf dieselbe Weise wie einfache Literalfelder verwendet. Der Hauptunterschied besteht darin, dass Datentypen mehrere Unterfelder definieren können. Ähnlich wie bei einem Mixin ermöglicht ein Datentyp die konsistente Verwendung einer Mehrfeldstruktur, verfügt aber über mehr Flexibilität als ein Mixin, da ein Datentyp an einer beliebigen Stelle in einem Schema eingefügt werden kann, indem er als &quot;Datentyp&quot;eines Felds hinzugefügt wird.

Experience Platform bietet eine Reihe von gebräuchlichen Datentypen als Teil der Schema Registry, um die Verwendung von Standardmustern zur Beschreibung gemeinsamer Datenstrukturen zu unterstützen. Dies wird in den Schema Registry Tutorials ausführlicher erläutert, wo es klarer wird, wenn Sie die Schritte zur Definition von Datentypen durchlaufen.

### Feld

Ein Feld ist der grundlegendste Baustein eines Schemas. Felder enthalten Einschränkungen hinsichtlich des Datentyps, den sie enthalten können, indem Sie einen bestimmten Datentyp definieren. Diese grundlegenden Datentypen definieren ein einzelnes Feld, während die zuvor erwähnten [Datentypen](#data-type) es Ihnen ermöglichen, mehrere Unterfelder zu definieren und die gleiche Mehrfeldstruktur in verschiedenen Schemas wiederzuverwenden. Zusätzlich zur Definition des &quot;Datentyps&quot;eines Felds als einen der in der Registrierung definierten Datentypen unterstützt Experience Platform grundlegende Skalartypen wie:

* Zeichenfolge
* Ganzzahl
* Zahl
* Boolesch
* Array
* Objekt

Die gültigen Bereiche dieser Skalartypen können weiter auf bestimmte Muster, Formate, minimale/maximale Werte oder vordefinierte Werte beschränkt werden. Mithilfe dieser Einschränkungen kann eine breite Palette speziellerer Feldtypen dargestellt werden, darunter:

* Enum
* lang
* Short
* Byte
* Datum
* Datum/Uhrzeit
* Landkarte

>[!NOTE]
>
>Der Feldtyp &quot;map&quot;ermöglicht die Eingabe von Daten zu Schlüsselwertpaaren, einschließlich mehrerer Werte zu einem Schlüssel. Karten können nur auf Systemebene definiert werden. Das bedeutet, dass Sie möglicherweise auf eine Zuordnung in einem branchenspezifischen oder herstellerspezifischen Schema stoßen, sie stehen jedoch nicht zur Verwendung in von Ihnen definierten Feldern zur Verfügung. Das Entwicklerhandbuch für die [Schema Registry API enthält weitere Informationen zum Definieren von Feldtypen](../api/getting-started.md) .

Einige Datenvorgänge, die von nachgeschalteten Diensten und Anwendungen verwendet werden, erzwingen Einschränkungen für bestimmte Feldtypen. Betroffene Dienste sind unter anderem:

* [Echtzeit-Kundenprofil](../../profile/home.md)
* [Identitätsdienst](../../identity-service/home.md)
* [Segmentierung](../../segmentation/home.md)
* [Abfrage](../../query-service/home.md)
* [Data Science-Arbeitsbereich](../../data-science-workspace/home.md)

Bevor Sie ein Schema zur Verwendung in nachgelagerten Diensten erstellen, lesen Sie bitte die entsprechende Dokumentation für diese Dienste, um die Feldanforderungen und Einschränkungen für die Datenvorgänge, für die das Schema bestimmt ist, besser zu verstehen.

### XDM-Felder

Zusätzlich zu Basisfeldern und der Möglichkeit, eigene Datentypen zu definieren, stellt XDM einen Standardsatz von Feldern und Datentypen bereit, die implizit von Experience Platformen-Diensten verstanden werden, und sorgt für mehr Konsistenz bei der Verwendung über mehrere Platformen hinweg.

Diese Felder wie &quot;Vorname&quot;und &quot;E-Mail-Adresse&quot;enthalten zusätzliche Konnotationen, die über die standardmäßigen Skalarfeldtypen hinausgehen, und weisen die Platform darauf hin, dass alle Felder, die denselben XDM-Datentyp verwenden, sich auf dieselbe Weise verhalten. Dieses Verhalten kann als konsistent betrachtet werden, unabhängig davon, woher die Daten stammen oder in welcher Platform die Daten verwendet werden.

Eine vollständige Liste der verfügbaren XDM-Felder finden Sie im [XDM-Feldwörterbuch](field-dictionary.md) . Es wird empfohlen, nach Möglichkeit XDM-Felder und Datentypen zu verwenden, um Konsistenz und Standardisierung in der gesamten Experience Platform zu unterstützen.

## Kompositionsbeispiel

Schemas stellen das Format und die Struktur der Daten dar, die in die Platform eingebunden und mithilfe eines Kompositionsmodells erstellt werden. Wie bereits erwähnt, bestehen diese Schema aus einer Klasse und Null oder mehr Mixins, die mit dieser Klasse kompatibel sind.

Beispielsweise könnte ein Schema, das Käufe in einem Einzelhandelsgeschäft beschreibt, als &quot;Store-Transaktionen&quot;bezeichnet werden. Das Schema implementiert die XDM ExperienceEvent-Klasse in Kombination mit dem standardmäßigen Commerce-Mixin und einem benutzerdefinierten Product Info-Mixin.

Ein anderes Schema, das den Website-Traffic verfolgt, könnte &quot;Webbesuche&quot;heißen. Es implementiert auch die XDM ExperienceEvent-Klasse, kombiniert diesmal jedoch das Standard-Webmixin.

Das folgende Diagramm zeigt diese Schemas und die von den einzelnen Mixins hinzugefügten Felder. Es enthält außerdem zwei Schema, die auf der XDM Individual Profil-Klasse basieren, einschließlich des Schemas &quot;Treuemitglieder&quot;, das zuvor in diesem Handbuch erwähnt wurde.

![](../images/schema-composition/composition.png)

### Vereinigung {#union}

Während Experience Platform es Ihnen ermöglicht, Schema für bestimmte Anwendungsfälle zu erstellen, können Sie damit auch eine &quot;Vereinigung&quot;von Schemas für einen bestimmten Klassentyp sehen. Das vorherige Diagramm zeigt zwei Schema, die auf der XDM ExperienceEvent-Klasse basieren, und zwei Schema, die auf der XDM Individual Profil-Klasse basieren. Die unten dargestellte Vereinigung Aggregat die Felder aller Schema, die dieselbe Klasse verwenden (XDM ExperienceEvent bzw. XDM Individual Profil).

![](../images/schema-composition/union.png)

Wenn Sie ein Schema für die Verwendung mit Echtzeit-Kundendaten-Profil aktivieren, wird es in die Vereinigung für diesen Klassentyp aufgenommen. Profil bietet stabile, zentralisierte Profil von Kundenattributen sowie ein zeitgestempeltes Kundenkonto für jedes Ereignis, das über ein in die Platform integriertes System verfügt. Profil verwendet die Ansicht Vereinigung, um diese Daten zu repräsentieren und eine ganzheitliche Ansicht jedes einzelnen Kunden bereitzustellen.

Weitere Informationen zum Arbeiten mit Profil finden Sie in der Übersicht über das [Echtzeit-Profil](../../profile/home.md).

## Zuordnen von Datendateien zu XDM-Schemas

Alle Datendateien, die in Experience Platform aufgenommen werden, müssen der Struktur eines XDM-Schemas entsprechen. Weitere Informationen zum Formatieren von Datendateien mit XDM-Hierarchien (einschließlich Beispieldateien) finden Sie im Dokument zu [Beispiel-ETL-Transformationen](../../etl/transformations.md). Allgemeine Informationen zum Einfügen von Datendateien in die Experience Platform finden Sie in der Übersicht über die [Stapelverarbeitung](../../ingestion/batch-ingestion/overview.md).

## Nächste Schritte

Jetzt, da Sie die Grundlagen der Schema-Komposition verstehen, können Sie mit dem Erstellen von Schemas mit der Schema-Registrierung beginnen.

Die Schema-Registrierung wird verwendet, um innerhalb der Adobe Experience Platform auf die Schema-Bibliothek zuzugreifen, und stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle verfügbaren Bibliotheksressourcen zugänglich sind. Die Schema-Bibliothek enthält Branchenressourcen, die von Adobe, von Geschäftspartnern definierten Händlerressourcen sowie Klassen, Mixins, Datentypen und Schema definiert wurden, die von Mitgliedern Ihres Unternehmens zusammengestellt wurden.

Um mit dem Erstellen von Schema über die Benutzeroberfläche zu beginnen, folgen Sie dem Lernprogramm zum [Schema-Editor, um das Schema &quot;Treuemitglieder&quot;zu erstellen, das in diesem Dokument erwähnt wird](../tutorials/create-schema-ui.md) .

Um mit der Schema Registry API zu beginnen, lesen Sie Beginn im Entwicklerhandbuch für die [Schema Registry API](../api/getting-started.md). Nachdem Sie das Entwicklerhandbuch gelesen haben, führen Sie die Schritte aus, die im Lernprogramm zum [Erstellen eines Schemas mit der Schema-Registrierungs-API](../tutorials/create-schema-api.md)beschrieben werden.
