---
title: Referenz zum Erstellen von Einverständnisrichtlinien-Regeln
description: Erfahren Sie, wie Sie XDM-Datentypen, unterstützte Operatoren und erweiterte Logik zum Erstellen granularer Regeln für Einverständnisrichtlinien in der Benutzeroberfläche von Adobe Experience Platform verwenden.
source-git-commit: 678220b14cefd4dd31ef7a12355d796575a77a50
workflow-type: tm+mt
source-wordcount: '1576'
ht-degree: 0%

---

# Referenz zum Erstellen von Einverständnisrichtlinien-Regeln

Verwenden Sie diese Referenz zur erweiterten Regellogik, um präzise, rechtsgültige Regeln in der **[!UICONTROL Then]**-Klausel des Builders für Einverständnisrichtlinien in Adobe Experience Platform festzulegen.

![Die Benutzeroberfläche des Builders für Einverständnisrichtlinien, die den Abschnitt &quot;[!UICONTROL Then]&quot; hervorhebt, in dem Benutzer Regelbedingungen definieren.](../images/policies/multiple-rules.png)

Erfahren Sie, wie Richtlinienregeln auf die Struktur und die Typen Ihrer Einverständnisdaten angewendet werden, um die Voreinstellungen für das Kundeneinverständnis genau durchzusetzen.

Lesen Sie dieses Dokument, um zu erfahren, wie Sie Profile basierend auf dem Einverständnis filtern können, indem Sie in Ihrem XDM-Schema in Container-Felder navigieren und ein primitives Feld auswählen. Verwenden Sie dann den entsprechenden Operator, um den genauen Wert zu definieren, mit dem ein Profil übereinstimmen muss.

## Voraussetzungen

Bevor Sie diese Referenz verwenden, stellen Sie sicher, dass die Einrichtung Ihrer Einverständnisrichtlinie abgeschlossen ist und Sie die grundlegenden Konzepte der Datenarchitektur und des Governance-Frameworks von Adobe Experience Platform verstehen.

Stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:

