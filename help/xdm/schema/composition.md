---
keywords: Experience Platform; home; beliebte Themen; Schema; Enum; Mixin; Feldergruppe; Feldergruppen; Feldergruppen; Mixins; Datentyp; Datentypen; Datentypen; Datentyp; primäre Identität; primäre Identität; XDM-individuelles Profil; XDM-Felder; Enum-Datentyp; Erlebnis-Ereignis; XDM Experience Event; XDM ExperienceEvent; ExperienceEvent; XDM ExperienceEvent; Schema-Design; Klasse; Klasse;Klassen;Datentyp;Datentyp;Datentyp;Datentyp;Datentyp;Schemas;Schemas;Identitätszuordnung;Identitätszuordnung;Identitätszuordnung;Schema-Design;Map;Map;Vereinigungsschema;Vereinigung
solution: Experience Platform
title: Grundlagen der Schemakomposition
description: Erfahren Sie mehr über Experience-Datenmodell (XDM)-Schemas und die Bausteine, Grundsätze und Best Practices zum Erstellen von Schemas in Adobe Experience Platform.
exl-id: d449eb01-bc60-4f5e-8d6f-ab4617878f7e
source-git-commit: 8113b5298120f710f43c5a02504f19ca3af67c5a
workflow-type: tm+mt
source-wordcount: '4229'
ht-degree: 25%

---

# Grundlagen der Schema-Komposition

Erfahren Sie mehr über Experience-Datenmodell (XDM)-Schemas und die Bausteine, Grundsätze und Best Practices zum Erstellen von Schemas in Adobe Experience Platform. Allgemeine Informationen zu XDM und dessen Verwendung in [!DNL Platform], siehe [XDM-System - Übersicht](../home.md).

## Verstehen von Schemata {#understanding-schemas}

Ein Schema ist ein Regelsatz, der die Datenstruktur und das Datenformat darstellt und überprüft. Auf hoher Ebene bieten Schemata eine abstrakte Definition eines realen Objekts (z. B. einer Person) und legen dar, welche Daten in jeder Instanz dieses Objekts enthalten sein sollen (z. B. Vorname, Nachname, Geburtsdatum usw.).

Zusätzlich zur Beschreibung der Datenstruktur wenden Schemata Einschränkungen und Erwartungen an Daten an, damit diese bei ihren Bewegungen zwischen den Systemen validiert werden können. Diese Standarddefinitionen ermöglichen eine konsistente Interpretation der Daten, unabhängig von ihrer Herkunft, und machen eine anwendungsübergreifende Übersetzung überflüssig.

Experience Platform behält diese semantische Normalisierung bei, indem Schemas verwendet werden. Schemata sind die Standardmethode zur Beschreibung von Daten in Experience Platform. Dadurch können alle Daten, die mit Schemata konform sind, innerhalb einer Organisation ohne Konflikte wiederverwendet oder sogar von mehreren Organisationen gemeinsam genutzt werden.

