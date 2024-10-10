---
keywords: Experience Platform; home; beliebte Themen; API; XDM; XDM; XDM-System; Erlebnisdatenmodell; Datenmodell; ui; workspace; field;
solution: Experience Platform
title: Definieren von XDM-Feldern in der Benutzeroberfläche
description: Erfahren Sie, wie Sie XDM-Felder in der Experience Platform-Benutzeroberfläche definieren.
exl-id: 2adb03d4-581b-420e-81f8-e251cf3d9fb9
source-git-commit: 807ce0b0304fd73a455f228529d75cfc68769bf5
workflow-type: tm+mt
source-wordcount: '1607'
ht-degree: 1%

---

# Definieren von XDM-Feldern in der Benutzeroberfläche

Mit dem Wert &quot;[!DNL Schema Editor]&quot;in der Adobe Experience Platform-Benutzeroberfläche können Sie Ihre eigenen Felder in benutzerdefinierten Experience-Datenmodell (XDM)-Klassen und Schemafeldgruppen definieren. In diesem Handbuch werden die Schritte zum Definieren von XDM-Feldern in der Benutzeroberfläche beschrieben, einschließlich der verfügbaren Konfigurationsoptionen für jeden Feldtyp.

## Voraussetzungen

Dieses Handbuch setzt ein Verständnis des XDM-Systems voraus. Eine Einführung in die Rolle von XDM im Experience Platform-Ökosystem finden Sie in der [XDM-Übersicht](../../home.md) und in den [Grundlagen der Schemakomposition](../../schema/composition.md) , um zu erfahren, wie Klassen und Feldgruppen Felder zu XDM-Schemas beitragen.

