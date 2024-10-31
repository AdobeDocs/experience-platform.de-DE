---
keywords: Experience Platform; home; beliebte Themen; Schema; Enum; Mixin; Feldergruppe; Feldergruppen; Feldergruppen; Mixins; Datentyp; Datentypen; Datentypen; Datentyp; primäre Identität; primäre Identität; XDM-individuelles Profil; XDM-Felder; Enum-Datentyp; Erlebnis-Ereignis; XDM Experience Event; XDM ExperienceEvent; ExperienceEvent; XDM ExperienceEvent; Schema-Design; Klasse; Klasse;Klassen;Datentyp;Datentyp;Datentyp;Datentyp;Datentyp;Schemas;Schemas;Identitätszuordnung;Identitätszuordnung;Identitätszuordnung;Schema-Design;Map;Map;Vereinigungsschema;Vereinigung
solution: Experience Platform
title: Grundlagen der Schemakomposition
description: Erfahren Sie mehr über Experience-Datenmodell (XDM)-Schemas und die Bausteine, Grundsätze und Best Practices zum Erstellen von Schemas in Adobe Experience Platform.
exl-id: d449eb01-bc60-4f5e-8d6f-ab4617878f7e
source-git-commit: 595d9bd6a0aa0c9f1059e485c54e89ce02b7ec68
workflow-type: tm+mt
source-wordcount: '4365'
ht-degree: 26%

---

# Grundlagen der Schema-Komposition

Erfahren Sie mehr über Experience-Datenmodell (XDM)-Schemas und die Bausteine, Grundsätze und Best Practices zum Erstellen von Schemas in Adobe Experience Platform. Allgemeine Informationen zu XDM und dessen Verwendung in [!DNL Platform] finden Sie in der [XDM-Systemübersicht](../home.md).

## Verstehen von Schemata {#understanding-schemas}

Ein Schema ist ein Regelsatz, der die Datenstruktur und das Datenformat darstellt und überprüft. Auf hoher Ebene bieten Schemata eine abstrakte Definition eines realen Objekts (z. B. einer Person) und legen dar, welche Daten in jeder Instanz dieses Objekts enthalten sein sollen (z. B. Vorname, Nachname, Geburtsdatum usw.).

Zusätzlich zur Beschreibung der Datenstruktur wenden Schemata Einschränkungen und Erwartungen an Daten an, damit diese bei ihren Bewegungen zwischen den Systemen validiert werden können. Diese Standarddefinitionen ermöglichen eine konsistente Interpretation der Daten, unabhängig von ihrer Herkunft, und machen eine anwendungsübergreifende Übersetzung überflüssig.

Experience Platform behält diese semantische Normalisierung bei, indem Schemas verwendet werden. Schemata sind die Standardmethode zur Beschreibung von Daten in Experience Platform. Dadurch können alle Daten, die mit Schemata konform sind, innerhalb einer Organisation ohne Konflikte wiederverwendet oder sogar von mehreren Organisationen gemeinsam genutzt werden.

XDM-Schemata eignen sich ideal zum Speichern großer Mengen komplexer Daten in einem eigenständigen Format. Weitere Informationen dazu, wie XDM dies erreicht, finden Sie in den Abschnitten zu [eingebetteten Objekten](#embedded) und [Big Data](#big-data) im Anhang zu diesem Dokument.

### Schema-basierte Workflows in Experience Platform {#schema-based-workflows}

Die Standardisierung ist ein Schlüsselkonzept der Experience Platform. Das von Adobe unterstützte XDM-System ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schemata für das Customer Experience Management zu definieren.

Die als [!DNL XDM System] bezeichnete Infrastruktur, auf der Experience Platform erstellt wird, erleichtert schemabasierte Workflows und umfasst die Muster [!DNL Schema Registry], [!DNL Schema Editor], Schemadaten und Dienstverbrauch. Weitere Informationen finden Sie in der [XDM-Systemübersicht](../home.md).

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

Um diesen Prozess zu unterstützen, können Schlüsselfelder in Ihren Schemas als Identitäten markiert werden. Bei der Datenerfassung werden die Daten in diesen Feldern in das &quot;[!UICONTROL Identitätsdiagramm]&quot;für diese Person eingefügt. Die Diagrammdaten können dann von [[!DNL Real-Time Customer Profile]](../../profile/home.md) und anderen Experience Platform-Services aufgerufen werden, um eine zusammengesetzte Ansicht jedes einzelnen-Kunden zu erhalten.

Zu den Feldern, die üblicherweise als &quot;[!UICONTROL Identität]&quot; gekennzeichnet werden, gehören: E-Mail-Adresse, Telefonnummer, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=de), CRM-ID oder andere eindeutige ID-Felder. Betrachten Sie alle eindeutigen Kennungen, die für Ihr Unternehmen spezifisch sind, da sie auch gut mit den Feldern &quot;[!UICONTROL Identität]&quot;sein können.

