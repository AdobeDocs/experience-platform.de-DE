---
keywords: Experience Platform;Home;beliebte Themen;ui;UI;XDM;XDM;Erlebnisdatenmodell;Erlebnisdatenmodell;Erlebnisdatenmodell;Datenmodell;Datenmodell;Datenmodell;Schema-Editor;Schema-Editor;Schema;Schema;Schema;Schemas;Erstellen;Beziehung;Beziehung;Referenz;Referenz;
solution: Experience Platform
title: Definieren einer Beziehung zwischen zwei Schemas mithilfe des Schema-Editors
description: Dieses Dokument bietet eine Anleitung zum Definieren einer Beziehung zwischen zwei Schemas mithilfe des Schema-Editors in der Benutzeroberfläche "Experience Platform".
topic-legacy: tutorial
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 31%

---

# Definieren Sie eine Beziehung zwischen zwei Schemas mithilfe des [!DNL Schema Editor]

Die Möglichkeit, Beziehungen zwischen Ihren Kunden und deren Interaktionen mit Ihrer Marke kanalübergreifend zu analysieren, ist ein wichtiger Bestandteil von Adobe Experience Platform. Durch die Definition dieser Beziehungen innerhalb der Struktur Ihrer [!DNL Experience Data Model] (XDM) Schema erhalten Sie komplexe Einblicke in Ihre Kundendaten.

Während Schema-Beziehungen durch die Verwendung des Vereinigung-Schemas und [!DNL Real-time Customer Profile] abgeleitet werden können, gilt dies nur für Schema, die dieselbe Klasse gemeinsam haben. Zur Herstellung einer Beziehung zwischen zwei Schemas, die zu verschiedenen Klassen gehören, muss einem Quell-Schema ein dediziertes Beziehungsfeld hinzugefügt werden, das auf die Identität eines Ziel-Schemas verweist.

Dieses Dokument bietet eine Anleitung zum Definieren einer Beziehung zwischen zwei Schemas mithilfe des Schema-Editors in der [!DNL Experience Platform]-Benutzeroberfläche. Anweisungen zum Definieren von Schemabeziehungen mithilfe der API finden Sie in der Anleitung zum [Definieren einer Beziehung mithilfe der Schema Registry-API](relationship-api.md).

## Erste Schritte

Dieses Lernprogramm erfordert ein Arbeitsverständnis mit [!DNL XDM System] und dem Schema-Editor in der [!DNL Experience Platform]-Benutzeroberfläche. Bevor Sie mit dem Tutorial beginnen, lesen Sie die folgenden Dokumente:

* [XDM-System in Experience Platform](../home.md): Eine Übersicht über XDM und seine Implementierung in  [!DNL Experience Platform].
* [Grundlagen der Schemakomposition](../schema/composition.md): Eine Einführung in die Bausteine von XDM-Schemas.
* [Erstellen Sie ein Schema mit dem [!DNL Schema Editor]](create-schema-ui.md) folgenden: Ein Tutorial, das die Grundlagen der Arbeit mit dem  [!DNL Schema Editor].

## Quell- und Zielschemas definieren

Wir gehen davon aus, dass Sie die beiden Schemas, die in der Beziehung definiert werden sollen, bereits erstellt haben. Zu Demonstrationszwecken wird in diesem Lernprogramm eine Beziehung zwischen den Mitgliedern des Loyalitätshotels (definiert in einem Schema &quot;[!DNL Loyalty Members]&quot;) und ihrem Lieblingshotel (definiert in einem Schema &quot;[!DNL Hotels]&quot;) hergestellt.

>[!IMPORTANT]
>
>Um eine Beziehung herzustellen, müssen beide Schema definierte primäre Identitäten haben und für [!DNL Real-time Customer Profile] aktiviert sein. Informationen zum Konfigurieren Ihrer Schema finden Sie im Abschnitt [Aktivieren eines Schemas zur Verwendung in Profil](./create-schema-ui.md#profile) im Lernprogramm zur Erstellung von Schemas.

Schema-Beziehungen werden durch ein dediziertes Feld innerhalb eines **source-Schemas** dargestellt, das auf ein anderes Feld innerhalb eines **destination-Schemas** verweist. In den folgenden Schritten ist &quot;[!DNL Loyalty Members]&quot;das Quell-Schema, während &quot;[!DNL Hotels]&quot;als Ziel-Schema fungiert.

Zu Referenzzwecken wird in den folgenden Abschnitten die Struktur der einzelnen Schemas beschrieben, die in dieser Anleitung verwendet werden, bevor eine Beziehung definiert wird.

### [!DNL Loyalty Members] schema

Das Quellcode-Schema &quot;[!DNL Loyalty Members]&quot;basiert auf der [!DNL XDM Individual Profile]-Klasse und ist das Schema, das im Lernprogramm für [Erstellen eines Schemas in der Benutzeroberfläche](create-schema-ui.md) erstellt wurde. Es enthält ein `loyalty`-Objekt unter seinem `_tenantId`-Namensraum, das mehrere treuespezifische Felder enthält. Eines dieser Felder, `loyaltyId`, dient als primäre Identität für das Schema unter dem Namensraum [!UICONTROL Email]. Wie unter **[!UICONTROL Schema-Eigenschaften]** dargestellt, wurde dieses Schema für die Verwendung in [!DNL Real-time Customer Profile] aktiviert.

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] Schema

