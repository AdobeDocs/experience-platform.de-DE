---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Definieren einer Beziehung zwischen zwei Schemas mithilfe des Schema Schema Editor
topic: tutorials
translation-type: tm+mt
source-git-commit: f8c34d84e30ae14c3936c2e32ee84a2fcd3abdc3
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---


# Definieren einer Beziehung zwischen zwei Schemas mithilfe des Schema-Editors

Die Fähigkeit, die Beziehungen zwischen Ihren Kunden und ihre Interaktionen mit Ihrer Marke über verschiedene Kanal hinweg zu verstehen, ist ein wichtiger Bestandteil der Adobe Experience Platform. Die Definition dieser Beziehungen innerhalb der Struktur Ihrer Experience Data Model (XDM)-Schema ermöglicht Ihnen, komplexe Einblicke in Ihre Kundendaten zu erhalten.

Dieses Dokument bietet eine Anleitung zum Definieren einer Eins-zu-Eins-Beziehung zwischen zwei Schemas, die von Ihrem Unternehmen mithilfe des Schema-Editors in der Experience Platform-Benutzeroberfläche definiert werden. Anweisungen zum Definieren von Schema-Beziehungen mithilfe der API finden Sie im Lernprogramm zum [Definieren einer Beziehung mithilfe der Schema Registry-API](relationship-api.md).

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis des XDM-Systems und des Schema-Editors in der Experience Platform-Benutzeroberfläche. Bevor Sie dieses Lernprogramm beginnen, lesen Sie bitte die folgende Dokumentation:

* [XDM-System in Experience Platform](../home.md): Eine Übersicht über XDM und seine Implementierung in Experience Platform.
* [Grundlagen der Zusammensetzung](../schema/composition.md)des Schemas: Eine Einführung in die Bausteine von XDM-Schemas.
* [Erstellen Sie ein Schema mit dem Schema-Editor](create-schema-ui.md): Ein Lernprogramm, das die Grundlagen der Arbeit mit dem Schema-Editor behandelt.

## Definieren eines Schemas für Quelle und Ziel

Es wird erwartet, dass Sie die beiden Schema, die in der Beziehung definiert werden, bereits erstellt haben. Zu Demonstrationszwecken wird in diesem Tutorial eine Beziehung zwischen den Mitgliedern des Loyalitätshotels (definiert im Schema &quot;Treuemitglieder&quot;) und ihren Lieblingshotels (definiert in einem &quot;Hotels&quot;-Schema) hergestellt.

Schema-Beziehungen werden durch ein **Quell-Schema** mit einem Feld dargestellt, das auf ein anderes Feld innerhalb eines **Ziel-Schemas** verweist. In den folgenden Schritten wird &quot;Treuemitglieder&quot;das Schema der Quelle sein, während &quot;Hotels&quot;als Schema des Zielortes fungieren.

Zu Referenzzwecken wird in den folgenden Abschnitten die Struktur der einzelnen Schema beschrieben, die in diesem Lernprogramm verwendet werden, bevor eine Beziehung definiert wurde.

### Schema von Treuemitgliedern

Das Quell-Schema &quot;Treuemitglieder&quot;ist das Schema, das im Lernprogramm zum [Erstellen eines Schemas in der Benutzeroberfläche](create-schema-ui.md)erstellt wurde. Es enthält ein &quot;Treueobjekt&quot;unter dem Namensraum &quot;\_tenantId&quot;, das mehrere treuespezifische Felder enthält. Eines dieser Felder, &quot;loyaltyId&quot;, dient als primäre Identität für das Schema unter dem Namensraum &quot;E-Mail&quot;. Wie unter _Schema-Eigenschaften_ dargestellt, wurde dieses Schema für die Verwendung im [Echtzeit-Kundendienstprogramm](../../profile/home.md)aktiviert.

![](../images/tutorials/relationship/loyalty-members.png)

### Hotels Schema

Das Schema &quot;Hotels&quot;enthält Hotelfelder, die die Adresse, die Markenbezeichnung, die Anzahl der Zimmer und die Sterneneinstufung beschreiben. Das Feld &quot;hotelId&quot;dient als primäre ID für das Schema unter dem Namensraum &quot;ECID&quot;. Im Gegensatz zu &quot;Treuemitgliedern&quot;wurde dieses Schema nicht für Echtzeit-Kundendaten-Profil aktiviert.

![](../images/tutorials/relationship/hotels.png)

## Erstellen eines Beziehungsmixins

