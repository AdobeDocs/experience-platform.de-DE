---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; Enum; Mixin; Feldergruppe; Feldergruppen; Feldergruppen; Mixins; Datentyp; Datentypen; Datentyp; Datentyp; primäre Identität; primäre Identität; XDM-individuelles Profil; XDM-Felder; Enum-Datentyp; Erlebnis-Ereignis; XDM Experience Event; XDM ExperienceEvent; ExperienceEvent; XDM ExperienceEvent; Schemadesign; Klasse; Klasse;Klassen;Datentyp;Datentyp;Datentyp;Datentyp;Datentyp;Schemas;Schemas;Identitätszuordnung;Identitätszuordnung;Identitätszuordnung;Schema-Design;Map;Map;Vereinigungsschema;Vereinigung
solution: Experience Platform
title: Grundlagen der Schemakomposition
topic-legacy: overview
description: Dieses Dokument bietet Ihnen eine Einführung in Experience-Datenmodell (XDM)-Schemas und die Bausteine, Grundsätze und Best Practices zum Erstellen von Schemas, die in Adobe Experience Platform verwendet werden sollen.
exl-id: d449eb01-bc60-4f5e-8d6f-ab4617878f7e
source-git-commit: 2bd7c12209a1944aa954ba4490bb0c57f2a5ea61
workflow-type: tm+mt
source-wordcount: '3684'
ht-degree: 30%

---

# Grundlagen der Schema-Komposition

Dieses Dokument bietet eine Einführung in [!DNL Experience Data Model] (XDM)-Schemas und die Bausteine, Grundsätze und Best Practices zum Erstellen von Schemas, die in Adobe Experience Platform verwendet werden sollen. Allgemeine Informationen zu XDM und dessen Verwendung in [!DNL Platform] finden Sie in der [XDM-Systemübersicht](../home.md).

## Verstehen von Schemas

Ein Schema ist ein Regelsatz, der die Datenstruktur und das Datenformat darstellt und überprüft. Auf hoher Ebene bieten Schemas eine abstrakte Definition eines realen Objekts (z. B. einer Person) und legen dar, welche Daten in jeder Instanz dieses Objekts enthalten sein sollen (z. B. Vorname, Nachname, Geburtsdatum usw.).

Zusätzlich zur Beschreibung der Datenstruktur wenden Schemas Einschränkungen und Erwartungen an Daten an, damit diese bei ihren Bewegungen zwischen den Systemen validiert werden können. Diese Standarddefinitionen ermöglichen eine konsistente Interpretation der Daten, unabhängig von ihrer Herkunft, und machen eine anwendungsübergreifende Übersetzung überflüssig.

[!DNL Experience Platform] behält diese semantische Normalisierung bei, indem Schemas verwendet werden. Schemas sind die Standardmethode zur Beschreibung von Daten in [!DNL Experience Platform], sodass alle Daten, die Schemas entsprechen, in einer Organisation ohne Konflikte wiederverwendet oder sogar von mehreren Organisationen gemeinsam genutzt werden können.