Das Ziel-Schema &quot;[!DNL Hotels]&quot;basiert auf einer benutzerspezifischen Klasse &quot;[!DNL Hotels]&quot;und enthält Felder, die ein Hotel beschreiben. Das Feld `hotelId` dient als primäre Identität für das Schema unter einem benutzerdefinierten Namensraum `hotelId`. Wie das [!DNL Loyalty Members]-Schema wurde auch dieses Schema für [!DNL Real-time Customer Profile] aktiviert.

![](../images/tutorials/relationship/hotels.png)

## Beziehungs-Mixin erstellen

>[!NOTE]
>
>Dieser Schritt ist nur erforderlich, wenn Ihr Quell-Schema über kein dediziertes Zeichenfolgenfeld verfügt, das als Verweis auf das Ziel-Schema verwendet werden kann. Wenn das Feld in Ihrem Quellschema bereits definiert ist, fahren Sie mit dem nächsten Schritt zum [Definieren eines Beziehungsfelds](#relationship-field) fort.

Um eine Beziehung zwischen zwei Schemas zu definieren, muss das Quellschema über ein dediziertes Feld verfügen, das als Verweis auf das Zielschema dient. Sie können dem Quellschema ein solches Feld hinzufügen, indem Sie ein neues Mixin erstellen.

Beginn durch Auswahl von **[!UICONTROL Hinzufügen]** im Abschnitt **[!UICONTROL Mixins]**.

![](../images/tutorials/relationship/loyalty-add-mixin.png)

Das Dialogfeld [!UICONTROL Mixin hinzufügen] wird angezeigt. Wählen Sie **[!UICONTROL Neue Mischung erstellen]**. Geben Sie in den angezeigten Textfeldern einen Anzeigenamen und eine Beschreibung für das neue Mixin ein. Wählen Sie **[!UICONTROL Hinzufügen mixin]** aus, wenn Sie fertig sind.

<img src="../images/tutorials/relationship/loyalty-create-new-mixin.png" width="750"><br>

Die Arbeitsfläche wird wieder angezeigt, wobei &quot;[!DNL Favorite Hotel]&quot;im Abschnitt **[!UICONTROL Mixins]** angezeigt wird. Wählen Sie den Namen des Mixins und dann **[!UICONTROL Hinzufügen Feld]** neben dem Feld `Loyalty Members` aus.

![](../images/tutorials/relationship/loyalty-add-field.png)

Unter dem Namensraum `_tenantId` wird ein neues Feld auf der Arbeitsfläche angezeigt. Geben Sie unter **[!UICONTROL Feldeigenschaften]** einen Feldnamen und einen Anzeigenamen für das Feld ein und legen Sie dessen Typ auf &quot;[!UICONTROL String]&quot;fest.

![](../images/tutorials/relationship/relationship-field-details.png)

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Apply]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

Das aktualisierte Feld `favoriteHotel` wird auf der Arbeitsfläche angezeigt. Wählen Sie **[!UICONTROL Speichern]**, um die Änderungen am Schema abzuschließen.

![](../images/tutorials/relationship/relationship-field-save.png)

## Beziehungsfeld für das Quellschema definieren {#relationship-field}

Sobald in Ihrem Quellschema ein dediziertes Referenzfeld definiert ist, können Sie es als Beziehungsfeld festlegen.

Wählen Sie das Feld `favoriteHotel` auf der Arbeitsfläche aus und blättern Sie dann unter **[!UICONTROL Feldeigenschaften]** nach unten, bis das Kontrollkästchen **[!UICONTROL Beziehung]** angezeigt wird. Aktivieren Sie das Kontrollkästchen, um die erforderlichen Parameter für die Konfiguration eines Beziehungsfelds anzuzeigen.

![](../images/tutorials/relationship/relationship-checkbox.png)

Wählen Sie die Dropdown-Liste für **[!UICONTROL Referenz-Schema]** und wählen Sie das Ziel-Schema für die Beziehung (&quot;[!DNL Hotels]&quot; in diesem Beispiel). Wenn das Ziel-Schema für [!DNL Profile] aktiviert ist, wird das Feld **[!UICONTROL Referenz-Identitäts-Namensraum]** automatisch auf den Namensraum der primären Identität des Schemas eingestellt. Wenn für das Schema keine primäre Identität definiert ist, müssen Sie den zu verwendenden Namespace manuell aus dem Dropdown-Menü auswählen. Wählen Sie **[!UICONTROL Anwenden]**, wenn Sie fertig sind.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

Das Feld `favoriteHotel` wird jetzt auf der Arbeitsfläche als Beziehung hervorgehoben, wobei der Namensraum name und der Referenz-Identitätsname des Ziel-Schemas angezeigt werden. Wählen Sie **[!UICONTROL Speichern]**, um Ihre Änderungen zu speichern und den Workflow abzuschließen.

![](../images/tutorials/relationship/relationship-save.png)

## Nächste Schritte

Durch Befolgen dieses Lernprogramms haben Sie mit dem [!DNL Schema Editor] erfolgreich eine 1-zu-1-Beziehung zwischen zwei Schemas erstellt. Anweisungen zum Definieren von Beziehungen mithilfe der API finden Sie in der Anleitung zum [Definieren einer Beziehung mithilfe der Schema Registry-API](relationship-api.md).