>[!NOTE] Dieser Schritt ist nur erforderlich, wenn Ihr Quell-Schema über kein dediziertes Zeichenfolgenfeld verfügt, das als Verweis auf ein anderes Schema verwendet werden kann. Wenn dieses Schema bereits im Quellfeld definiert ist, gehen Sie zum nächsten Schritt zum [Definieren eines Beziehungsfelds](#relationship-field)über.

Um eine Beziehung zwischen zwei Schemas zu definieren, muss das Quell-Schema über ein dediziertes Feld verfügen, das als Verweis auf das Ziel-Schema verwendet werden soll. Sie können dieses Feld dem Quellfeld hinzufügen, indem Sie eine neue Mischung erstellen.

Beginn durch Klicken auf **Hinzufügen** im Abschnitt _Mixins_ .

![](../images/tutorials/relationship/loyalty-add-mixin.png)

Das Dialogfeld _Hinzufügen Mixin_ wird angezeigt. Klicken Sie von hier auf Neues Mixin **erstellen**. Geben Sie in die angezeigten Textfelder einen Anzeigenamen und eine Beschreibung für das neue Mixin ein. Klicken Sie auf **Hinzufügen Mixin** , wenn Sie fertig sind.

<img src="../images/tutorials/relationship/loyalty-create-new-mixin.png" width="750"><br>

Die Arbeitsfläche wird mit &quot;Treuebeziehung&quot;im Abschnitt _Mixins_ wieder angezeigt. Klicken Sie auf den Namen des Mixins und dann auf **Hinzufügen Feld** neben dem Stammfeld &quot;Treuemitglieder&quot;.

![](../images/tutorials/relationship/loyalty-add-field.png)

Ein neues Feld wird auf der Arbeitsfläche unter dem Namensraum &quot;\_tenantId&quot;angezeigt. Geben Sie unter _Feldeigenschaften_ einen Feldnamen und einen Anzeigenamen für das Feld ein und legen Sie dessen Typ auf &quot;String&quot;fest.

![](../images/tutorials/relationship/relationship-field-details.png)

Klicken Sie abschließend auf **Übernehmen**.

![](../images/tutorials/relationship/relationship-field-apply.png)

Das aktualisierte Feld &quot;loyaltyRelationship&quot;wird auf der Arbeitsfläche angezeigt. Klicken Sie auf **Speichern** , um die Änderungen am Schema abzuschließen.

![](../images/tutorials/relationship/relationship-field-save.png)

## Definieren eines Beziehungsfelds für das Quell-Schema {#relationship-field}

Sobald in Ihrem Quellcode-Schema ein dediziertes Referenzfeld definiert ist, können Sie es als Beziehungsfeld festlegen.

Klicken Sie auf das Referenzfeld auf der Arbeitsfläche und blättern Sie dann unter _Feldeigenschaften_ nach unten, bis das Kontrollkästchen **Beziehung** angezeigt wird. Aktivieren Sie das Kontrollkästchen, um die erforderlichen Parameter für die Konfiguration eines Beziehungsfelds anzuzeigen.

![](../images/tutorials/relationship/relationship-checkbox.png)

Klicken Sie auf die Dropdown-Liste für das **Referenz-Schema** und wählen Sie das Ziel-Schema für die Beziehung (&quot;Hotels&quot; in diesem Beispiel). Wenn das Ziel-Schema für die Vereinigung aktiviert ist, wird das Feld &quot; **Referenz-Identitäts-Namensraum** &quot;automatisch auf den Namensraum der primären Identität des Schemas eingestellt. Wenn für das Schema keine primäre Identität definiert ist, müssen Sie den zu verwendenden Namensraum manuell aus dem Dropdown-Menü auswählen. Click **Apply** when finished.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

Das Feld wird als Beziehung auf der Arbeitsfläche angezeigt und zeigt den Namensraum der Namen- und Referenzidentität des Schemas an. Klicken Sie auf **Speichern** , um Ihre Änderungen zu speichern und den Workflow abzuschließen.

![](../images/tutorials/relationship/relationship-save.png)

## Nächste Schritte

In diesem Lernprogramm haben Sie mit dem Schema-Editor eine 1-zu-1-Beziehung zwischen zwei Schemas erstellt. Anweisungen zum Definieren von Beziehungen mithilfe der API finden Sie im Lernprogramm zum [Definieren einer Beziehung mithilfe der Schema Registry-API](relationship-api.md).