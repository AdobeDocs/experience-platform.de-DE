---
keywords: Experience Platform;Startseite;beliebte Themen;schema;Schema;Aufzählung;Mixin;Feldergruppe;Feldergruppen;Mixins;Datentyp;Datentypen;Datentypen;Datentyp;primäre Identität;primäre Identität;XDM-Individualprofil;XDM-Felder;Aufzählungsdatentyp;Erlebnisereignis;XDM ExperienceEvent;experienceEvent;experienceEvent;XDM ExperienceEvent;Schema-Design;Klasse;Klasse;Klassen;Klassen;Datentyp;Datentyp;Datentyp;Datentyp;Schemata;Schemata;identityMap;identityMap;Identitätszuordnung;Schema-Design;Map;Map;Map;Map;Vereinigungsschema;Vereinigung
solution: Experience Platform
title: Grundlagen der Schemakomposition
description: Erfahren Sie mehr über Experience-Datenmodell-Schemas (XDM) und die Bausteine, Prinzipien und Best Practices zum Erstellen von Schemas in Adobe Experience Platform.
exl-id: d449eb01-bc60-4f5e-8d6f-ab4617878f7e
source-git-commit: dcb6770d739d0da5cfa339584a769f5311a8c7e1
workflow-type: tm+mt
source-wordcount: '4350'
ht-degree: 25%

---

# Grundlagen der Schema-Komposition

Erfahren Sie mehr über Experience-Datenmodell-Schemas (XDM) und die Bausteine, Prinzipien und Best Practices zum Erstellen von Schemas in Adobe Experience Platform. Allgemeine Informationen zu XDM und seiner Verwendung in [!DNL Experience Platform] finden Sie in der [XDM-Systemübersicht](../home.md).

## Verstehen von Schemata {#understanding-schemas}

Ein Schema ist ein Regelsatz, der die Datenstruktur und das Datenformat darstellt und überprüft. Auf hoher Ebene bieten Schemata eine abstrakte Definition eines realen Objekts (z. B. einer Person) und legen dar, welche Daten in jeder Instanz dieses Objekts enthalten sein sollen (z. B. Vorname, Nachname, Geburtsdatum usw.).

Zusätzlich zur Beschreibung der Datenstruktur wenden Schemata Einschränkungen und Erwartungen an Daten an, damit diese bei ihren Bewegungen zwischen den Systemen validiert werden können. Diese Standarddefinitionen ermöglichen eine konsistente Interpretation der Daten, unabhängig von ihrer Herkunft, und machen eine anwendungsübergreifende Übersetzung überflüssig.

Experience Platform erhält diese semantische Normalisierung mithilfe von Schemata aufrecht. Schemata sind die Standardmethode zur Beschreibung von Daten in Experience Platform. Dadurch können alle Daten, die mit Schemata konform sind, innerhalb einer Organisation ohne Konflikte wiederverwendet oder sogar von mehreren Organisationen gemeinsam genutzt werden.

XDM-Schemata eignen sich ideal zum Speichern großer Mengen komplexer Daten in einem eigenständigen Format. Weitere Informationen dazu, wie XDM dies [, finden Sie in den Abschnitten ](#embedded)Eingebettete Objekte[ und Big Data](#big-data) im Anhang zu diesem Dokument.

### Schema-basierte Workflows in Experience Platform {#schema-based-workflows}

Die Standardisierung ist ein Schlüsselkonzept der Experience Platform. Das von Adobe unterstützte XDM-System ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schemata für das Customer Experience Management zu definieren.

Die Infrastruktur [!DNL XDM System], auf der Experience Platform basiert, vereinfacht schemabasierte Workflows und umfasst die [!DNL Schema Registry], [!DNL Schema Editor], Schemadateien und Dienstnutzungsmuster. Weitere Informationen finden Sie in der [XDM-Systemübersicht](../home.md).

Die Verwendung von Schemata in Experience Platform bietet mehrere wichtige Vorteile. Erstens ermöglichen Schemata eine bessere Data Governance und Datenminimierung, was besonders bei Datenschutzbestimmungen wichtig ist. Zweitens ermöglicht die Erstellung von Schemata mit den Standardkomponenten von Adobe vordefinierte Einblicke und die Verwendung von KI-/ML-Services mit minimalen Anpassungen. Schließlich bieten Schemata eine Infrastruktur für Einblicke in die gemeinsame Datennutzung und effiziente Orchestrierung.

## Planen Ihres Schemas {#planning}

Der erste Schritt beim Erstellen eines Schemas besteht darin, das Konzept oder das Objekt der realen Welt zu bestimmen, das Sie im Schema erfassen möchten. Sobald Sie das Konzept, das Sie zu beschreiben versuchen, identifiziert haben, beginnen Sie mit der Planung Ihres Schemas, indem Sie über Dinge wie den Datentyp, potenzielle Identitätsfelder und die zukünftige Entwicklung des Schemas nachdenken.

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

Schemata definieren die Datenstruktur, die in Experience Platform aufgenommen werden. Diese Daten ermöglichen mehrere Services innerhalb der Plattform und tragen dazu bei, eine einheitliche Ansicht jedes Einzelnen zu erstellen. Überlegen Sie daher beim Entwerfen von Schemata sorgfältig, welche Felder als Identitäten markiert werden sollen. Diese steuern, wie Profile über Datensätze hinweg zugeordnet werden.

Um diesen Prozess zu unterstützen, können Schlüsselfelder in Ihren Schemata als Identitäten markiert werden. Bei der Datenaufnahme werden die Daten in diesen Feldern für diese Person in das [!UICONTROL Identitätsdiagramm] eingefügt. Auf die Diagrammdaten können dann [[!DNL Real-Time Customer Profile]](../../profile/home.md) und andere Experience Platform-Services zugreifen, um eine zusammengefügte Ansicht jedes einzelnen Kunden zu erhalten.

Zu den Feldern, die häufig als &quot;[!UICONTROL Identität] gekennzeichnet sind, gehören: E-Mail-Adresse, Telefonnummer, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=de), CRM-ID oder andere eindeutige ID-Felder. Erwägen Sie alle eindeutigen Kennungen, die für Ihr Unternehmen spezifisch sind, da sie auch gute &quot;[!UICONTROL &quot;-] sein können.