* **Einrichtung der Richtlinie abgeschlossen**: Sie haben in der Benutzeroberfläche von Adobe Experience Platform mit der Erstellung einer Einverständnisrichtlinie begonnen. Ausführliche Anweisungen finden Sie im [Benutzerhandbuch zu Datennutzungsrichtlinien](user-guide.md#consent-policy).

* **Vertrautheit mit Datenstrukturen**: Diese Referenz setzt Grundkenntnisse der folgenden Kernkonzepte voraus:
   * **XDM- und Vereinigungsschema**: Erfahren Sie, wie Experience-Datenmodellstrukturen Datenbeziehungen definieren und wie das Vereinigungsschema einheitliche Kundenprofile darstellt. Weitere Informationen finden Sie [ „XDM-](../../xdm/home.md) - Übersicht“.
   * **Data Governance-Framework**: Wissen, wie Adobe Experience Platform Datennutzungsrichtlinien und Governance-Regeln durchsetzt. Einzelheiten finden Sie [ „Übersicht ](../home.md) Data Governance“.
   * **Verarbeitung des Kundeneinverständnisses**: Erfahren Sie, wie Einverständnisdaten in Workflows für Kundenerlebnisse erfasst, gespeichert und angewendet werden. Siehe [Übersicht über die Einverständnisverarbeitung](../../landing/governance-privacy-security/consent/adobe/overview.md).

## Grundlegende Konzepte: Primitive- und Container-Felder

In diesem Abschnitt erfahren Sie, wie Einverständnisrichtlinien-Regeln verschiedene Feldtypen in XDM-Schemata verwenden. Wenn Sie den Unterschied zwischen Container- und Primitivfeldern verstehen, können Sie beim Definieren von Richtlinienbedingungen das richtige Feld und den richtigen Operator auswählen.

### Unterstützte Feldtypen und Regellogik

Einverständnisrichtlinien unterstützen mehrere Feldtypen mit jeweils spezifischen Operatoren zum Erstellen von Regelbedingungen. Feldtypen werden in zwei Kategorien unterteilt: **Containertypen** und **primitive Typen**.

### Container-Typen (Schemanavigation)

Container-Typen organisieren Einverständnisdaten, können jedoch in Richtlinienbedingungen nicht direkt verwendet werden. Sie dienen als Navigationspfade, um die primitiven Felder zu erreichen, die die tatsächlichen Werte enthalten.

| Container-Typ | Beschreibung |
|----------------|-------------|
| **Objekt** | Ein Container mit einem festen Schema, das mehrere Felder verschiedener Typen enthält. |
| **Array** | Ein Container, der mehrere Werte desselben Typs enthält. |
| **Landkarte** | Ein Container mit dynamischen Schlüsseln, der Objekte oder andere Feldtypen enthalten kann. |

>[!IMPORTANT]
>
>Container-Felder können in Einverständnisrichtlinien-Bedingungen nicht direkt ausgewählt werden. Sie müssen in Container navigieren, um **primitive Felder** (z. B. Zeichenfolge, Zahl oder Boolescher Wert) für die Regelerstellung auszuwählen. Container-Operatoren werden nur für die Schemanavigation verwendet, nicht zum Festlegen von Richtlinienbedingungen.

### Primitive Typen (Regelbedingungen)

Primitive Felder enthalten die tatsächlichen Einverständnisdatenwerte (z. B. `true` oder `"weekly"`) und sind die einzigen Feldtypen, die zum Definieren von Richtlinienbedingungen verwendet werden können.

In der folgenden Tabelle werden die einzelnen unterstützten primitiven Typen und die verfügbaren Operatoren beschrieben.

| Primitiver Typ | Unterstützte Operatoren | Beschreibung |
|----------------|---------------------|-------------|
| **String** | `is equal to`, `is not equal to`, `exists`, `does not exist` | Textbasierte Einverständnisattribute. |
| **Zahl** | `is equal to`, `is not equal to`, `is greater than`, `is less than`, `exists`, `does not exist` | Numerische Einverständnisattribute. |
| **Boolesch** | `is equal to`, `is not equal to` | Wahr oder falsch Einverständniswerte. |
| **Datum** | `is equal to`, `is not equal to`, `exists`, `does not exist` | Datumsbasierte Einverständnisattribute. |


## Arbeiten mit komplexen Datenstrukturen

In diesem Abschnitt erfahren Sie, wie Sie in Ihrem Einverständnisschema durch verschachtelte Container navigieren, um primitive Felder zu erreichen. Es führt gängige Schemamuster ein und erklärt, wie tiefere Strukturen eine detailliertere Einverständnislogik ermöglichen.

### Umgang mit verschachtelten und komplexen Schemastrukturen

Komplexe Einverständnisschemata enthalten oft verschachtelte Container-Strukturen, die ein flexibles und skalierbares Daten-Management unterstützen. Da Richtlinienregeln nur auf primitive Felder verweisen können, müssen Sie durch Container-Hierarchien navigieren, um die Felder zu erreichen, die in Einverständnisrichtlinienbedingungen verwendet werden können. Eine tiefere Verschachtelung ermöglicht ein detaillierteres und spezifischeres Regeltargeting.

Zu den gebräuchlichen verschachtelten Container-Mustern gehören:

* **Zuordnung der Zuordnung** - Dynamische Schlüssel, die andere Zuordnungen enthalten.
* **Objektzuordnung** - Dynamische Schlüssel, die Objekte mit festen Schemata enthalten.
* **Array von**: Arrays, die Zuordnungen mit dynamischen Schlüsseln enthalten.
* **Array von Objekt** - Arrays, die Objekte mit festen Schemata enthalten.
* **Objekt mit Zuordnungs- oder Array-Eigenschaften** - Objekte, die Zuordnungs- oder Array-Felder enthalten.

### Beispiel für eine Feldstruktur

Die folgende Struktur dient als visuelle Referenz für Regelbeispiele in diesem Handbuch.

```
consent.marketing (Object)
├── email (Boolean)
├── sms (Boolean)
├── preferences (Map with dynamic keys)
│   ├── "email_preferences" (Object)
│   │   ├── frequency (String)
│   │   └── channels (Array of Strings)
│   ├── "sms_preferences" (Object)
│   │   ├── frequency (String)
│   │   └── opt_in_time (Date)
│   └── "push_preferences" (Object)
│       ├── frequency (String)
│       └── categories (Array of Strings)
└── lastUpdated (Date)
```

## Erweiterte Regelerstellung nach Feldtyp

Lesen Sie diesen Abschnitt für eine detaillierte Anleitung zum Erstellen von Einverständnisrichtlinienregeln basierend auf dem Feldtyp. Sie erfahren, wie Sie Regellogik für Boolesche Werte, Zuordnungen, Objekte und Arrays konfigurieren, um präzise Einverständnisbedingungen zu erfassen.

### Regelerstellungskomponenten und -schritte

Um effektive Einverständnisrichtlinien zu erstellen, müssen Sie verstehen, wie Sie in Ihrer Schemastruktur navigieren und die richtigen Operatoren für jeden Feldtyp anwenden können. Jede Regel folgt demselben grundlegenden Ansatz: Navigieren Sie zu einem primitiven Feld, wählen Sie den entsprechenden Operator aus und definieren Sie die Bedingung, die erfüllt werden muss.

Gehen Sie wie folgt vor, um eine Regel zu erstellen:

1. **Feld auswählen** - Navigieren durch Container-Felder, um ein primitives Feld zu erreichen.
2. **Operator auswählen** - Wählen Sie den Operator aus, der vom Feldtyp unterstützt wird.
   ![Das hierarchische Navigationsfenster des Schemas, das einem Benutzer zeigt, der einen Container erweitert, um ein primitives Feld zu erreichen.](../images/policies/consent-policy-map-field.png)
3. **Wert festlegen** - Definieren Sie den Wert oder die Bedingung, der bzw. der entsprochen werden soll.
4. **Zuordnungsschlüssel abgleichen** - Wählen Sie aus, ob ein bestimmter Schlüssel als Ziel ausgewählt oder über alle Schlüssel in einer Zuordnung hinweg eine Übereinstimmung gefunden werden soll.
5. **Bedingungen hinzufügen** - Kombinieren Sie bei Bedarf mehrere Regeln mithilfe der Logik AND oder OR.

### Arbeiten mit booleschen Feldern (implizite Einverständnislogik)

Boolesche Felder speichern wahre oder falsche Einverständniswerte und stellen die häufigsten Einverständnisattribute dar. Mit dem `is not equal to`-Operator können Sie Profile einbeziehen, die sich nicht explizit abgemeldet haben, wodurch implizite Einverständnisszenarien unterstützt werden.

**Boolesche Operatoren und Ergebnisse**

| Operator | Wert | Ergebnis |
|----------|-------|--------|
| `is equal to` | `true` | Schließt Profile mit expliziter Zustimmung ein (`true`). |
| `is equal to` | `false` | Umfasst Profile mit expliziter Abmeldung (`false`). |
| `is not equal to` | `true` | Umfasst Profile ohne explizite Zustimmung (`false` oder fehlende). |
| `is not equal to` | `false` | Umfasst Profile, die sich nicht explizit abgemeldet haben (`true` oder fehlen). |

**Beispiel: Implizites E-Mail-Einverständnis**

```
Field: consent.marketing.email (boolean)
Operator: is not equal to
Value: false
Result: Includes profiles who have not explicitly opted out of email marketing (includes both true and missing/null values).
```

### Arbeiten mit Zuordnungsfeldern (dynamische Voreinstellungen)

Zuordnungsfelder speichern Schlüssel-Wert-Paare mit dynamischen Schlüsseln, im Gegensatz zu Objekten mit festen Schemata. Zuordnungen werden häufig in Präferenzzentren verwendet, in denen neue Kategorien ohne Schemaaktualisierungen hinzugefügt werden können. Sie können bestimmte Schlüssel als Ziel auswählen oder den Platzhalterabgleich für alle Schlüssel verwenden.

**Spezifischer Schlüsselabgleich**

Verwenden Sie diesen Ansatz, um eine bestimmte Präferenzkategorie anzusprechen.

```
Field: consent.preferences["email_preferences"].frequency (string) - navigated to from the map container
Operator: is equal to
Value: "weekly"
Result: Includes profiles who set the email frequency to weekly (for the "email_preferences" key)
```

**Beliebiger Schlüssel, der übereinstimmt**

Verwenden Sie die Checkbox-Option &quot;**[!UICONTROL find any matching item]**&quot;, um eine Übereinstimmung über alle dynamischen Schlüssel in einer Zuordnung hinweg zu erhalten.

![Policy Rule Builder, der für Zuordnungsfelder das Kontrollkästchen „Übereinstimmendes Element finden“ anzeigt. Wird verwendet, um Werte über alle dynamischen Schlüssel hinweg abzugleichen.](../images/policies/find-any-matching-item.png)

```
Field: consent.preferences.*.frequency (string)
Operator: is equal to
Value: "weekly"
Result: Includes profiles who set frequency to weekly in ANY preference category (for example, email_preferences, sms_preferences, or push_preferences)
```

### Arbeiten mit Objektfeldern (feste Navigation)

Objektfelder dienen als Container mit festen Schemata. Sie dienen nur der Navigation und können in Richtlinienbedingungen nicht direkt referenziert werden.

**Navigationsbeispiel**

```
consent.marketing (object) → consent.marketing.email (boolean)
```

**Anwendungsbeispiel:**

```
Field: consent.marketing.email (Boolean) - navigated to from the object
Operator: is equal to
Value: true
Result: Include profiles who have explicitly consented to marketing emails
```


### Arbeiten mit Array-Feldern (mehrere Werte)

Array-Felder enthalten mehrere Werte desselben Typs und erfordern eine unterschiedliche Behandlung, je nachdem, ob sie Primitive oder Objekte speichern. Die Navigations- und Operatoroptionen variieren je nach Array-Typ.

**Beispiel für ein Array von Primitiven**

Verwenden Sie den Operator `contains` , um Profile anhand bestimmter Werte in einem Array zu identifizieren.

```
Field: consent.communication_channels (array of strings)
Operator: contains
Value: "email"
Result: Include profiles who have consented to email communication
```

**Beispiel für Objekt-Array**

Navigieren Sie in das -Array, um auf primitive Felder in verschachtelten Objekten zuzugreifen.

```
Field: consent.preferences["email_preferences"].categories[].type - navigated to from the array
Operator: is equal to
Value: "promotional"
Result: Include profiles where any email category is "promotional"
```

## Kombinieren von Regeln mit komplexer Logik

In diesem Abschnitt wird erläutert, wie Sie mehrere Regelbedingungen mithilfe der Logik UND oder ODER kombinieren. Sie erfahren, wie logische Operatoren zusammenarbeiten, um erweiterte Einverständnisrichtlinien mit mehreren Bedingungen zu definieren.

### Kombinieren mehrerer Bedingungen (UND- oder ODER-Logik)

Sie können mehrere Regelbedingungen mithilfe der UND- oder ODER-Logik kombinieren, um komplexere Einverständnisrichtlinien zu erstellen, die auf bestimmte Profilsegmente abzielen.\
**UND-**: Alle Bedingungen müssen erfüllt sein, was zu engeren Übereinstimmungen mit der Zielgruppe führt.\
**ODER-**: Ermöglicht die Erfüllung jeder Bedingung, wodurch sich die Reichweite der Zielgruppe vergrößert.

Verwenden Sie in der Schnittstelle für Einverständnisrichtlinien den Logikselektor, der zwischen Regelbedingungen angezeigt wird, um zwischen der UND- und der ODER-Logik zu wechseln.

### Beispiel für allgemeine komplexe Regeln

Im folgenden Beispiel wird der Einverständnisgrundstatus mit der Präferenzhäufigkeit kombiniert, um ein Zielsegment zu erstellen.

```
Field: consent.marketing.email
Operator: is equal to true
AND
Field: consent.preferences.frequency
Operator: is not equal to "daily"
Result: Include profiles who consent to email marketing but not to a daily frequency
```

### Erweiterte Logik für Objekt-Arrays

Wenn Sie Bedingungen innerhalb von Arrays von Objekten kombinieren, hängt das Verhalten davon ab, ob Sie zwischen den Bedingungen eine UND- oder ODER-Logik verwenden.

**Beispiel: Array von Objekten mit AND-Bedingungen**

Verwenden Sie die Logik UND , wenn alle Bedingungen auf *Array* Element angewendet werden müssen.

```
Field: consent.preferences["email_preferences"].categories[].enabled (boolean)
Operator: is equal to
Value: true
AND
Field: consent.preferences["email_preferences"].categories[].type (string)
Operator: is equal to
Value: "promotional"
Result: Includes profiles where the same category entry has both enabled=true and type="promotional".
Note: AND conditions apply to the same array entry. Using OR logic would include profiles if any array entry matches any of the conditions.
```

>[!TIP]
>
>**Best Practices für die Logik von und**
>
>Beachten Sie diese wichtigen Verhaltensweisen beim Erstellen von AND-basierten Array-Bedingungen:
>
>* Verwenden Sie die Logik UND , wenn alle Bedingungen auf das **gleiche Array-Element“ angewendet** müssen.
>* Denken Sie daran, dass UND eine restriktive Zielgruppenbestimmung erstellt (es stimmen weniger Profile überein).
>* Erwarten Sie nicht, dass UND-Logik über mehrere Array-Einträge hinweg übereinstimmt. Dies gilt für jeden Eintrag.
>* Vermeiden Sie die Verwendung der UND-Logik, wenn Sie eine flexible Abgleichung über Einträge hinweg benötigen.

>[!IMPORTANT]
>
>Mit AND-Logik muss jeder Array-Eintrag alle angegebenen Bedingungen gleichzeitig erfüllen. Dieses Verhalten ist optimal, wenn Sie kombinierte Attribute zuordnen müssen, z. B. Kategorien, die sowohl aktiviert als auch fördernd sind.

>[!NOTE]
>
>UND-Logik gilt für denselben Array-Eintrag **nur für Arrays von Objekten.**\
>Bei Arrays von Primitiven wird die AND-Logik auf Feldebene über das gesamte Array hinweg ausgewertet.

**Beispiel: Array von Objekten mit OR-Bedingungen**

Verwenden Sie die OR-Logik, um inklusive Zielgruppenübereinstimmungen zu erstellen, indem Sie zulassen, dass jede Bedingung über Array-Einträge hinweg wahr ist.

```
Field: consent.preferences["email_preferences"].categories[].enabled (boolean)
Operator: is equal to
Value: true
OR
Field: consent.preferences["email_preferences"].categories[].type (string)
Operator: is equal to
Value: "newsletter"
Result: Includes profiles where any category entry has enabled=true or any entry has type="newsletter".
Note: OR logic allows matching across different array entries. One entry can meet the first condition while another meets the second.
```

### Nächste Schritte

Nachdem Sie Ihre Einverständnisrichtlinien-Regeln erstellt und verfeinert haben, verwenden Sie die folgenden Ressourcen, um die Konfiguration abzuschließen, die Durchsetzung der Richtlinien zu validieren und die zugrunde liegenden Datenmodelle zu überprüfen.

* **Workflow für die Richtlinienerstellung**: Implementieren Sie die in der Benutzeroberfläche des Policy Builders definierten Regeln mit dem [Handbuch für die Benutzeroberfläche der Einverständnisrichtlinie](user-guide.md#consent-policy.md)
* **Bewertung und Durchsetzung der Einverständnisrichtlinie** Überprüfen Sie, wie sich die aktivierte Richtlinie auf die Zielgruppenaktivierung und die Verwendung von Profildaten auswirkt. Weitere Informationen finden Sie [Handbuch zur automatischen Richtliniendurchsetzung](../enforcement/auto-enforcement.md)
* **XDM-Einverständnisdatentypen**: Verweisen Sie auf die spezifischen Schemastrukturen und Felddefinitionen für Einverständnisattribute, die in Ihren Richtlinienregeln verwendet werden. Siehe das [Handbuch zu XDM-Einverständnissen und -Voreinstellungen](../../xdm/data-types/consents.md).
