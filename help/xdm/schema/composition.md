---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;enum;mixin;Mixin;Mixins;Mixins;Datentyp;Datentypen;Datentypen;Datentyp;Primäridentität;Primäridentität;XDM-Profil;XDM-Felder;Enum-Datentyp;Experience-Ereignis;XDM Experience-Ereignis;XDM-ExperienceEvent;ExperienceEvent;XDM-Erlebnis;Schema-Design;class;Class;classes;Classes;datatype;datatype;datatype;Datentyp;Datentyp;Schema;Schema;;Identitätszuordnung;Identitätszuordnung;Schema;;Landkarte;Vereinigung Schema;Vereinigung
solution: Experience Platform
title: Grundlagen der Schema-Komposition
topic: Übersicht
description: Dieses Dokument bietet Ihnen eine Einführung in Experience-Datenmodell (XDM)-Schemas und die Bausteine, Grundsätze und Best Practices zum Erstellen von Schemas, die in Adobe Experience Platform verwendet werden sollen.
translation-type: tm+mt
source-git-commit: ae2c5f9fa4e732fefe55a8536894844986aea1e2
workflow-type: tm+mt
source-wordcount: '3502'
ht-degree: 40%

---


# Grundlagen der Schema-Komposition

Dieses Dokument bietet eine Einführung in [!DNL Experience Data Model] (XDM)-Schema und die Bausteine, Grundsätze und Best Practices für das Erstellen von Schemas, die in Adobe Experience Platform verwendet werden sollen. Allgemeine Informationen zu XDM und dazu, wie es in [!DNL Platform] verwendet wird, finden Sie unter [XDM-Systemübersicht](../home.md).

## Verstehen von Schemas

Ein Schema ist ein Regelsatz, der die Datenstruktur und das Datenformat darstellt und überprüft. Auf hoher Ebene bieten Schemas eine abstrakte Definition eines realen Objekts (z. B. einer Person) und legen dar, welche Daten in jeder Instanz dieses Objekts enthalten sein sollen (z. B. Vorname, Nachname, Geburtsdatum usw.).

Zusätzlich zur Beschreibung der Datenstruktur wenden Schemas Einschränkungen und Erwartungen an Daten an, damit diese bei ihren Bewegungen zwischen den Systemen validiert werden können. Diese Standarddefinitionen ermöglichen eine konsistente Interpretation der Daten, unabhängig von ihrer Herkunft, und machen eine anwendungsübergreifende Übersetzung überflüssig.

[!DNL Experience Platform] diese semantische Normalisierung mithilfe von Schemas aufrecht zu erhalten. Schema sind die Standardmethode zum Beschreiben von Daten in [!DNL Experience Platform], sodass alle Daten, die Schemas entsprechen, innerhalb eines Unternehmens ohne Konflikte wiederverwendet oder sogar von mehreren Organisationen gemeinsam genutzt werden können.

