---
keywords: Experience Platform;Home;beliebte Themen;API;XDM;XDM;XDM-System;Erlebnisdatenmodell;Datenmodell;ui;Arbeitsbereich;Feld;
solution: Experience Platform
title: Definieren von XDM-Feldern in der Benutzeroberfläche
description: Erfahren Sie, wie Sie XDM-Felder in der Benutzeroberfläche "Experience Platform"definieren.
topic-legacy: user guide
exl-id: 2adb03d4-581b-420e-81f8-e251cf3d9fb9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 5%

---

# Definieren von XDM-Feldern in der Benutzeroberfläche

Mit dem Operator [!DNL Schema Editor] in der Adobe Experience Platform-Benutzeroberfläche können Sie Ihre eigenen Felder in benutzerdefinierten Experience Data Model-(XDM-)Klassen und Mixins definieren. Dieses Handbuch beschreibt die Schritte zum Definieren von XDM-Feldern in der Benutzeroberfläche, einschließlich der verfügbaren Konfigurationsoptionen für jeden Feldtyp.

## Voraussetzungen

Dieses Handbuch erfordert ein funktionierendes Verständnis des XDM-Systems. In der [XDM-Übersicht](../../home.md) finden Sie eine Einführung in die Rolle von XDM im Experience Platform-Ökosystem und in den [Grundlagen der Schema-Komposition](../../schema/composition.md), um zu erfahren, wie Klassen und Mixins Felder zu XDM-Schemas beitragen.

Es wird empfohlen, das Tutorial zum [Erstellen eines Schemas in der Benutzeroberfläche](../../tutorials/create-schema-ui.md) zu befolgen, um sich mit den verschiedenen Funktionen von [!DNL Schema Editor] vertraut zu machen.

## Wählen Sie eine Ressource aus, der Sie Felder zu {#select-resource} hinzufügen möchten