XDM-Schemata eignen sich ideal zum Speichern großer Mengen komplexer Daten in einem eigenständigen Format. Siehe die Abschnitte unter [Eingebettete Objekte](#embedded) und [Big Data](#big-data) im Anhang zu diesem Dokument finden Sie weitere Informationen dazu, wie XDM dies erreicht.

### Schema-basierte Workflows in Experience Platform {#schema-based-workflows}

Die Standardisierung ist ein Schlüsselkonzept der Experience Platform. Das von Adobe unterstützte XDM-System ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schemata für das Customer Experience Management zu definieren.

Die Infrastruktur, auf der Experience Platform gebaut wird, auch bekannt als [!DNL XDM System], erleichtert schemabasierte Workflows und schließt die [!DNL Schema Registry], [!DNL Schema Editor], Schemadaten und Dienstkonsummuster. Weitere Informationen finden Sie in der [XDM-Systemübersicht](../home.md).

Die Verwendung von Schemas im Experience Platform bietet verschiedene wichtige Vorteile. Erstens ermöglichen Schemata eine bessere Data Governance und eine bessere Datenminimierung, was besonders bei Datenschutzbestimmungen wichtig ist. Zweitens ermöglicht das Erstellen von Schemas mit Adobe-Standardkomponenten vordefinierte Einblicke und die Verwendung von KI-/ML-Diensten mit minimalen Anpassungen. Schließlich bieten Schemas eine Infrastruktur für Erkenntnisse über die Datenweitergabe und eine effiziente Orchestrierung.

## Planen Ihres Schemas {#planning}

Der erste Schritt beim Erstellen eines Schemas besteht darin, das Konzept oder das Objekt der realen Welt zu bestimmen, das Sie im Schema erfassen möchten. Sobald Sie das Konzept, das Sie beschreiben möchten, identifizieren, beginnen Sie mit der Planung Ihres Schemas, indem Sie über Dinge wie den Datentyp, potenzielle Identitätsfelder und darüber nachdenken, wie sich das Schema in Zukunft entwickeln kann.

### Datenverhalten in Experience Platform {#data-behaviors}

Daten, die in Experience Platform verwendet werden sollen, sind in zwei Verhaltenstypen unterteilt:

* **Aufzeichnen von Daten**: Stellt Informationen zu den Attributen eines Subjekts bereit. Ein Subjekt könnte eine Organisation oder eine Einzelperson sein.
* **Zeitreihendaten**: Stellt eine Momentaufnahme des Systems zum Zeitpunkt bereit, zu dem eine Aktion entweder direkt oder indirekt von einem Datensatzsubjekt durchgeführt wurde.

Alle XDM-Schemata beschreiben Daten, die als Datensatz oder Zeitreihe kategorisiert werden können. Das Datenverhalten eines Schemas wird durch die Klasse des Schemas definiert, die einem Schema bei dessen Erstellung zugewiesen wird. XDM-Klassen werden nachstehend in diesem Dokument detailliert beschrieben.

Sowohl Schemata der Datensätze als auch der Zeitreihen enthalten eine Zuordnung der Identitäten (`xdm:identityMap`). Dieses Feld enthält die Identitätsdarstellung eines Subjekts, die aus den als „Identität“ markierten Feldern gezogen wird, wie im nächsten Abschnitt beschrieben.

### [!UICONTROL Identität] {#identity}

>[!CONTEXTUALHELP]
>id="platform_schemas_identities"
>title="Identitäten in Schemata"
>abstract="Identitäten sind Schlüsselfelder innerhalb eines Schemas, mit denen ein Objekt identifiziert werden kann, z. B. eine E-Mail-Adresse oder eine Marketing-ID. Diese Felder werden verwendet, um für jede Person ein Identitätsdiagramm sowie Kundenprofile zu erstellen. Weitere Informationen zu Identitäten in Schemata finden Sie in der Dokumentation."

Schemata werden für die Aufnahme von Daten in Experience Platform verwendet. Diese Daten können über mehrere Dienste hinweg verwendet werden, um eine einzelne, einheitliche Ansicht einer einzelnen Entität zu erstellen. Daher ist es beim Entwerfen von Schemas für Kundenidentitäten wichtig zu berücksichtigen, welche Felder zur Identifizierung eines Subjekts verwendet werden können, unabhängig davon, woher die Daten stammen.

Um diesen Prozess zu unterstützen, können Schlüsselfelder in Ihren Schemas als Identitäten markiert werden. Bei der Datenerfassung werden die Daten in diesen Feldern in die[!UICONTROL Identitätsdiagramm]&quot;für diese Person. Auf die Diagrammdaten kann dann zugegriffen werden durch [[!DNL Real-Time Customer Profile]](../../profile/home.md) und anderen Experience Platform-Services, um eine zusammengesetzte Sicht auf jeden einzelnen Kunden zu ermöglichen.

Felder, die normalerweise als[!UICONTROL Identität]&quot; include: email address, phone number, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=de), CRM-ID oder andere eindeutige ID-Felder. Betrachten Sie alle eindeutigen Kennungen, die für Ihr Unternehmen spezifisch sind, da sie gut sein können.[!UICONTROL Identität]&quot;.

