---
keywords: Experience Platform; home; beliebte Themen; API; XDM; XDM; XDM-System; Erlebnisdatenmodell; Datenmodell; ui; workspace; field;
solution: Experience Platform
title: Definieren von XDM-Feldern in der Benutzeroberfläche
description: Erfahren Sie, wie Sie XDM-Felder in der Experience Platform-Benutzeroberfläche definieren.
exl-id: 2adb03d4-581b-420e-81f8-e251cf3d9fb9
source-git-commit: 89519918aa830dc09365fa80449099229dc475d5
workflow-type: tm+mt
source-wordcount: '1734'
ht-degree: 1%

---

# Definieren von XDM-Feldern in der Benutzeroberfläche

Die [!DNL Schema Editor] In der Benutzeroberfläche von Adobe Experience Platform können Sie Ihre eigenen Felder in benutzerdefinierten Experience-Datenmodell (XDM)-Klassen und Schemafeldgruppen definieren. In diesem Handbuch werden die Schritte zum Definieren von XDM-Feldern in der Benutzeroberfläche beschrieben, einschließlich der verfügbaren Konfigurationsoptionen für jeden Feldtyp.

## Voraussetzungen

Dieses Handbuch setzt ein Verständnis des XDM-Systems voraus. Siehe Abschnitt [XDM-Übersicht](../../home.md) für eine Einführung in die Rolle von XDM im Experience Platform-Ökosystem und [Grundlagen der Schemakomposition](../../schema/composition.md) um zu erfahren, wie Klassen und Feldergruppen Felder zu XDM-Schemas beitragen.

Für dieses Handbuch ist zwar nicht erforderlich, es wird jedoch empfohlen, auch das Tutorial zu [Erstellen eines Schemas in der Benutzeroberfläche](../../tutorials/create-schema-ui.md) sich mit den verschiedenen Fähigkeiten der [!DNL Schema Editor].

## Ressource auswählen, der Felder hinzugefügt werden sollen {#select-resource}

