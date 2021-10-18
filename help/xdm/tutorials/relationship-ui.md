---
keywords: Experience Platform; Startseite; beliebte Themen; UI; XDM; XDM; XDM-System; Experience-Datenmodell; Experience-Datenmodell; Experience-Datenmodell; Datenmodell; Datenmodell; Schema-Editor; Schema; Schema; Schemas; Erstellen; Beziehung; Beziehung; Referenz; Referenz;
solution: Experience Platform
title: Definieren einer Beziehung zwischen zwei Schemas mithilfe des Schema-Editors
description: Dieses Dokument bietet eine Anleitung zum Definieren einer Beziehung zwischen zwei Schemas mithilfe des Schema-Editors in der Experience Platform-Benutzeroberfläche.
topic-legacy: tutorial
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
source-git-commit: 2118dc175b421e856c6b0a33a83a7238f01b7ee3
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 24%

---

# Definieren einer Beziehung zwischen zwei Schemas mithilfe von [!DNL Schema Editor]

>[!NOTE]
>
>Wenn Sie Real-time Customer Data Platform B2B Edition verwenden, lesen Sie stattdessen das Handbuch zum Erstellen von B2B-Beziehungen](./relationship-b2b.md) .[

Die Möglichkeit, Beziehungen zwischen Ihren Kunden und deren Interaktionen mit Ihrer Marke kanalübergreifend zu analysieren, ist ein wichtiger Bestandteil von Adobe Experience Platform. Wenn Sie diese Beziehungen innerhalb der Struktur Ihrer [!DNL Experience Data Model] (XDM)-Schemas definieren, erhalten Sie komplexe Einblicke in Ihre Kundendaten.

Während Schemabeziehungen durch die Verwendung des Vereinigungsschemas und [!DNL Real-time Customer Profile] abgeleitet werden können, gilt dies nur für Schemas, die dieselbe Klasse aufweisen. Um eine Beziehung zwischen zwei Schemas herzustellen, die zu verschiedenen Klassen gehören, muss einem Quellschema ein dediziertes Beziehungsfeld hinzugefügt werden, das auf die Identität eines Zielschemas verweist.

Dieses Dokument bietet eine Anleitung zum Definieren einer Beziehung zwischen zwei Schemas mithilfe des Schema-Editors in der [!DNL Experience Platform]-Benutzeroberfläche. Anweisungen zum Definieren von Schemabeziehungen mithilfe der API finden Sie in der Anleitung zum [Definieren einer Beziehung mithilfe der Schema Registry-API](relationship-api.md).

## Erste Schritte

Dieses Tutorial setzt ein grundlegendes Verständnis von [!DNL XDM System] und des Schema-Editors in der Benutzeroberfläche von [!DNL Experience Platform] voraus. Bevor Sie mit dem Tutorial beginnen, lesen Sie die folgenden Dokumente:

* [XDM-System in Experience Platform](../home.md): Eine Übersicht über XDM und dessen Implementierung in  [!DNL Experience Platform].
* [Grundlagen der Schemakomposition](../schema/composition.md): Eine Einführung in die Bausteine von XDM-Schemas.
* [Erstellen Sie ein Schema mit [!DNL Schema Editor]](create-schema-ui.md): Ein Tutorial, das die Grundlagen der Arbeit mit dem  [!DNL Schema Editor]behandelt.

## Quell- und Zielschemas definieren

Wir gehen davon aus, dass Sie die beiden Schemas, die in der Beziehung definiert werden sollen, bereits erstellt haben. Zu Demonstrationszwecken erstellt dieses Tutorial eine Beziehung zwischen Mitgliedern des Treueprogramms einer Organisation (definiert in einem Schema &quot;[!DNL Loyalty Members]&quot;) und deren Lieblingshotel (definiert in einem Schema &quot;[!DNL Hotels]&quot;).

>[!IMPORTANT]
>
>Um eine Beziehung herzustellen, müssen beide Schemas definierte primäre Identitäten aufweisen und für [!DNL Real-time Customer Profile] aktiviert sein. Lesen Sie den Abschnitt zum Aktivieren eines Schemas für die Verwendung in Profil](./create-schema-ui.md#profile) im Tutorial zur Schemaerstellung , wenn Sie Anleitungen zum Konfigurieren Ihrer Schemas benötigen.[

Schemabeziehungen werden durch ein dediziertes Feld innerhalb eines **Quellschemas** dargestellt, das auf ein anderes Feld innerhalb eines **Zielschemas** verweist. In den folgenden Schritten wird &quot;[!DNL Loyalty Members]&quot;das Quellschema sein, während &quot;[!DNL Hotels]&quot;als Zielschema fungiert.

Zu Referenzzwecken wird in den folgenden Abschnitten die Struktur der einzelnen Schemas beschrieben, die in dieser Anleitung verwendet werden, bevor eine Beziehung definiert wird.

### [!DNL Loyalty Members] schema

Das Quellschema &quot;[!DNL Loyalty Members]&quot;basiert auf der Klasse [!DNL XDM Individual Profile] und ist das Schema, das im Tutorial zum Erstellen eines Schemas in der Benutzeroberfläche](create-schema-ui.md) erstellt wurde. [ Sie enthält ein `loyalty`-Objekt unter dem Namespace `_tenantId`, das mehrere loyalitätsspezifische Felder enthält. Eines dieser Felder, `loyaltyId`, dient als primäre Identität für das Schema unter dem Namespace [!UICONTROL E-Mail]. Wie unter **[!UICONTROL Schemaeigenschaften]** zu sehen ist, wurde dieses Schema zur Verwendung in [!DNL Real-time Customer Profile] aktiviert.

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] schema