Es ist wichtig, während der Schemaplanungsphase über Kundenidentitäten nachzudenken, um sicherzustellen, dass Daten zusammengeführt werden, um ein möglichst robustes Profil zu erstellen. Weitere Informationen dazu, wie Identitätsinformationen Ihnen dabei helfen können, Ihren Kunden digitale Erlebnisse bereitzustellen, finden Sie unter [Identity Service - Übersicht](../../identity-service/home.md). Weitere Informationen finden Sie im Dokument Best Practices für die Datenmodellierung für [Tipps zur Verwendung von Identitäten beim Erstellen eines Schemas](./best-practices.md#data-validation-fields).

Es gibt zwei Möglichkeiten, Identitätsdaten an Platform zu senden:

1. Hinzufügen von Identitätsdeskriptoren zu einzelnen Feldern, entweder über das [Benutzeroberfläche des Schema Editors](../ui/fields/identity.md) oder unter Verwendung der [Schema Registry-API](../api/descriptors.md#create)
1. Verwenden eines [`identityMap` field](#identityMap)

#### `identityMap` {#identityMap}

`identityMap` ist ein Feld vom Typ Zuordnung , das die verschiedenen Identitätswerte einer Person zusammen mit den zugehörigen Namespaces beschreibt. Dieses Feld kann verwendet werden, um Identitätsinformationen für Ihre Schemas bereitzustellen, anstatt Identitätswerte innerhalb der Struktur des Schemas selbst zu definieren.

Der größte Nachteil der Verwendung von `identityMap` ist, dass Identitäten in die Daten eingebettet und dadurch weniger sichtbar werden. Wenn Sie Rohdaten erfassen, sollten Sie stattdessen einzelne Identitätsfelder innerhalb der tatsächlichen Schemastruktur definieren.

>[!NOTE]
>
>Ein Schema, das `identityMap` kann als Quellschema in einer Beziehung verwendet werden, kann jedoch nicht als Referenzschema verwendet werden. Dies liegt daran, dass alle Referenzschemas eine sichtbare Identität aufweisen müssen, die in einem Referenzfeld innerhalb des Quellschemas zugeordnet werden kann. Weitere Informationen finden Sie im UI-Handbuch unter [Beziehungen](../tutorials/relationship-ui.md) für weitere Informationen über die Anforderungen an Quell- und Referenzschemas.

Identitätszuordnungen können jedoch nützlich sein, wenn eine variable Anzahl von Identitäten für ein Schema vorhanden ist oder Sie Daten aus Quellen zusammenführen, die Identitäten speichern (z. B. [!DNL Airship] oder Adobe Audience Manager). Darüber hinaus sind Identitätszuordnungen erforderlich, wenn Sie die [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/).

Ein Beispiel für eine einfache Identitätszuordnung würde wie folgt aussehen:

```json
"identityMap": {
  "email": [
    {
      "id": "jsmith@example.com",
      "primary": true
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
  "CRMID": [
    {
      "id": "2e33192000007456-0365c00000000000",
      "primary": false
    }
  ]
}
```

Wie das obige Beispiel zeigt, enthält jeder Schlüssel im `identityMap` -Objekt stellt einen Identitäts-Namespace dar. Der Wert für jeden Schlüssel ist ein Array von Objekten, die die Identitätswerte (`id`) für den entsprechenden Namespace. Siehe Abschnitt [!DNL Identity Service] Dokumentation für [Liste der standardmäßigen Identitäts-Namespaces](../../identity-service/troubleshooting-guide.md#standard-namespaces) von Adobe-Anwendungen erkannt werden.

>[!NOTE]
>
>Ein boolescher Wert, der angibt, ob der Wert eine primäre Identität ist (`primary`) kann auch für jeden Identitätswert bereitgestellt werden. Sie müssen nur primäre Identitäten für Schemas festlegen, die in [!DNL Real-Time Customer Profile]. Siehe Abschnitt zu [Vereinigungsschemas](#union) für weitere Informationen.

### Prinzipien der Schemaentwicklung {#evolution}

In dem Maße, wie sich die Art der digitalen Erfahrungen weiterentwickelt, müssen sich auch die Schemata, die zu ihrer Darstellung verwendet werden, weiterentwickeln. Ein gut entworfenes Schema ist daher in der Lage, sich bei Bedarf anzupassen und weiterzuentwickeln, ohne destruktive Änderungen an früheren Versionen des Schemas zu verursachen.

Da die Aufrechterhaltung der Abwärtskompatibilität für die Schemaentwicklung von entscheidender Bedeutung ist, erzwingt Experience Platform ein rein additives Versionierungsprinzip. Dieser Grundsatz stellt sicher, dass alle Änderungen am Schema nur zu zerstörungsfreien Aktualisierungen und Änderungen führen. Mit anderen Worten: **brechende Änderungen werden nicht unterstützt.**

>[!NOTE]
>
>Sie können eine brechende Änderung nur dann an einem Schema vornehmen, wenn es noch nicht zur Aufnahme von Daten in Experience Platform verwendet wurde und nicht für die Verwendung im Echtzeit-Kundenprofil aktiviert wurde. Sobald das Schema jedoch in [!DNL Platform], muss sie der Richtlinie zur additiven Versionierung entsprechen.

In der folgenden Tabelle werden die Änderungen aufgeschlüsselt, die beim Bearbeiten von Schemas, Feldergruppen und Datentypen unterstützt werden:

| Unterstützte Änderungen | Brechende Änderungen (nicht unterstützt) |
| --- | --- |
| <ul><li>Hinzufügen neuer Felder zur Ressource</li><li>Festlegen eines erforderlichen Felds als optional</li><li>Neue erforderliche Felder einführen*</li><li>Anzeigename und Beschreibung der Ressource ändern</li><li>Aktivieren des Schemas zur Teilnahme am Profil</li></ul> | <ul><li>Entfernen zuvor definierter Felder</li><li>Umbenennen oder Neudefinieren vorhandener Felder</li><li>Entfernen oder Eingrenzen zuvor unterstützter Feldwerte</li><li>Verschieben vorhandener Felder an eine andere Position im Baum</li><li>Löschen des Schemas</li><li>Deaktivieren der Teilnahme des Schemas am Profil</li></ul> |

\**Wichtige Aspekte zu [Festlegen neuer erforderlicher Felder](#post-ingestion-required-fields).*

### Erforderliche Felder

Einzelne Schemafelder können [markiert als erforderlich](../ui/fields/required.md), d. h. alle erfassten Datensätze müssen Daten in diesen Feldern enthalten, um die Validierung zu bestehen. Wenn Sie beispielsweise das primäre Identitätsfeld eines Schemas nach Bedarf festlegen, können Sie sicherstellen, dass alle erfassten Datensätze am Echtzeit-Kundenprofil teilnehmen. Gleichermaßen stellt die Festlegung eines Zeitstempelfelds nach Bedarf sicher, dass alle Zeitreihenereignisse chronologisch beibehalten werden.

>[!IMPORTANT]
>
>Unabhängig davon, ob ein Schemafeld erforderlich ist oder nicht, akzeptiert Platform nicht `null` oder leere Werte für alle erfassten Felder. Wenn in einem Datensatz oder Ereignis kein Wert für ein bestimmtes Feld vorhanden ist, sollte der Schlüssel für dieses Feld aus der Aufnahme-Payload ausgeschlossen werden.

#### Felder nach der Aufnahme entsprechend einstellen {#post-ingestion-required-fields}

Wenn ein Feld zum Erfassen von Daten verwendet wurde und ursprünglich nicht als erforderlich festgelegt wurde, kann dieses Feld für einige Datensätze einen Nullwert aufweisen. Wenn Sie dieses Feld nach der Erfassung als erforderlich festlegen, müssen alle zukünftigen Datensätze einen Wert für dieses Feld enthalten, auch wenn historische Datensätze möglicherweise null sind.

Beachten Sie beim Festlegen eines zuvor optionalen Felds nach Bedarf Folgendes:

1. Wenn Sie historische Daten abfragen und die Ergebnisse in einen neuen Datensatz schreiben, schlagen einige Zeilen fehl, da sie Nullwerte für das erforderliche Feld enthalten.
1. Wenn das Feld an [Echtzeit-Kundenprofil](../../profile/home.md) und wenn Sie Daten exportieren, bevor Sie sie nach Bedarf festlegen, können sie bei einigen Profilen null sein.
1. Sie können die Schema Registry-API verwenden, um einen Änderungsvorschlag mit Zeitstempel für alle XDM-Ressourcen in Platform anzuzeigen, einschließlich neuer erforderlicher Felder. Siehe Handbuch im Abschnitt [Endpunkt des Auditprotokolls](../api/audit-log.md) für weitere Informationen.

### Schemata und Datenerfassung

Um Daten in die Experience Platform aufnehmen zu können, muss zunächst ein Datensatz erstellt werden. Datensätze sind die Bausteine für die Datenumwandlung und -verfolgung für [[!DNL Catalog Service]](../../catalog/home.md)und stellen im Allgemeinen Tabellen oder Dateien dar, die aufgenommene Daten enthalten. Alle Datensätze basieren auf vorhandenen XDM-Schemata, die Einschränkungen dafür enthalten, was die aufgenommenen Daten enthalten und wie sie strukturiert sein sollten. Weitere Informationen hierzu finden Sie in der Übersicht über die [Datenerfassung in Adobe Experience Platform](../../ingestion/home.md).

## Bausteine eines Schemas {#schema-building-blocks}

Die Experience Platform verwendet einen Kompositionsansatz, bei dem Standardbausteine kombiniert werden, um Schemata zu erstellen. Dieser Ansatz fördert die Wiederverwendbarkeit vorhandener Komponenten und sorgt für Standardisierung in der gesamten Branche, um Schemas und Komponenten von Anbietern in [!DNL Platform].

Schemata werden nach folgender Formel zusammengestellt:

**Klasse + Schemafeldgruppe&amp;ast; = XDM-Schema**

&amp;ast;Ein Schema besteht aus einer Klasse und null oder mehr Schemafeldgruppen. Das bedeutet, dass Sie ein Datensatzschema erstellen können, ohne überhaupt Feldgruppen zu verwenden.

### Klasse {#class}

>[!CONTEXTUALHELP]
>id="platform_schemas_class"
>title="Klasse"
>abstract="Jedes Schema basiert auf einer einzelnen Klasse. Die Klasse definiert das Verhalten des Schemas und die allgemeinen Eigenschaften, die alle Schemata enthalten müssen, die auf dieser Klasse basieren. Weitere Informationen dazu, wie Klassen bei der Schemakomposition genutzt werden, finden Sie in der Dokumentation."

Das Erstellen eines Schemas beginnt mit dem Zuweisen einer Klasse. Klassen definieren die Verhaltensaspekte der Daten, die das Schema enthalten wird (Datensatz oder Zeitreihen). Darüber hinaus beschreiben Klassen die kleinste Anzahl gemeinsamer Eigenschaften, die alle Schemata, die auf dieser Klasse basieren, beinhalten müssen, und bieten eine Möglichkeit zum Zusammenführen mehrerer kompatibler Datensätze.

Die Klasse eines Schemas bestimmt, welche Feldergruppen für die Verwendung in diesem Schema geeignet sind. Weitere Informationen hierzu finden Sie im Abschnitt [nächster Abschnitt](#field-group).

Adobe bietet mehrere Standard-XDM-Klassen (&quot;Core&quot;). Zwei dieser Klassen, [!DNL XDM Individual Profile] und [!DNL XDM ExperienceEvent], sind für fast alle nachgelagerten Platform-Prozesse erforderlich. Zusätzlich zu diesen Core-Klassen können Sie auch eigene benutzerdefinierte Klassen erstellen, um spezifischere Anwendungsfälle für Ihr Unternehmen zu beschreiben. Benutzerdefinierte Klassen werden von einer Organisation definiert, wenn keine Adobe-definierten Core-Klassen zur Beschreibung eines eindeutigen Anwendungsfalls verfügbar sind.

Der folgende Screenshot zeigt, wie Klassen in der Platform-Benutzeroberfläche dargestellt werden. Da das angezeigte Beispielschema keine Feldergruppen enthält, werden alle angezeigten Felder von der Klasse des Schemas ([!UICONTROL Individuelles XDM-Profil]).

![Die [!UICONTROL Individuelles XDM-Profil] im Schema-Editor.](../images/schema-composition/class.png)

Die aktuellste Liste der verfügbaren Standard-XDM-Klassen finden Sie im Abschnitt [Offizielles XDM-Repository](https://github.com/adobe/xdm/tree/master/components/classes). Sie können auch das Handbuch unter [Erkunden von XDM-Komponenten](../ui/explore.md) , wenn Sie lieber Ressourcen in der Benutzeroberfläche anzeigen möchten.

### Feldergruppe {#field-group}

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup"
>title="Feldergruppe"
>abstract="Feldergruppen sind wiederverwendbare Komponenten, mit denen Sie Schemata durch zusätzliche Attribute erweitern können. Die meisten Feldergruppen sind nur mit bestimmten Klassen kompatibel. Sie können die von Adobe definierten Standardfeldergruppen verwenden oder eigene benutzerdefinierte Feldergruppen manuell erstellen. Weitere Informationen zur Verwendung von Feldergruppen bei der Schemakomposition finden Sie in der Dokumentation."

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup_requiredFieldgroup"
>title="Erforderliche Feldergruppe"
>abstract="Diese Feldergruppe ist für die verwendete Quelle erforderlich. Aus diesem Grund können Sie sie nicht aus Ihrem Schema löschen."

Eine Feldergruppe ist eine wiederverwendbare Komponente, die ein oder mehrere Felder definiert, die bestimmte Funktionen wie persönliche Details, Hotelpräferenzen oder Adressen implementieren. Feldergruppen sind als Teil eines Schemas vorgesehen, das eine kompatible Klasse implementiert.

Feldergruppen definieren, mit welcher Klasse(n) sie kompatibel sind, basierend auf dem Verhalten der Daten, die sie darstellen (Datensatz oder Zeitreihen). Das bedeutet, dass nicht alle Feldergruppen für alle Klassen verfügbar sind.

Experience Platform umfasst viele standardmäßige Adobe-Feldergruppen und ermöglicht es Anbietern, Feldergruppen für ihre zu definieren, sowie einzelnen Benutzern, Feldergruppen für ihre eigenen spezifischen Konzepte zu definieren.

So erfassen Sie beispielsweise Details wie[!UICONTROL Vorname]&quot; und &quot;[!UICONTROL Hausanschrift]&quot; für Ihre &quot;[!UICONTROL Mitglieder des Treueprogramms]&quot;Schema&quot;, können Sie Standardfeldgruppen verwenden, die diese gemeinsamen Konzepte definieren. Konzepte, die für Ihr Unternehmen spezifischer sind (z. B. Details zum Treueprogramm oder Produktattribute), die möglicherweise nicht von Standardfeldgruppen abgedeckt werden. In diesem Fall müssen Sie Ihre eigene Feldergruppe definieren, um diese Informationen zu erfassen.

>[!NOTE]
>
>Es wird dringend empfohlen, Standardfeldgruppen in Ihren Schemas zu verwenden, wann immer dies möglich ist, da diese Felder implizit von Experience Platform-Diensten verstanden werden und eine größere Konsistenz bieten, wenn sie über alle [!DNL Platform] Komponenten.
>
>Felder, die von Standardkomponenten bereitgestellt werden (z. B. &quot;Vorname&quot;und &quot;E-Mail-Adresse&quot;), enthalten zusätzliche Konnotationen, die über die grundlegenden Skalarfeldtypen hinausgehen. Sie sagen [!DNL Platform] dass alle Felder, die denselben Datentyp aufweisen, sich auf die gleiche Weise verhalten. Dieses Verhalten kann als konsistent betrachtet werden, unabhängig davon, woher die Daten stammen oder in welchem [!DNL Platform] -Dienst die Daten verwendet werden.

Beachten Sie, dass Schemas aus &quot;null oder mehr&quot;Feldergruppen bestehen. Dies bedeutet, dass Sie ein gültiges Schema erstellen können, ohne überhaupt Feldgruppen zu verwenden.

Der folgende Screenshot zeigt, wie Feldgruppen in der Platform-Benutzeroberfläche dargestellt werden. Eine einzelne Feldergruppe ([!UICONTROL Demografische Details]) wird in diesem Beispiel einem Schema hinzugefügt, das eine Gruppierung von Feldern zur Schemastruktur bereitstellt.

![Der Schema-Editor mit dem [!UICONTROL Demografische Details] in einem Beispielschema hervorgehobene Feldergruppe.](../images/schema-composition/field-group.png)

Die aktuellste Liste der verfügbaren Standard-XDM-Feldgruppen finden Sie im Abschnitt [Offizielles XDM-Repository](https://github.com/adobe/xdm/tree/master/components/fieldgroups). Sie können auch das Handbuch unter [Erkunden von XDM-Komponenten](../ui/explore.md) , wenn Sie lieber Ressourcen in der Benutzeroberfläche anzeigen möchten.

### Datentyp {#data-type}

Datentypen werden als Referenzfeldtypen in Klassen oder Schemata auf die gleiche Weise verwendet wie grundlegende literale Felder. Der wesentliche Unterschied besteht darin, dass Datentypen mehrere Unterfelder auf die gleiche Weise definieren können wie Feldgruppen. Der wesentliche Unterschied besteht darin, dass Datentypen an einer beliebigen Stelle in ein Schema eingefügt werden können, indem sie als &quot;Datentyp&quot;eines Felds hinzugefügt werden. Während Feldergruppen nur mit bestimmten Klassen kompatibel sind, können Datentypen in jede übergeordnete Klasse oder Feldergruppe aufgenommen werden.

>[!NOTE]
>
>Wenn ein Feld als spezifischer Datentyp definiert ist, können Sie dasselbe Feld mit einem anderen Datentyp nicht in einem anderen Schema erstellen. Diese Einschränkung gilt für den gesamten Mandanten Ihres Unternehmens.

Experience Platform bietet eine Reihe gängiger Datentypen im Rahmen der [!DNL Schema Registry] Unterstützung der Verwendung von Standardmustern zur Beschreibung gemeinsamer Datenstrukturen. Dies wird im Abschnitt [Tutorials zur Schema Registry](../tutorials/create-schema-api.md) und werden klarer, wenn Sie die Schritte zur Definition von Datentypen durchlaufen.

Der folgende Screenshot zeigt, wie Datentypen in der Platform-Benutzeroberfläche dargestellt werden. Eines der Felder, die vom [!UICONTROL Demografische Details] -Feldergruppe verwendet die[!UICONTROL Objekt]&quot;Datentyp, wie durch den Text nach dem senkrechten Strich (`|`) neben dem Feldnamen. Dieser bestimmte Datentyp bietet mehrere Unterfelder, die sich auf den Namen einer Person beziehen, ein Konstrukt, das für andere Felder wiederverwendet werden kann, in denen der Name einer Person erfasst werden muss.

![Ein Diagramm im Schema Editor für eine einzelne Person mit dem Objekt &quot;Vollständiger Name&quot;und den Attributen, die hervorgehoben sind.](../images/schema-composition/data-type.png)

Die aktuellste Liste der verfügbaren Standard-XDM-Datentypen finden Sie im Abschnitt [Offizielles XDM-Repository](https://github.com/adobe/xdm/tree/master/components/datatypes). Sie können auch das Handbuch unter [Erkunden von XDM-Komponenten](../ui/explore.md) , wenn Sie lieber Ressourcen in der Benutzeroberfläche anzeigen möchten.

### Feld {#field}

Ein Feld ist der grundlegendste Baustein eines Schemas. Felder bieten Einschränkungen hinsichtlich des Datentyps, den sie enthalten können, indem sie einen bestimmten Datentyp definieren. Diese grundlegenden Datentypen definieren ein einzelnes Feld, während die Variable [Datentypen](#data-type) können Sie mehrere Unterfelder definieren und dieselbe Struktur für mehrere Felder in verschiedenen Schemas wiederverwenden. Zusätzlich zur Definition des „Datentyps“ eines Feldes als einen der in der Registrierung definierten Datentypen unterstützt die Experience Platform also grundlegende Skalartypen wie:

* Zeichenfolge
* Ganzzahl
* Double
* Boolesch
* Array
* Objekt

>[!TIP]
>
>Siehe [Anhang](#objects-v-freeform) für Informationen über die Vor- und Nachteile der Verwendung von Freiformfeldern gegenüber Objekttypen.

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
>Der Feldtyp &quot;map&quot;ermöglicht Daten aus Schlüssel/Wert-Paaren, einschließlich mehrerer Werte für einen einzelnen Schlüssel. Karten finden Sie in Standard-XDM-Klassen und Feldergruppen, Sie können jedoch auch benutzerdefinierte Maps mithilfe der Schema Registry-API definieren. Siehe Tutorial zu [Definieren von benutzerdefinierten Feldern](../tutorials/custom-fields-api.md#custom-maps) für weitere Informationen.

## Kompositionsbeispiel {#composition-example}

Schemas werden mithilfe eines Kompositionsmodells erstellt und stellen das Format und die Struktur der Daten dar, in die aufgenommen werden sollen [!DNL Platform]. Wie bereits erwähnt, bestehen diese Schemas aus einer Klasse und null oder mehr Feldergruppen, die mit dieser Klasse kompatibel sind.

Beispielsweise könnte ein Schema, das Käufe in einem Einzelhandelsgeschäft beschreibt, wie folgt lauten:[!UICONTROL Store-Transaktionen]&quot;. Das Schema implementiert die [!DNL XDM ExperienceEvent] mit der Standardklasse kombiniert [!UICONTROL Handel] Feldergruppe und eine benutzerdefinierte [!UICONTROL Produktinformationen] Feldergruppe.

Ein anderes Schema, das den Website-Traffic verfolgt, könnte als &quot;[!UICONTROL Webbesuche]&quot;. Sie implementiert auch die [!DNL XDM ExperienceEvent] -Klasse, kombiniert diesmal jedoch den Standard [!UICONTROL Web] Feldergruppe.

Das folgende Diagramm zeigt diese Schemas und die von den einzelnen Feldergruppen hinzugefügten Felder. Es enthält außerdem zwei Schemas, die auf der Variablen [!DNL XDM Individual Profile] -Klasse, einschließlich &quot;[!UICONTROL Mitglieder des Treueprogramms]&quot; Schema, das zuvor in diesem Handbuch erwähnt wurde.

![Ein Flussdiagramm mit vier Schemas und den Feldergruppen, die zu ihnen beitragen.](../images/schema-composition/composition.png)

### Union {#union}

Während Experience Platform es Ihnen ermöglicht, Schemata für bestimmte Anwendungsfälle zusammenzustellen, können Sie auch eine „Vereinigung“ von Schemata für einen bestimmten Klassentyp sehen. Das vorherige Diagramm zeigt zwei Schemas, die auf der XDM ExperienceEvent-Klasse basieren, und zwei Schemas, die auf [!DNL XDM Individual Profile] -Klasse. Die unten dargestellte Vereinigung aggregiert die Felder aller Schemas, die dieselbe Klasse ([!DNL XDM ExperienceEvent] und [!DNL XDM Individual Profile], bzw. ).

![Ein Flussdiagramm für Vereinigungsschemata, das die Felder darstellt, aus denen sie bestehen.](../images/schema-composition/union.png)

Durch Aktivierung eines Schemas zur Verwendung mit [!DNL Real-Time Customer Profile], ist sie in der Vereinigung für diesen Klassentyp enthalten. [!DNL Profile] bietet zuverlässige, zentralisierte Profile mit Kundenattributen und ein zeitgestempeltes Konto für jedes Ereignis, das Kunden in allen Systemen hatten, die mit [!DNL Platform]. [!DNL Profile] verwendet die Vereinigungsansicht, um diese Daten darzustellen und eine ganzheitliche Sicht auf jeden einzelnen Kunden bereitzustellen.

Weitere Informationen zum Arbeiten mit [!DNL Profile], siehe [Übersicht über das Echtzeit-Kundenprofil](../../profile/home.md).

## Zuordnen von Datendateien zu XDM-Schemata {#mapping-datafiles}

Alle Datendateien, die in Experience Platform aufgenommen werden, müssen der Struktur eines XDM-Schemas entsprechen. Weitere Informationen zum Formatieren von Datendateien mit XDM-Hierarchien (einschließlich Beispieldateien) finden Sie im Dokument zu [Beispiel-ETL-Transformationen](../../etl/transformations.md). Allgemeine Informationen zur Aufnahme von Datendateien in Experience Platform finden Sie unter [Batch-Erfassung – Übersicht](../../ingestion/batch-ingestion/overview.md).

## Schemata für externe Zielgruppen

Wenn Sie Zielgruppen aus externen Systemen in Platform integrieren, müssen Sie die folgenden Komponenten verwenden, um sie in Ihren Schemas zu erfassen:

* [[!UICONTROL Segmentdefinition] class](../classes/segment-definition.md): Verwenden Sie diese Standardklasse, um Schlüsselattribute einer externen Segmentdefinition zu erfassen.
* [[!UICONTROL Details zur Segmentzugehörigkeit] Feldergruppe](../field-groups/profile/segmentation.md): Fügen Sie diese Feldergruppe zu Ihrer [!UICONTROL Individuelles XDM-Profil] Schema zur Zuordnung von Kundenprofilen zu bestimmten Zielgruppen.

## Nächste Schritte

Jetzt, da Sie die Grundlagen der Schemakomposition kennen, können Sie mit der Erforschung und Erstellung von Schemas beginnen, indem Sie die [!DNL Schema Registry].

Informationen zum Überprüfen der Struktur der beiden Core-XDM-Klassen und der häufig verwendeten kompatiblen Feldergruppen finden Sie in der folgenden Referenzdokumentation:

* [[!DNL XDM Individual Profile]](../classes/individual-profile.md)
* [[!DNL XDM ExperienceEvent]](../classes/experienceevent.md)

Die [!DNL Schema Registry] wird verwendet, um auf die [!DNL Schema Library] in Adobe Experience Platform und bietet eine Benutzeroberfläche und eine RESTful-API, über die alle verfügbaren Bibliotheksressourcen zugänglich sind. Die [!DNL Schema Library] enthält Branchenressourcen, die von Adobe definiert werden, von Experience Platform-Partnern definierte Vendor-Ressourcen sowie Klassen, Feldergruppen, Datentypen und Schemata, die von Mitgliedern Ihres Unternehmens zusammengestellt wurden.

Um mit dem Erstellen von Schemas über die Benutzeroberfläche zu beginnen, folgen Sie dem [Schema-Editor-Tutorial](../tutorials/create-schema-ui.md), um das Schema „Loyalty Members“ zu erstellen, das in diesem Dokument erwähnt wird.

So verwenden Sie die [!DNL Schema Registry] API, lesen Sie zunächst die [Entwicklerhandbuch zur Schema Registry-API](../api/getting-started.md). Nachdem Sie das Entwicklerhandbuch gelesen haben, führen Sie die Schritte aus, die im Tutorial zum [Erstellen eines Schemas mit der Schema Registry-API](../tutorials/create-schema-api.md) beschrieben werden.

## Anhang

Die folgenden Abschnitte enthalten zusätzliche Informationen zu den Prinzipien der Schemakomposition.

### Relationale Tabellen versus eingebettete Objekte {#embedded}

Bei der Arbeit mit relationalen Datenbanken bestehen die Best Practices darin, Daten zu normalisieren oder eine Entität in diskrete Teile zu zerlegen, die dann in mehreren Tabellen angezeigt werden. Um die Daten insgesamt zu lesen oder die Entität zu aktualisieren, müssen Lese- und Schreibvorgänge über viele einzelne Tabellen mit JOIN durchgeführt werden.

Durch die Verwendung eingebetteter Objekte können XDM-Schemas komplexe Daten direkt darstellen und in eigenständigen Dokumenten mit hierarchischer Struktur speichern. Einer der Hauptvorteile dieser Struktur besteht darin, dass Sie die Daten abfragen können, ohne die Entität durch teure Verbindungen zu mehreren denormalisierten Tabellen rekonstruieren zu müssen. Es gibt keine Einschränkungen dafür, wie viele Ebenen Ihre Schemahierarchie sein kann.

### Schemata und Big Data {#big-data}

Moderne digitale Systeme generieren enorme Mengen von Verhaltenssignalen (Transaktionsdaten, Weblogs, Internet der Dinge, Anzeige usw.). Diese Big-Data-Daten bieten außergewöhnliche Möglichkeiten zur Optimierung von Erlebnissen, sind aber aufgrund der Größe und Vielfalt der Daten schwierig zu nutzen. Um aus den Daten Nutzen zu ziehen, müssen Struktur, Format und Definitionen standardisiert werden, damit sie konsistent und effizient verarbeitet werden können.

Schemata lösen dieses Problem, indem sie die Integration von Daten aus mehreren Quellen, die Standardisierung durch gemeinsame Strukturen und Definitionen und die lösungsübergreifende gemeinsame Nutzung ermöglichen. Dadurch können nachfolgende Prozesse und Dienste jede Art von Frage beantworten, die von den Daten gestellt wird. Es entfernt sich vom herkömmlichen Ansatz zur Datenmodellierung, bei dem alle Fragen, die an die Daten gestellt werden sollen, im Voraus bekannt sind und die Daten modelliert werden, um diesen Erwartungen zu entsprechen.

### Objekte versus Freiformfelder {#objects-v-freeform}

Bei der Auswahl von Objekten gegenüber Freiformfeldern bei der Erstellung von Schemata sind einige wichtige Faktoren zu beachten:

| Objekte | Freiformfelder |
| --- | --- |
| Erhöht die Verschachtelung | Weniger oder keine Verschachtelung |
| Erstellt logische Feldgruppierungen | Felder werden an Ad-hoc-Positionen platziert |

{style="table-layout:auto"}

#### Objekte

Die Vor- und Nachteile der Verwendung von Objekten über Freiformfeldern sind unten aufgeführt.

**Vorteile**:

* Objekte eignen sich am besten, wenn Sie eine logische Gruppierung bestimmter Felder erstellen möchten.
* Objekte ordnen das Schema strukturierter an.
* Objekte helfen indirekt bei der Erstellung einer guten Menüstruktur in der Benutzeroberfläche von Segment Builder. Die gruppierten Felder innerhalb des Schemas werden direkt in der Ordnerstruktur angezeigt, die in der Benutzeroberfläche von Segment Builder bereitgestellt wird.

**Nachteile**:

* Felder werden verschachtelter.
* Bei Verwendung von [Adobe Experience Platform Query Service](../../query-service/home.md)müssen für Abfragefelder, die in Objekten verschachtelt sind, längere Referenzzeichenfolgen angegeben werden.

#### Freiformfelder

Die Vor- und Nachteile der Verwendung von Freiformfeldern gegenüber Objekten sind unten aufgeführt.

**Vorteile**:

* Freiformfelder werden direkt unter dem Stammobjekt des Schemas (`_tenantId`), um die Sichtbarkeit zu erhöhen.
* Bei Verwendung von Query Service sind Referenzzeichenfolgen für Freiformfelder in der Regel kürzer.

**Nachteile**:

* Der Speicherort von Freiformfeldern im Schema ist Ad-hoc, d. h. sie werden im Schema Editor in alphabetischer Reihenfolge angezeigt. Dies kann dazu führen, dass Schemas weniger strukturiert sind und ähnliche Freiformfelder je nach Namen weit voneinander getrennt werden.
