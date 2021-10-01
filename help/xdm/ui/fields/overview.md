---
keywords: Experience Platform; Startseite; beliebte Themen; API; XDM; XDM; XDM-System; Experience-Datenmodell; Datenmodell; ui; Workspace; Feld;
solution: Experience Platform
title: Definieren von XDM-Feldern in der Benutzeroberfläche
description: Erfahren Sie, wie Sie XDM-Felder in der Experience Platform-Benutzeroberfläche definieren.
topic-legacy: user guide
exl-id: 2adb03d4-581b-420e-81f8-e251cf3d9fb9
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '1331'
ht-degree: 5%

---

# Definieren von XDM-Feldern in der Benutzeroberfläche

Mit [!DNL Schema Editor] in der Adobe Experience Platform-Benutzeroberfläche können Sie Ihre eigenen Felder in benutzerdefinierten Experience-Datenmodell (XDM)-Klassen und Schemafeldgruppen definieren. In diesem Handbuch werden die Schritte zum Definieren von XDM-Feldern in der Benutzeroberfläche beschrieben, einschließlich der verfügbaren Konfigurationsoptionen für jeden Feldtyp.

## Voraussetzungen

Dieses Handbuch setzt ein Verständnis des XDM-Systems voraus. Eine Einführung in die Rolle von XDM im Experience Platform-Ökosystem finden Sie in der [XDM-Übersicht](../../home.md) und den [Grundlagen der Schemakomposition](../../schema/composition.md) , um zu erfahren, wie Klassen und Feldgruppen Felder zu XDM-Schemas beitragen.