Um neue XDM-Felder in der Benutzeroberfläche zu definieren, müssen Sie zunächst ein Schema innerhalb von [!DNL Schema Editor] öffnen. Je nachdem, welche Schema derzeit im Ordner [!DNL Schema Library] verfügbar sind, können Sie [ein neues Schema](../resources/schemas.md#create) oder [ein vorhandenes Schema zur Bearbeitung auswählen.](../resources/schemas.md#edit)

Wenn Sie [!DNL Schema Editor] geöffnet haben, wählen Sie mit der linken Leiste die Klasse oder das Mixin aus, für die Sie Felder definieren möchten. Wenn es sich bei der Ressource um eine benutzerdefinierte Ressource handelt, die von Ihrem Unternehmen definiert wurde, werden Steuerelemente zum Hinzufügen oder Bearbeiten von Feldern auf der Arbeitsfläche angezeigt. Diese Steuerelemente werden neben dem Namen des Schemas sowie allen Objekttypfeldern angezeigt, die unter der ausgewählten Klasse oder Mischung definiert wurden.

![](../../images/ui/fields/overview/select-resource.png)

>[!NOTE]
>
>Wenn die ausgewählte Klasse oder das ausgewählte Mixin eine von der Adobe bereitgestellte Kernressource ist, kann sie nicht bearbeitet werden und daher werden die oben aufgeführten Steuerelemente nicht angezeigt. Wenn das Schema, dem Sie Felder hinzufügen möchten, auf einer XDM-Hauptklasse basiert und keine benutzerdefinierten Mixins enthält, können Sie [eine neue Mixin](../resources/mixins.md#create) erstellen, um stattdessen dem Schema hinzuzufügen.

Um der Ressource ein neues Feld hinzuzufügen, klicken Sie auf das Symbol **plus (+)** neben dem Namen des Schemas auf der Arbeitsfläche oder neben dem Objekttypfeld, unter dem Sie das Feld definieren möchten.

![](../../images/ui/fields/overview/plus-icon.png)

## Definieren eines Felds für eine Ressource {#define}

Nach Auswahl des Symbols **plus (+)** wird in der Arbeitsfläche ein **[!UICONTROL Neues Feld]** angezeigt, das sich in einem Objekt auf der Stammebene befindet, das mit Ihrer eindeutigen Mandanten-ID benannt wird (siehe `_tenantId` im Beispiel unten). Alle Felder, die über benutzerdefinierte Klassen und Mixins zu einem Schema hinzugefügt werden, werden automatisch in diesen Namensraum eingefügt, um Konflikte mit anderen Feldern aus von der Adobe bereitgestellten Klassen und Mixins zu vermeiden.

![](../../images/ui/fields/overview/new-field.png)

In der rechten Leiste unter **[!UICONTROL Feldeigenschaften]** können Sie die Details der neuen Felder konfigurieren. Für jedes Feld sind die folgenden Informationen erforderlich:

| Feldeigenschaft | Beschreibung |
| --- | --- |
| [!UICONTROL Feldname] | Ein eindeutiger, beschreibender Name für das Feld. Beachten Sie, dass der Feldname nach dem Speichern des Schemas nicht mehr geändert werden kann.<br><br>Der Name sollte idealerweise in camelCase geschrieben werden. Es kann alphanumerische Zeichen, Bindestriche oder Unterstriche enthalten, jedoch darf **kein** Beginn mit Unterstrich vorhanden sein.<ul><li>**Richtig**:  `fieldName`</li><li>**Zulässig:** `field_name2`,  `Field-Name`,  `field-name_3`</li><li>**Falsch**: `_fieldName`</li></ul> |
| [!UICONTROL Anzeigename] | Ein benutzerfreundlicher Name für das Feld. |
| [!UICONTROL Typ] | Der Datentyp, den das Feld enthalten soll. In diesem Dropdown-Menü können Sie einen der von XDM unterstützten [standardmäßigen Skalartypen](../../schema/field-constraints.md) oder einen der Multifield [Datentypen](../resources/data-types.md) auswählen, die zuvor in [!DNL Schema Registry] definiert wurden.<br><br>Sie können auch  **[!UICONTROL Erweiterte Typsuche auswählen, um vorhandene Datentypen]** zu suchen und zu filtern und den gewünschten Typ leichter zu finden. |

Sie können dem Feld auch eine optionale, für Menschen lesbare **[!UICONTROL Beschreibung]** bereitstellen, um mehr Kontext hinsichtlich des vorgesehenen Anwendungsfalls des Felds bereitzustellen.

>[!NOTE]
>
>Je nachdem, welche **[!UICONTROL Typ]** Sie für das Feld ausgewählt haben, können in der rechten Leiste zusätzliche Konfigurationssteuerelemente angezeigt werden. Weitere Informationen zu diesen Steuerelementen finden Sie im Abschnitt [Typspezifische Feldeigenschaften](#type-specific-properties).
>
>Die rechte Leiste bietet außerdem Kontrollkästchen für die Zuweisung von speziellen Feldtypen. Weitere Informationen finden Sie im Abschnitt [Spezielle Feldtypen](#special).

Nachdem Sie das Feld konfiguriert haben, wählen Sie **[!UICONTROL Apply]**.

![](../../images/ui/fields/overview/field-details.png)

Die Arbeitsfläche wird aktualisiert, um den Feldnamen und -typ anzuzeigen. Die rechte Leiste Liste jetzt den Feldpfad zusätzlich zu den anderen Eigenschaften.

![](../../images/ui/fields/overview/field-added.png)

Sie können die oben stehenden Schritte ausführen, um dem Schema weitere Felder hinzuzufügen. Sobald das Schema gespeichert wurde, werden seine Basisklasse und Mixins auch gespeichert, wenn daran Änderungen vorgenommen wurden.

>[!NOTE]
>
>Alle Änderungen, die Sie an den Mixins oder der Klasse eines Schemas vornehmen, werden in allen anderen Schemas übernommen, die diese verwenden.

## Typspezifische Feldeigenschaften {#type-specific-properties}

Wenn Sie ein neues Feld definieren, werden in der rechten Leiste ggf. zusätzliche Konfigurationsoptionen angezeigt, je nachdem, welchen **[!UICONTROL Typ]** Sie für das Feld auswählen. In der folgenden Tabelle sind diese zusätzlichen Feldeigenschaften zusammen mit den kompatiblen Typen aufgeführt:

| Feldeigenschaft | Kompatible Typen | Beschreibung |
| --- | --- | --- |
| [!UICONTROL Standardwert] | [!UICONTROL String],  [!UICONTROL Dublette],  [!UICONTROL Long],  [!UICONTROL Integer],  [!UICONTROL Short],    [!UICONTROL ByteBoolean] | Ein Standardwert, der diesem Feld zugewiesen wird, wenn während der Erfassung kein anderer Wert angegeben wird. Dieser Wert muss dem ausgewählten Feldtyp entsprechen. |
| [!UICONTROL Muster] | [!UICONTROL Zeichenfolge] | Ein [regulärer Ausdruck](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions), dem der Feldwert entsprechen muss, damit er während der Erfassung akzeptiert werden kann. |
| [!UICONTROL Format] | [!UICONTROL Zeichenfolge] | Wählen Sie aus einer Liste vordefinierter Formate für Zeichenfolgen, denen der Wert entsprechen muss. Zu den verfügbaren Formaten gehören: <ul><li>[[!UICONTROL date-time]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL email]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL Hostname]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL uri-reference]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json-zeiger]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL Mindestlänge] | [!UICONTROL Zeichenfolge] | Die Mindestanzahl von Zeichen, die die Zeichenfolge enthalten muss, damit der Wert während der Erfassung akzeptiert werden kann. |
| [!UICONTROL Maximale Länge] | [!UICONTROL Zeichenfolge] | Die maximale Anzahl von Zeichen, die die Zeichenfolge enthalten muss, damit der Wert während der Erfassung akzeptiert werden kann. |
| [!UICONTROL Mindestwert] | [!UICONTROL Double] | Der Mindestwert für die Dublette, die während der Aufnahme akzeptiert wird. Wenn der erfasste Wert exakt mit dem hier eingegebenen Wert übereinstimmt, wird der Wert akzeptiert. Bei Verwendung dieser Beschränkung muss die Beschränkung &quot;[!UICONTROL Ausschließlicher Mindestwert]&quot;leer gelassen werden. |
| [!UICONTROL Höchstwert] | [!UICONTROL Dublette] | Der Höchstwert für die Dublette, die während der Erfassung akzeptiert wird. Wenn der erfasste Wert exakt mit dem hier eingegebenen Wert übereinstimmt, wird der Wert akzeptiert. Bei Verwendung dieser Beschränkung muss die Beschränkung &quot;[!UICONTROL Exklusiver Maximalwert]&quot;leer gelassen werden. |
| [!UICONTROL Exklusiver Mindestwert] | [!UICONTROL Dublette] | Der Höchstwert für die Dublette, die während der Erfassung akzeptiert wird. Wenn der erfasste Wert exakt mit dem hier eingegebenen Wert übereinstimmt, wird der Wert zurückgewiesen. Bei Verwendung dieser Beschränkung muss die Beschränkung &quot;[!UICONTROL Mindestwert]&quot;(nicht exklusiv) leer gelassen werden. |
| [!UICONTROL Exklusiver Maximalwert] | [!UICONTROL Dublette] | Der Höchstwert für die Dublette, die während der Erfassung akzeptiert wird. Wenn der erfasste Wert exakt mit dem hier eingegebenen Wert übereinstimmt, wird der Wert zurückgewiesen. Bei Verwendung dieser Beschränkung muss die Beschränkung &quot;[!UICONTROL Maximum value]&quot;(nicht exklusiv) leer gelassen werden. |