Das Zielschema &quot;[!DNL Hotels]&quot;basiert auf einer benutzerdefinierten Klasse &quot;[!DNL Hotels]&quot;und enthält Felder, die ein Hotel beschreiben.

![](../images/tutorials/relationship/hotels.png)

Um an einer Beziehung teilnehmen zu können, muss das Zielschema über eine primäre Identität verfügen. In diesem Beispiel wird das Feld `hotelId` als primäre Identität mithilfe eines benutzerdefinierten Identitäts-Namespace &quot;Hotel-ID&quot;verwendet.

![Primäre Identität des Hotels](../images/tutorials/relationship/hotel-identity.png)

>[!NOTE]
>
>Informationen zum Erstellen benutzerdefinierter Identitäts-Namespaces finden Sie in der [Dokumentation zum Identitätsdienst](../../identity-service/namespaces.md#manage-namespaces).

Nachdem die primäre Identität festgelegt wurde, muss das Zielschema für [!DNL Real-time Customer Profile] aktiviert werden.

![Profil aktivieren](../images/tutorials/relationship/hotel-profile.png)

## Erstellen einer Beziehungsschemafeldgruppe

>[!NOTE]
>
>Dieser Schritt ist nur erforderlich, wenn Ihr Quellschema über kein dediziertes Zeichenfolgenfeld verfügt, das als Verweis auf das Zielschema verwendet werden kann. Wenn das Feld in Ihrem Quellschema bereits definiert ist, fahren Sie mit dem nächsten Schritt zum [Definieren eines Beziehungsfelds](#relationship-field) fort.

Um eine Beziehung zwischen zwei Schemas zu definieren, muss das Quellschema über ein dediziertes Feld verfügen, das als Verweis auf das Zielschema dient. Sie können dieses Feld zum Quellschema hinzufügen, indem Sie eine neue Schemafeldergruppe erstellen.

Wählen Sie zunächst **[!UICONTROL Hinzufügen]** im Abschnitt **[!UICONTROL Feldergruppen]** aus.

![](../images/tutorials/relationship/loyalty-add-field-group.png)

Das Dialogfeld [!UICONTROL Feldergruppe hinzufügen] wird angezeigt. Wählen Sie hier **[!UICONTROL Neue Feldergruppe]** erstellen. Geben Sie in den angezeigten Textfeldern einen Anzeigenamen und eine Beschreibung für die neue Feldergruppe ein. Wählen Sie **[!UICONTROL Feldergruppen hinzufügen]** aus, wenn Sie fertig sind.

![](../images/tutorials/relationship/create-field-group.png)

Die Arbeitsfläche wird mit &quot;[!DNL Favorite Hotel]&quot;im Abschnitt **[!UICONTROL Feldergruppen]** erneut angezeigt. Wählen Sie den Namen der Feldergruppe aus und klicken Sie dann auf **[!UICONTROL Feld hinzufügen]** neben dem Feld auf der Stammebene `Loyalty Members` .

![](../images/tutorials/relationship/loyalty-add-field.png)

Auf der Arbeitsfläche wird unter dem Namespace `_tenantId` ein neues Feld angezeigt. Geben Sie unter **[!UICONTROL Feldeigenschaften]** einen Feldnamen und einen Anzeigenamen für das Feld ein und legen Sie dessen Typ auf &quot;[!UICONTROL String]&quot;fest.

![](../images/tutorials/relationship/relationship-field-details.png)

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Apply]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

Das aktualisierte Feld `favoriteHotel` wird auf der Arbeitsfläche angezeigt. Wählen Sie **[!UICONTROL Save]** aus, um die Änderungen am Schema abzuschließen.

![](../images/tutorials/relationship/relationship-field-save.png)

## Beziehungsfeld für das Quellschema definieren {#relationship-field}

Sobald in Ihrem Quellschema ein dediziertes Referenzfeld definiert ist, können Sie es als Beziehungsfeld festlegen.

Wählen Sie das Feld `favoriteHotel` auf der Arbeitsfläche aus und scrollen Sie dann unter **[!UICONTROL Feldeigenschaften]** nach unten, bis das Kontrollkästchen **[!UICONTROL Beziehung]** angezeigt wird. Aktivieren Sie das Kontrollkästchen, um die erforderlichen Parameter für die Konfiguration eines Beziehungsfelds anzuzeigen.

![](../images/tutorials/relationship/relationship-checkbox.png)

Wählen Sie das Dropdown-Menü für **[!UICONTROL Referenzschema]** aus und wählen Sie das Zielschema für die Beziehung aus (&quot;[!DNL Hotels]&quot; in diesem Beispiel). Wenn das Zielschema für [!DNL Profile] aktiviert ist, wird das Feld **[!UICONTROL Referenz-Identitäts-Namespace]** automatisch auf den Namespace der primären Identität des Zielschemas gesetzt. Wenn für das Schema keine primäre Identität definiert ist, müssen Sie den zu verwendenden Namespace manuell aus dem Dropdown-Menü auswählen. Wählen Sie **[!UICONTROL Anwenden]**, wenn Sie fertig sind.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

Das Feld `favoriteHotel` wird jetzt auf der Arbeitsfläche als Beziehung hervorgehoben, die den Namen- und Referenz-Identitäts-Namespace des Zielschemas anzeigt. Wählen Sie **[!UICONTROL Save]** aus, um Ihre Änderungen zu speichern und den Workflow abzuschließen.

![](../images/tutorials/relationship/relationship-save.png)

## Nächste Schritte

In diesem Tutorial haben Sie mithilfe von [!DNL Schema Editor] erfolgreich eine Eins-zu-Eins-Beziehung zwischen zwei Schemas erstellt. Anweisungen zum Definieren von Beziehungen mithilfe der API finden Sie in der Anleitung zum [Definieren einer Beziehung mithilfe der Schema Registry-API](relationship-api.md).