Für dieses Handbuch ist zwar nicht erforderlich, Sie sollten jedoch auch das Tutorial zum Erstellen eines Schemas in der Benutzeroberfläche](../../tutorials/create-schema-ui.md) befolgen, um sich mit den verschiedenen Funktionen von [!DNL Schema Editor] vertraut zu machen.[

## Ressource auswählen, der Felder hinzugefügt werden sollen {#select-resource}

Um neue XDM-Felder in der Benutzeroberfläche zu definieren, müssen Sie zunächst ein Schema innerhalb von [!DNL Schema Editor] öffnen. Je nachdem, welche Schemas Ihnen derzeit im [!DNL Schema Library] zur Verfügung stehen, können Sie [ein neues Schema](../resources/schemas.md#create) oder [ erstellen und ein vorhandenes Schema auswählen, um](../resources/schemas.md#edit) zu bearbeiten.

Sobald Sie [!DNL Schema Editor] geöffnet haben, wählen Sie in der linken Leiste die Klasse oder Feldergruppe aus, für die Sie Felder definieren möchten. Wenn es sich bei der Ressource um eine von Ihrer Organisation definierte benutzerdefinierte Ressource handelt, werden Steuerelemente zum Hinzufügen oder Bearbeiten von Feldern auf der Arbeitsfläche angezeigt. Diese Steuerelemente werden neben dem Namen des Schemas sowie allen Feldern vom Typ Objekt angezeigt, die unter der ausgewählten Klasse oder Feldergruppe definiert wurden.

![](../../images/ui/fields/overview/select-resource.png)

>[!NOTE]
>
>Wenn es sich bei der ausgewählten Klasse oder Feldergruppe um eine von Adobe bereitgestellte Kernressource handelt, kann sie nicht bearbeitet werden. Daher werden die oben gezeigten Steuerelemente nicht angezeigt. Wenn das Schema, dem Sie Felder hinzufügen möchten, auf einer Kern-XDM-Klasse basiert und keine benutzerdefinierten Feldergruppen enthält, können Sie [eine neue Feldergruppe](../resources/field-groups.md#create) erstellen, um sie stattdessen dem Schema hinzuzufügen.

Um der Ressource ein neues Feld hinzuzufügen, wählen Sie auf der Arbeitsfläche das Symbol **plus (+)** neben dem Namen des Schemas oder neben dem Feld vom Typ Objekt, unter dem Sie das Feld definieren möchten.

![](../../images/ui/fields/overview/plus-icon.png)

## Feld für eine Ressource definieren {#define}

Nach Auswahl des Symbols **plus (+)** erscheint auf der Arbeitsfläche ein **[!UICONTROL Neues Feld]**, das sich in einem Objekt auf der Stammebene befindet, das mit Ihrer eindeutigen Mandanten-ID benannt ist (im Beispiel unten unter `_tenantId` dargestellt). Alle Felder, die über benutzerdefinierte Klassen und Feldergruppen zu einem Schema hinzugefügt werden, werden automatisch in diesen Namespace eingefügt, um Konflikte mit anderen Feldern aus von der Adobe bereitgestellten Klassen und Feldergruppen zu vermeiden.

![](../../images/ui/fields/overview/new-field.png)

In der rechten Leiste unter **[!UICONTROL Feldeigenschaften]** können Sie die Details der neuen Felder konfigurieren. Für jedes Feld sind folgende Informationen erforderlich:

| Feldeigenschaft | Beschreibung |
| --- | --- |
| [!UICONTROL Feldname] | Ein eindeutiger, beschreibender Name für das Feld. Beachten Sie, dass der Feldname nach dem Speichern des Schemas nicht mehr geändert werden kann.<br><br>Der Name sollte idealerweise in camelCase geschrieben werden. Es kann alphanumerische Zeichen, Bindestriche oder Unterstriche enthalten, **darf jedoch nicht** mit einem Unterstrich beginnen.<ul><li>**Richtig**:  `fieldName`</li><li>**Zulässig:** `field_name2`,  `Field-Name`,  `field-name_3`</li><li>**Falsch**: `_fieldName`</li></ul> |
| [!UICONTROL Anzeigename] | Ein benutzerfreundlicher Name für das Feld. |
| [!UICONTROL Typ] | Der Datentyp, den das Feld enthalten soll. In diesem Dropdown-Menü können Sie einen der [standardmäßigen Skalartypen](../../schema/field-constraints.md) auswählen, die von XDM unterstützt werden, oder einen der mehrfeldigen [Datentypen](../resources/data-types.md), die zuvor in [!DNL Schema Registry] definiert wurden.<br><br>Sie können auch  **[!UICONTROL Erweiterte Typsuche auswählen,]** um vorhandene Datentypen zu suchen und zu filtern und den gewünschten Typ leichter zu finden. |

{style=&quot;table-layout:auto&quot;}

Sie können dem Feld auch eine optionale, für Menschen lesbare **[!UICONTROL Beschreibung]** bereitstellen, um mehr Kontext für den vorgesehenen Anwendungsfall des Felds bereitzustellen.

>[!NOTE]
>
>Je nachdem, welchen **[!UICONTROL Typ]** Sie für das Feld ausgewählt haben, werden in der rechten Leiste möglicherweise zusätzliche Konfigurationssteuerelemente angezeigt. Weitere Informationen zu diesen Steuerelementen finden Sie im Abschnitt [Typspezifische Feldeigenschaften](#type-specific-properties) .
>
>Die rechte Leiste bietet außerdem Kontrollkästchen für die Bezeichnung spezieller Feldtypen. Weitere Informationen finden Sie im Abschnitt [Spezielle Feldtypen](#special) .

Nachdem Sie die Konfiguration des Felds abgeschlossen haben, wählen Sie **[!UICONTROL Anwenden]** aus.

![](../../images/ui/fields/overview/field-details.png)

Die Arbeitsfläche wird aktualisiert, um den Namen und Typ des Felds anzuzeigen. In der rechten Leiste wird jetzt der Pfad des Felds zusätzlich zu den anderen Eigenschaften aufgelistet.

![](../../images/ui/fields/overview/field-added.png)

Sie können die oben beschriebenen Schritte fortsetzen, um dem Schema weitere Felder hinzuzufügen. Nach dem Speichern des Schemas werden seine Basisklasse und Feldgruppen auch dann gespeichert, wenn Änderungen an ihnen vorgenommen wurden.

>[!NOTE]
>
>Alle Änderungen, die Sie an den Feldergruppen oder der Klasse eines Schemas vornehmen, werden in allen anderen Schemas übernommen, die sie anwenden.

## Typspezifische Feldeigenschaften {#type-specific-properties}

Bei der Definition eines neuen Felds werden in der rechten Leiste je nach **[!UICONTROL Typ]**, den Sie für das Feld auswählen, möglicherweise zusätzliche Konfigurationsoptionen angezeigt. In der folgenden Tabelle sind diese zusätzlichen Feldeigenschaften zusammen mit den kompatiblen Typen aufgeführt:

| Feldeigenschaft | Kompatible Typen | Beschreibung |
| --- | --- | --- |
| [!UICONTROL Standardwert] | [!UICONTROL String],  [!UICONTROL Double],  [!UICONTROL Long],  [!UICONTROL Integer],  [!UICONTROL Short],  [!UICONTROL Byte],  [!UICONTROL Boolean] | Ein Standardwert, der diesem Feld zugewiesen wird, wenn während der Aufnahme kein anderer Wert angegeben wird. Dieser Wert muss dem ausgewählten Feldtyp entsprechen. |
| [!UICONTROL Muster] | [!UICONTROL Zeichenfolge] | Ein [regulärer Ausdruck](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) , dem der Wert für dieses Feld entsprechen muss, damit er während der Aufnahme akzeptiert werden kann. |
| [!UICONTROL Format] | [!UICONTROL Zeichenfolge] | Wählen Sie aus einer Liste vordefinierter Formate für Zeichenfolgen aus, denen der Wert entsprechen muss. Zu den verfügbaren Formaten gehören: <ul><li>[[!UICONTROL date-time]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL email]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL hostname]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL URI-Referenz]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json-pointer]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL Mindestlänge] | [!UICONTROL Zeichenfolge] | Die Mindestanzahl von Zeichen, die die Zeichenfolge enthalten muss, damit der Wert während der Aufnahme akzeptiert wird. |
| [!UICONTROL Maximale Länge] | [!UICONTROL Zeichenfolge] | Die maximale Zeichenanzahl, die die Zeichenfolge enthalten muss, damit der Wert während der Aufnahme akzeptiert werden kann. |
| [!UICONTROL Mindestwert] | [!UICONTROL Double] | Der Mindestwert für das Double, das bei der Aufnahme akzeptiert werden soll. Wenn der erfasste Wert exakt mit dem hier eingegebenen Wert übereinstimmt, wird der Wert akzeptiert. Bei Verwendung dieser Beschränkung muss die Beschränkung &quot;[!UICONTROL Ausschließlicher Mindestwert]&quot;leer gelassen werden. |
| [!UICONTROL Höchstwert] | [!UICONTROL Double] | Der Maximalwert für das Double, das bei der Erfassung akzeptiert werden soll. Wenn der erfasste Wert exakt mit dem hier eingegebenen Wert übereinstimmt, wird der Wert akzeptiert. Bei Verwendung dieser Beschränkung muss die Begrenzung &quot;[!UICONTROL Exklusiver Maximalwert]&quot;leer gelassen werden. |
| [!UICONTROL Ausschließlicher Mindestwert] | [!UICONTROL Double] | Der Maximalwert für das Double, das bei der Erfassung akzeptiert werden soll. Wenn der erfasste Wert exakt mit dem hier eingegebenen Wert übereinstimmt, wird der Wert zurückgewiesen. Bei Verwendung dieser Einschränkung muss die (nicht exklusive) Beschränkung &quot;[!UICONTROL Minimaler Wert]&quot;leer gelassen werden. |
| [!UICONTROL Exklusiver Maximalwert] | [!UICONTROL Double] | Der Maximalwert für das Double, das bei der Erfassung akzeptiert werden soll. Wenn der erfasste Wert exakt mit dem hier eingegebenen Wert übereinstimmt, wird der Wert zurückgewiesen. Bei Verwendung dieser Einschränkung muss die (nicht exklusive) Beschränkung &quot;[!UICONTROL Maximaler Wert]&quot;leer gelassen werden. |

{style=&quot;table-layout:auto&quot;}

## Spezielle Feldtypen {#special}

Die rechte Leiste enthält mehrere Kontrollkästchen, mit denen Sie spezielle Rollen für das ausgewählte Feld festlegen können. Die Anwendungsfälle für einige dieser Optionen beinhalten wichtige Aspekte in Bezug auf Ihre Datenmodellierungsstrategie und die beabsichtigte Verwendung nachgelagerter Platform-Dienste.

Weitere Informationen zu diesen speziellen Typen finden Sie in der folgenden Dokumentation:

* [[!UICONTROL Erforderlich]](./required.md)
* [[!UICONTROL Array]](./array.md)
* [[!UICONTROL Enum]](./enum.md)
* [[!UICONTROL Identität]](./identity.md)  (nur für Zeichenfolgenfelder verfügbar)
* [[!UICONTROL Beziehung]](./relationship.md)  (nur für Zeichenfolgenfelder verfügbar)

Obwohl es sich technisch nicht um einen speziellen Feldtyp handelt, wird empfohlen, das Handbuch [Definieren von Objekttypfeldern](./object.md) zu besuchen, um mehr über das Definieren verschachtelter Unterfelder zu erfahren, wenn Ihre Schemastrukturen vorhanden sind.

## Nächste Schritte

Dieses Handbuch bietet einen Überblick darüber, wie XDM-Felder in der Benutzeroberfläche definiert werden. Beachten Sie, dass Felder nur mithilfe von Klassen und Feldergruppen zu Schemas hinzugefügt werden können. Weitere Informationen zum Verwalten dieser Ressourcen in der Benutzeroberfläche finden Sie in den Handbüchern zum Erstellen und Bearbeiten von [Klassen](../resources/classes.md) und [Feldergruppen](../resources/field-groups.md).

Weitere Informationen zu den Funktionen des Arbeitsbereichs [!UICONTROL Schemas] finden Sie unter [[!UICONTROL Schemas] Workspace - Übersicht](../overview.md).