Für dieses Handbuch ist zwar nicht erforderlich, Sie sollten jedoch auch das Tutorial zum Erstellen eines Schemas in der Benutzeroberfläche ](../../tutorials/create-schema-ui.md) befolgen, um sich mit den verschiedenen Funktionen von [!DNL Schema Editor] vertraut zu machen.[

## Ressource auswählen, der Felder hinzugefügt werden sollen {#select-resource}

Um neue XDM-Felder in der Benutzeroberfläche zu definieren, müssen Sie zunächst ein Schema innerhalb des [!DNL Schema Editor] öffnen. Je nachdem, welche Schemas Ihnen derzeit in der [!DNL Schema Library] zur Verfügung stehen, können Sie [ein neues Schema erstellen](../resources/schemas.md#create) oder [ein vorhandenes Schema auswählen, um es zu bearbeiten](../resources/schemas.md#edit).

Sobald Sie die [!DNL Schema Editor] geöffnet haben, werden Steuerelemente zum Hinzufügen von Feldern auf der Arbeitsfläche angezeigt. Diese Steuerelemente werden neben dem Namen des Schemas sowie allen Feldern vom Typ Objekt angezeigt, die unter der ausgewählten Klasse oder Feldergruppe definiert wurden.

![Der Schema-Editor mit hervorgehobenen Add-Symbolen.](../../images/ui/fields/overview/select-resource.png)

>[!WARNING]
>
>Wenn Sie versuchen, ein Feld zu einem Objekt hinzuzufügen, das von einer Standardfeldgruppe bereitgestellt wird, wird diese Feldergruppe in eine benutzerdefinierte Feldergruppe konvertiert und die ursprüngliche Feldergruppe ist nicht mehr verfügbar. Weitere Informationen finden Sie im Abschnitt zum Hinzufügen von Feldern zu Standardfeldgruppen ](../resources/schemas.md#custom-fields-for-standard-groups) im Handbuch zur Schemabenutzeroberfläche.[

Um der Ressource ein neues Feld hinzuzufügen, wählen Sie auf der Arbeitsfläche das Symbol **Plus (+)** neben dem Namen des Schemas oder neben dem Feld vom Typ &quot;Objekt&quot;, unter dem das Feld definiert werden soll.

![Der Schema-Editor mit einem hervorgehobenen Symbol zum Hinzufügen.](../../images/ui/fields/overview/plus-icon.png)

Je nachdem, ob Sie ein Feld direkt zu einem Schema oder seiner zugehörigen Klasse und Feldergruppen hinzufügen, variieren die erforderlichen Schritte zum Hinzufügen des Felds. Der Rest dieses Dokuments konzentriert sich auf die Konfiguration der Eigenschaften eines Felds, unabhängig davon, wo dieses Feld im Schema erscheint. Weiterführende Informationen zu den verschiedenen Methoden zum Hinzufügen von Feldern zu einem Schema finden Sie in den folgenden Abschnitten des Handbuchs zur Schemabenutzeroberfläche:

* [Felder zu Feldergruppen hinzufügen](../resources/schemas.md#add-fields)
* [Felder direkt zu einem Schema hinzufügen](../resources/schemas.md#add-individual-fields)

## Definieren der Eigenschaften eines Felds {#define}

Nach Auswahl des Symbols **plus (+)** wird auf der Arbeitsfläche ein Platzhalter für das Feld **[!UICONTROL Unbenannt]** angezeigt.

![Der Schema-Editor mit einem neuen unbenannten Feld ist hervorgehoben.](../../images/ui/fields/overview/new-field.png)

In der rechten Leiste unter **[!UICONTROL Feldeigenschaften]** können Sie die Details des neuen Felds konfigurieren. Für jedes Feld sind folgende Informationen erforderlich:

| Feldeigenschaft | Beschreibung |
| --- | --- |
| [!UICONTROL Feldname] | Ein eindeutiger, beschreibender Name für das Feld. Beachten Sie, dass der Feldname nach dem Speichern des Schemas nicht mehr geändert werden kann. Dieser Wert wird verwendet, um das Feld im Code und in anderen nachgelagerten Anwendungen zu identifizieren und zu referenzieren<br><br>Der Name sollte idealerweise in camelCase geschrieben werden. Es kann alphanumerische Zeichen, Bindestriche oder Unterstriche enthalten, aber **darf nicht** mit einem Unterstrich beginnen.<ul><li>**Korrekt**: `fieldName`</li><li>**Acceptable:** `field_name2`, `Field-Name`, `field-name_3`</li><li>**Falsch**: `_fieldName`</li></ul> |
| [!UICONTROL Anzeigename] | Ein Anzeigename für das Feld. Dies ist der Name, mit dem das Feld auf der Arbeitsfläche des Schema-Editors dargestellt wird. Der Feldname kann mit dem Umschalter [Anzeigename ](../resources/schemas.md#display-name-toggle) in den Anzeigenamen geändert werden. |
| [!UICONTROL Typ] | Der Datentyp, den das Feld enthalten soll. In diesem Dropdown-Menü können Sie einen der von XDM unterstützten [standardmäßigen Skalartypen](../../schema/field-constraints.md) oder einen der mehrfelligen [Datentypen](../resources/data-types.md) auswählen, die zuvor in [!DNL Schema Registry] definiert wurden.<br>Hinweis: Wenn Sie den Datentyp Zuordnung auswählen, wird die Eigenschaft [!UICONTROL Map value type] angezeigt.<br><br>Sie können auch **[!UICONTROL Erweiterte Suche nach Typ]** auswählen, um vorhandene Datentypen zu suchen und zu filtern und den gewünschten Typ leichter zu finden. |
| [!UICONTROL Map value type] | Dieser Wert ist erforderlich, wenn Sie [!UICONTROL Map] als Datentyp für das Feld auswählen. Verfügbare Werte für die Zuordnung sind [!UICONTROL String] und [!UICONTROL Integer]. Wählen Sie einen Wert aus der Dropdownliste der verfügbaren Optionen aus.<br>Weitere Informationen zu [typspezifischen Feldeigenschaften](#type-specific-properties) finden Sie in der Übersicht über Felder definieren . |

{style="table-layout:auto"}

Sie können auch für jedes Feld eine Beschreibung und Notizen angeben. Verwenden Sie das Feld **[!UICONTROL Beschreibung]** , um Kontext hinzuzufügen und die Funktionalität des Zuordnungs-Datentyps zu beschreiben. Dies trägt zur Wartbarkeit und Lesbarkeit der Implementierung bei. Sie können auch Notizen hinzufügen, um die ursprüngliche Beschreibung zu ergänzen. Dies sollte detailliertere und spezifischere Informationen bieten, die Entwicklern dabei helfen, die Zuordnung im Kontext der Codebasis effektiv zu verstehen, zu verwalten und zu nutzen. |


>[!NOTE]
>
>Je nach dem für das Feld ausgewählten **[!UICONTROL Typ]** können in der rechten Leiste zusätzliche Konfigurationssteuerelemente angezeigt werden. Weitere Informationen zu diesen Steuerelementen finden Sie im Abschnitt zu [typspezifischen Feldeigenschaften](#type-specific-properties) .
>
>Die rechte Leiste bietet außerdem Kontrollkästchen für die Bezeichnung spezieller Feldtypen. Weitere Informationen finden Sie im Abschnitt zu [speziellen Feldtypen](#special) .

Nachdem Sie die Konfiguration des Felds abgeschlossen haben, wählen Sie **[!UICONTROL Anwenden]** aus.

![Der Abschnitt [!UICONTROL Feldeigenschaften] des Schema-Editors wird hervorgehoben.](../../images/ui/fields/overview/field-details.png)

Die Arbeitsfläche wird aktualisiert und zeigt das neu hinzugefügte Feld an, das sich in einem Objekt befindet, das mit Ihrer eindeutigen Mandanten-ID benannt ist (im Beispiel unten als `_tenantId` angezeigt). Alle benutzerdefinierten Felder, die einem Schema hinzugefügt werden, werden automatisch in diesen Namespace eingefügt, um Konflikte mit anderen Feldern von von Adobe-bereitgestellten Klassen und Feldergruppen zu vermeiden. In der rechten Leiste wird jetzt der Pfad des Felds zusätzlich zu den anderen Eigenschaften aufgelistet.

![Ein neues Feld im Schemadiagramm und der zugehörige Pfad im Abschnitt [!UICONTROL Feldeigenschaften] werden hervorgehoben.](../../images/ui/fields/overview/field-added.png)

Sie können die oben beschriebenen Schritte fortsetzen, um dem Schema weitere Felder hinzuzufügen. Nach dem Speichern des Schemas werden seine Basisklasse und Feldgruppen auch dann gespeichert, wenn Änderungen an ihnen vorgenommen wurden.

>[!NOTE]
>
>Alle Änderungen, die Sie an den Feldergruppen oder der Klasse eines Schemas vornehmen, werden in allen anderen Schemas übernommen, die sie anwenden.

## Typspezifische Feldeigenschaften {#type-specific-properties}

Beim Definieren eines neuen Felds werden in der rechten Leiste je nach dem für das Feld ausgewählten **[!UICONTROL Typ]** zusätzliche Konfigurationsoptionen angezeigt. In der folgenden Tabelle sind diese zusätzlichen Feldeigenschaften zusammen mit den kompatiblen Typen aufgeführt:

| Feldeigenschaft | Kompatible Typen | Beschreibung |
| --- | --- | --- |
| [!UICONTROL Map value type] | [!UICONTROL Landkarte] | Die Eigenschaft [!UICONTROL Map value type] wird nur dann in der Benutzeroberfläche angezeigt, wenn Sie den Wert Map aus den Dropdown-Optionen [!UICONTROL Typ] auswählen. Sie können zwischen den Werttypen String und Integer für die Zuordnung auswählen.<br>![Der Schemaeditor mit hervorgehobenen Feldern vom Typ Typ und Typ Zuordnungs-Wert.](../../images/ui/fields/overview/map-type.png "Der Schemaeditor mit hervorgehobenen Feldern vom Typ Typ und Typ Zuordnungs-Wert."){width="100" zoomable="yes"}<br>Hinweis: Alle über die API erstellten Zuordnungs-Datentypen, die weder vom Typ String noch vom Typ Integer sind, werden als Datentyp &quot;[!UICONTROL Komplex]&quot;angezeigt. Über die Benutzeroberfläche können keine Datentypen vom Typ &quot;[!UICONTROL Komplex]&quot;erstellt werden. |
| [!UICONTROL Muster] | [!UICONTROL String] | Ein [regulärer Ausdruck](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) , mit dem der Wert für dieses Feld übereinstimmen muss, damit er während der Aufnahme akzeptiert werden kann. |
| [!UICONTROL Format] | [!UICONTROL String] | Wählen Sie aus einer Liste vordefinierter Formate für Zeichenfolgen aus, denen der Wert entsprechen muss. Zu den verfügbaren Formaten gehören: <ul><li>[[!UICONTROL date-time]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL email]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL hostname]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL uri-reference]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json-pointer]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL Mindestlänge] | [!UICONTROL String] | Die Mindestanzahl von Zeichen, die die Zeichenfolge enthalten muss, damit der Wert während der Aufnahme akzeptiert wird. |
| [!UICONTROL Maximale Länge] | [!UICONTROL String] | Die maximale Zeichenanzahl, die die Zeichenfolge enthalten muss, damit der Wert während der Aufnahme akzeptiert werden kann. |
| [!UICONTROL Mindestwert] | [!UICONTROL Double] | Der Mindestwert für das Double, das bei der Aufnahme akzeptiert werden soll. Wenn der erfasste Wert exakt mit dem hier eingegebenen Wert übereinstimmt, wird der Wert akzeptiert. Bei Verwendung dieser Beschränkung muss die Beschränkung &quot;[!UICONTROL Ausschließlicher Mindestwert]&quot; leer gelassen werden. |
| [!UICONTROL Höchstwert] | [!UICONTROL Double] | Der Maximalwert für das Double, das bei der Erfassung akzeptiert werden soll. Wenn der erfasste Wert exakt mit dem hier eingegebenen Wert übereinstimmt, wird der Wert akzeptiert. Bei Verwendung dieser Beschränkung muss die Beschränkung &quot;[!UICONTROL Ausschließlicher Maximalwert]&quot; leer gelassen werden. |
| [!UICONTROL Ausschließlicher Mindestwert] | [!UICONTROL Double] | Der Maximalwert für das Double, das bei der Erfassung akzeptiert werden soll. Wenn der erfasste Wert exakt mit dem hier eingegebenen Wert übereinstimmt, wird der Wert zurückgewiesen. Bei Verwendung dieser Einschränkung muss die (nicht exklusive) Beschränkung &quot;[!UICONTROL Mindestwert]&quot; leer gelassen werden. |
| [!UICONTROL Exklusiver Maximalwert] | [!UICONTROL Double] | Der Maximalwert für das Double, das bei der Erfassung akzeptiert werden soll. Wenn der erfasste Wert exakt mit dem hier eingegebenen Wert übereinstimmt, wird der Wert zurückgewiesen. Bei Verwendung dieser Einschränkung muss die &quot;[!UICONTROL Maximaler Wert]&quot;(nicht exklusiv) Beschränkung leer gelassen werden. |

{style="table-layout:auto"}

## Spezielle Feldtypen {#special}

Die rechte Leiste enthält mehrere Kontrollkästchen, mit denen Sie spezielle Rollen für das ausgewählte Feld festlegen können. Die Anwendungsfälle für einige dieser Optionen beinhalten wichtige Aspekte in Bezug auf Ihre Datenmodellierungsstrategie und die beabsichtigte Verwendung nachgelagerter Platform-Dienste.

Weitere Informationen zu diesen speziellen Typen finden Sie in der folgenden Dokumentation:

* [Zuordnung](./map.md)
* [[!UICONTROL Erforderlich]](./required.md)
* [[!UICONTROL Array]](./array.md)
* [[!UICONTROL Enum]](./enum.md)
* [[!UICONTROL Identität]](./identity.md) (nur für Zeichenfolgenfelder verfügbar)
* [[!UICONTROL Beziehung]](./relationship.md) (Nur für Zeichenfolgenfelder verfügbar)

Obwohl es sich technisch nicht um einen speziellen Feldtyp handelt, wird empfohlen, die Anleitung zum [Definieren von Objekttypfeldern](./object.md) aufzurufen, um mehr über das Definieren verschachtelter Unterfelder zu erfahren, wenn Ihre Schemastrukturen vorhanden sind.

## Nächste Schritte

Dieses Handbuch bietet einen Überblick darüber, wie XDM-Felder in der Benutzeroberfläche definiert werden. Beachten Sie, dass Felder nur mithilfe von Klassen und Feldergruppen zu Schemas hinzugefügt werden können. Weitere Informationen zum Verwalten dieser Ressourcen in der Benutzeroberfläche finden Sie in den Handbüchern zum Erstellen und Bearbeiten von [Klassen](../resources/classes.md) und [Feldergruppen](../resources/field-groups.md).

Weitere Informationen zu den Funktionen des Arbeitsbereichs [!UICONTROL Schemas] finden Sie in der Übersicht über den Arbeitsbereich [[!UICONTROL Schemas] ](../overview.md) .