Es ist wichtig, während der Schemaplanungsphase über Kundenidentitäten nachzudenken, um sicherzustellen, dass Daten zusammengeführt werden, um ein möglichst robustes Profil zu erstellen. Weitere Informationen dazu, wie Identitätsinformationen Ihnen dabei helfen können, Ihren Kunden digitale Erlebnisse bereitzustellen, finden Sie in der [Übersicht über den Identity Service](../../identity-service/home.md) . Tipps zur Verwendung von Identitäten beim Erstellen eines Schemas finden Sie im Dokument Best Practices für die Datenmodellierung [ .](./best-practices.md#data-validation-fields)

Es gibt zwei Möglichkeiten, Identitätsdaten an Platform zu senden:

1. Hinzufügen von Identitätsdeskriptoren zu einzelnen Feldern entweder über die [Schema Editor UI](../ui/fields/identity.md) oder die [Schema Registry-API](../api/descriptors.md#create)
1. Verwenden eines [`identityMap`-Felds](#identityMap)

#### `identityMap` {#identityMap}

`identityMap` ist ein Feld vom Typ Zuordnung , das die verschiedenen Identitätswerte einer Person zusammen mit den zugehörigen Namespaces beschreibt. Dieses Feld kann verwendet werden, um Identitätsinformationen für Ihre Schemas bereitzustellen, anstatt Identitätswerte innerhalb der Struktur des Schemas selbst zu definieren.

Der größte Nachteil der Verwendung von `identityMap` besteht darin, dass Identitäten in die Daten eingebettet und dadurch weniger sichtbar werden. Wenn Sie Rohdaten erfassen, sollten Sie stattdessen einzelne Identitätsfelder innerhalb der tatsächlichen Schemastruktur definieren.

>[!NOTE]
>
>Ein Schema, das `identityMap` verwendet, kann als Quellschema in einer Beziehung verwendet werden, kann jedoch nicht als Referenzschema verwendet werden. Dies liegt daran, dass alle Referenzschemas eine sichtbare Identität aufweisen müssen, die in einem Referenzfeld innerhalb des Quellschemas zugeordnet werden kann. Weitere Informationen zu den Anforderungen von Quell- und Referenzschemas finden Sie im UI-Handbuch zu [Beziehungen](../tutorials/relationship-ui.md) .

Identitätszuordnungen können jedoch nützlich sein, wenn für ein Schema eine variable Anzahl von Identitäten vorhanden ist oder Sie Daten aus Quellen zusammenführen, die Identitäten speichern (z. B. [!DNL Airship] oder Adobe Audience Manager). Darüber hinaus sind Identitätszuordnungen erforderlich, wenn Sie das [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/) verwenden.

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

Wie das obige Beispiel zeigt, stellt jeder Schlüssel im Objekt `identityMap` einen Identitäts-Namespace dar. Der Wert für jeden Schlüssel ist ein Array von Objekten, die die Identitätswerte (`id`) für den jeweiligen Namespace darstellen. Eine [Liste der von Adobe-Anwendungen erkannten standardmäßigen Identitäts-Namespaces](../../identity-service/troubleshooting-guide.md#standard-namespaces) finden Sie in der Dokumentation zu [!DNL Identity Service] .

>[!NOTE]
>
>Ein boolean -Wert, der angibt, ob der Wert eine primäre Identität (`primary`) ist, kann auch für jeden Identitätswert angegeben werden. Sie müssen nur primäre Identitäten für Schemas festlegen, die in [!DNL Real-Time Customer Profile] verwendet werden sollen. Weitere Informationen finden Sie im Abschnitt zu [Vereinigungsschemas](#union) .

### Prinzipien der Schemaentwicklung {#evolution}

In dem Maße, wie sich die Art der digitalen Erfahrungen weiterentwickelt, müssen sich auch die Schemata, die zu ihrer Darstellung verwendet werden, weiterentwickeln. Ein gut entworfenes Schema ist daher in der Lage, sich bei Bedarf anzupassen und weiterzuentwickeln, ohne destruktive Änderungen an früheren Versionen des Schemas zu verursachen.

Da die Aufrechterhaltung der Abwärtskompatibilität für die Schemaentwicklung von entscheidender Bedeutung ist, erzwingt Experience Platform ein rein additives Versionierungsprinzip. Dieser Grundsatz stellt sicher, dass alle Änderungen am Schema nur zu zerstörungsfreien Aktualisierungen und Änderungen führen. Mit anderen Worten: **brechende Änderungen werden nicht unterstützt.**

>[!NOTE]
>
>Sie können eine brechende Änderung nur dann an einem Schema vornehmen, wenn es noch nicht zur Aufnahme von Daten in Experience Platform verwendet wurde und nicht für die Verwendung im Echtzeit-Kundenprofil aktiviert wurde. Sobald das Schema jedoch in [!DNL Platform] verwendet wurde, muss es der Richtlinie für die additive Versionierung entsprechen.

In der folgenden Tabelle werden die Änderungen aufgeschlüsselt, die beim Bearbeiten von Schemas, Feldergruppen und Datentypen unterstützt werden:

| Unterstützte Änderungen | Brechende Änderungen (nicht unterstützt) |
| --- | --- |
| <ul><li>Hinzufügen neuer Felder zur Ressource</li><li>Festlegen eines erforderlichen Felds als optional</li><li>Neue erforderliche Felder einführen*</li><li>Anzeigename und Beschreibung der Ressource ändern</li><li>Aktivieren des Schemas zur Teilnahme am Profil</li></ul> | <ul><li>Entfernen zuvor definierter Felder</li><li>Umbenennen oder Neudefinieren vorhandener Felder</li><li>Entfernen oder Eingrenzen zuvor unterstützter Feldwerte</li><li>Verschieben vorhandener Felder an eine andere Position im Baum</li><li>Löschen des Schemas</li><li>Deaktivieren der Teilnahme des Schemas am Profil</li></ul> |

\**Wichtige Überlegungen zum Festlegen neuer erforderlicher Felder finden Sie im folgenden Abschnitt[.](#post-ingestion-required-fields)*

### Erforderliche Felder

Einzelne Schemafelder können [als erforderlich markiert werden](../ui/fields/required.md). Das bedeutet, dass alle erfassten Datensätze Daten in diesen Feldern enthalten müssen, damit die Validierung besteht. Wenn Sie beispielsweise das primäre Identitätsfeld eines Schemas nach Bedarf festlegen, können Sie sicherstellen, dass alle erfassten Datensätze am Echtzeit-Kundenprofil teilnehmen. Gleichermaßen stellt die Festlegung eines Zeitstempelfelds nach Bedarf sicher, dass alle Zeitreihenereignisse chronologisch beibehalten werden.

>[!IMPORTANT]
>
>Unabhängig davon, ob ein Schemafeld erforderlich ist oder nicht, akzeptiert Platform für ein erfasstes Feld weder `null` noch leere Werte. Wenn in einem Datensatz oder Ereignis kein Wert für ein bestimmtes Feld vorhanden ist, sollte der Schlüssel für dieses Feld aus der Aufnahme-Payload ausgeschlossen werden.

#### Felder nach der Aufnahme entsprechend einstellen {#post-ingestion-required-fields}

Wenn ein Feld zum Erfassen von Daten verwendet wurde und ursprünglich nicht als erforderlich festgelegt wurde, kann dieses Feld für einige Datensätze einen Nullwert aufweisen. Wenn Sie dieses Feld nach der Erfassung als erforderlich festlegen, müssen alle zukünftigen Datensätze einen Wert für dieses Feld enthalten, auch wenn historische Datensätze möglicherweise null sind.

Beachten Sie beim Festlegen eines zuvor optionalen Felds nach Bedarf Folgendes:

1. Wenn Sie historische Daten abfragen und die Ergebnisse in einen neuen Datensatz schreiben, schlagen einige Zeilen fehl, da sie Nullwerte für das erforderliche Feld enthalten.
1. Wenn das Feld zum [Echtzeit-Kundenprofil](../../profile/home.md) gehört und Sie Daten exportieren, bevor Sie es als erforderlich festlegen, kann es für einige Profile null sein.
1. Sie können die Schema Registry-API verwenden, um einen Änderungsvorschlag mit Zeitstempel für alle XDM-Ressourcen in Platform anzuzeigen, einschließlich neuer erforderlicher Felder. Weitere Informationen finden Sie im Handbuch zum [Auditprotokoll-Endpunkt](../api/audit-log.md) .

### Schemata und Datenerfassung

Um Daten in die Experience Platform aufnehmen zu können, muss zunächst ein Datensatz erstellt werden. Datensätze sind die Bausteine für die Datenumwandlung und -verfolgung für [[!DNL Catalog Service]](../../catalog/home.md) und stellen im Allgemeinen Tabellen oder Dateien dar, die aufgenommene Daten enthalten. Alle Datensätze basieren auf vorhandenen XDM-Schemata, die Einschränkungen dafür enthalten, was die aufgenommenen Daten enthalten und wie sie strukturiert sein sollten. Weitere Informationen hierzu finden Sie in der Übersicht über die [Datenerfassung in Adobe Experience Platform](../../ingestion/home.md).

## Bausteine eines Schemas {#schema-building-blocks}

Die Experience Platform verwendet einen Kompositionsansatz, bei dem Standardbausteine kombiniert werden, um Schemata zu erstellen. Dieser Ansatz fördert die Wiederverwendbarkeit vorhandener Komponenten und sorgt für Standardisierung in der gesamten Branche, um Schemas und Komponenten von Anbietern in [!DNL Platform] zu unterstützen.

Schemata werden nach folgender Formel zusammengestellt:

**Klasse + Schemafeldgruppe&amp;ast; = XDM-Schema**

&amp;ast;Ein Schema besteht aus einer Klasse und null oder mehr Schemafeldgruppen. Das bedeutet, dass Sie ein Datensatzschema erstellen können, ohne überhaupt Feldgruppen zu verwenden.

### Klasse {#class}

>[!CONTEXTUALHELP]
>id="platform_schemas_class"
>title="Klasse"
>abstract="Jedes Schema basiert auf einer einzelnen Klasse. Die Klasse definiert das Verhalten des Schemas und die allgemeinen Eigenschaften, die alle Schemata enthalten müssen, die auf dieser Klasse basieren. Weitere Informationen dazu, wie Klassen bei der Schemakomposition genutzt werden, finden Sie in der Dokumentation."

>[!CONTEXTUALHELP]
>id="platform_schemas_class_industries"
>title="Branchentyp"
>abstract="Wenn Sie eine für Ihr Unternehmen relevante Branche auswählen, kann das Modell für maschinelles Lernen eine bessere Organisation der Daten ermöglichen, indem die Quellfelder genauer den Standardfeldgruppen zugeordnet werden, die den Branchenstandards entsprechen. Dadurch wird sichergestellt, dass die Datenintegration auf Ihre branchenspezifischen Anforderungen zugeschnitten ist, was zu präziseren und relevanteren Datenerkenntnissen führt."

Das Erstellen eines Schemas beginnt mit dem Zuweisen einer Klasse. Klassen definieren die Verhaltensaspekte der Daten, die das Schema enthalten wird (Datensatz oder Zeitreihen). Darüber hinaus beschreiben Klassen die kleinste Anzahl gemeinsamer Eigenschaften, die alle Schemata, die auf dieser Klasse basieren, beinhalten müssen, und bieten eine Möglichkeit zum Zusammenführen mehrerer kompatibler Datensätze.

Die Klasse eines Schemas bestimmt, welche Feldergruppen für die Verwendung in diesem Schema geeignet sind. Dies wird im Abschnitt [Nächster Abschnitt](#field-group) ausführlicher erläutert.

Adobe bietet mehrere Standard-XDM-Klassen (&quot;Core&quot;). Zwei dieser Klassen, [!DNL XDM Individual Profile] und [!DNL XDM ExperienceEvent], sind für fast alle nachgelagerten Platform-Prozesse erforderlich. Zusätzlich zu diesen Core-Klassen können Sie auch eigene benutzerdefinierte Klassen erstellen, um spezifischere Anwendungsfälle für Ihr Unternehmen zu beschreiben. Benutzerdefinierte Klassen werden von einer Organisation definiert, wenn keine Adobe-definierten Core-Klassen zur Beschreibung eines eindeutigen Anwendungsfalls verfügbar sind.

Der folgende Screenshot zeigt, wie Klassen in der Platform-Benutzeroberfläche dargestellt werden. Da das angezeigte Beispielschema keine Feldergruppen enthält, werden alle angezeigten Felder von der Klasse des Schemas ([!UICONTROL XDM Individual Profile]) bereitgestellt.

![Das [!UICONTROL XDM Individual Profile] im Schema Editor](../images/schema-composition/class.png).

Die aktuellste Liste der verfügbaren Standard-XDM-Klassen finden Sie im [offiziellen XDM-Repository](https://github.com/adobe/xdm/tree/master/components/classes). Alternativ können Sie das Handbuch zum [Erkunden von XDM-Komponenten](../ui/explore.md) lesen, wenn Sie es vorziehen, Ressourcen in der Benutzeroberfläche anzuzeigen.

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

Um beispielsweise Details wie &quot;[!UICONTROL Vorname]&quot;und &quot;[!UICONTROL Privatadresse]&quot;für Ihr Schema &quot;[!UICONTROL Mitglieder des Treueprogramms]&quot;zu erfassen, können Sie Standardfeldgruppen verwenden, die diese gemeinsamen Konzepte definieren. Konzepte, die für Ihr Unternehmen spezifischer sind (z. B. Details zum Treueprogramm oder Produktattribute), die möglicherweise nicht von Standardfeldgruppen abgedeckt werden. In diesem Fall müssen Sie Ihre eigene Feldergruppe definieren, um diese Informationen zu erfassen.

>[!NOTE]
>
>Es wird dringend empfohlen, Standardfeldgruppen zu verwenden, wann immer dies in Ihren Schemas möglich ist, da diese Felder implizit von Experience Platform-Diensten verstanden werden und eine größere Konsistenz bei der Verwendung über [!DNL Platform] -Komponenten hinweg bieten.
>
>Felder, die von Standardkomponenten bereitgestellt werden (z. B. &quot;Vorname&quot;und &quot;E-Mail-Adresse&quot;), enthalten zusätzliche Konnotationen, die über die grundlegenden Skalarfeldtypen hinausgehen. Sie teilen [!DNL Platform] mit, dass sich alle Felder, die denselben Datentyp aufweisen, auf die gleiche Weise verhalten. Dieses Verhalten kann als konsistent betrachtet werden, unabhängig davon, woher die Daten stammen oder in welchem [!DNL Platform]-Dienst die Daten verwendet werden.

Beachten Sie, dass Schemas aus &quot;null oder mehr&quot;Feldergruppen bestehen. Dies bedeutet, dass Sie ein gültiges Schema erstellen können, ohne überhaupt Feldgruppen zu verwenden.

Der folgende Screenshot zeigt, wie Feldgruppen in der Platform-Benutzeroberfläche dargestellt werden. In diesem Beispiel wird einem Schema eine einzelne Feldergruppe ([!UICONTROL Demografische Details]) hinzugefügt, die der Schemastruktur eine Gruppierung von Feldern bietet.

![Der Schema-Editor mit der Feldergruppe [!UICONTROL Demografische Details] , die in einem Beispielschema hervorgehoben ist.](../images/schema-composition/field-group.png)

Die aktuellste Liste der verfügbaren Standard-XDM-Feldergruppen finden Sie im [offiziellen XDM-Repository](https://github.com/adobe/xdm/tree/master/components/fieldgroups). Alternativ können Sie das Handbuch zum [Erkunden von XDM-Komponenten](../ui/explore.md) lesen, wenn Sie es vorziehen, Ressourcen in der Benutzeroberfläche anzuzeigen.

>[!NOTE]
>
> Standard-XDM-Feldergruppen entwickeln sich immer weiter und einige Feldergruppen werden nicht mehr unterstützt. Die aktuellste Liste veralteter Feldergruppen finden Sie im Abschnitt [veraltete Feldergruppen](https://github.com/adobe/xdm/tree/master/components/fieldgroups/deprecated) im offiziellen XDM-Repository.

### Datentyp {#data-type}

Datentypen werden als Referenzfeldtypen in Klassen oder Schemata auf die gleiche Weise verwendet wie grundlegende literale Felder. Der wesentliche Unterschied besteht darin, dass Datentypen mehrere Unterfelder auf die gleiche Weise definieren können wie Feldgruppen. Der wesentliche Unterschied besteht darin, dass Datentypen an einer beliebigen Stelle in ein Schema eingefügt werden können, indem sie als &quot;Datentyp&quot;eines Felds hinzugefügt werden. Während Feldergruppen nur mit bestimmten Klassen kompatibel sind, können Datentypen in jede übergeordnete Klasse oder Feldergruppe aufgenommen werden.

>[!NOTE]
>
>Wenn ein Feld als spezifischer Datentyp definiert ist, können Sie dasselbe Feld mit einem anderen Datentyp nicht in einem anderen Schema erstellen. Diese Einschränkung gilt für den gesamten Mandanten Ihres Unternehmens.

Experience Platform bietet eine Reihe gängiger Datentypen im Rahmen von [!DNL Schema Registry], um die Verwendung von Standardmustern zur Beschreibung gemeinsamer Datenstrukturen zu unterstützen. Dies wird in den Tutorials [Schemaregistrierung](../tutorials/create-schema-api.md) ausführlicher erläutert und wird beim Durchlaufen der Schritte zur Definition von Datentypen verständlicher.

Der folgende Screenshot zeigt, wie Datentypen in der Platform-Benutzeroberfläche dargestellt werden. Eines der Felder, die von der Feldergruppe [!UICONTROL Demografische Details] bereitgestellt werden, verwendet den Datentyp &quot;[!UICONTROL Objekt]&quot;, wie durch den Text nach dem Pipe-Zeichen (`|`) neben dem Feldnamen angegeben. Dieser bestimmte Datentyp bietet mehrere Unterfelder, die sich auf den Namen einer Person beziehen, ein Konstrukt, das für andere Felder wiederverwendet werden kann, in denen der Name einer Person erfasst werden muss.

![Ein Diagramm im Schema Editor für eine einzelne Person mit dem Objekt und den Attributen &quot;Vollständiger Name&quot;.](../images/schema-composition/data-type.png)

Die aktuellste Liste der verfügbaren Standard-XDM-Datentypen finden Sie im [offiziellen XDM-Repository](https://github.com/adobe/xdm/tree/master/components/datatypes). Alternativ können Sie das Handbuch zum [Erkunden von XDM-Komponenten](../ui/explore.md) lesen, wenn Sie es vorziehen, Ressourcen in der Benutzeroberfläche anzuzeigen.

>[!NOTE]
>
> Standard-XDM-Datentypen entwickeln sich immer, und einige Datentypen sind veraltet. Die aktuellste Liste veralteter Datentypen finden Sie im Abschnitt [veraltete Datentypen](https://github.com/adobe/xdm/tree/master/components/datatypes/deprecated) im offiziellen XDM-Repository.

### Feld {#field}

Ein Feld ist der grundlegendste Baustein eines Schemas. Felder bieten Einschränkungen hinsichtlich des Datentyps, den sie enthalten können, indem sie einen bestimmten Datentyp definieren. Diese grundlegenden Datentypen definieren ein einzelnes Feld, während die zuvor erwähnten [Datentypen](#data-type) es ermöglichen, mehrere Unterfelder zu definieren und dieselbe Mehrfeldstruktur in verschiedenen Schemas wiederzuverwenden. Zusätzlich zur Definition des „Datentyps“ eines Feldes als einen der in der Registrierung definierten Datentypen unterstützt die Experience Platform also grundlegende Skalartypen wie:

* Zeichenfolge
* Ganzzahl
* Double
* Boolesch
* Array
* Objekt

>[!TIP]
>
>Informationen zu den Vor- und Nachteilen der Verwendung von Freiformfeldern über Objekttypen finden Sie im [Anhang](#objects-v-freeform) .

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
>Der Feldtyp &quot;map&quot;ermöglicht Daten aus Schlüssel/Wert-Paaren, einschließlich mehrerer Werte für einen einzelnen Schlüssel. Maps finden Sie in Standard-XDM-Klassen und Feldergruppen, Sie können aber auch benutzerdefinierte Maps definieren. Weitere Informationen finden Sie im API-Tutorial zum Definieren von benutzerdefinierten Zuordnungsfeldern ](../tutorials/custom-fields-api.md#custom-maps) oder im Handbuch zum Definieren von Zuordnungsfeldern in der Benutzeroberfläche [.[](../ui/fields/map.md)

## Kompositionsbeispiel {#composition-example}

Schemas werden mithilfe eines Kompositionsmodells erstellt und stellen das Format und die Struktur der Daten dar, die in [!DNL Platform] aufgenommen werden sollen. Wie bereits erwähnt, bestehen diese Schemas aus einer Klasse und null oder mehr Feldergruppen, die mit dieser Klasse kompatibel sind.

Beispielsweise könnte ein Schema, das Käufe in einem Einzelhandelsgeschäft beschreibt, &quot;[!UICONTROL Store-Transaktionen]&quot;heißen. Das Schema implementiert die [!DNL XDM ExperienceEvent] -Klasse in Kombination mit der standardmäßigen [!UICONTROL Commerce] -Feldergruppe und einer benutzerdefinierten [!UICONTROL Product Info] -Feldergruppe.

Ein weiteres Schema, das den Website-Traffic verfolgt, könnte &quot;[!UICONTROL Webbesuche]&quot;heißen. Es implementiert auch die [!DNL XDM ExperienceEvent] -Klasse, kombiniert diesmal jedoch die standardmäßige [!UICONTROL Web] -Feldergruppe.

Das folgende Diagramm zeigt diese Schemas und die von den einzelnen Feldergruppen hinzugefügten Felder. Es enthält außerdem zwei Schemas, die auf der Klasse [!DNL XDM Individual Profile] basieren, einschließlich des Schemas &quot;[!UICONTROL Mitglieder des Treueprogramms]&quot;, das zuvor in diesem Handbuch erwähnt wurde.

![Ein Flussdiagramm mit vier Schemas und den Feldergruppen, die zu ihnen beitragen.](../images/schema-composition/composition.png)

### Union {#union}

Während Experience Platform es Ihnen ermöglicht, Schemata für bestimmte Anwendungsfälle zusammenzustellen, können Sie auch eine „Vereinigung“ von Schemata für einen bestimmten Klassentyp sehen. Das vorherige Diagramm zeigt zwei Schemas, die auf der XDM ExperienceEvent-Klasse basieren, und zwei Schemas, die auf der [!DNL XDM Individual Profile]-Klasse basieren. Die unten dargestellte Vereinigung aggregiert die Felder aller Schemas, die dieselbe Klasse besitzen ([!DNL XDM ExperienceEvent] bzw. [!DNL XDM Individual Profile]).

![Ein Vereinigungsschema-Flussdiagramm, das die Felder darstellt, aus denen sie bestehen.](../images/schema-composition/union.png)

Durch Aktivierung eines Schemas zur Verwendung mit [!DNL Real-Time Customer Profile] wird es in die Vereinigung für diesen Klassentyp aufgenommen. [!DNL Profile] liefert robuste, zentralisierte Profile mit Kundenattributen und ein mit Zeitstempel versehenes Konto für jedes Ereignis, das der Kunde in einem beliebigen mit [!DNL Platform] integrierten System hatte. [!DNL Profile] verwendet die Vereinigungsansicht, um diese Daten darzustellen und eine ganzheitliche Sicht auf jeden einzelnen Kunden bereitzustellen.

Weitere Informationen zum Arbeiten mit [!DNL Profile] finden Sie in der [Übersicht über das Echtzeit-Kundenprofil](../../profile/home.md).

## Zuordnen von Datendateien zu XDM-Schemata {#mapping-datafiles}

Alle Datendateien, die in Experience Platform aufgenommen werden, müssen der Struktur eines XDM-Schemas entsprechen. Weitere Informationen zum Formatieren von Datendateien mit XDM-Hierarchien (einschließlich Beispieldateien) finden Sie im Dokument zu [Beispiel-ETL-Transformationen](../../etl/transformations.md). Allgemeine Informationen zur Aufnahme von Datendateien in Experience Platform finden Sie unter [Batch-Erfassung – Übersicht](../../ingestion/batch-ingestion/overview.md).

## Schemata für externe Zielgruppen

Wenn Sie Zielgruppen aus externen Systemen in Platform integrieren, müssen Sie die folgenden Komponenten verwenden, um sie in Ihren Schemas zu erfassen:

* [[!UICONTROL Segmentdefinition] class](../classes/segment-definition.md): Verwenden Sie diese Standardklasse, um Schlüsselattribute einer externen Segmentdefinition zu erfassen.
* [[!UICONTROL Segmentzugehörigkeitsdetails] Feldergruppe](../field-groups/profile/segmentation.md): Fügen Sie diese Feldergruppe Ihrem Schema [!UICONTROL XDM Individual Profile] hinzu, um Kundenprofile bestimmten Zielgruppen zuzuordnen.

## Nächste Schritte

Nachdem Sie nun die Grundlagen der Schemakomposition kennen, können Sie mit der Erforschung und Erstellung von Schemas mit dem [!DNL Schema Registry] beginnen.

Informationen zum Überprüfen der Struktur der beiden Core-XDM-Klassen und der häufig verwendeten kompatiblen Feldergruppen finden Sie in der folgenden Referenzdokumentation:

* [[!DNL XDM Individual Profile]](../classes/individual-profile.md)
* [[!DNL XDM ExperienceEvent]](../classes/experienceevent.md)

Der [!DNL Schema Registry] wird verwendet, um auf den [!DNL Schema Library] in Adobe Experience Platform zuzugreifen. Er bietet eine Benutzeroberfläche und eine RESTful-API, über die alle verfügbaren Bibliotheksressourcen zugänglich sind. Der [!DNL Schema Library] enthält Branchenressourcen, die von Adobe definiert werden, von Experience Platform-Partnern definierte Vendor-Ressourcen sowie Klassen, Feldergruppen, Datentypen und Schemata, die von Mitgliedern Ihres Unternehmens zusammengestellt wurden.

Um mit dem Erstellen von Schemas über die Benutzeroberfläche zu beginnen, folgen Sie dem [Schema-Editor-Tutorial](../tutorials/create-schema-ui.md), um das Schema „Loyalty Members“ zu erstellen, das in diesem Dokument erwähnt wird.

Um mit der Verwendung der [!DNL Schema Registry] -API zu beginnen, lesen Sie zunächst das [Entwicklerhandbuch zur Schema Registry-API](../api/getting-started.md) . Nachdem Sie das Entwicklerhandbuch gelesen haben, führen Sie die Schritte aus, die im Tutorial zum [Erstellen eines Schemas mit der Schema Registry-API](../tutorials/create-schema-api.md) beschrieben werden.

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

**pros**:

* Objekte eignen sich am besten, wenn Sie eine logische Gruppierung bestimmter Felder erstellen möchten.
* Objekte ordnen das Schema strukturierter an.
* Objekte helfen indirekt bei der Erstellung einer guten Menüstruktur in der Benutzeroberfläche von Segment Builder. Die gruppierten Felder innerhalb des Schemas werden direkt in der Ordnerstruktur angezeigt, die in der Benutzeroberfläche von Segment Builder bereitgestellt wird.

**cons**:

* Felder werden verschachtelter.
* Bei Verwendung von [Adobe Experience Platform Query Service](../../query-service/home.md) müssen für Abfragefelder, die in Objekten verschachtelt sind, längere Referenzzeichenfolgen bereitgestellt werden.

#### Freiformfelder

Die Vor- und Nachteile der Verwendung von Freiformfeldern gegenüber Objekten sind unten aufgeführt.

**pros**:

* Freiformfelder werden direkt unter dem Stammobjekt des Schemas (`_tenantId`) erstellt, was die Sichtbarkeit erhöht.
* Bei Verwendung von Query Service sind Referenzzeichenfolgen für Freiformfelder in der Regel kürzer.

**cons**:

* Der Speicherort von Freiformfeldern im Schema ist Ad-hoc, d. h. sie werden im Schema Editor in alphabetischer Reihenfolge angezeigt. Dies kann dazu führen, dass Schemas weniger strukturiert sind und ähnliche Freiformfelder je nach Namen weit voneinander getrennt werden.