XDM-Schemas eignen sich ideal zum Speichern großer Mengen komplexer Daten in einem eigenständigen Format. Weitere Informationen dazu, wie XDM dies erreicht, finden Sie in den Abschnitten zu [eingebettete Objekte](#embedded) und [Big Data](#big-data) im Anhang zu diesem Dokument.

### Schemabasierte Workflows in [!DNL Experience Platform]

Die Standardisierung ist ein Schlüsselkonzept hinter [!DNL Experience Platform]. Das von Adobe unterstützte XDM-System ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schemas für das Customer Experience Management zu definieren.

Die als [!DNL XDM System] bekannte Infrastruktur, auf der [!DNL Experience Platform] erstellt wird, erleichtert schemabasierte Workflows und umfasst die Muster [!DNL Schema Registry], [!DNL Schema Editor], Schemadaten und Dienstnutzung. Weitere Informationen finden Sie in der [XDM-Systemübersicht](../home.md).

Die Nutzung von Schemas in [!DNL Experience Platform] bietet verschiedene wichtige Vorteile. Erstens ermöglichen Schemata eine bessere Data Governance und eine bessere Datenminimierung, was besonders bei Datenschutzbestimmungen wichtig ist. Zweitens ermöglicht das Erstellen von Schemas mit Standardkomponenten von Adobe vordefinierte Einblicke und die Verwendung von KI-/ML-Diensten mit minimalen Anpassungen. Schließlich bieten Schemas eine Infrastruktur für Erkenntnisse über die Datenweitergabe und eine effiziente Orchestrierung.

## Planen Ihres Schemas

Der erste Schritt beim Erstellen eines Schemas besteht darin, das Konzept oder das Objekt der realen Welt zu bestimmen, das Sie im Schema erfassen möchten. Sobald Sie das Konzept, das Sie beschreiben möchten, identifizieren, können Sie mit der Planung Ihres Schemas beginnen, indem Sie über Dinge wie die Art der Daten, potenzielle Identitätsfelder und wie sich das Schema in Zukunft entwickeln könnte, nachdenken.

### Datenverhalten in [!DNL Experience Platform]

Daten, die in [!DNL Experience Platform] verwendet werden sollen, sind in zwei Verhaltenstypen unterteilt:

* **Aufzeichnen von Daten**: Stellt Informationen zu den Attributen eines Subjekts bereit. Ein Subjekt könnte eine Organisation oder eine Einzelperson sein.
* **Zeitreihendaten**: Stellt eine Momentaufnahme des Systems zum Zeitpunkt bereit, zu dem eine Aktion entweder direkt oder indirekt von einem Datensatzsubjekt durchgeführt wurde.

Alle XDM-Schemas beschreiben Daten, die als Datensatz- oder Zeitreihen kategorisiert werden können. Das Datenverhalten eines Schemas wird durch die Klasse des Schemas definiert, die einem Schema beim ersten Erstellen zugewiesen wird. XDM-Klassen werden nachstehend in diesem Dokument detailliert beschrieben.

Sowohl Schemas der Datensätze als auch der Zeitreihen enthalten eine Zuordnung der Identitäten (`xdm:identityMap`). Dieses Feld enthält die Identitätsdarstellung eines Subjekts, die aus den als „Identität“ markierten Feldern gezogen wird, wie im nächsten Abschnitt beschrieben.

### [!UICONTROL Identität] {#identity}

Schemas werden zur Aufnahme von Daten in [!DNL Experience Platform] verwendet. Diese Daten können über mehrere Dienste hinweg verwendet werden, um eine einzelne, einheitliche Ansicht einer einzelnen Entität zu erstellen. Daher ist es wichtig, wenn man über Schemas nachdenkt, über Kundenidentitäten nachzudenken und welche Felder zur Identifizierung eines Subjekts verwendet werden können, unabhängig davon, woher die Daten stammen.

Um diesen Prozess zu unterstützen, können Schlüsselfelder in Ihren Schemas als Identitäten markiert werden. Bei der Datenerfassung werden die Daten in diesen Feldern in das &quot;[!UICONTROL Identitätsdiagramm]&quot;für diese Person eingefügt. Die Diagrammdaten können dann von [[!DNL Real-time Customer Profile]](../../profile/home.md) und anderen [!DNL Experience Platform]-Diensten aufgerufen werden, um eine zusammengesetzte Ansicht jedes einzelnen Kunden bereitzustellen.

Zu den Feldern, die häufig als &quot;[!UICONTROL Identität]&quot;gekennzeichnet sind, gehören: E-Mail-Adresse, Telefonnummer, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=de), CRM-ID oder andere eindeutige ID-Felder. Sie sollten auch alle eindeutigen Kennungen berücksichtigen, die für Ihr Unternehmen spezifisch sind, da sie auch gut mit den Feldern &quot;[!UICONTROL Identität]&quot;sein können.

Es ist wichtig, während der Schema-Planungsphase über Kundenidentitäten nachzudenken, um sicherzustellen, dass Daten zusammengeführt werden, um ein möglichst robustes Profil zu erstellen. In der Übersicht zu [Adobe Experience Platform Identity Service](../../identity-service/home.md) erfahren Sie mehr darüber, wie Identitätsinformationen Ihnen dabei helfen können, Ihren Kunden digitale Erlebnisse bereitzustellen.

Es gibt zwei Möglichkeiten, Identitätsdaten an Platform zu senden:

