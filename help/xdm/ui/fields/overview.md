---
keywords: Experience Platform;Startseite;beliebte Themen;API;API;XDM;XDM-System;Experience-Datenmodell;Datenmodell;UI;Arbeitsbereich;Feld;
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

Mit der [!DNL Schema Editor] in der Adobe Experience Platform-Benutzeroberfläche können Sie Ihre eigenen Felder in benutzerdefinierten Experience-Datenmodell(XDM)-Klassen und Schemafeldgruppen definieren. In diesem Handbuch werden die Schritte zum Definieren von XDM-Feldern in der Benutzeroberfläche beschrieben, einschließlich der verfügbaren Konfigurationsoptionen für jeden Feldtyp.

## Voraussetzungen

Dieses Handbuch setzt ein Grundverständnis des XDM-Systems voraus. Unter [XDM-Übersicht](../../home.md) finden Sie eine Einführung in die Rolle von XDM im Experience Platform-Ökosystem und die [Grundlagen der Schemakomposition](../../schema/composition.md) um zu erfahren, wie Klassen und Feldergruppen Felder zu XDM-Schemata beitragen.

Obwohl dies für dieses Handbuch nicht erforderlich ist, wird empfohlen, auch das Tutorial zum Erstellen [ Schemas in der Benutzeroberfläche zu befolgen](../../tutorials/create-schema-ui.md) um sich mit den verschiedenen Funktionen des [!DNL Schema Editor] vertraut zu machen.

## Ressource auswählen, der Felder hinzugefügt werden sollen {#select-resource}