## Spezielle Feldtypen {#special}

Die rechte Leiste enthält mehrere Kontrollkästchen, mit denen Sonderrollen für das ausgewählte Feld festgelegt werden können. Die Anwendungsfälle für einige dieser Optionen beinhalten wichtige Aspekte in Bezug auf Ihre Datenmodellierungsstrategie und die Art und Weise, wie Sie nachgelagerte Plattformdienste verwenden möchten.

Weitere Informationen zu diesen speziellen Typen finden Sie in der folgenden Dokumentation:

* [[!UICONTROL Erforderlich]](./required.md)
* [[!UICONTROL Array]](./array.md)
* [[!UICONTROL Enum]](./enum.md)
* [[!UICONTROL Identity]](./identity.md)  (nur für Zeichenfolgenfelder verfügbar)
* [[!UICONTROL Beziehung]](./relationship.md)  (nur für Zeichenfolgenfelder verfügbar)

Obwohl es sich technisch nicht um einen speziellen Feldtyp handelt, wird empfohlen, im Handbuch [Definieren von Objekttypfeldern](./object.md) weitere Informationen zum Definieren verschachtelter Unterfelder anzuzeigen, wenn Ihr Schema strukturiert ist.

## Nächste Schritte

Dieses Handbuch gab einen Überblick darüber, wie XDM-Felder in der Benutzeroberfläche definiert werden. Beachten Sie, dass Felder nur mithilfe von Klassen und Mixins zu Schemas hinzugefügt werden können. Weitere Informationen zum Verwalten dieser Ressourcen in der Benutzeroberfläche finden Sie in den Handbüchern zum Erstellen und Bearbeiten von [Klassen](../resources/classes.md) und [mixins](../resources/mixins.md).

Weitere Informationen zu den Funktionen des Arbeitsbereichs [!UICONTROL Schema] finden Sie unter [[!UICONTROL Schema] Arbeitsbereichsübersicht](../overview.md).