1. Hinzufügen von Identitätsdeskriptoren zu einzelnen Feldern entweder über die [Schema Editor-Benutzeroberfläche](../ui/fields/identity.md) oder über die [Schema Registry-API](../api/descriptors.md#create)
1. Verwenden eines [`identityMap`-Felds](#identityMap)

#### `identityMap` {#identityMap}

`identityMap` ist ein Feld vom Typ Zuordnung , das die verschiedenen Identitätswerte einer Person zusammen mit den zugehörigen Namespaces beschreibt. Dieses Feld kann verwendet werden, um Identitätsinformationen für Ihre Schemas bereitzustellen, anstatt Identitätswerte innerhalb der Struktur des Schemas selbst zu definieren.

Der größte Nachteil der Verwendung von `identityMap` besteht darin, dass Identitäten in die Daten eingebettet und dadurch weniger sichtbar werden. Wenn Sie Rohdaten erfassen, sollten Sie stattdessen einzelne Identitätsfelder innerhalb der tatsächlichen Schemastruktur definieren.

>[!NOTE]
>
>Ein Schema, das `identityMap` verwendet, kann als Quellschema in einer Beziehung verwendet werden, kann jedoch nicht als Zielschema verwendet werden. Dies liegt daran, dass alle Zielschemas über eine sichtbare Identität verfügen müssen, die in einem Referenzfeld innerhalb des Quellschemas zugeordnet werden kann. Weitere Informationen zu den Anforderungen von Quell- und Zielschemas finden Sie im UI-Handbuch zu [Beziehungen](../tutorials/relationship-ui.md) .

Identitätszuordnungen können jedoch besonders nützlich sein, wenn Sie Daten aus Quellen zusammenführen, die Identitäten speichern (z. B. [!DNL Airship] oder Adobe Audience Manager), oder wenn für ein Schema eine variable Anzahl von Identitäten vorhanden ist. Darüber hinaus sind Identitätszuordnungen erforderlich, wenn Sie das [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/) verwenden.

Ein Beispiel für eine einfache Identitätszuordnung würde wie folgt aussehen:

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

Wie das obige Beispiel zeigt, stellt jeder Schlüssel im `identityMap` -Objekt einen Identitäts-Namespace dar. Der Wert für jeden Schlüssel ist ein Array von Objekten, die die Identitätswerte (`id`) für den jeweiligen Namespace darstellen. Eine [Liste der von Adobe-Anwendungen erkannten Standard-Identitäts-Namespaces](../../identity-service/troubleshooting-guide.md#standard-namespaces) finden Sie in der [!DNL Identity Service] -Dokumentation.

>[!NOTE]
>
>Ein boolean -Wert, der angibt, ob der Wert eine primäre Identität (`primary`) ist, kann auch für jeden Identitätswert angegeben werden. Primäre Identitäten müssen nur für Schemata festgelegt werden, die in [!DNL Real-time Customer Profile] verwendet werden sollen. Weitere Informationen finden Sie im Abschnitt zu [Vereinigungsschemas](#union) .

### Schema-Evolutionsprinzipien {#evolution}

In dem Maße, wie sich die Art der digitalen Erfahrungen weiterentwickelt, müssen sich auch die Schemas, die zu ihrer Darstellung verwendet werden, weiterentwickeln. Ein gut entworfenes Schema ist daher in der Lage, sich bei Bedarf anzupassen und weiterzuentwickeln, ohne destruktive Änderungen an früheren Versionen des Schemas zu verursachen.

Da die Beibehaltung der Abwärtskompatibilität für die Schemaentwicklung von entscheidender Bedeutung ist, erzwingt [!DNL Experience Platform] ein rein additives Versionierungsprinzip. Dieser Grundsatz stellt sicher, dass alle Änderungen am Schema nur zu zerstörungsfreien Aktualisierungen und Änderungen führen. Mit anderen Worten: **brechende Änderungen werden nicht unterstützt.**

>[!NOTE]
>
>Wenn ein Schema noch nicht zur Aufnahme von Daten in [!DNL Experience Platform] verwendet wurde und nicht für die Verwendung im Echtzeit-Kundenprofil aktiviert wurde, können Sie eine brechende Änderung an diesem Schema vornehmen. Sobald das Schema jedoch in [!DNL Platform] verwendet wurde, muss es der Richtlinie für additive Versionierung entsprechen.

In der folgenden Tabelle werden die Änderungen aufgeschlüsselt, die beim Bearbeiten von Schemas, Feldergruppen und Datentypen unterstützt werden:

| Unterstützte Änderungen | Brechende Änderungen (nicht unterstützt) |
| --- | --- |
| <ul><li>Hinzufügen neuer Felder zur Ressource</li><li>Definieren eines obligatorischen Felds als optional</li><li>Anzeigename und Beschreibung der Ressource ändern</li><li>Aktivieren des Schemas zur Teilnahme am Profil</li></ul> | <ul><li>Entfernen zuvor definierter Felder</li><li>Einführen neuer obligatorischer Felder</li><li>Umbenennen oder Neudefinieren vorhandener Felder</li><li>Entfernen oder Eingrenzen zuvor unterstützter Feldwerte</li><li>Verschieben vorhandener Felder an eine andere Position im Baum</li><li>Löschen des Schemas</li><li>Deaktivieren der Teilnahme des Schemas am Profil</li></ul> |

### Schemas und Datenerfassung

Um Daten in [!DNL Experience Platform] zu erfassen, muss zunächst ein Datensatz erstellt werden. Datensätze sind die Bausteine für die Datenumwandlung und -verfolgung für [[!DNL Catalog Service]](../../catalog/home.md) und stellen im Allgemeinen Tabellen oder Dateien dar, die aufgenommene Daten enthalten. Alle Datensätze basieren auf vorhandenen XDM-Schemas, die Einschränkungen dafür enthalten, was die aufgenommenen Daten enthalten und wie sie strukturiert sein sollten. Weitere Informationen hierzu finden Sie in der Übersicht über die [Datenerfassung in Adobe Experience Platform](../../ingestion/home.md).

## Bausteine eines Schemas

[!DNL Experience Platform]Die verwendet einen Kompositionsansatz, bei dem Standardbausteine kombiniert werden, um Schemas zu erstellen. Dieser Ansatz fördert die Wiederverwendbarkeit vorhandener Komponenten und sorgt für Standardisierung in der gesamten Branche, um Schemas und Komponenten von Anbietern in [!DNL Platform] zu unterstützen.

Schemas werden nach folgender Formel zusammengestellt:

**Klasse + Schemafeldgruppe&amp;ast; = XDM-Schema**

&amp;ast;Ein Schema besteht aus einer Klasse und null oder mehr Schemafeldgruppen. Das bedeutet, dass Sie ein Datensatzschema erstellen können, ohne überhaupt Feldgruppen zu verwenden.

### Klasse {#class}

Das Erstellen eines Schemas beginnt mit dem Zuweisen einer Klasse. Klassen definieren die Verhaltensaspekte der Daten, die das Schema enthalten soll (Datensatz oder Zeitreihen). Darüber hinaus beschreiben Klassen die kleinste Anzahl gemeinsamer Eigenschaften, die alle Schemas, die auf dieser Klasse basieren, beinhalten müssen, und bieten eine Möglichkeit zum Zusammenführen mehrerer kompatibler Datensätze.

Die Klasse eines Schemas bestimmt, welche Feldergruppen für die Verwendung in diesem Schema infrage kommen. Weitere Informationen hierzu finden Sie im Abschnitt [Nächster Abschnitt](#field-group).

Adobe bietet mehrere Standard-XDM-Klassen (&quot;Core&quot;). Zwei dieser Klassen, [!DNL XDM Individual Profile] und [!DNL XDM ExperienceEvent], sind für fast alle nachgelagerten Platform-Prozesse erforderlich. Zusätzlich zu diesen Core-Klassen können Sie auch eigene benutzerdefinierte Klassen erstellen, um spezifischere Anwendungsfälle für Ihr Unternehmen zu beschreiben. Benutzerdefinierte Klassen werden von einer Organisation definiert, wenn keine von der Adobe definierten Core-Klassen verfügbar sind, um einen eindeutigen Anwendungsfall zu beschreiben.

Der folgende Screenshot zeigt, wie Klassen in der Platform-Benutzeroberfläche dargestellt werden. Da das angezeigte Beispielschema keine Feldergruppen enthält, werden alle angezeigten Felder von der Klasse des Schemas bereitgestellt ([!UICONTROL XDM Individual Profile]).

![](../images/schema-composition/class.png)

Die aktuellste Liste der verfügbaren Standard-XDM-Klassen finden Sie im [offiziellen XDM-Repository](https://github.com/adobe/xdm/tree/master/components/classes). Sie können auch das Handbuch [Erkunden von XDM-Komponenten](../ui/explore.md) lesen, wenn Sie lieber Ressourcen in der Benutzeroberfläche anzeigen möchten.

### Feldergruppe {#field-group}

Eine Feldergruppe ist eine wiederverwendbare Komponente, die ein oder mehrere Felder definiert, die bestimmte Funktionen wie persönliche Details, Hotelpräferenzen oder Adressen implementieren. Feldergruppen sind als Teil eines Schemas vorgesehen, das eine kompatible Klasse implementiert.

Feldergruppen definieren, mit welchen Klassen sie kompatibel sind, basierend auf dem Verhalten der Daten, die sie darstellen (Datensatz oder Zeitreihen). Das bedeutet, dass nicht alle Feldergruppen für alle Klassen verfügbar sind.

[!DNL Experience Platform] umfasst viele Standardfeldgruppen für Adoben, ermöglicht es jedoch Anbietern, Feldgruppen für ihre  zu definieren, und einzelnen Benutzern, Feldgruppen für ihre eigenen spezifischen Konzepte zu definieren.

Um beispielsweise Details wie &quot;[!UICONTROL Vorname]&quot;und &quot;[!UICONTROL Privatadresse]&quot;für Ihr Schema &quot;[!UICONTROL Mitglieder des Treueprogramms]&quot;zu erfassen, können Sie Standardfeldgruppen verwenden, die diese gemeinsamen Konzepte definieren. Für Konzepte, die für weniger häufige Anwendungsfälle spezifisch sind (z. B. &quot;[!UICONTROL Treueprogramm-Ebene]&quot;), gibt es jedoch häufig keine vordefinierte Feldergruppe. In diesem Fall müssen Sie Ihre eigene Feldergruppe definieren, um diese Informationen zu erfassen.

>[!NOTE]
>
>Es wird dringend empfohlen, Standardfeldgruppen nach Möglichkeit in Ihren Schemas zu verwenden, da diese Felder implizit von [!DNL Experience Platform]-Diensten verstanden werden und eine größere Konsistenz bei der Verwendung über [!DNL Platform]-Komponenten hinweg bieten.
>
>Felder, die von Standardkomponenten bereitgestellt werden (z. B. &quot;Vorname&quot;und &quot;E-Mail-Adresse&quot;), enthalten zusätzliche Konnotationen, die über die grundlegenden Skalarfeldtypen hinausgehen und [!DNL Platform] darauf hinweisen, dass sich alle Felder, die denselben Datentyp aufweisen, genauso verhalten. Dieses Verhalten kann als konsistent betrachtet werden, unabhängig davon, woher die Daten stammen oder in welchem [!DNL Platform]-Dienst die Daten verwendet werden.

Beachten Sie, dass Schemas aus &quot;null oder mehr&quot;Feldergruppen bestehen. Dies bedeutet, dass Sie ein gültiges Schema erstellen können, ohne überhaupt Feldgruppen zu verwenden.

Der folgende Screenshot zeigt, wie Feldgruppen in der Platform-Benutzeroberfläche dargestellt werden. In diesem Beispiel wird einem Schema eine Feldergruppe ([!UICONTROL Demografische Details]) hinzugefügt, die eine Gruppierung der Felder zur Schemastruktur bietet.

![](../images/schema-composition/field-group.png)

Die aktuellste Liste der verfügbaren Standard-XDM-Feldgruppen finden Sie im [offiziellen XDM-Repository](https://github.com/adobe/xdm/tree/master/components/fieldgroups). Sie können auch das Handbuch [Erkunden von XDM-Komponenten](../ui/explore.md) lesen, wenn Sie lieber Ressourcen in der Benutzeroberfläche anzeigen möchten.

### Datentyp {#data-type}

Datentypen werden als Referenzfeldtypen in Klassen oder Schemata auf die gleiche Weise verwendet wie grundlegende literale Felder. Der wesentliche Unterschied besteht darin, dass Datentypen mehrere Teilfelder definieren können. Ähnlich wie bei einer Feldergruppe ermöglicht ein Datentyp die konsistente Verwendung einer Struktur mit mehreren Feldern, bietet jedoch mehr Flexibilität als eine Feldergruppe, da ein Datentyp an einer beliebigen Stelle in ein Schema eingefügt werden kann, indem er ihn als &quot;Datentyp&quot;eines Felds hinzufügt.

[!DNL Experience Platform] bietet eine Reihe gemeinsamer Datentypen als Teil von ,  [!DNL Schema Registry] um die Verwendung von Standardmustern zur Beschreibung gemeinsamer Datenstrukturen zu unterstützen. Dies wird in den [!DNL Schema Registry]-Tutorials ausführlicher erklärt, wo es beim Durchlaufen der Schritte zur Definition von Datentypen klarer wird.

Der folgende Screenshot zeigt, wie Datentypen in der Platform-Benutzeroberfläche dargestellt werden. Eines der Felder, die von der Feldergruppe [!UICONTROL Demografische Details] bereitgestellt werden, verwendet den Datentyp &quot;[!UICONTROL Personenname]&quot;, wie durch den Text neben dem Feldnamen angegeben, der auf das senkrechte Strichzeichen (`|`) folgt. Dieser bestimmte Datentyp bietet mehrere Unterfelder, die sich auf den Namen einer Person beziehen, ein Konstrukt, das für andere Felder wiederverwendet werden kann, in denen der Name einer Person erfasst werden muss.

![](../images/schema-composition/data-type.png)

Die aktuellste Liste der verfügbaren Standard-XDM-Datentypen finden Sie im [offiziellen XDM-Repository](https://github.com/adobe/xdm/tree/master/components/datatypes). Sie können auch das Handbuch [Erkunden von XDM-Komponenten](../ui/explore.md) lesen, wenn Sie lieber Ressourcen in der Benutzeroberfläche anzeigen möchten.

### Feld

Ein Feld ist der grundlegendste Baustein eines Schemas. Felder bieten Einschränkungen hinsichtlich der Art der Daten, die sie enthalten können, indem sie einen bestimmten Datentyp definieren. Diese grundlegenden Datentypen definieren ein einzelnes Feld, wohingegen die zuvor erwähnten [Datentypen](#data-type) es Ihnen ermöglichen, mehrere Teilfelder zu definieren und dieselbe Mehrfeldstruktur in verschiedenen Schemas wiederzuverwenden. Neben der Definition des &quot;Datentyps&quot;eines Felds als einen der in der Registrierung definierten Datentypen unterstützt [!DNL Experience Platform] daher grundlegende Skalartypen wie:

* Zeichenfolge
* Ganzzahl
* Double
* Boolesch
* Array
* Objekt

>[!TIP]
>
>Informationen zu den Vor- und Nachteilen der Verwendung von Freiformfeldern gegenüber Objekttypen finden Sie im [Anhang](#objects-v-freeform) .

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

## Kompositionsbeispiel

Schemas stellen das Format und die Struktur von Daten dar, die in [!DNL Platform] aufgenommen und mithilfe eines Kompositionsmodells erstellt werden. Wie bereits erwähnt, bestehen diese Schemas aus einer Klasse und null oder mehr Feldergruppen, die mit dieser Klasse kompatibel sind.

Beispielsweise könnte ein Schema, das Käufe in einem Einzelhandelsgeschäft beschreibt, als &quot;[!UICONTROL Store-Transaktionen]&quot;bezeichnet werden. Das Schema implementiert die [!DNL XDM ExperienceEvent]-Klasse in Kombination mit der standardmäßigen Feldergruppe [!UICONTROL Commerce] und einer benutzerdefinierten Feldergruppe [!UICONTROL Product Info].

Ein weiteres Schema, das den Website-Traffic verfolgt, könnte &quot;[!UICONTROL Webbesuche]&quot;heißen. Es implementiert auch die [!DNL XDM ExperienceEvent]-Klasse, kombiniert diesmal jedoch die standardmäßige [!UICONTROL Web]-Feldergruppe.

Das folgende Diagramm zeigt diese Schemas und die von den einzelnen Feldergruppen hinzugefügten Felder. Es enthält außerdem zwei Schemas, die auf der [!DNL XDM Individual Profile]-Klasse basieren, einschließlich des Schemas &quot;[!UICONTROL Mitglieder des Treueprogramms]&quot;, das zuvor in diesem Handbuch erwähnt wurde.

![](../images/schema-composition/composition.png)

### Vereinigung {#union}

Während [!DNL Experience Platform] es Ihnen ermöglicht, Schemas für bestimmte Anwendungsfälle zu erstellen, können Sie damit auch eine &quot;Vereinigung&quot;von Schemas für einen bestimmten Klassentyp sehen. Das vorherige Diagramm zeigt zwei Schemas, die auf der XDM ExperienceEvent-Klasse basieren, und zwei Schemas, die auf der [!DNL XDM Individual Profile]-Klasse basieren. Die unten dargestellte Vereinigung aggregiert die Felder aller Schemas, die dieselbe Klasse besitzen ([!DNL XDM ExperienceEvent] bzw. [!DNL XDM Individual Profile]).

![](../images/schema-composition/union.png)

Wenn Sie ein Schema zur Verwendung mit [!DNL Real-time Customer Profile] aktivieren, wird es in die Vereinigung für diesen Klassentyp aufgenommen. [!DNL Profile] bietet robuste, zentralisierte Profile von Kundenattributen sowie ein mit Zeitstempel versehenes Konto für alle Ereignisse, die Kunden in allen Systemen hatten, die mit  [!DNL Platform]integriert wurden. [!DNL Profile] verwendet die vereinigte Ansicht, um diese Daten zu repräsentieren und eine ganzheitliche Ansicht jedes einzelnen Kunden bereitzustellen.

Weitere Informationen zum Arbeiten mit [!DNL Profile] finden Sie unter [Übersicht über das Echtzeit-Kundenprofil](../../profile/home.md).

## Zuordnen von Datendateien zu XDM-Schemas

Alle Datendateien, die in [!DNL Experience Platform] aufgenommen werden, müssen der Struktur eines XDM-Schemas entsprechen. Weitere Informationen zum Formatieren von Datendateien mit XDM-Hierarchien (einschließlich Beispieldateien) finden Sie im Dokument zu [Beispiel-ETL-Transformationen](../../etl/transformations.md). Allgemeine Informationen zur Aufnahme von Datendateien in [!DNL Experience Platform] finden Sie unter [Batch-Erfassung - Übersicht](../../ingestion/batch-ingestion/overview.md).

## Schemata für externe Segmente

Wenn Sie Segmente aus externen Systemen in Platform integrieren, müssen Sie diese mit den folgenden Komponenten in Ihren Schemata erfassen:

* [[!UICONTROL Segment ] definitionclass](../classes/segment-definition.md): Verwenden Sie diese Standardklasse, um Schlüsselattribute einer externen Segmentdefinition zu erfassen.
* [[!UICONTROL Segmentzugehörigkeitsdetails ] Feldergruppe](../field-groups/profile/segmentation.md): Fügen Sie diese Feldergruppe zu Ihrem  [!UICONTROL individuellen XDM-] Profilschema hinzu, um Kundenprofile bestimmten Segmenten zuzuordnen.

## Nächste Schritte

Nachdem Sie nun die Grundlagen der Schemakomposition kennen, können Sie mit der Erforschung und Erstellung von Schemas mit [!DNL Schema Registry] beginnen.

Informationen zum Überprüfen der Struktur der beiden Core-XDM-Klassen und der häufig verwendeten kompatiblen Feldergruppen finden Sie in der folgenden Referenzdokumentation:

* [[!DNL XDM Individual Profile]](../classes/individual-profile.md)
* [[!DNL XDM ExperienceEvent]](../classes/experienceevent.md)

Der [!DNL Schema Registry] wird verwendet, um auf die [!DNL Schema Library] in Adobe Experience Platform zuzugreifen. Er bietet eine Benutzeroberfläche und eine RESTful-API, über die alle verfügbaren Bibliotheksressourcen zugänglich sind. Der [!DNL Schema Library] enthält Branchenressourcen, die durch Adobe definiert werden, von [!DNL Experience Platform]-Partnern definierte Anbieterressourcen sowie Klassen, Feldergruppen, Datentypen und Schemata, die von Mitgliedern Ihres Unternehmens zusammengestellt wurden.

Um mit dem Erstellen von Schemas über die Benutzeroberfläche zu beginnen, folgen Sie dem [Schema-Editor-Tutorial](../tutorials/create-schema-ui.md), um das Schema „Loyalty Members“ zu erstellen, das in diesem Dokument erwähnt wird.

Um mit der [!DNL Schema Registry]-API zu beginnen, lesen Sie zunächst das [Schema Registry-API-Entwicklerhandbuch](../api/getting-started.md). Nachdem Sie das Entwicklerhandbuch gelesen haben, führen Sie die Schritte aus, die im Tutorial zum [Erstellen eines Schemas mit der Schema Registry-API](../tutorials/create-schema-api.md) beschrieben werden.

## Anhang

Die folgenden Abschnitte enthalten zusätzliche Informationen zu den Prinzipien der Schemakomposition.

### Relationale Tabellen versus eingebettete Objekte {#embedded}

Bei der Arbeit mit relationalen Datenbanken bestehen die Best Practices darin, Daten zu normalisieren oder eine Entität in diskrete Teile zu zerlegen, die dann in mehreren Tabellen angezeigt werden. Um die Daten als Ganzes zu lesen oder die Entität zu aktualisieren, müssen Lese- und Schreibvorgänge über viele einzelne Tabellen mit JOIN durchgeführt werden.

Durch die Verwendung von eingebetteten Objekten können XDM-Schemas komplexe Daten direkt darstellen und in eigenständigen Dokumenten mit hierarchischer Struktur speichern. Einer der Hauptvorteile dieser Struktur besteht darin, dass Sie damit die Daten abfragen können, ohne die Entität durch teure Verbindungen zu mehreren denormalisierten Tabellen rekonstruieren zu müssen. Es gibt keine Einschränkungen dafür, wie viele Ebenen Ihre Schemahierarchie sein kann.

### Schemas und Big Data {#big-data}

Moderne digitale Systeme generieren enorme Mengen von Verhaltenssignalen (Transaktionsdaten, Weblogs, Internet der Dinge, Anzeige usw.). Diese Big-Data-Daten bieten außergewöhnliche Möglichkeiten zur Optimierung von Erlebnissen, sind aber aufgrund der Größe und Vielfalt der Daten schwierig zu nutzen. Um aus den Daten Nutzen zu ziehen, müssen Struktur, Format und Definitionen standardisiert werden, damit sie konsistent und effizient verarbeitet werden können.

Schemas lösen dieses Problem, indem sie die Integration von Daten aus mehreren Quellen, die Standardisierung durch gemeinsame Strukturen und Definitionen und die lösungsübergreifende gemeinsame Nutzung ermöglichen. Dadurch können nachfolgende Prozesse und Dienste jede Art von Frage beantworten, die von den Daten gestellt wird, und sich von dem herkömmlichen Ansatz zur Datenmodellierung abwenden, bei dem alle Fragen, die an die Daten gestellt werden, im Voraus bekannt sind und die Daten modelliert werden, um diesen Erwartungen zu entsprechen.

### Objekte versus Freiformfelder {#objects-v-freeform}

Bei der Auswahl von Objekten gegenüber Freiformfeldern bei der Erstellung von Schemata sind einige wichtige Faktoren zu beachten:

| Objekte | Freiformfelder |
| --- | --- |
| Erhöht die Verschachtelung | Weniger oder keine Verschachtelung |
| Erstellt logische Feldgruppierungen | Felder werden an Ad-hoc-Positionen platziert |

{style=&quot;table-layout:auto&quot;}

#### Objekte

Die Vor- und Nachteile der Verwendung von Objekten über Freiformfeldern sind unten aufgeführt.

**Vorteile**:

* Objekte eignen sich am besten, wenn Sie eine logische Gruppierung bestimmter Felder erstellen möchten.
* Objekte ordnen das Schema strukturierter an.
* Objekte helfen indirekt bei der Erstellung einer guten Menüstruktur in der Benutzeroberfläche von Segment Builder. Die gruppierten Felder innerhalb des Schemas werden direkt in der Ordnerstruktur angezeigt, die in der Benutzeroberfläche von Segment Builder bereitgestellt wird.

**Nachteile**:

* Felder werden verschachtelter.
* Bei Verwendung von [Adobe Experience Platform Query Service](../../query-service/home.md) müssen für Abfragefelder, die in Objekten verschachtelt sind, längere Referenzzeichenfolgen bereitgestellt werden.

#### Freiformfelder

Die Vor- und Nachteile der Verwendung von Freiformfeldern gegenüber Objekten sind unten aufgeführt.

**Vorteile**:

* Freiformfelder werden direkt unter dem Stammobjekt des Schemas (`_tenantId`) erstellt, was die Sichtbarkeit erhöht.
* Bei Verwendung von Query Service sind Referenzzeichenfolgen für Freiformfelder in der Regel kürzer.

**Nachteile**:

* Der Speicherort von Freiformfeldern im Schema ist Ad-hoc, d. h. sie werden im Schema Editor in alphabetischer Reihenfolge angezeigt. Dies kann dazu führen, dass Schemas weniger strukturiert sind und ähnliche Freiformfelder je nach Namen weit voneinander getrennt werden.