Um neue XDM-Felder in der Benutzeroberfläche zu definieren, müssen Sie zunächst ein Schema innerhalb der [!DNL Schema Editor]. Je nachdem, welche Schemas Ihnen derzeit im [!DNL Schema Library], können Sie [Erstellen eines neuen Schemas](../resources/schemas.md#create) oder [ein vorhandenes Schema zur Bearbeitung auswählen](../resources/schemas.md#edit).

Sobald Sie [!DNL Schema Editor] geöffnet, werden Steuerelemente zum Hinzufügen von Feldern auf der Arbeitsfläche angezeigt. Diese Steuerelemente werden neben dem Namen des Schemas sowie allen Feldern vom Typ Objekt angezeigt, die unter der ausgewählten Klasse oder Feldergruppe definiert wurden.

![Der Schema-Editor mit hervorgehobenen Add-Symbolen.](../../images/ui/fields/overview/select-resource.png)

>[!WARNING]
>
>Wenn Sie versuchen, ein Feld zu einem Objekt hinzuzufügen, das von einer Standardfeldgruppe bereitgestellt wird, wird diese Feldergruppe in eine benutzerdefinierte Feldergruppe konvertiert und die ursprüngliche Feldergruppe ist nicht mehr verfügbar. Siehe Abschnitt zu [Felder zu Standardfeldgruppen hinzufügen](../resources/schemas.md#custom-fields-for-standard-groups) Weitere Informationen finden Sie im Handbuch zur Schemabenutzeroberfläche .

Um der Ressource ein neues Feld hinzuzufügen, wählen Sie die **plus (+)** neben dem Namen des Schemas auf der Arbeitsfläche oder neben dem Feld vom Typ Objekt, unter dem Sie das Feld definieren möchten.

![Der Schema Editor mit einem Symbol zum Hinzufügen, hervorgehoben.](../../images/ui/fields/overview/plus-icon.png)

Je nachdem, ob Sie ein Feld direkt zu einem Schema oder seiner zugehörigen Klasse und Feldergruppen hinzufügen, variieren die erforderlichen Schritte zum Hinzufügen des Felds. Der Rest dieses Dokuments konzentriert sich auf die Konfiguration der Eigenschaften eines Felds, unabhängig davon, wo dieses Feld im Schema erscheint. Weiterführende Informationen zu den verschiedenen Methoden zum Hinzufügen von Feldern zu einem Schema finden Sie in den folgenden Abschnitten des Handbuchs zur Schemabenutzeroberfläche:

* [Felder zu Feldergruppen hinzufügen](../resources/schemas.md#add-fields)
* [Felder direkt zu einem Schema hinzufügen](../resources/schemas.md#add-individual-fields)

## Definieren der Eigenschaften eines Felds {#define}

Nach Auswahl der **plus (+)** -Symbol, ein **[!UICONTROL Unbenanntes Feld]** Platzhalter wird in der Arbeitsfläche angezeigt.

![Der Schema-Editor mit einem neuen unbenannten Feld hervorgehoben.](../../images/ui/fields/overview/new-field.png)

Rechts unter **[!UICONTROL Feldeigenschaften]** können Sie die Details des neuen Felds konfigurieren. Für jedes Feld sind folgende Informationen erforderlich:

| Feldeigenschaft | Beschreibung |
| --- | --- |
| [!UICONTROL Feldname] | Ein eindeutiger, beschreibender Name für das Feld. Beachten Sie, dass der Feldname nach dem Speichern des Schemas nicht mehr geändert werden kann. Dieser Wert dient zur Identifizierung und Referenzierung des Felds im Code und in anderen nachgelagerten Anwendungen<br><br>Der Name sollte idealerweise in camelCase geschrieben werden. Sie kann alphanumerische Zeichen, Bindestriche oder Unterstriche enthalten, sie enthält jedoch **darf nicht** Beginnen Sie mit einem Unterstrich.<ul><li>**Richtig**: `fieldName`</li><li>**Zulässig:** `field_name2`, `Field-Name`, `field-name_3`</li><li>**Falsch**: `_fieldName`</li></ul> |
| [!UICONTROL Anzeigename] | Ein Anzeigename für das Feld. Dies ist der Name, mit dem das Feld auf der Arbeitsfläche des Schema-Editors dargestellt wird. Der Feldname kann mithilfe der [Umschalter für Anzeigenamen](../resources/schemas.md#display-name-toggle). |
| [!UICONTROL Typ] | Der Datentyp, den das Feld enthalten soll. In diesem Dropdown-Menü können Sie eine der [Standard-Skalartypen](../../schema/field-constraints.md) unterstützt von XDM oder einem der Mehrfachfelder [Datentypen](../resources/data-types.md) die zuvor in der [!DNL Schema Registry].<br>Hinweis: Wenn Sie den Datentyp Zuordnung auswählen, dann [!UICONTROL Map value type] -Eigenschaft angezeigt.<br><br>Sie können auch **[!UICONTROL Erweiterte Typsuche]** , um vorhandene Datentypen zu suchen und zu filtern und den gewünschten Typ leichter zu finden. |
| [!UICONTROL Map value type] | Dieser Wert ist erforderlich, wenn Sie [!UICONTROL Zuordnung] als Datentyp für das Feld. Verfügbare Werte für die Zuordnung sind [!UICONTROL Zeichenfolge] und [!UICONTROL Ganzzahl]. Wählen Sie einen Wert aus der Dropdownliste der verfügbaren Optionen aus.<br>Weitere Informationen zu [Typspezifische Feldeigenschaften](#type-specific-properties), siehe Übersicht über Felder definieren . |

{style="table-layout:auto"}

Sie können auch für jedes Feld eine Beschreibung und Notizen angeben. Verwenden Sie die **[!UICONTROL Beschreibung]** -Feld, um Kontext hinzuzufügen und die Funktionalität des Zuordnungs-Datentyps zu beschreiben. Dies trägt zur Wartbarkeit und Lesbarkeit der Implementierung bei. Sie können auch Notizen hinzufügen, um die ursprüngliche Beschreibung zu ergänzen. Dies sollte detailliertere und spezifischere Informationen bieten, die Entwicklern dabei helfen, die Zuordnung im Kontext der Codebasis effektiv zu verstehen, zu verwalten und zu nutzen. |


>[!NOTE]
>
>Je nach **[!UICONTROL Typ]** Wenn Sie für das Feld ausgewählt haben, werden in der rechten Leiste möglicherweise zusätzliche Konfigurationssteuerelemente angezeigt. Siehe Abschnitt zu [Typspezifische Feldeigenschaften](#type-specific-properties) für weitere Informationen zu diesen Steuerelementen.
>
>Die rechte Leiste bietet außerdem Kontrollkästchen für die Bezeichnung spezieller Feldtypen. Siehe Abschnitt zu [spezielle Feldtypen](#special) für weitere Informationen.

Wählen Sie nach der Konfiguration des Felds **[!UICONTROL Anwenden]**.

![Die [!UICONTROL Feldeigenschaften] im Schema Editor hervorgehoben.](../../images/ui/fields/overview/field-details.png)

Die Arbeitsfläche wird aktualisiert und zeigt das neu hinzugefügte Feld an, das sich in einem Objekt befindet, das mit Ihrer eindeutigen Mandanten-ID benannt ist (angezeigt als `_tenantId` im Beispiel unten). Alle benutzerdefinierten Felder, die einem Schema hinzugefügt werden, werden automatisch in diesen Namespace eingefügt, um Konflikte mit anderen Feldern von von Adobe-bereitgestellten Klassen und Feldergruppen zu vermeiden. In der rechten Leiste wird jetzt der Pfad des Felds zusätzlich zu den anderen Eigenschaften aufgelistet.

![Ein neues Feld im Schemadiagramm und der zugehörige Pfad im [!UICONTROL Feldeigenschaften] -Abschnitt markiert ist.](../../images/ui/fields/overview/field-added.png)

Sie können die oben beschriebenen Schritte fortsetzen, um dem Schema weitere Felder hinzuzufügen. Nach dem Speichern des Schemas werden seine Basisklasse und Feldgruppen auch dann gespeichert, wenn Änderungen an ihnen vorgenommen wurden.

>[!NOTE]
>
>Alle Änderungen, die Sie an den Feldergruppen oder der Klasse eines Schemas vornehmen, werden in allen anderen Schemas übernommen, die sie anwenden.

## Typspezifische Feldeigenschaften {#type-specific-properties}

Bei der Definition eines neuen Felds werden je nach der **[!UICONTROL Typ]** wählen Sie für das Feld aus. In der folgenden Tabelle sind diese zusätzlichen Feldeigenschaften zusammen mit den kompatiblen Typen aufgeführt:

| Feldeigenschaft | Kompatible Typen | Beschreibung |
| --- | --- | --- |
| [!UICONTROL Map value type] | [!UICONTROL Landkarte] | Die [!UICONTROL Map value type] -Eigenschaft wird nur dann in der Benutzeroberfläche angezeigt, wenn Sie den Wert Zuordnung aus dem [!UICONTROL Typ] Dropdown-Optionen. Sie können zwischen den Werttypen String und Integer für die Zuordnung auswählen.<br>![Der Schemaeditor mit den Feldern Typ und Typ Zuordnungs-Wert hervorgehoben.](../../images/ui/fields/overview/map-type.png "Der Schemaeditor mit den Feldern Typ und Typ Zuordnungs-Wert hervorgehoben."){width="100" zoomable="yes"}<br>Hinweis: Alle über die API erstellten Zuordnungs-Datentypen, die weder vom Typ String noch vom Typ Integer sind, werden als[!UICONTROL Komplex]Datentyp. &quot;&quot;kann nicht erstellt werden[!UICONTROL Komplex]Datentypen über die Benutzeroberfläche. |
| [!UICONTROL Standardwert] | [!UICONTROL Zeichenfolge], [!UICONTROL Double], [!UICONTROL Lang], [!UICONTROL Ganzzahl], [!UICONTROL Short], [!UICONTROL Byte], [!UICONTROL Boolesch] | Ein Standardwert, der diesem Feld zugewiesen wird, wenn während der Erfassung kein anderer Wert angegeben wird. Dieser Wert muss dem ausgewählten Feldtyp entsprechen.<br><br>Die Standardwerte werden zum Zeitpunkt der Aufnahme nicht im Datensatz gespeichert, da sie sich im Laufe der Zeit ändern können. Die im Schema festgelegten Standardwerte werden von nachgelagerten Platform-Diensten und -Anwendungen abgeleitet, wenn sie die Daten aus dem Datensatz lesen. Wenn das Attribut beispielsweise bei der Abfrage der Daten mit Query Service einen NULL-Wert hat, der Standardwert jedoch auf `5` auf Schemaebene wird erwartet, dass Query Service `5` anstelle von NULL. Beachten Sie, dass dieses Verhalten derzeit nicht für alle AEP-Dienste einheitlich ist. |
| [!UICONTROL Muster] | [!UICONTROL String] | A [regulärer Ausdruck](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) dass der Wert für dieses Feld übereinstimmen muss, damit er während der Aufnahme akzeptiert werden kann. |
| [!UICONTROL Format] | [!UICONTROL String] | Wählen Sie aus einer Liste vordefinierter Formate für Zeichenfolgen aus, denen der Wert entsprechen muss. Zu den verfügbaren Formaten gehören: <ul><li>[[!UICONTROL date-time]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL email]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL hostname]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL URI-Referenz]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json-pointer]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL Mindestlänge] | [!UICONTROL String] | Die Mindestanzahl von Zeichen, die die Zeichenfolge enthalten muss, damit der Wert während der Aufnahme akzeptiert wird. |
| [!UICONTROL Maximale Länge] | [!UICONTROL String] | Die maximale Zeichenanzahl, die die Zeichenfolge enthalten muss, damit der Wert während der Aufnahme akzeptiert werden kann. |
| [!UICONTROL Mindestwert] | [!UICONTROL Double] | Der Mindestwert für das Double, das bei der Aufnahme akzeptiert werden soll. Wenn der erfasste Wert exakt mit dem hier eingegebenen Wert übereinstimmt, wird der Wert akzeptiert. Bei Verwendung dieser Beschränkung wird der Wert[!UICONTROL Ausschließlicher Mindestwert]&quot;Beschränkung muss leer gelassen werden. |
| [!UICONTROL Höchstwert] | [!UICONTROL Double] | Der Maximalwert für das Double, das bei der Erfassung akzeptiert werden soll. Wenn der erfasste Wert exakt mit dem hier eingegebenen Wert übereinstimmt, wird der Wert akzeptiert. Bei Verwendung dieser Beschränkung wird der Wert[!UICONTROL Exklusiver Maximalwert]&quot;Beschränkung muss leer gelassen werden. |
| [!UICONTROL Ausschließlicher Mindestwert] | [!UICONTROL Double] | Der Maximalwert für das Double, das bei der Erfassung akzeptiert werden soll. Wenn der erfasste Wert exakt mit dem hier eingegebenen Wert übereinstimmt, wird der Wert zurückgewiesen. Bei Verwendung dieser Beschränkung wird der Wert[!UICONTROL Mindestwert]&quot;(Nicht-exklusive) Beschränkung muss leer gelassen werden. |
| [!UICONTROL Exklusiver Maximalwert] | [!UICONTROL Double] | Der Maximalwert für das Double, das bei der Erfassung akzeptiert werden soll. Wenn der erfasste Wert exakt mit dem hier eingegebenen Wert übereinstimmt, wird der Wert zurückgewiesen. Bei Verwendung dieser Beschränkung wird der Wert[!UICONTROL Höchstwert]&quot;(Nicht-exklusive) Beschränkung muss leer gelassen werden. |

{style="table-layout:auto"}

## Spezielle Feldtypen {#special}

Die rechte Leiste enthält mehrere Kontrollkästchen, mit denen Sie spezielle Rollen für das ausgewählte Feld festlegen können. Die Anwendungsfälle für einige dieser Optionen beinhalten wichtige Aspekte in Bezug auf Ihre Datenmodellierungsstrategie und die beabsichtigte Verwendung nachgelagerter Platform-Dienste.

Weitere Informationen zu diesen speziellen Typen finden Sie in der folgenden Dokumentation:

* [Zuordnung](./map.md)
* [[!UICONTROL Erforderlich]](./required.md)
* [[!UICONTROL Array]](./array.md)
* [[!UICONTROL Enum]](./enum.md)
* [[!UICONTROL Identität]](./identity.md) (Nur für Zeichenfolgenfelder verfügbar)
* [[!UICONTROL Beziehung]](./relationship.md) (Nur für Zeichenfolgenfelder verfügbar)

Obwohl es sich technisch nicht um einen speziellen Feldtyp handelt, wird empfohlen, das Handbuch zu [Definieren von Objekttypfeldern](./object.md) , um mehr über das Definieren verschachtelter Unterfelder zu erfahren, wenn Ihre Schemastrukturen vorhanden sind.

## Nächste Schritte

Dieses Handbuch bietet einen Überblick darüber, wie XDM-Felder in der Benutzeroberfläche definiert werden. Beachten Sie, dass Felder nur mithilfe von Klassen und Feldergruppen zu Schemas hinzugefügt werden können. Weitere Informationen zum Verwalten dieser Ressourcen in der Benutzeroberfläche finden Sie in den Handbüchern zum Erstellen und Bearbeiten [classes](../resources/classes.md) und [Feldergruppen](../resources/field-groups.md).

Weitere Informationen zu den Funktionen der [!UICONTROL Schemas] Arbeitsbereich, siehe [[!UICONTROL Schemas] Arbeitsbereich - Übersicht](../overview.md).