XDM-Schema eignen sich ideal zum Speichern umfangreicher komplexer Daten in einem eigenständigen Format. Weitere Informationen dazu, wie XDM dies erreicht, finden Sie in den Abschnitten unter [Eingebettete Objekte](#embedded) und [Big Data](#big-data) im Anhang zu diesem Dokument.

### Schema-basierte Workflows in [!DNL Experience Platform]

Die Standardisierung ist ein Schlüsselkonzept hinter [!DNL Experience Platform]. Das von Adobe unterstützte XDM-System ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schemas für das Customer Experience Management zu definieren.

Die als [!DNL XDM System] bekannte Infrastruktur, auf der [!DNL Experience Platform] aufgebaut ist, erleichtert Schema-basierte Workflows und umfasst die Muster [!DNL Schema Registry], [!DNL Schema Editor], Schema-Metadaten und Dienstkonsum. Weitere Informationen finden Sie in der [XDM-Systemübersicht](../home.md).

Das Erstellen und Verwenden von Schemas in [!DNL Experience Platform] bietet mehrere wichtige Vorteile. Erstens ermöglichen Schemas eine bessere Datenverwaltung und eine Minimierung der Daten, was besonders bei Datenschutzbestimmungen wichtig ist. Zweitens ermöglicht das Erstellen von Schemas mit Standardkomponenten der Adobe sofortige Einblicke und die Verwendung von AI/ML-Diensten mit minimalen Anpassungen. Und schließlich bieten Schema eine Infrastruktur für die gemeinsame Nutzung von Daten und eine effiziente Orchestrierung.

## Planen Ihres Schemas

Der erste Schritt beim Erstellen eines Schemas besteht darin, das Konzept oder das Objekt der realen Welt zu bestimmen, das Sie im Schema erfassen möchten. Sobald Sie das Konzept, das Sie beschreiben möchten, identifizieren, können Sie mit der Planung Ihres Schemas beginnen, indem Sie über Dinge wie die Art der Daten, potenzielle Identitätsfelder und wie sich das Schema in Zukunft entwickeln könnte, nachdenken.

### Datenverhalten in [!DNL Experience Platform]

Daten, die in [!DNL Experience Platform] verwendet werden sollen, sind in zwei Verhaltenstypen unterteilt:

* **Aufzeichnen von Daten**: Stellt Informationen zu den Attributen eines Subjekts bereit. Ein Subjekt könnte eine Organisation oder eine Einzelperson sein.
* **Zeitreihendaten**: Stellt eine Momentaufnahme des Systems zum Zeitpunkt bereit, zu dem eine Aktion entweder direkt oder indirekt von einem Datensatzsubjekt durchgeführt wurde.

Alle XDM-Schemas beschreiben Daten, die als Datensatz- oder Zeitreihen kategorisiert werden können. Das Datenverhalten eines Schemas wird durch die Klasse des Schemas definiert, die einem Schema beim ersten Erstellen zugewiesen wird. XDM-Klassen werden nachstehend in diesem Dokument detailliert beschrieben.

Sowohl Schemas der Datensätze als auch der Zeitreihen enthalten eine Zuordnung der Identitäten (`xdm:identityMap`). Dieses Feld enthält die Identitätsdarstellung eines Subjekts, die aus den als „Identität“ markierten Feldern gezogen wird, wie im nächsten Abschnitt beschrieben.

### [!UICONTROL Identität] {#identity}

Schema werden zum Erfassen von Daten in [!DNL Experience Platform] verwendet. Diese Daten können über mehrere Dienste hinweg verwendet werden, um eine einzelne, einheitliche Ansicht einer einzelnen Entität zu erstellen. Daher ist es wichtig, bei der Betrachtung von Schemas über Kundenidentitäten nachzudenken und welche Felder zur Identifizierung eines Objekts verwendet werden können, unabhängig davon, woher die Daten stammen.

Um diesen Vorgang zu unterstützen, können Schlüsselfelder in Ihren Schemas als Identitäten gekennzeichnet werden. Bei der Datenerfassung werden die Daten in diesen Feldern in das Identitätsdiagramm &quot;[!UICONTROL a1/>&quot;für diese Person eingefügt. ] Die Diagrammdaten können dann von [[!DNL Real-time Customer Profile]](../../profile/home.md) und anderen [!DNL Experience Platform]-Diensten aufgerufen werden, um eine zusammengeführte Ansicht für jeden einzelnen Kunden bereitzustellen.

Zu den Feldern, die häufig als &quot;[!UICONTROL Identity]&quot;gekennzeichnet sind, gehören: E-Mail-Adresse, Telefonnummer, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html)-, CRM-ID oder andere eindeutige ID-Felder. Sie sollten außerdem alle eindeutigen IDs berücksichtigen, die für Ihr Unternehmen spezifisch sind, da sie möglicherweise auch gut in den Feldern &quot;[!UICONTROL Identität]&quot;stehen.

Es ist wichtig, während der Planungsphase des Schemas über Kundenidentitäten nachzudenken, um sicherzustellen, dass Daten zusammengeführt werden, um ein möglichst stabiles Profil zu schaffen. In der Übersicht zu [Adobe Experience Platform Identity Service](../../identity-service/home.md) erfahren Sie mehr darüber, wie Identitätsinformationen Ihnen dabei helfen können, Ihren Kunden digitale Erlebnisse bereitzustellen.

#### `xdm:identityMap` {#identityMap}

`xdm:identityMap` ist ein Feld vom Typ &quot;Map&quot;, das die verschiedenen Identitätswerte einer Person zusammen mit den zugehörigen Namensräumen beschreibt. Mit diesem Feld können Sie Identitätsdaten für Ihre Schema bereitstellen, anstatt Identitätswerte innerhalb der Struktur des Schemas selbst zu definieren.

Ein Beispiel für eine einfache Identitätskarte würde wie folgt aussehen:

```json
"identityMap": {
  "email": [
    {
      "id": "jsmith@example.com",
      "primary": false
    }
  ],
  "ECID": [
    {
      "id": "87098882279810196101440938110216748923",
      "primary": false
    },
    {
      "id": "55019962992006103186215643814973128178",
      "primary": false
    }
  ],
  "loyaltyId": [
    {
      "id": "2e33192000007456-0365c00000000000",
      "primary": true
    }
  ]
}
```

Wie im Beispiel oben gezeigt, stellt jeder Schlüssel im `identityMap`-Objekt einen Identitäts-Namensraum dar. Der Wert für jeden Schlüssel ist ein Array von Objekten, das die Identitätswerte (`id`) für den jeweiligen Namensraum darstellt. Eine [Liste von standardmäßigen Identitäts-Namensräumen](../../identity-service/troubleshooting-guide.md#standard-namespaces), die von Adobe-Anwendungen erkannt werden, finden Sie in der [!DNL Identity Service]-Dokumentation.

>[!NOTE]
>
>Für jeden Identitätswert kann auch ein boolescher Wert angegeben werden, um festzustellen, ob es sich bei dem Wert um eine primäre Identität (`primary`) handelt. Primär-IDs müssen nur für Schema festgelegt werden, die in [!DNL Real-time Customer Profile] verwendet werden sollen. Weitere Informationen finden Sie im Abschnitt zu [Vereinigung-Schemas](#union).

### Schema-Evolutionsprinzipien {#evolution}

In dem Maße, wie sich die Art der digitalen Erfahrungen weiterentwickelt, müssen sich auch die Schemas, die zu ihrer Darstellung verwendet werden, weiterentwickeln. Ein gut entworfenes Schema ist daher in der Lage, sich bei Bedarf anzupassen und weiterzuentwickeln, ohne destruktive Änderungen an früheren Versionen des Schemas zu verursachen.

Da die Abwärtskompatibilität für die Entwicklung von Schemas entscheidend ist, setzt [!DNL Experience Platform] ein rein additives Versionsprinzip um, um sicherzustellen, dass Änderungen am Schema nur zu nicht-destruktiven Aktualisierungen und Änderungen führen. Mit anderen Worten: **brechende Änderungen werden nicht unterstützt.**

| Unterstützte Änderungen | Brechende Änderungen (nicht unterstützt) |
|------------------------------------|---------------------------------|
| <ul><li>Hinzufügen neuer Felder zu einem vorhandenen Schema</li><li>Definieren eines obligatorischen Felds als optional</li></ul> | <ul><li>Entfernen zuvor definierter Felder</li><li>Einführen neuer obligatorischer Felder</li><li>Umbenennen oder Neudefinieren vorhandener Felder</li><li>Entfernen oder Eingrenzen zuvor unterstützter Feldwerte</li><li>Verschieben von Attributen an eine andere Position in der Baumstruktur</li></ul> |

>[!NOTE]
>
>Wenn ein Schema noch nicht zum Erfassen von Daten in [!DNL Experience Platform] verwendet wurde, können Sie eine Umbruchänderung an diesem Schema vornehmen. Sobald das Schema jedoch in [!DNL Platform] verwendet wurde, muss es die Richtlinie für die additive Versionierung einhalten.

### Schemas und Datenerfassung

Um Daten in [!DNL Experience Platform] zu erfassen, muss zunächst ein Datensatz erstellt werden. Datasets sind die Bausteine für die Datenumwandlung und -verfolgung für [[!DNL Catalog Service]](../../catalog/home.md) und stellen im Allgemeinen Tabellen oder Dateien dar, die erfasste Daten enthalten. Alle Datensätze basieren auf vorhandenen XDM-Schemas, die Einschränkungen dafür enthalten, was die aufgenommenen Daten enthalten und wie sie strukturiert sein sollten. Weitere Informationen hierzu finden Sie in der Übersicht über die [Datenerfassung in Adobe Experience Platform](../../ingestion/home.md).

## Bausteine eines Schemas

[!DNL Experience Platform]Die verwendet einen Kompositionsansatz, bei dem Standardbausteine kombiniert werden, um Schemas zu erstellen. Dieser Ansatz fördert die Wiederverwendbarkeit bestehender Komponenten und treibt die Standardisierung in der gesamten Branche voran, um Schema und Komponenten von Anbietern in [!DNL Platform] zu unterstützen.

Schemas werden nach folgender Formel zusammengestellt:

**Klasse + Mixin&amp;ast; = XDM-Schema**

&amp;ast;Ein Schema besteht aus einer Klasse und null oder mehr Mixins. Dies bedeutet, dass Sie in Datensatzschema ohne jegliche Verwendung von Mixins erstellen könnten.

### Klasse {#class}

Das Erstellen eines Schemas beginnt mit dem Zuweisen einer Klasse. Klassen definieren die Verhaltensaspekte der Daten, die das Schema enthalten soll (Datensatz oder Zeitreihen). Darüber hinaus beschreiben Klassen die kleinste Anzahl gemeinsamer Eigenschaften, die alle Schemas, die auf dieser Klasse basieren, beinhalten müssen, und bieten eine Möglichkeit zum Zusammenführen mehrerer kompatibler Datensätze.

Die Klasse eines Schemas legt fest, welche Mixins in diesem Schema verwendet werden dürfen. Dies wird im [nächsten Abschnitt](#mixin) ausführlicher erläutert.

Adobe bietet mehrere Standard-(Core-)XDM-Klassen. Zwei dieser Klassen, [!DNL XDM Individual Profile] und [!DNL XDM ExperienceEvent], sind für fast alle nachgeschalteten Plattformprozesse erforderlich. Zusätzlich zu diesen Hauptklassen können Sie auch eigene benutzerdefinierte Klassen erstellen, um spezifischere Anwendungsfälle für Ihr Unternehmen zu beschreiben. Benutzerspezifische Klassen werden von einer Organisation definiert, wenn keine von der Adobe definierten Hauptklassen zur Beschreibung eines individuellen Anwendungsfalls verfügbar sind.

Der folgende Screenshot zeigt, wie Klassen in der Plattform-Benutzeroberfläche dargestellt werden. Da das hier dargestellte Schema keine Mixins enthält, werden alle angezeigten Felder von der Klasse des Schemas ([!UICONTROL XDM Individuelles Profil]) bereitgestellt.

![](../images/schema-composition/class.png)

Die aktuellste Liste der verfügbaren Standard-XDM-Klassen finden Sie im [offiziellen XDM-Repository](https://github.com/adobe/xdm/tree/master/components/classes). Alternativ können Sie auch auf das Handbuch [XDM-Komponenten ](../ui/explore.md) zugreifen, wenn Sie lieber Ansichten in der Benutzeroberfläche vornehmen möchten.

### Mixin {#mixin}

Ein Mixin ist eine wiederverwendbare Komponente, die ein oder mehrere Felder definiert, die bestimmte Funktionen wie persönliche Details, Hotelpräferenzen oder Adressen implementieren. Mixins sind als Teil eines Schemas vorgesehen, das eine kompatible Klasse implementiert.

Mixins definieren, mit welcher/n Klasse(n) sie kompatibel sind, basierend auf dem Verhalten der Daten, die sie darstellen (Datensatz- oder Zeitreihen). Das bedeutet, dass nicht alle Mixins für alle Klassen verfügbar sind.

[!DNL Experience Platform] enthält viele standardmäßige Mixins für Adoben und ermöglicht es Anbietern, Mixins für ihre Anwender zu definieren, sowie einzelnen Anwendern, Mixins für ihre eigenen spezifischen Konzepte zu definieren.

Um beispielsweise Details wie &quot;[!UICONTROL Vorname]&quot;und &quot;[!UICONTROL Hausadresse]&quot;für Ihr Schema &quot;[!UICONTROL Treuemitglieder]&quot;zu erfassen, können Sie Standardmixins verwenden, die diese allgemeinen Begriffe definieren. Konzepte, die für seltener auftretende Anwendungsfälle spezifisch sind (z. B. &quot;[!UICONTROL Kundentreue-Programm-Ebene]&quot;), verfügen jedoch häufig nicht über eine vordefinierte Mischung. In diesem Fall müssen Sie einen eigenen Mixin definieren, um diese Informationen zu erfassen.

Denken Sie daran, dass Schemas aus „Null oder mehr“ Mixins bestehen, was bedeutet, dass Sie ein gültiges Schema zusammenstellen können, ohne überhaupt Mixins zu verwenden.

Der folgende Screenshot zeigt, wie Mixins in der Plattform-Benutzeroberfläche dargestellt werden. In diesem Beispiel wird einem Schema ein einzelnes Mixin ([!UICONTROL Demografische Details]) hinzugefügt, das eine Gruppierung der Felder zur Feldstruktur des Schemas bereitstellt.

![](../images/schema-composition/mixin.png)

Die aktuellste Liste der verfügbaren Standard-XDM-Mixins finden Sie im [offiziellen XDM-Repository](https://github.com/adobe/xdm/tree/master/components/mixins). Alternativ können Sie auch auf das Handbuch [XDM-Komponenten ](../ui/explore.md) zugreifen, wenn Sie lieber Ansichten in der Benutzeroberfläche vornehmen möchten.

### Datentyp {#data-type}

Datentypen werden als Referenzfeldtypen in Klassen oder Schemata auf die gleiche Weise verwendet wie grundlegende literale Felder. Der wesentliche Unterschied besteht darin, dass Datentypen mehrere Teilfelder definieren können. Ähnlich wie ein Mixin ermöglicht ein Datentyp die konsistente Verwendung einer Mehrfeldstruktur, ist jedoch flexibler als ein Mixin, da ein Datentyp an beliebiger Stelle in ein Schema aufgenommen werden kann, indem er als „Datentyp“ eines Feldes hinzugefügt wird.

[!DNL Experience Platform] bietet eine Reihe von gebräuchlichen Datentypen als Teil der ,  [!DNL Schema Registry] um die Verwendung von Standardmustern zur Beschreibung allgemeiner Datenstrukturen zu unterstützen. Dies wird in den [!DNL Schema Registry]-Tutorials ausführlicher erklärt, wo es klarer wird, wenn Sie die Schritte zur Definition von Datentypen durchlaufen.

Der folgende Screenshot zeigt, wie Datentypen in der Plattform-Benutzeroberfläche dargestellt werden. Eines der Felder, die vom Mixin [!UICONTROL Demografische Details] bereitgestellt werden, verwendet den Datentyp &quot;[!UICONTROL Personenname]&quot;, wie durch den Text nach dem Senkrechtstrich (`|`) neben dem Feldnamen angegeben. Dieser bestimmte Datentyp enthält mehrere Unterfelder, die sich auf den Namen einer Person beziehen, ein Konstrukt, das für andere Felder wiederverwendet werden kann, in denen der Name einer Person erfasst werden muss.

![](../images/schema-composition/data-type.png)

Die aktuellste Liste der verfügbaren Standard-XDM-Datentypen finden Sie im [offiziellen XDM-Repository](https://github.com/adobe/xdm/tree/master/components/datatypes). Alternativ können Sie auch auf das Handbuch [XDM-Komponenten ](../ui/explore.md) zugreifen, wenn Sie lieber Ansichten in der Benutzeroberfläche vornehmen möchten.

### Feld

Ein Feld ist der grundlegendste Baustein eines Schemas. Felder bieten Einschränkungen hinsichtlich der Art der Daten, die sie enthalten können, indem sie einen bestimmten Datentyp definieren. Diese grundlegenden Datentypen definieren ein einzelnes Feld, wohingegen die zuvor erwähnten [Datentypen](#data-type) es Ihnen ermöglichen, mehrere Teilfelder zu definieren und dieselbe Mehrfeldstruktur in verschiedenen Schemas wiederzuverwenden. Neben der Definition des &quot;Datentyps&quot;eines Felds als einen der in der Registrierung definierten Datentypen unterstützt [!DNL Experience Platform] grundlegende Skalartypen wie:

* Zeichenfolge
* Ganzzahl
* Double
* Boolesch
* Array
* Objekt

>[!TIP]
>
>Informationen zu den Vor- und Nachteile der Verwendung von Freiformfeldern über Objekttypen finden Sie im Anhang [Anhang](#objects-v-freeform).

Die gültigen Bereiche dieser Skalartypen können weiter auf bestimmte Muster, Formate, Minima/Maxima oder vordefinierte Werte eingeschränkt werden. Mithilfe dieser Einschränkungen kann eine breite Palette speziellerer Feldtypen dargestellt werden, darunter:

* Enum
* Lang
* Kurz
* Byte
* Datum
* Datum-Uhrzeit
* Karte

>[!NOTE]
>
> Der Feldtyp „Karte“ ermöglicht Daten für Schlüssel-Wertepaare, einschließlich mehrerer Werte für einen einzelnen Schlüssel. Karten können nur auf Systemebene definiert werden, d. h. Sie können in einem branchen- oder herstellerdefinierten Schema auf eine Karte stoßen, diese steht jedoch nicht für die Verwendung in von Ihnen definierten Feldern zur Verfügung. Das [Entwicklerhandbuch für Schema-Registry-API](../api/getting-started.md) enthält weitere Informationen zum Definieren von Feldtypen.

Einige Datenoperationen, die von nachgeschalteten Diensten und Anwendungen verwendet werden, erzwingen Einschränkungen für bestimmte Feldtypen. Betroffene Dienste sind u. a., aber nicht ausschließlich:

* [[!DNL Real-time Customer Profile]](../../profile/home.md)
* [[!DNL Identity Service]](../../identity-service/home.md)
* [[!DNL Segmentation]](../../segmentation/home.md)
* [[!DNL Query Service]](../../query-service/home.md)
* [[!DNL Data Science Workspace]](../../data-science-workspace/home.md)

Bevor Sie ein Schema für die Verwendung in nachgelagerten Diensten erstellen, lesen Sie bitte die entsprechende Dokumentation für diese Dienste, um die Feldanforderungen und Einschränkungen für die Datenoperationen, für die das Schema bestimmt ist, besser zu verstehen.

### XDM-Felder

Zusätzlich zu Basisfeldern und der Möglichkeit, eigene Datentypen zu definieren, stellt XDM einen Standardsatz von Feldern und Datentypen bereit, die implizit von [!DNL Experience Platform]-Diensten verstanden werden, und bietet eine größere Konsistenz, wenn sie über [!DNL Platform]-Komponenten hinweg verwendet werden.

Diese Felder wie &quot;Vorname&quot;und &quot;E-Mail-Adresse&quot;enthalten zusätzliche Verbindungen, die über die grundlegenden Skalarfeldtypen hinausgehen, wobei [!DNL Platform] angegeben wird, dass alle Felder, die denselben XDM-Datentyp verwenden, sich auf dieselbe Weise verhalten. Dieses Verhalten kann als konsistent betrachtet werden, unabhängig davon, woher die Daten stammen oder in welchem [!DNL Platform]-Dienst die Daten verwendet werden.

Eine vollständige Liste der verfügbaren XDM-Felder finden Sie im [XDM-Feldwörterbuch](field-dictionary.md). Es wird empfohlen, nach Möglichkeit XDM-Felder und Datentypen zu verwenden, um Konsistenz und Standardisierung über [!DNL Experience Platform] zu unterstützen.

## Kompositionsbeispiel

Schema stellen das Format und die Struktur der Daten dar, die in [!DNL Platform] eingeschlossen und mithilfe eines Kompositionsmodells erstellt werden. Wie bereits erwähnt, bestehen diese Schemas aus einer Klasse und Null oder mehr Mixins, die mit dieser Klasse kompatibel sind.

Beispielsweise könnte ein Schema, das Käufe in einem Einzelhandelsgeschäft beschreibt, als &quot;[!UICONTROL Geschäfte speichern]&quot;bezeichnet werden. Das Schema implementiert die [!DNL XDM ExperienceEvent]-Klasse in Kombination mit dem standardmäßigen [!UICONTROL Commerce]-Mixin und einem benutzerdefinierten [!UICONTROL Product Info]-Mixin.

Ein anderes Schema, das den Website-Traffic verfolgt, könnte &quot;[!UICONTROL Webbesuche]&quot;heißen. Es implementiert auch die [!DNL XDM ExperienceEvent]-Klasse, kombiniert diesmal jedoch das standardmäßige [!UICONTROL Web]-Mixin.

Das folgende Diagramm zeigt diese Schemas und die von den einzelnen Mixins hinzugefügten Felder. Es enthält außerdem zwei Schema, die auf der [!DNL XDM Individual Profile]-Klasse basieren, einschließlich des zuvor in diesem Handbuch erwähnten Schemas &quot;[!UICONTROL Treuemitglieder]&quot;.

![](../images/schema-composition/composition.png)

### Vereinigung {#union}

[!DNL Experience Platform] ermöglicht es Ihnen, Schema für bestimmte Anwendungsfälle zu erstellen, es ermöglicht Ihnen aber auch, eine &quot;Vereinigung&quot;von Schemas für einen bestimmten Klassentyp anzuzeigen. Das vorherige Diagramm zeigt zwei Schema, die auf der XDM ExperienceEvent-Klasse basieren, und zwei Schema, die auf der [!DNL XDM Individual Profile]-Klasse basieren. Die unten dargestellte Vereinigung Aggregat die Felder aller Schema, die dieselbe Klasse besitzen ([!DNL XDM ExperienceEvent] bzw. [!DNL XDM Individual Profile]).

![](../images/schema-composition/union.png)

Wenn Sie ein Schema zur Verwendung mit [!DNL Real-time Customer Profile] aktivieren, wird es in die Vereinigung für diesen Klassentyp aufgenommen. [!DNL Profile] bietet stabile, zentralisierte Profil von Kundenattributen sowie ein zeitgestempeltes Kundenkonto für jedes Ereignis, das über ein in  [!DNL Platform]das System integriertes System verfügt. [!DNL Profile] verwendet die vereinigte Ansicht, um diese Daten zu repräsentieren und eine ganzheitliche Ansicht jedes einzelnen Kunden bereitzustellen.

Weitere Informationen zum Arbeiten mit [!DNL Profile] finden Sie unter [Übersicht über das Echtzeit-Profil des Kunden](../../profile/home.md).

## Zuordnen von Datendateien zu XDM-Schemas

Alle Datendateien, die in [!DNL Experience Platform] eingeschlossen werden, müssen der Struktur eines XDM-Schemas entsprechen. Weitere Informationen zum Formatieren von Datendateien mit XDM-Hierarchien (einschließlich Beispieldateien) finden Sie im Dokument zu [Beispiel-ETL-Transformationen](../../etl/transformations.md). Allgemeine Informationen zum Einfügen von Datendateien in [!DNL Experience Platform] finden Sie unter [Überblick über die Stapelverarbeitung](../../ingestion/batch-ingestion/overview.md).

## Schema für externe Segmente

Wenn Sie Segmente aus externen Systemen in Platform integrieren, müssen Sie diese mit den folgenden Komponenten in Ihren Schemas erfassen:

* [[!UICONTROL Segment-] Definitionsklasse](../classes/segment-definition.md): Verwenden Sie diese Standardklasse, um Schlüsselattribute einer externen Segmentdefinition zu erfassen.
* [[!UICONTROL Details ] zum Segmentmanagement](../mixins/profile/segmentation.md): hinzufügen Sie diese Mischung mit Ihrem  [!UICONTROL XDM Individual ] Profileschema, um Kundensegmente mit bestimmten Segmenten zu verbinden.

## Nächste Schritte

Jetzt, da Sie die Grundlagen der Schema-Komposition verstehen, können Sie mit dem [!DNL Schema Registry] beginnen, Schema zu erkunden und zu bauen.

Informationen zur Übersicht über die Struktur der beiden Core-XDM-Klassen und ihrer häufig verwendeten kompatiblen Mixins finden Sie in der folgenden Referenzdokumentation:

* [[!DNL XDM Individual Profile]](../classes/individual-profile.md)
* [[!DNL XDM ExperienceEvent]](../classes/experienceevent.md)

Das [!DNL Schema Registry] wird verwendet, um auf das [!DNL Schema Library] in Adobe Experience Platform zuzugreifen, und stellt eine Benutzeroberfläche und RESTful-API bereit, über die alle verfügbaren Bibliotheksressourcen zugänglich sind. Das [!DNL Schema Library] enthält Branchenressourcen, die durch Adobe, Händlerressourcen definiert werden, die von [!DNL Experience Platform]-Partnern definiert werden, sowie Klassen, Mixins, Datentypen und Schema, die von Mitgliedern Ihres Unternehmens zusammengestellt wurden.

Um mit dem Erstellen von Schemas über die Benutzeroberfläche zu beginnen, folgen Sie dem [Schema-Editor-Tutorial](../tutorials/create-schema-ui.md), um das Schema „Loyalty Members“ zu erstellen, das in diesem Dokument erwähnt wird.

Um mit der [!DNL Schema Registry]-API zu beginnen, lesen Sie den Beginn im [Schema Registry API Developer Guide](../api/getting-started.md). Nachdem Sie das Entwicklerhandbuch gelesen haben, führen Sie die Schritte aus, die im Tutorial zum [Erstellen eines Schemas mit der Schema Registry-API](../tutorials/create-schema-api.md) beschrieben werden.

## Anhang

Die folgenden Abschnitte enthalten zusätzliche Informationen zu den Grundsätzen der Zusammensetzung des Schemas.

### Relationale Tabellen versus eingebettete Objekte {#embedded}

Bei der Arbeit mit relationalen Datenbanken bestehen die Best Practices darin, Daten zu normalisieren oder eine Entität in diskrete Teile zu zerlegen, die dann in mehreren Tabellen angezeigt werden. Um die Daten als Ganzes zu lesen oder die Entität zu aktualisieren, müssen Lese- und Schreibvorgänge über viele einzelne Tabellen mit JOIN durchgeführt werden.

Durch den Einsatz von eingebetteten Objekten können XDM-Schema komplexe Daten direkt darstellen und in eigenständigen Dokumenten mit einer hierarchischen Struktur speichern. Einer der Hauptvorteile dieser Struktur besteht darin, dass Sie damit die Daten abfragen können, ohne die Entität durch teure Verbindungen zu mehreren denormalisierten Tabellen rekonstruieren zu müssen. Es gibt keine Einschränkungen, wie viele Ebenen Ihre Schema-Hierarchie sein kann.

### Schemas und Big Data {#big-data}

Moderne digitale Systeme generieren enorme Mengen von Verhaltenssignalen (Transaktionsdaten, Weblogs, Internet der Dinge, Anzeige usw.). Diese Big-Data-Daten bieten außergewöhnliche Möglichkeiten zur Optimierung von Erlebnissen, sind aber aufgrund der Größe und Vielfalt der Daten schwierig zu nutzen. Um aus den Daten Nutzen zu ziehen, müssen Struktur, Format und Definitionen standardisiert werden, damit sie konsistent und effizient verarbeitet werden können.

Schemas lösen dieses Problem, indem sie die Integration von Daten aus mehreren Quellen, die Standardisierung durch gemeinsame Strukturen und Definitionen und die lösungsübergreifende gemeinsame Nutzung ermöglichen. Dadurch können nachfolgende Prozesse und Dienste jede Art von Frage beantworten, die von den Daten gestellt wird, und sich von dem herkömmlichen Ansatz zur Datenmodellierung abwenden, bei dem alle Fragen, die an die Daten gestellt werden, im Voraus bekannt sind und die Daten modelliert werden, um diesen Erwartungen zu entsprechen.

### Objekte gegen Freiformfelder {#objects-v-freeform}

Beim Entwerfen Ihrer Schemas sind einige wichtige Faktoren zu beachten, die bei der Auswahl von Objekten über Freiformfeldern zu beachten sind:

| Objekte | Freiformfelder |
| --- | --- |
| Erhöht die Verschachtelung | Weniger oder keine Verschachtelung |
| Erstellt logische Feldgruppierungen | Felder werden an Ad-hoc-Positionen platziert |

#### Objekte

Die Vor- und Nachteile der Verwendung von Objekten über freien Feldern sind unten aufgeführt.

**Vorteile**:

* Objekte werden am besten verwendet, wenn Sie eine logische Gruppierung bestimmter Felder erstellen möchten.
* Objekte organisieren das Schema strukturierter.
* Objekte tragen indirekt zur Erstellung einer guten Menüstruktur in der Segment Builder-Benutzeroberfläche bei. Die gruppierten Felder innerhalb des Schemas werden direkt in der Ordnerstruktur angezeigt, die in der Segmentaufbau-Benutzeroberfläche bereitgestellt wird.

**Nachteile**:

* Felder werden verschachtelter.
* Bei Verwendung von [Adobe Experience Platform Abfrage Service](../../query-service/home.md) müssen für Abfragen, die in Objekten verschachtelt sind, längere Referenzzeichenfolgen bereitgestellt werden.

#### Freiformfelder

Die Vor- und Nachteile der Verwendung von Freiformfeldern über Objekten sind unten aufgeführt.

**Vorteile**:

* Freiformfelder werden direkt unter dem Stammobjekt des Schemas (`_tenantId`) erstellt, wodurch die Sichtbarkeit erhöht wird.
* Referenzzeichenfolgen für Freiformfelder sind in der Regel kürzer, wenn Abfrage Service verwendet wird.

**Nachteile**:

* Die Position von Freiformfeldern im Schema ist ad hoc, d. h. sie werden in alphabetischer Reihenfolge im Schema-Editor angezeigt. Dies kann dazu führen, dass Schema weniger strukturiert sind und ähnliche Freiformfelder je nach Name weit voneinander getrennt werden.