Um neue XDM-Felder in der Benutzeroberfläche zu definieren, müssen Sie zunächst ein Schema in der [!DNL Schema Editor] öffnen. Je nachdem, welche Schemata Ihnen derzeit im [!DNL Schema Library] zur Verfügung stehen, können Sie wählen, [ein neues Schema erstellen](../resources/schemas.md#create) oder [ein vorhandenes Schema zur Bearbeitung auswählen](../resources/schemas.md#edit).

Sobald die [!DNL Schema Editor] geöffnet ist, werden die Steuerelemente zum Hinzufügen von Feldern auf der Arbeitsfläche angezeigt. Diese Steuerelemente werden neben dem Namen des Schemas sowie allen Feldern vom Typ „Objekt“ angezeigt, die unter der ausgewählten Klasse oder Feldergruppe definiert wurden.

![Der Schema-Editor mit den hervorgehobenen Symbolen zum Hinzufügen.](../../images/ui/fields/overview/select-resource.png)

>[!WARNING]
>
>Wenn Sie versuchen, ein Feld zu einem Objekt hinzuzufügen, das von einer Standardfeldgruppe bereitgestellt wird, wird diese Feldgruppe in eine benutzerdefinierte Feldgruppe konvertiert und die ursprüngliche Feldgruppe ist nicht mehr verfügbar. Weitere Informationen finden Sie [ Abschnitt zum Hinzufügen von Feldern zu Standardfeldgruppen ](../resources/schemas.md#custom-fields-for-standard-groups) Handbuch zur Benutzeroberfläche von Schemata .

Um der Ressource ein neues Feld hinzuzufügen, wählen Sie auf der Arbeitsfläche das Symbol **plus (+)** neben dem Namen des Schemas oder neben dem Feld vom Typ „Objekt“ aus, unter dem Sie das Feld definieren möchten.

![Der Schema-Editor mit einem hervorgehobenen Hinzufügen-Symbol.](../../images/ui/fields/overview/plus-icon.png)

Je nachdem, ob Sie ein Feld direkt zu einem Schema oder seinen konstituierenden Klassen- und Feldergruppen hinzufügen, variieren die erforderlichen Schritte zum Hinzufügen des Felds. Der Rest dieses Dokuments konzentriert sich auf die Konfiguration der Eigenschaften eines Felds, unabhängig davon, wo dieses Feld im Schema angezeigt wird. Weitere Informationen zu den verschiedenen Möglichkeiten, wie Felder zu einem Schema hinzugefügt werden können, finden Sie in den folgenden Abschnitten im Handbuch zur Benutzeroberfläche für Schemata:

* [Hinzufügen von Feldern zu Feldergruppen](../resources/schemas.md#add-fields)
* [Hinzufügen von Feldern direkt zu einem Schema](../resources/schemas.md#add-individual-fields)

## Definieren der Eigenschaften eines Felds {#define}

Nach Auswahl des Symbols **plus (+)** wird auf **[!UICONTROL Arbeitsfläche]** Platzhalter „Nicht benanntes Feld“ angezeigt.

![Der Schema-Editor mit einem neuen, nicht benannten Feld wurde hervorgehoben.](../../images/ui/fields/overview/new-field.png)

In der rechten Leiste unter **[!UICONTROL Feldeigenschaften]** können Sie die Details des neuen Felds konfigurieren. Für jedes Feld sind die folgenden Informationen erforderlich:

| Feldeigenschaft | Beschreibung |
| --- | --- |
| [!UICONTROL Feldname] | Ein eindeutiger, beschreibender Name für das Feld. Beachten Sie, dass der Name des Felds nach dem Speichern des Schemas nicht mehr geändert werden kann. Dieser Wert wird verwendet, um das Feld im Code und in anderen nachgelagerten Anwendungen zu identifizieren und darauf <br><br> verweisen. Der Name sollte idealerweise in Binnenmajuskel-Schreibweise geschrieben werden. Sie kann alphanumerische Zeichen, Bindestriche oder Unterstriche enthalten, **darf jedoch nicht** mit einem Unterstrich beginnen.<ul><li>**Richtig**: `fieldName`</li><li>**Akzeptiert:** `field_name2`, `Field-Name`, `field-name_3`</li><li>**Falsch**: `_fieldName`</li></ul> |
| [!UICONTROL Anzeigename] | Ein Anzeigename für das Feld. Dies ist der Name, der zur Darstellung des Felds auf der Arbeitsfläche des Schema-Editors verwendet wird. Der Feldname kann mithilfe des Umschalters für den Anzeigenamen in [ Anzeigenamen geändert ](../resources/schemas.md#display-name-toggle). |
| [!UICONTROL Typ] | Der Typ der Daten, die das Feld enthalten soll. Aus diesem Dropdown-Menü können Sie einen der [standardmäßigen Skalartypen](../../schema/field-constraints.md) die von XDM unterstützt werden, oder einen der Mehrfeld-[Datentypen](../resources/data-types.md) auswählen, die zuvor in der [!DNL Schema Registry] definiert wurden.<br>Hinweis: Wenn Sie den Datentyp Zuordnung auswählen, wird [!UICONTROL  Eigenschaft &quot;]&quot; angezeigt.<br><br>Sie können auch **[!UICONTROL Erweiterte Typsuche]** auswählen, um vorhandene Datentypen zu suchen und zu filtern und den gewünschten Typ leichter zu finden. |
| [!UICONTROL Zuordnungs-Werttyp] | Dieser Wert ist erforderlich, wenn Sie [!UICONTROL Zuordnung] als Datentyp für das Feld auswählen. Verfügbare Werte für die Zuordnung sind [!UICONTROL Zeichenfolge] und [!UICONTROL Ganzzahl]. Wählen Sie einen Wert aus der Dropdown-Liste der verfügbaren Optionen aus.<br>Weitere Informationen zu [typspezifischen Feldeigenschaften](#type-specific-properties) finden Sie in der Übersicht zum Definieren von Feldern . |

{style="table-layout:auto"}

Sie können auch eine Beschreibung und Anmerkungen für jedes Feld angeben. Verwenden Sie **[!UICONTROL Feld]** Beschreibung“, um Kontext hinzuzufügen und die Funktionalität des Zuordnungsdatentyps zu beschreiben. Dies trägt zur Wartbarkeit und Lesbarkeit der Implementierung bei. Sie können auch Anmerkungen hinzufügen, um die ursprüngliche Beschreibung zu ergänzen. Dies sollte detailliertere und spezifischere Informationen bieten, die Entwicklern beim Verstehen, Pflegen und effektiven Nutzen der Zuordnung im Kontext der Codebasis helfen. |


>[!NOTE]
>
>Je nach dem **[!UICONTROL Feld]** Typ“ werden in der rechten Leiste möglicherweise zusätzliche Konfigurationssteuerelemente angezeigt. Weitere Informationen zu [ Steuerelementen finden Sie im Abschnitt ](#type-specific-properties)Typspezifische Feldeigenschaften“.
>
>Die rechte Leiste enthält auch Kontrollkästchen zum Festlegen spezieller Feldtypen. Weitere Informationen finden Sie [ Abschnitt ](#special)Spezielle Feldtypen“.

Nachdem Sie die Konfiguration des Felds abgeschlossen haben, wählen Sie **[!UICONTROL Anwenden]** aus.

![Der [!UICONTROL Feldeigenschaften] im Schema-Editor ist hervorgehoben.](../../images/ui/fields/overview/field-details.png)

Die Arbeitsfläche wird aktualisiert und zeigt das neu hinzugefügte Feld an, das sich in einem -Objekt befindet, das gemäß Ihrer eindeutigen Mandanten-ID mit einem Namespace versehen ist (wie im `_tenantId` Beispiel unten gezeigt). Alle benutzerdefinierten Felder, die einem Schema hinzugefügt werden, werden automatisch in diesem Namespace platziert, um Konflikte mit anderen Feldern aus von Adobe bereitgestellten Klassen und Feldergruppen zu verhindern. In der rechten Leiste wird nun der Pfad des Felds zusätzlich zu seinen anderen Eigenschaften aufgeführt.

![Ein neues Feld im Schemadiagramm und der entsprechende Pfad im Abschnitt [!UICONTROL Feldeigenschaften] ist hervorgehoben.](../../images/ui/fields/overview/field-added.png)

Sie können mit den oben genannten Schritten fortfahren, um dem Schema weitere Felder hinzuzufügen. Nach dem Speichern des Schemas werden auch dessen Basisklasse und Feldergruppen gespeichert, sofern Änderungen daran vorgenommen wurden.

>[!NOTE]
>
>Alle Änderungen, die Sie an den Feldergruppen oder der Klasse eines Schemas vornehmen, werden in allen anderen Schemata übernommen, die sie verwenden.

## Typspezifische Feldeigenschaften {#type-specific-properties}

Beim Definieren eines neuen Felds können in der rechten Leiste zusätzliche Konfigurationsoptionen angezeigt werden, je nachdem, **[!UICONTROL Sie]** Feld „Typ“ ausgewählt haben. In der folgenden Tabelle sind diese zusätzlichen Feldeigenschaften zusammen mit ihren kompatiblen Typen aufgeführt:

| Feldeigenschaft | Kompatible Typen | Beschreibung |
| --- | --- | --- |
| [!UICONTROL Zuordnungs-Werttyp] | [!UICONTROL Landkarte] | Die Eigenschaft [!UICONTROL Zuordnungs]Werttyp wird nur in der Benutzeroberfläche angezeigt, wenn Sie den Zuordnungswert aus den [!UICONTROL Typ] auswählen. Sie können für die Zuordnung zwischen den Werttypen „Zeichenfolge“ und „Ganzzahl“ wählen.<br>![Der Schemaeditor mit den hervorgehobenen Feldern Typ und Zuordnungswerttyp.](../../images/ui/fields/overview/map-type.png "Der Schemaeditor mit den hervorgehobenen Feldern Typ und Zuordnungswerttyp."){width="100" zoomable="yes"}<br>Hinweis: Alle über die API erstellten Zuordnungsdatentypen, die weder vom Typ Zeichenfolge noch Ganzzahl sind, werden als Datentyp [!UICONTROL Komplex] angezeigt. Datentypen vom Typ [!UICONTROL Komplex] können nicht über die Benutzeroberfläche erstellt werden. |
| [!UICONTROL Muster] | [!UICONTROL String] | Ein [regulärer Ausdruck](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) dem der Wert für dieses Feld entsprechen muss, damit er bei der Aufnahme akzeptiert wird. |
| [!UICONTROL Format] | [!UICONTROL String] | Wählen Sie aus einer Liste vordefinierter Formate für Zeichenfolgen, denen der Wert entsprechen muss. Zu den verfügbaren Formaten gehören: <ul><li>[[!UICONTROL Datum-Uhrzeit]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL email]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL hostname]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL IPv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL IPv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL URI]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL URI-Referenz]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json-pointer]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL Mindestlänge] | [!UICONTROL String] | Die Mindestanzahl von Zeichen, die die Zeichenfolge enthalten muss, damit der Wert während der Aufnahme akzeptiert wird. |
| [!UICONTROL Maximale Länge] | [!UICONTROL String] | Die maximale Anzahl von Zeichen, die die Zeichenfolge enthalten muss, damit der Wert während der Aufnahme akzeptiert wird. |
| [!UICONTROL Mindestwert] | [!UICONTROL Double] | Der Mindestwert für den Double-Wert, der bei der Aufnahme akzeptiert werden soll. Wenn der aufgenommene Wert genau mit dem hier eingegebenen übereinstimmt, wird der Wert akzeptiert. Bei Verwendung dieser Einschränkung muss die Beschränkung [!UICONTROL Ohne Mindestwert] leer bleiben. |
| [!UICONTROL Höchstwert] | [!UICONTROL Double] | Der Höchstwert für den Double-Wert, der bei der Aufnahme akzeptiert wird. Wenn der aufgenommene Wert genau mit dem hier eingegebenen übereinstimmt, wird der Wert akzeptiert. Bei Verwendung dieser Einschränkung muss die Beschränkung [!UICONTROL Ohne Maximalwert] leer gelassen werden. |
| [!UICONTROL Ohne Mindestwert] | [!UICONTROL Double] | Der Höchstwert für den Double-Wert, der bei der Aufnahme akzeptiert wird. Wenn der aufgenommene Wert genau mit dem hier eingegebenen übereinstimmt, wird der Wert zurückgewiesen. Bei Verwendung dieser Einschränkung muss die Beschränkung [!UICONTROL Mindestwert] (nicht ausschließlich) leer gelassen werden. |
| [!UICONTROL Ohne Maximalwert] | [!UICONTROL Double] | Der Höchstwert für den Double-Wert, der bei der Aufnahme akzeptiert wird. Wenn der aufgenommene Wert genau mit dem hier eingegebenen übereinstimmt, wird der Wert zurückgewiesen. Bei Verwendung dieser Einschränkung muss die Beschränkung [!UICONTROL Maximalwert] (nicht exklusiv) leer gelassen werden. |

{style="table-layout:auto"}

## Spezielle Feldtypen {#special}

Die rechte Leiste enthält mehrere Kontrollkästchen zum Festlegen spezieller Rollen für das ausgewählte Feld. Die Anwendungsfälle für einige dieser Optionen beinhalten wichtige Überlegungen bezüglich Ihrer Datenmodellierungsstrategie und der Art und Weise, wie Sie nachgelagerte Platform-Services verwenden möchten.

Weitere Informationen zu diesen speziellen Typen finden Sie in der folgenden Dokumentation:

* [Zuordnung](./map.md)
* [[!UICONTROL Erforderlich]](./required.md)
* [[!UICONTROL Array]](./array.md)
* [[!UICONTROL enum]](./enum.md)
* [[!UICONTROL Identität]](./identity.md) (nur für Zeichenfolgenfelder verfügbar)
* [[!UICONTROL Beziehung]](./relationship.md) (nur für Zeichenfolgenfelder verfügbar)

Obwohl es sich technisch gesehen nicht um einen speziellen Feldtyp handelt, wird auch empfohlen, das Handbuch unter [Definieren von Feldern vom Typ „Objekt](./object.md) zu lesen, um mehr über das Definieren verschachtelter Unterfelder Ihrer Schemastrukturen zu erfahren.

## Nächste Schritte

Dieses Handbuch bietet einen Überblick darüber, wie XDM-Felder in der Benutzeroberfläche definiert werden. Denken Sie daran, dass Felder nur mithilfe von Klassen und Feldergruppen zu Schemata hinzugefügt werden können. Weitere Informationen zum Verwalten dieser Ressourcen in der Benutzeroberfläche finden Sie in den Handbüchern zum Erstellen und Bearbeiten [Klassen](../resources/classes.md) und [Feldergruppen](../resources/field-groups.md).

Weitere Informationen zu den Funktionen des Arbeitsbereichs [!UICONTROL Schemata] finden Sie unter [[!UICONTROL Schemata] Arbeitsbereich - Übersicht](../overview.md).