Weitere Informationen dazu, wie Sie Ihren Kunden mit Identitätsinformationen digitale Erlebnisse bereitstellen können, finden Sie unter [Identity Service - Übersicht](../../identity-service/home.md). Tipps zur Verwendung von Identitäten beim Erstellen [ Schemas finden Sie im Dokument Best Practices für die Datenmodellierung ](./best-practices.md#data-validation-fields).

Es gibt zwei Möglichkeiten, Identitätsdaten an Experience Platform zu senden:

1. Hinzufügen von Identitätsdeskriptoren zu einzelnen Feldern, entweder über die [Benutzeroberfläche des Schema-Editors](../ui/fields/identity.md) oder mithilfe der [Schema Registry-API](../api/descriptors.md#create)
2. Verwenden eines [`identityMap` Felds](#identityMap)

#### `identityMap` {#identityMap}

`identityMap` ist ein Feld vom Typ Zuordnung , das die verschiedenen Identitätswerte einer Person zusammen mit den zugehörigen Namespaces beschreibt. Dieses Feld kann verwendet werden, um Identitätsinformationen für Ihre Schemata bereitzustellen, anstatt Identitätswerte innerhalb der Struktur des Schemas selbst zu definieren.

Der Hauptnachteil der Verwendung von `identityMap` besteht darin, dass Identitätswerte verschachtelt sind und es schwieriger sein kann, mit ihnen in Tools zu arbeiten, die Identitätsfelder der obersten Ebene erwarten, z. B. Segment Builder oder einige Integrationen von Drittanbietern.

>[!NOTE]
>
>Ein Schema, das `identityMap` verwendet, kann in einer Beziehung als Quellschema, aber nicht als Referenzschema verwendet werden. Dies liegt daran, dass alle Referenzschemata eine sichtbare Identität aufweisen müssen, die in einem Referenzfeld innerhalb des Quellschemas zugeordnet werden kann. Weitere Informationen zu den Anforderungen von Quell[ und Referenzschemas finden ](../tutorials/relationship-ui.md) im Handbuch zur Benutzeroberfläche unter Beziehungen .

Identitätszuordnungen können jedoch nützlich sein, wenn es eine variable Anzahl von Identitäten für ein Schema gibt oder Sie Daten aus Quellen einbringen, die Identitäten speichern (z. B. [!DNL Airship] oder Adobe Audience Manager). Darüber hinaus sind Identitätszuordnungen erforderlich, wenn Sie die [Adobe Experience Platform Mobile SDK verwenden](https://developer.adobe.com/client-sdks/home/).

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

Wie im obigen Beispiel gezeigt, stellt jeder Schlüssel im `identityMap`-Objekt einen Identity-Namespace dar. Der Wert für jeden Schlüssel ist ein Array von Objekten, das die Identitätswerte (`id`) für den jeweiligen Namespace darstellt. In der [!DNL Identity Service] finden Sie eine [Liste der Standard-Identity-Namespaces](../../identity-service/troubleshooting-guide.md#standard-namespaces) die von Adobe-Programmen erkannt wird.

>[!NOTE]
>
>Für jeden Identitätswert kann auch ein boolescher Wert angegeben werden, der angibt, ob der Wert eine primäre Identität (`primary`) ist. Sie müssen nur primäre Identitäten für Schemata festlegen, die in [!DNL Real-Time Customer Profile] verwendet werden sollen. Weitere Informationen finden Sie im Abschnitt [Vereinigungsschemata](#union) .

### Prinzipien der Schemaentwicklung {#evolution}

In dem Maße, wie sich die Art der digitalen Erfahrungen weiterentwickelt, müssen sich auch die Schemata, die zu ihrer Darstellung verwendet werden, weiterentwickeln. Ein gut entworfenes Schema ist daher in der Lage, sich bei Bedarf anzupassen und weiterzuentwickeln, ohne destruktive Änderungen an früheren Versionen des Schemas zu verursachen.

Da die Beibehaltung der Abwärtskompatibilität für die Schemaentwicklung von entscheidender Bedeutung ist, erzwingt Experience Platform ein rein additives Versionierungsprinzip. Dieses Prinzip stellt sicher, dass alle Änderungen am Schema nur zu zerstörungsfreien Aktualisierungen und Änderungen führen. Mit anderen Worten: **brechende Änderungen werden nicht unterstützt.**

>[!NOTE]
>
>Sie können eine grundlegende Änderung an einem Schema nur vornehmen, wenn es noch nicht zur Aufnahme von Daten in Experience Platform verwendet wurde und noch nicht für die Verwendung im Echtzeit-Kundenprofil aktiviert wurde. Sobald das Schema jedoch in [!DNL Experience Platform] verwendet wurde, muss es der additiven Versionierungsrichtlinie entsprechen.

In der folgenden Tabelle ist aufgeführt, welche Änderungen beim Bearbeiten von Schemata, Feldergruppen und Datentypen unterstützt werden:

| Unterstützte Änderungen | Brechende Änderungen (nicht unterstützt) |
| --- | --- |
| <ul><li>Hinzufügen neuer Felder zur Ressource</li><li>Optionales Festlegen eines erforderlichen Felds</li><li>Einführung neuer Pflichtfelder*</li><li>Anzeigename und Beschreibung der Ressource ändern</li><li>Aktivieren des Schemas für die Profilteilnahme</li></ul> | <ul><li>Entfernen zuvor definierter Felder</li><li>Umbenennen oder Neudefinieren vorhandener Felder</li><li>Entfernen oder Eingrenzen zuvor unterstützter Feldwerte</li><li>Verschieben vorhandener Felder an eine andere Position im Baum</li><li>Löschen des Schemas</li><li>Deaktivieren des Schemas aus der Profilteilnahme</li><li>Ändern des Felds für die primäre Identität in einem Schema, das für das Profil aktiviert ist und Daten aufgenommen hat</li></ul> |

\**Im folgenden Abschnitt finden Sie wichtige Überlegungen zum [Festlegen neuer Pflichtfelder](#post-ingestion-required-fields).*

### Erforderliche Felder

Einzelne Schemafelder können [als erforderlich markiert) werden](../ui/fields/required.md) was bedeutet, dass alle aufgenommenen Datensätze Daten in diesen Feldern enthalten müssen, damit die Validierung erfolgreich ist. Wenn Sie beispielsweise das Feld für die primäre Identität eines Schemas nach Bedarf festlegen, kann sichergestellt werden, dass alle aufgenommenen Datensätze beim Echtzeit-Kundenprofil berücksichtigt werden. Ebenso wird durch die Festlegung eines Zeitstempelfelds nach Bedarf sichergestellt, dass alle Zeitreihenereignisse chronologisch beibehalten werden.

>[!IMPORTANT]
>
>Unabhängig davon, ob ein Schemafeld erforderlich ist oder nicht, akzeptiert Experience Platform für kein aufgenommenes Feld `null` oder leere Werte. Wenn in einem Datensatz oder Ereignis kein Wert für ein bestimmtes Feld vorhanden ist, sollte der Schlüssel für dieses Feld aus der Aufnahme-Payload ausgeschlossen werden.

#### Festlegen von Feldern nach Bedarf nach der Aufnahme {#post-ingestion-required-fields}

Wenn ein Feld zur Aufnahme von Daten verwendet wurde und ursprünglich nicht wie erforderlich festgelegt wurde, kann dieses Feld für einige Datensätze einen Nullwert aufweisen. Wenn Sie dieses Feld nach der Aufnahme als erforderlich festlegen, müssen alle zukünftigen Datensätze einen Wert für dieses Feld enthalten, auch wenn historische Datensätze null sein können.

Beachten Sie beim Festlegen eines zuvor optionalen Felds nach Bedarf Folgendes:

1. Wenn Sie historische Daten abfragen und die Ergebnisse in einen neuen Datensatz schreiben, schlagen einige Zeilen fehl, da sie Nullwerte für das erforderliche Feld enthalten.
1. Wenn das Feld am [Echtzeit-Kundenprofil](../../profile/home.md) beteiligt ist und Sie Daten exportieren, bevor Sie sie nach Bedarf festlegen, kann es für einige Profile null sein.
1. Sie können die Schema Registry-API verwenden, um ein Änderungsprotokoll mit Zeitstempel für alle XDM-Ressourcen in Experience Platform anzuzeigen, einschließlich neuer erforderlicher Felder. Weitere Informationen finden Sie im Handbuch zum [Endpunkt ](../api/audit-log.md)Administratorprotokoll“.

### Schemata und Datenerfassung

Um Daten in die Experience Platform aufnehmen zu können, muss zunächst ein Datensatz erstellt werden. Datensätze sind die Bausteine für die Datenumwandlung und das Tracking für [[!DNL Catalog Service]](../../catalog/home.md) und stellen im Allgemeinen Tabellen oder Dateien dar, die aufgenommene Daten enthalten. Alle Datensätze basieren auf vorhandenen XDM-Schemata, die Einschränkungen dafür enthalten, was die aufgenommenen Daten enthalten und wie sie strukturiert sein sollten. Weitere Informationen hierzu finden Sie in der Übersicht über die [Datenerfassung in Adobe Experience Platform](../../ingestion/home.md).

## Bausteine eines Schemas {#schema-building-blocks}

Die Experience Platform verwendet einen Kompositionsansatz, bei dem Standardbausteine kombiniert werden, um Schemata zu erstellen. Dieser Ansatz fördert die Wiederverwendbarkeit vorhandener Komponenten und treibt die Standardisierung in der gesamten Branche voran, um Anbieterschemas und Komponenten in [!DNL Experience Platform] zu unterstützen.

Schemata werden nach folgender Formel zusammengestellt:

**Klasse + Schemafeldgruppe&amp;ast; = XDM-Schema**

&amp;map;ast;Ein Schema besteht aus einer Klasse und keiner oder mehreren Schemafeldgruppen. Dies bedeutet, dass Sie ein Datensatzschema erstellen können, ohne Feldergruppen zu verwenden.

### Klasse {#class}

>[!CONTEXTUALHELP]
>id="platform_schemas_class"
>title="Klasse"
>abstract="Jedes Schema basiert auf einer einzelnen Klasse. Die Klasse definiert das Verhalten des Schemas und die allgemeinen Eigenschaften, die alle Schemata enthalten müssen, die auf dieser Klasse basieren. Weitere Informationen dazu, wie Klassen bei der Schemakomposition genutzt werden, finden Sie in der Dokumentation."

>[!CONTEXTUALHELP]
>id="platform_schemas_class_industries"
>title="Branchentyp"
>abstract="Wenn Sie eine für Ihr Unternehmen relevante Branche auswählen, kann das Modell für maschinelles Lernen eine bessere Organisation der Daten ermöglichen, indem die Quellfelder genauer den Standardfeldgruppen zugeordnet werden, die den Branchenstandards entsprechen. Dadurch wird sichergestellt, dass die Datenintegration auf Ihre branchenspezifischen Anforderungen zugeschnitten ist, was zu präziseren und relevanteren Datenerkenntnissen führt."

Das Erstellen eines Schemas beginnt mit dem Zuweisen einer Klasse. Klassen definieren die Verhaltensaspekte der Daten, die das Schema enthalten soll (Datensatz oder Zeitreihen). Darüber hinaus beschreiben Klassen die kleinste Anzahl gemeinsamer Eigenschaften, die alle Schemata, die auf dieser Klasse basieren, beinhalten müssen, und bieten eine Möglichkeit zum Zusammenführen mehrerer kompatibler Datensätze.

Die Klasse eines Schemas bestimmt, welche Feldergruppen für die Verwendung in diesem Schema geeignet sind. Weitere Informationen hierzu finden Sie im [ Abschnitt ](#field-group).

Adobe bietet mehrere standardmäßige XDM-Klassen („Kern„). Zwei dieser Klassen, [!DNL XDM Individual Profile] und [!DNL XDM ExperienceEvent], sind für fast alle nachgelagerten Experience Platform-Prozesse erforderlich. Zusätzlich zu diesen Kernklassen können Sie auch eigene benutzerdefinierte Klassen erstellen, um spezifischere Anwendungsfälle für Ihre Organisation zu beschreiben. Benutzerdefinierte Klassen werden von einem Unternehmen definiert, wenn keine von Adobe definierten Kernklassen verfügbar sind, um einen eindeutigen Anwendungsfall zu beschreiben.

Der folgende Screenshot zeigt, wie Klassen in der Experience Platform-Benutzeroberfläche dargestellt werden. Da das angezeigte Beispielschema keine Feldergruppen enthält, werden alle angezeigten Felder von der Klasse des Schemas bereitgestellt ([!UICONTROL XDM Individual Profile]).

![Das [!UICONTROL XDM Individual Profile] im Schema-Editor.](../images/schema-composition/class.png)

Die aktuellste Liste der verfügbaren Standard-XDM-Klassen finden Sie im [offiziellen XDM-Repository](https://github.com/adobe/xdm/tree/master/components/classes). Alternativ können Sie auch das Handbuch unter [Erkunden von XDM-Komponenten“ lesen](../ui/explore.md) wenn Sie Ressourcen lieber in der Benutzeroberfläche anzeigen möchten.

### Feldergruppe {#field-group}

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup"
>title="Feldergruppe"
>abstract="Feldergruppen sind wiederverwendbare Komponenten, mit denen Sie Schemata durch zusätzliche Attribute erweitern können. Die meisten Feldergruppen sind nur mit bestimmten Klassen kompatibel. Sie können die von Adobe definierten Standardfeldergruppen verwenden oder eigene benutzerdefinierte Feldergruppen manuell erstellen. Weitere Informationen zur Verwendung von Feldergruppen bei der Schemakomposition finden Sie in der Dokumentation."

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup_requiredFieldgroup"
>title="Erforderliche Feldergruppe"
>abstract="Diese Feldergruppe ist für die verwendete Quelle erforderlich. Aus diesem Grund können Sie sie nicht aus Ihrem Schema löschen."

Eine Feldergruppe ist eine wiederverwendbare Komponente, die ein oder mehrere Felder definiert, die bestimmte Funktionen wie persönliche Details, Hotelvoreinstellungen oder Adresse implementieren. Feldergruppen sind als Teil eines Schemas vorgesehen, das eine kompatible Klasse implementiert.

Feldergruppen definieren basierend auf dem Verhalten der Daten, die sie darstellen (Datensatz oder Zeitreihe), mit welcher Klasse oder welchen Klassen sie kompatibel sind. Das bedeutet, dass nicht alle Feldergruppen für die Verwendung mit allen Klassen verfügbar sind.

Experience Platform umfasst viele standardmäßige Adobe-Feldergruppen, ermöglicht es aber auch Anbietern, Feldergruppen für ihre Benutzenden und einzelnen Benutzenden, Feldergruppen für ihre eigenen spezifischen Konzepte zu definieren.

Um beispielsweise Details wie &quot;[!UICONTROL Vorname] und &quot;[!UICONTROL Privatadresse] für Ihr Schema &quot;[!UICONTROL Mitglieder des Treueprogramms] zu erfassen, können Sie Standardfeldgruppen verwenden, die diese allgemeinen Konzepte definieren. Konzepte, die spezifischer für Ihr Unternehmen sind (z. B. Details zu benutzerdefinierten Treueprogrammen oder Produktattributen) und möglicherweise nicht von Standardfeldgruppen abgedeckt werden. In diesem Fall müssen Sie Ihre eigene Feldergruppe definieren, um diese Informationen zu erfassen.

>[!NOTE]
>
>Es wird dringend empfohlen, in Ihren Schemata nach Möglichkeit Standardfeldgruppen zu verwenden, da diese Felder von Experience Platform-Services implizit verstanden werden und eine größere Konsistenz bei der Verwendung über [!DNL Experience Platform] hinweg gewährleisten.
>
>Felder, die von Standardkomponenten bereitgestellt werden (z. B. „Vorname“ und „E-Mail-Adresse„), enthalten über grundlegende skalare Feldtypen hinaus hinzugefügte Konnotationen. Sie weisen [!DNL Experience Platform] darauf hin, dass sich alle Felder mit demselben Datentyp gleich verhalten. Dieses Verhalten ist konsistent, unabhängig davon, woher die Daten kommen oder in welchem [!DNL Experience Platform]-Service die Daten verwendet werden.

Denken Sie daran, dass Schemata aus „null oder mehr“ Feldergruppen bestehen. Dies bedeutet, dass Sie ein gültiges Schema erstellen können, ohne überhaupt Feldergruppen zu verwenden.

Der folgende Screenshot zeigt, wie Feldergruppen in der Experience Platform-Benutzeroberfläche dargestellt werden. Eine einzelne Feldergruppe ([!UICONTROL Demografische Details]) wird in diesem Beispiel einem Schema hinzugefügt, das eine Gruppierung von Feldern zur Schemastruktur bereitstellt.

![Der Schema-Editor mit der [!UICONTROL Demografische Details] Feldergruppe, die in einem Beispielschema hervorgehoben ist.](../images/schema-composition/field-group.png)

Die aktuellste Liste der verfügbaren Standard-XDM-Feldergruppen finden Sie im [offiziellen XDM-Repository](https://github.com/adobe/xdm/tree/master/components/fieldgroups). Alternativ können Sie auch das Handbuch unter [Erkunden von XDM-Komponenten“ lesen](../ui/explore.md) wenn Sie Ressourcen lieber in der Benutzeroberfläche anzeigen möchten.

>[!NOTE]
>
> Standard-XDM-Feldergruppen entwickeln sich immer weiter, und einige Feldergruppen werden nicht mehr unterstützt. Die aktuellste Liste veralteter Feldergruppen finden Sie im Abschnitt [veraltete Feldergruppen“ ](https://github.com/adobe/xdm/tree/master/components/fieldgroups/deprecated) offiziellen XDM-Repository.

### Datentyp {#data-type}

Datentypen werden als Referenzfeldtypen in Klassen oder Schemata auf die gleiche Weise verwendet wie grundlegende literale Felder. Der Hauptunterschied besteht darin, dass Datentypen mehrere Unterfelder auf die gleiche Weise definieren können wie Feldergruppen. Der wesentliche Unterschied zwischen ihnen besteht darin, dass Datentypen überall in einem Schema enthalten sein können, indem sie als „Datentyp“ eines Felds hinzugefügt werden. Während Feldgruppen nur mit bestimmten Klassen kompatibel sind, können Datentypen in jeder übergeordneten Klasse oder Feldergruppe enthalten sein.

>[!NOTE]
>
>Wenn ein Feld als spezifischer Datentyp definiert ist, können Sie dasselbe Feld mit einem anderen Datentyp in einem anderen Schema nicht erstellen. Diese Einschränkung gilt für den Mandanten Ihrer Organisation.

Experience Platform bietet eine Reihe allgemeiner Datentypen als Teil der [!DNL Schema Registry], um die Verwendung von Standardmustern zur Beschreibung allgemeiner Datenstrukturen zu unterstützen. Dies wird in den [Tutorials zur Schemaregistrierung](../tutorials/create-schema-api.md) ausführlicher erläutert und wird klarer, wenn Sie die Schritte zum Definieren von Datentypen durchlaufen.

Der folgende Screenshot zeigt, wie Datentypen in der Experience Platform-Benutzeroberfläche dargestellt werden. Eines der Felder, die von der Feldergruppe [!UICONTROL Demografische Details] bereitgestellt werden, verwendet den Datentyp [!UICONTROL Objekt], wie durch den Text angegeben, der auf das Pipe-Zeichen (`|`) neben dem Feldnamen folgt. Dieser Datentyp bietet mehrere Unterfelder, die sich auf den Namen einer einzelnen Person beziehen - ein Konstrukt, das für andere Felder wiederverwendet werden kann, in denen der Name einer Person erfasst werden muss.

![Ein Diagramm im Schema-Editor für eine einzelne Person mit hervorgehobenem vollständigen Namensobjekt und hervorgehobenen Attributen.](../images/schema-composition/data-type.png)

Die aktuellste Liste der verfügbaren Standard-XDM-Datentypen finden Sie im [offiziellen XDM-Repository](https://github.com/adobe/xdm/tree/master/components/datatypes). Alternativ können Sie auch das Handbuch unter [Erkunden von XDM-Komponenten“ lesen](../ui/explore.md) wenn Sie Ressourcen lieber in der Benutzeroberfläche anzeigen möchten.

>[!NOTE]
>
> Standard-XDM-Datentypen entwickeln sich immer weiter, und einige Datentypen werden nicht mehr unterstützt. Die aktuellste Liste veralteter Datentypen finden Sie im Abschnitt [veraltete Datentypen](https://github.com/adobe/xdm/tree/master/components/datatypes/deprecated) im offiziellen XDM-Repository.

### Feld {#field}

Ein Feld ist der grundlegendste Baustein eines Schemas. Felder bieten Einschränkungen hinsichtlich des Datentyps, den sie enthalten können, indem sie einen bestimmten Datentyp definieren. Diese grundlegenden Datentypen definieren ein einzelnes Feld, während die [Datentypen](#data-type) zuvor erwähnten es Ihnen ermöglichen, mehrere Unterfelder zu definieren und dieselbe Struktur mit mehreren Feldern in verschiedenen Schemata wiederzuverwenden. Zusätzlich zur Definition des „Datentyps“ eines Feldes als einen der in der Registrierung definierten Datentypen unterstützt die Experience Platform also grundlegende Skalartypen wie:

* Zeichenfolge
* Ganzzahl
* Double
* Boolesch
* Array
* Objekt

>[!TIP]
>
>Siehe [Anhang](#objects-v-freeform) für Informationen zu den Vor- und Nachteilen der Verwendung von Freiformfeldern gegenüber Feldern vom Typ „Objekt“.

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
>Der Feldtyp „Zuordnung“ ermöglicht Schlüssel-Wert-Paardaten, einschließlich mehrerer Werte für einen einzelnen Schlüssel. Zuordnungen finden Sie in standardmäßigen XDM-Klassen und -Feldergruppen. Sie können aber auch benutzerdefinierte Zuordnungen definieren. Weitere Informationen finden Sie im API[Tutorial zum Definieren benutzerdefinierter ](../tutorials/custom-fields-api.md#custom-maps) oder im Handbuch [Definieren von Zuordnungsfeldern in ](../ui/fields/map.md) Benutzeroberfläche“.

## Kompositionsbeispiel {#composition-example}

Schemata werden mithilfe eines Kompositionsmodells erstellt und stellen das Format und die Struktur von Daten dar, die in [!DNL Experience Platform] aufgenommen werden sollen. Wie bereits erwähnt, bestehen diese Schemata aus einer Klasse und keiner oder mehreren Feldergruppen, die mit dieser Klasse kompatibel sind.

Ein Schema, das Käufe in einem Einzelhandelsgeschäft beschreibt, kann beispielsweise „Store[!UICONTROL Transaktionen“ ]. Das Schema implementiert die [!DNL XDM ExperienceEvent]-Klasse in Kombination mit der standardmäßigen [!UICONTROL Commerce]-Feldergruppe und einer benutzerdefinierten Feldergruppe [!UICONTROL Produktinfo].

Ein weiteres Schema, das den Website-Traffic verfolgt, wird möglicherweise als &quot;[!UICONTROL &quot; ]. Sie implementiert auch die [!DNL XDM ExperienceEvent]-Klasse, kombiniert aber dieses Mal die standardmäßige [!UICONTROL Web]-Feldergruppe.

Das folgende Diagramm zeigt diese Schemata und die von den einzelnen Feldergruppen bereitgestellten Felder. Sie enthält außerdem zwei Schemata, die auf der [!DNL XDM Individual Profile]-Klasse basieren, einschließlich des Schemas [!UICONTROL Mitglieder des Treueprogramms], das zuvor in diesem Handbuch erwähnt wurde.

![Flussdiagramm mit vier Schemata und den Feldergruppen, die zu ihnen beitragen.](../images/schema-composition/composition.png)

### Union {#union}

Während Experience Platform es Ihnen ermöglicht, Schemata für bestimmte Anwendungsfälle zusammenzustellen, können Sie auch eine „Vereinigung“ von Schemata für einen bestimmten Klassentyp sehen. Das vorherige Diagramm zeigt zwei Schemas, die auf der XDM ExperienceEvent-Klasse basieren, und zwei Schemas, die auf [!DNL XDM Individual Profile] Klasse basieren. Die unten dargestellte Vereinigung aggregiert die Felder aller Schemata, die dieselbe Klasse aufweisen ([!DNL XDM ExperienceEvent] bzw. [!DNL XDM Individual Profile]).

![Ein Vereinigungsschema-Flussdiagramm, das die Felder darstellt, aus denen sie bestehen.](../images/schema-composition/union.png)

Wenn Sie ein Schema für die Verwendung mit [!DNL Real-Time Customer Profile] aktivieren, wird es in die Vereinigung für diesen Klassentyp aufgenommen. [!DNL Profile] bietet zuverlässige, zentralisierte Profile von Kundenattributen und eine Darstellung jedes Ereignisses mit Zeitstempel, das ein Kunde über eines der in [!DNL Experience Platform] integrierten Systeme hatte. [!DNL Profile] verwendet die Vereinigungsansicht, um diese Daten darzustellen und eine ganzheitliche Ansicht jedes einzelnen Kunden bereitzustellen.

Weitere Informationen zum Arbeiten mit [!DNL Profile] finden Sie in der [Übersicht über das Echtzeit-Kundenprofil](../../profile/home.md).

## Zuordnen von Datendateien zu XDM-Schemata {#mapping-datafiles}

Alle Datendateien, die in Experience Platform aufgenommen werden, müssen der Struktur eines XDM-Schemas entsprechen. Weitere Informationen zum Formatieren von Datendateien mit XDM-Hierarchien (einschließlich Beispieldateien) finden Sie im Dokument zu [Beispiel-ETL-Transformationen](../../etl/transformations.md). Allgemeine Informationen zur Aufnahme von Datendateien in Experience Platform finden Sie unter [Batch-Erfassung – Übersicht](../../ingestion/batch-ingestion/overview.md).

## Schemata für externe Zielgruppen

Wenn Sie Zielgruppen aus externen Systemen in Experience Platform importieren möchten, müssen Sie die folgenden Komponenten verwenden, um sie in Ihren Schemata zu erfassen:

* [[!UICONTROL Segmentdefinition] Klasse](../classes/segment-definition.md): Verwenden Sie diese Standardklasse, um Schlüsselattribute einer externen Segmentdefinition zu erfassen.
* [[!UICONTROL Details zur Segmentzugehörigkeit] Feldergruppe](../field-groups/profile/segmentation.md): Fügen Sie diese Feldergruppe zu Ihrem Schema [!UICONTROL XDM Individual Profile] hinzu, um Kundenprofile mit bestimmten Zielgruppen zu verknüpfen.

## Nächste Schritte

Nachdem Sie nun die Grundlagen der Schemakomposition kennen, können Sie mit dem Erkunden und Erstellen von Schemas mit dem [!DNL Schema Registry] beginnen.

Die Struktur der beiden XDM-Kernklassen und ihrer häufig verwendeten kompatiblen Feldergruppen finden Sie in der folgenden Referenzdokumentation:

* [[!DNL XDM Individual Profile]](../classes/individual-profile.md)
* [[!DNL XDM ExperienceEvent]](../classes/experienceevent.md)

Die [!DNL Schema Registry] wird verwendet, um auf die [!DNL Schema Library] in Adobe Experience Platform zuzugreifen, und bietet eine Benutzeroberfläche und eine RESTful-API, über die alle verfügbaren Bibliotheksressourcen verfügbar sind. Die [!DNL Schema Library] enthält von Adobe definierte Branchenressourcen, von Experience Platform-Partnern definierte Anbieterressourcen sowie Klassen, Feldergruppen, Datentypen und Schemata, die von Mitgliedern Ihres Unternehmens erstellt wurden.

Um mit dem Erstellen von Schemas über die Benutzeroberfläche zu beginnen, folgen Sie dem [Schema-Editor-Tutorial](../tutorials/create-schema-ui.md), um das Schema „Loyalty Members“ zu erstellen, das in diesem Dokument erwähnt wird.

Um mit der Verwendung der [!DNL Schema Registry]-API zu beginnen, lesen Sie zunächst das [Entwicklerhandbuch zur Schema Registry-API](../api/getting-started.md). Nachdem Sie das Entwicklerhandbuch gelesen haben, führen Sie die Schritte aus, die im Tutorial zum [Erstellen eines Schemas mit der Schema Registry-API](../tutorials/create-schema-api.md) beschrieben werden.

## Anhang

Die folgenden Abschnitte enthalten zusätzliche Informationen zu den Prinzipien der Schemakomposition.

### Relationale Tabellen versus eingebettete Objekte {#embedded}

Bei der Arbeit mit relationalen Datenbanken bestehen die Best Practices darin, Daten zu normalisieren oder eine Entität in diskrete Teile zu zerlegen, die dann in mehreren Tabellen angezeigt werden. Um die Daten als Ganzes zu lesen oder die Entität zu aktualisieren, müssen Lese- und Schreibvorgänge über viele einzelne Tabellen hinweg mithilfe von JOIN durchgeführt werden.

Durch die Verwendung eingebetteter Objekte können XDM-Schemata komplexe Daten direkt darstellen und in eigenständigen Dokumenten mit hierarchischer Struktur speichern. Einer der Hauptvorteile dieser Struktur besteht darin, dass Sie die Daten abfragen können, ohne die Entität durch teure Joins zu mehreren denormalisierten Tabellen rekonstruieren zu müssen. Es gibt keine harten Einschränkungen bezüglich der möglichen Anzahl von Ebenen Ihrer Schemahierarchie.

### Schemata und Big Data {#big-data}

Moderne digitale Systeme generieren enorme Mengen von Verhaltenssignalen (Transaktionsdaten, Weblogs, Internet der Dinge, Anzeige usw.). Diese Big-Data-Daten bieten außergewöhnliche Möglichkeiten zur Optimierung von Erlebnissen, sind aber aufgrund der Größe und Vielfalt der Daten schwierig zu nutzen. Um Wert aus den Daten zu gewinnen, müssen ihre Struktur, ihr Format und ihre Definitionen standardisiert werden, damit sie konsistent und effizient verarbeitet werden können.

Schemata lösen dieses Problem, indem sie die Integration von Daten aus mehreren Quellen, die Standardisierung durch gemeinsame Strukturen und Definitionen und die lösungsübergreifende gemeinsame Nutzung ermöglichen. Auf diese Weise können nachfolgende Prozesse und Services alle Fragen beantworten, die in Bezug auf die Daten gestellt werden. Sie entfernt sich vom herkömmlichen Ansatz zur Datenmodellierung, bei dem alle Fragen, die im Zusammenhang mit den Daten gestellt werden müssen, im Voraus bekannt sind, und die Daten so modelliert werden, dass sie diesen Erwartungen entsprechen.

### Objekte versus Freiformfelder {#objects-v-freeform}

Beim Entwerfen Ihrer Schemata sind einige Schlüsselfaktoren zu berücksichtigen, wenn Sie Objekte anstelle von Freiformfeldern auswählen:

| Objekte | Freiformfelder |
| --- | --- |
| Erhöht die Verschachtelung | Weniger oder keine Verschachtelung |
| Erstellt logische Feldergruppierungen | Felder werden an Ad-hoc-Speicherorten platziert |

{style="table-layout:auto"}

#### Objekte

Die Vor- und Nachteile der Verwendung von -Objekten über Freiformfeldern sind unten aufgeführt.

**Vorteile**:

* Objekte eignen sich am besten für die Erstellung einer logischen Gruppierung bestimmter Felder.
* Objekte organisieren das Schema strukturierter.
* Objekte helfen indirekt bei der Erstellung einer guten Menüstruktur in der Segment Builder-Benutzeroberfläche. Die gruppierten Felder innerhalb des Schemas werden direkt in der Ordnerstruktur angezeigt, die in der Benutzeroberfläche von Segment Builder bereitgestellt wird.

**Nachteile**:

* Die Felder werden verschachtelter.
* Bei Verwendung von [Adobe Experience Platform Query Service](../../query-service/home.md) müssen für die Abfragefelder, die in -Objekten verschachtelt sind, längere Referenzzeichenfolgen bereitgestellt werden.

#### Freiformfelder

Die Vor- und Nachteile der Verwendung von Freiformfeldern über Objekten sind unten aufgeführt.

**Vorteile**:

* Freiformfelder werden direkt unter dem Stammobjekt des Schemas (`_tenantId`) erstellt, wodurch die Sichtbarkeit erhöht wird.
* Referenzzeichenfolgen für Freiformfelder sind bei Verwendung des Abfrage-Service in der Regel kürzer.

**Nachteile**:

* Die Position von Freiformfeldern innerhalb des Schemas ist ad hoc, d. h. sie werden im Schema-Editor in alphabetischer Reihenfolge angezeigt. Dadurch können Schemata weniger strukturiert sein und ähnliche Freiformfelder können je nach ihrem Namen weit voneinander getrennt sein.
